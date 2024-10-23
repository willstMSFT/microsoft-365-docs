---
title: Integrate your workforce management system with Shifts using a custom connector
author: lana-chin
ms.author: v-chinlana
manager: jtremper
ms.reviewer: harrywong
ms.topic: conceptual
audience: admin
ms.service: microsoft-365-frontline
search.appverid: MET150
description: Learn how to create your own custom connector using Microsoft Graph APIs to integrate your workforce management (WFM) system with Shifts. 
ms.localizationpriority: high
ms.collection: 
  - M365-collaboration
  - m365-frontline
  - teams-1p-app-admin
appliesto: 
  - Microsoft Teams
  - Microsoft 365 for frontline workers
ms.date: 
---

# Integrate your workforce management system with Shifts using a custom connector

## Overview

## Prerequisites

Before you get started, complete the following prerequisites:

- Determine what data you want to sync between your WFM system and Shifts according to your business needs.
- Register an application in Microsoft Entra for the [workforceIntegration](/graph/api/resources/workforceintegration?view=graph-rest-1.0) Graph API.

    Choose the **Accounts in this organizational directory only (Single tenant)** option so that only users in your tenant can use the application. To learn more, see [Register an application with the Microsoft identity platform](/entra/identity-platform/quickstart-register-app).

- (Optional) Create teams in Teams that match the teams and locations in your WFM system, and add people to each team:
  - Add your frontline managers as team owners and/or schedule owners. Learn more about [team owners and schedule owners in Shifts](shifts-frontline-manager-worker-roles.md).
  - Add your frontline workers as team members.
  
  For guidance on creating frontline teams, see [How to find the best frontline team solution for your organization](frontline-team-options.md). To create teams at scale, see [Deploy frontline dynamic teams at scale](deploy-dynamic-teams-at-scale.md) and [Deploy frontline static teams at scale](deploy-teams-at-scale.md).

    > [!NOTE]
    > This prerequisite step is optional but recommended. If you choose not to set up your teams beforehand, you can do so after you create and register your connector.

## Step 1: Create your connector

### Sync data from your WFM system to Shifts

Use Shifts Graph APIs to read schedule data from your WFM system and write the data to Shifts. For example, to add a shift to Shifts, use the [Create shift](/graph/api/schedule-post-shifts?view=graph-rest-1.0) API.

See the [Graph API v1.0 reference for Shifts APIs](/graph/api/resources/shift?view=graph-rest-1.0). They're listed under **Shift management**.

#### Graph API permissions

To access Shifts data, you need to have the appropriate permissions and scopes. You can find the list of permissions and scopes required for each entity and operation in the Graph API documentation. You also need to obtain an access token from Microsoft Entra and include it in the authorization header of the requests.

Developers can authenticate against the Graph API either using delegated access (on behalf of a user) or as an application.

|Permission type |Read-only permissions|Read/write permissions|
|---------|---------|---------|
|[Delegated](#delegated-authentication)|Schedule.Read.All|Schedule.ReadWrite.All|
|[Application](#application-authentication)|Schedule.Read.All|Schedule.ReadWrite.All|

#### Delegated authentication

When authenticating on behalf of a user, the application uses the user's identity to authenticate and is authorized based on the user's permissions. This is useful for client applications where a user is signed in and the application needs to access data or perform tasks on behalf of the user. For example, a client application where a user is signed in should authenticate as a user.

#### Application authentication

When authenticating as an application, the application uses its own identity to authenticate and is authorized based on its own permissions. This is useful for background services or daemons that need to access data or perform tasks without user interaction. For example, a background sync service should be authenticated as an application.

> [!NOTE]
> The `MS-APP-ACT-AS` header is required when you use application authentication. The header should contain the user ID (GUID) of the user that your application is acting on behalf of. It’s recommended that you use the user ID of a team owner when updating the schedule.

### Initial sync

For the first sync, the service should read all data in your WFM system and write it to Shifts.

### Periodic sync

The service should also perform a periodic sync by writing all changes that occurred in your WFM system within a certain timeframe, excluding the changes initiated from Shifts (as described in Sync data from Shifts to your WFM system), as these changes are already written in Shifts.

All write operations to Shifts (including write operations initiated from the connector) trigger a call to the connector’s `/update` endpoint. Therefore, we recommend that you add the `X-MS-WFMPassthrough: workforceIntegratonId` header to all write calls. This allows you to identify and ignore your own changes in callback notifications and prevent the connector from getting stuck in an infinite loop.

### Sync data from Shifts to your WFM system

### Base URL

The base URL is determined based on your [workforceIntegration](/graph/api/resources/workforceintegration?view=graph-rest-1.0).

## Step 2: Register your connector

## Step 3: Enable your connector

## Related articles

- [Shifts connectors](shifts-connectors.md)
- [Manage the Shifts app in Teams](/microsoftteams/expand-teams-across-your-org/shifts/manage-the-shifts-app-for-your-organization-in-teams?bc=/microsoft-365/frontline/breadcrumb/toc.json&toc=/microsoft-365/frontline/toc.json)

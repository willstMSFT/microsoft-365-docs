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

- (Optional) Create teams in Teams that match the teams and locations in your WFM system, and add people to each team:
  - Add your frontline managers as team owners and/or schedule owners. Learn more about [team owners and schedule owners in Shifts](shifts-frontline-manager-worker-roles.md).
  - Add your frontline workers as team members.
  
  For guidance on creating frontline teams, see [How to find the best frontline team solution for your organization](frontline-team-options.md). To create teams at scale, see [Deploy frontline dynamic teams at scale](deploy-dynamic-teams-at-scale.md) and [Deploy frontline static teams at scale](deploy-teams-at-scale.md).

    > [!NOTE]
    > This prerequisite step is optional but recommended. If you choose not to set up your teams beforehand, you can do so after you create and register your connector.

## Register an app in the Microsoft Entra admin center

1. Sign in to the Microsoft Entra admin center as at least a [Cloud Application Administrator](/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator).
1. Register your app. For steps, see [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).
1. Assign the following Microsoft Graph [application permissions](/graph/permissions-overview?tabs=http#application-permissions) to your app for app-only access.

      |Permission type |Read-only permissions|Read/write permissions|
      |---------|---------|---------|
      |Application|Schedule.Read.All|Schedule.ReadWrite.All|

      Then, grant admin consent to the permissions, and get an access token.

      For step-by-step guidance, see [Get access without a user](/graph/auth-v2-service?view=graph-rest-1.0).

      The access token verifies that your app is authorized to [call Microsoft Graph using its own identity](/graph/auth/auth-concepts#access-scenarios). Developers must include it in the Authorization header of requests.

## Sync data from your WFM system to Shifts

Use Shifts Graph APIs to read schedule data from your WFM system and write the data to Shifts.

For example, to add a shift to Shifts, use the [Create shift](/graph/api/schedule-post-shifts?view=graph-rest-1.0) API.

See the [Microsoft Graph API v1.0 reference](/graph/api/resources/shift?view=graph-rest-1.0) and [Microsoft Graph API beta reference](/graph/api/resources/shift?view=graph-rest-beta) reference for Shifts APIs, which are listed under **Shift management**.

> [!NOTE]
> The `MS-APP-ACT-AS` header is required when you use application permissions. The header must the ID (GUID) of the user your application is acting on behalf of. We recommended you use the user ID of a team owner when updating the schedule.

### Initial sync

For the first sync, the service should read data in your WFM system and write the data to Shifts. We recommend you sync two weeks of future data.

### After the initial sync

After the first sync, you can choose to:

- **Synchronously update Shifts with changes in your WFM system**: Use Graph API to send an update to Shifts for every change made in your WFM system.
- **Asynchronously update Shifts with changes in your WFM system**: Perform a periodic sync by writing all changes that occurred in your WFM system within a certain timeframe (for example, 30 seconds, 10 minutes) to Shifts.

    All write operations to Shifts, including write operations initiated by the connector, trigger a call to the connector’s /update endpoint. We recommend that you include the `X-MS-WFMPassthrough: workforceIntegratonId` header to all write calls so the connector can identify and handle them appropriately. For example, if the change was initiated by your WFM system, approve it without applying an update to your WFM system.

  > [!NOTE]
  > If you're configuring the connector to sync data bidirectionally between your WFM system and Shifts, exclude changes initiated from Shifts in the periodic sync. These changes are already written in Shifts.

## Register and enable  workforce integration

### Register your workforce integration in your tenant

1. Register your [workforceIntegration](/graph/api/workforceintegration-post?view=graph-rest-1.0) in your tenant.

    Here's an example:

    ```http
    POST /teamwork/workforceIntegrations
    { 
      "displayName": "Contoso Integration", 
      "apiVersion": 1, 
      "encryption": { 
        "protocol": "sharedSecret", 
        "secret": "secret-value" 
      }, 
      "isActive": true, 
      "url": "https://contosoWorkforceIntegration.com/contoso", 
      "supportedEntities": "Shift,SwapRequest,TimeOffReason”, 
      "eligibilityFilteringEnabledEntities": "SwapRequest,OfferShiftRequest,TimeOffReason" 
    }
    ```

    - Specify the endpoint where Shifts can reach your connector for synchronous calls. The base URL is `${url}/v${apiVersion}/`. In this example, the base URL is `https://contosoWorkforceIntegration.com/contoso/v1/`.
    - During this API call, Shifts calls the /connect endpoint of your WFI application to test the connection. The connect endpoint is `${baseUrl}/connect`. In this example, the /connect endpoint is `https://contosoWorkforceIntegration.com/contoso/v1/connect`. The API returns a success response only if the /connect endpoint returns an HTTP `200 OK` response.
    - The shared secret for encryption is generated by your application and shared with the Shifts service during WFI registration. Use the secret to decrypt the encrypted JSON payloads sent to your WFI endpoint from Shifts. The payload is encrypted using `AES-256-CBC-HMAC-SHA256`. Your application should persist this secret safely. For example, in a key vault.
    - Specify the entities to sync. Your connector's /update endpoint is called when any of these entities are changed so you can approve or reject the change. For a list of entities, see [workforceIntegration resource type](/graph/api/resources/workforceintegration?view=graph-rest-1.0).

        > [!NOTE]
        > This list is an [evolvable enumeration](/graph/best-practices-concept#handling-future-members-in-evolvable-enumerations). You must use the `Prefer: include-unknown-enum-members` request header to get all the values.
    - Specify the entities for eligibility filtering. Options are:

      - `None`: Empty list
      - `SwapRequests`: Get a filtered list of shifts a user can choose in a swap request.
      - `TimeOffReasons`: Get a filtered list of time off reasons a user can select when they request time off.

        > [!NOTE]
        > This list is an [evolvable enumeration](/graph/best-practices-concept#handling-future-members-in-evolvable-enumerations). You must use the `Prefer: include-unknown-enum-members` request header to get all the values.

### Enable your workforce integration for a team schedule

Enable your workforce integration on the schedules you want to manage. This is done when you create or update the schedule on the team.

```http
POST teams/{teamId}/schedule
{
  enabled: true,
  timezone: “America/New_York”,
  workforceIntegrationIds: [ “workforceIntegrationId”]
}
```

- Your workforceIntegrationId is obtained when you registered your app.
- You can enable a maximum of one workforce integration on a schedule. If you include multiple workforce integration Ids, the first one is used.

### Sync data from Shifts to your WFM system

#### Base URL

The base URL is determined by your [workforceIntegration](/graph/api/resources/workforceintegration?view=graph-rest-1.0).

For example, if **url** is https://contosoconnector.com/wfi and **apiVersion** is 1:

- The base URL is `https://contosoconnector/com/wfi`.
- The /connect endpoint is `https://contosoconnector/wfi/v1/connect`.
- The /update endpoint is `https://contosoconnector/wfi/v1/connect/v1/teams/{teamsId}/update`.

#### Encryption

All requests are encrypted using AES-256-CBC-HMAC-SHA256 with the shared key provided in the workForceIntegration Create request.

#### Endpoints

##### POST /connect

This endpoint is only called during Graph API `POST /teamwork/workforceIntegrations`. This is basically a ping test to test the connection.

**Request**<br>
ConnectRequest

```http
{
   "tenantId": "a1s2s355-a2s3-j7h6-f4d3-k2h9j4mqpz",
   "userId": "4fbc12d7-1234-56ef-8a90-bc123d45678f"
}
```

**Response**

Return HTTP `200 OK`

##### POST /teams/{teamsId}/update

When a change is made to an entity in a [schedule](/graph/api/resources/schedule?view=graph-rest-1.0) with a [workforceIntegration](/graph/api/resources/workforceintegration?view=graph-rest-1.0), Shifts calls this endpoint to get approval. When approved, the change is saved in Shifts.

As your WFM system is the source of truth, when the connector receives a request to this endpoint, it should first attempt to make the change in the WFM system. If the change is successful, return success. Otherwise, return failure.

##### X-MS-WFMPassthrough header

Shifts calls this endpoint for every change (including changes initiated from the connector/WFM system). If the connector sent an update to Shifts using Graph API and added the `X-MS-WFMPassthrough: workforceIntegratonId` header, the request coming to this endpoint will have the same header.

This allows you to identify and handle these requests appropriately. For example, return success without making the same change in the WFM system because it would be redundant and can cause the connector to get stuck in an infinite loop.

**Return response code**<br>
Any response from the integration, including an error, must have an HTTP response code `200 OK`. The response body must have the status and error message reflecting the appropriate sub call error state. Any response from the integration other than `200 OK` is treated as an error and returned to the caller (client or Graph).

**Request**<br>
WfiRequestContainer

```http
{
  "requests": [
    {
      "id": "SHFT_12345678-1234-1234-1234-1234567890ab",
      "method": "POST",
      "url": "/shifts/SHFT_12345678-1234-1234-1234-1234567890ab",
      "headers": {
        "X-MS-Transaction-ID": "1",
        "X-MS-Expires": "2024-10-11T21:27:59.0134605Z"
      },
      "body": {
        "draftShift": {
          "activities": [],
          "isActive": true,
          "startDateTime": "2024-10-12T15:00:00.000Z",
          "endDateTime": "2024-10-12T17:00:00.000Z",
          "theme": "Blue"
        },
        "isStagedForDeletion": false,
        "schedulingGroupId": "TAG_a3e0b3f1-4a5c-4c2e-8eeb-5b8c3d1e3f8b",
        "userId": "f47ac10b-58cc-4372-a567-0e02b2c3d479",
        "createdDateTime": "2024-10-11T21:27:28.762Z",
        "lastModifiedDateTime": "2024-10-11T21:27:28.762Z",
        "lastModifiedBy": {
          "user": {
            "id": "f47ac10b-58cc-4372-a567-0e02b2c3d479",
            "displayName": "Jon Doe"
          }
        },
        "id": "SHFT_12345678-1234-1234-1234-1234567890ab"
      }
    }
  ]
}
```

**Response**<br>
WfiResponse

Success: Return HTTP `200 OK`

```http
{
  "responses": [
    {
      "id": "SHFT_12345678-1234-1234-1234-1234567890ab",
      "status": 200,
      "body": {
        "eTag": "3f4e5d6c-7a8b-9c0d-1e2f-3g4h5i6j7k8l",
        "error": null,
        "data": null
      }
    }
  ]
}
```

Failure: return HTTP `200 OK`

```http
{
    "responses": [
        {
            "id": "SHFT_12345678-1234-1234-1234-1234567890ab",
            "status": 500,
            "body": {
                "error": {
                    "code": "500",
                    "message": “Could not add the shift”
                },
                "data": null
            }
        }
    ]
}
```

##### POST /teams/{teamsId}/read

This endpoint handles requests from Shifts to fetch eligible time off reasons for a user or eligible shifts for swap requests.

> [!NOTE]
> This endpoint is supported only when using the beta Graph API (as of October 2024) and adding `eligibilityFilteringEnabledEntities` in workforceIntegration.

## Frequently asked questions

**What happens if I return any response code other than 200? Does it make any difference whether I return a status other than 200 in the response body?**

There's a difference between these two scenarios.

- If you return a response code other than 200, Shifts attempts to retry the read/update endpoint multiple times. Eventually, Shifts displays a "Something went wrong. The workforce integration setup on your team has responded with invalid data." error message.
- If you return a status other than 200 in the response body, Shifts displays a "Something went wrong. Sorry, your change couldn’t be completed," error message and stops retrying the endpoints.

**What happens if I return any invalid data in the response body?**

Shifts attempts to retry the read/update endpoint multiple times. Eventually, Shifts displays a "Something went wrong. The workforce integration setup on your team has responded with invalid data." error message.

**How do I identify whether the request is being made originally in Shifts or in the WFM system to prevent an infinite loop?**

Add the `X-MS-WFMPassthrough: workforceIntegratonId` header to all write/update calls to identify/ignore the changes triggered by connector. This header is used to indicate that the request is being made because of a preceding call made by the WFM connector service to Shifts Graph API when performing a data sync.

**I registered the WFI through Graph API with eligibilityFilteringEnabledEntities including SwapRequest,OfferShiftRequest,TimeOffReason but the response body doesn't show the eligibilityFilteringEnabledEntities list.**

Eligibility filtering is currently supported through the `https://graph.microsoft.com/beta` endpoint, not the `https://graph.microsoft.com/v1` endpoint.

**I registered the WFI through Graph API with supportedEntities but get a 400 Bad Request response and an "Invalid payload: Requested value 'shift, ....' was not found. message**

Every Shifts entity in the `supportedEntities` list request body must start with an uppercase letter. For example:

`"supportedEntities": "Shift, SwapRequest, TimeOffReason, UserShiftPreferences, OpenShift, OpenShiftRequest, OfferShiftRequest, TimeOff,TimeOffRequest,TimeCard"`

**I registered the WFI through GraphAPI and implemented the /update, /read, and /connect endpoints, but the webhook isn't working.**

Maybe you haven't enabled the WFI for your team, or you registered the wrong WFI ID with a different callback URL.

## Related articles

- [Shifts for your frontline organization](shifts-for-teams-landing-page.md)
- [Shifts connectors](shifts-connectors.md)

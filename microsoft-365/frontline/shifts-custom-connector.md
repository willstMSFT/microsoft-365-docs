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

Integrate Shifts, the schedule management tool in Microsoft Teams, with your workforce management (WFM) system. After you set up an integration, your frontline can access their schedules in your WFM system from within Shifts.

This article gives you an overview of how to create a connector using the Microsoft Graph API to integrate Shifts with your WFM system.

A connector syncs schedule data between your WFM system and Shifts, bringing your organization’s schedules into Teams. Shifts is where your frontline engage for their scheduling needs. Your WFM system is the system of record for business rules, compliance, and intelligence.

You can set up your connector to sync data unidirectionally or bidirectionally.

- **Sync data from your WFM system to Shifts**: This is a one-way sync where schedule data in your WFM system is synced to Shifts. The connector reads data in your WFM system and writes the data to Shifts. Any changes made in Shifts aren’t reflected in your WFM system. 
- **Sync data between your WFM system and Shifts**: This is a two-way sync. Schedule data in your WFM system is synced to Shifts and changes made to schedules in Shifts are synced back to your WFM system. The connector validates and approves changes made in Shifts according to business rules enforced by your WFM system before the changes are written to Shifts.

## Prerequisites

- Determine what data you want to sync between your WFM system and Shifts according to your business needs.
- Admin roles required:
  - At least a [Cloud Application Administrator](/entra/identity/role-based-access-control/permissions-reference?toc=%2Fgraph%2Ftoc.json#cloud-application-administrator) to register an app in the Microsoft Entra admin center
  - Global Administrator to register your workforce integration
  
## Create a connector

### Sync changes made in Shifts to your WFM system

To set up your connector to receive and process requests from Shifts, you need to implement the following endpoints:

- [/connect](#post-connect)
- [/update](#post-teamsteamsidupdate)

**Determine your base URL and /connect and /update endpoint URLs**

The base URL (webhook) is `https://{url}/v{apiVersion}`, where **url** and **apiVersion** are the properties of the [workforceIntegration](/graph/api/resources/workforceintegration?view=graph-rest-1.0) object for when you [register your workforce integration](#register-your-workforce-integration-in-your-tenant).

For example, if **url** is `https://contosoconnector.com/wfi` and **apiVersion** is 1:

- The base URL is `https://contosoconnector/com/wfi/v1`.
- The /connect endpoint is `https://contosoconnector/wfi/v1/connect`.
- The /update endpoint is `https://contosoconnector/wfi/v1/teams/{teamsId}/update`.

**Encryption**

All requests are encrypted using `AES-256-CBC-HMAC-SHA256`. You specify the shared secret key when you [register your workforce integration](#register-your-workforce-integration-in-your-tenant).

#### Endpoints

##### POST /connect

When you [register your workforce integration](#register-your-workforce-integration-in-your-tenant), Shifts calls this endpoint to test the connection. A success response is returned only if this endpoint returns an HTTP 200 OK response.

###### Example

**Request**<br>
ConnectRequest

```http
{
   "tenantId": "a1s2s355-a2s3-j7h6-f4d3-k2h9j4mqpz",
   "userId": "4fbc12d7-1234-56ef-8a90-bc123d45678f"
}
```

**Response**<br>
Return HTTP `200 OK`

##### POST /teams/{teamsId}/update

When a change is made to an Shifts entity in a [schedule](/graph/api/resources/schedule?view=graph-rest-1.0) with a [workforceIntegration](/graph/api/resources/workforceintegration?view=graph-rest-1.0), Shifts calls this endpoint to get approval. When approved, the change is saved in Shifts.

As your WFM system is the system of record, when the connector receives a request to this endpoint, it should first attempt to make the change in the WFM system. If the change is successful, return success. Otherwise, return failure.

Shifts calls this endpoint for every change (including changes initiated from the connector/WFM system). If the connector sent an update to Shifts using Graph API and added the `X-MS-WFMPassthrough: workforceIntegratonId` header, the request coming to this endpoint will have the same header. This allows you to identify and handle these requests appropriately. For example, return success without making the same change in the WFM system as it would be redundant and can cause the connector to get stuck in an infinite loop.

**Return response code**<br>
Any response from the integration, including an error, must have an HTTP response code `200 OK`. The response body must have the status and error message that reflects the appropriate sub call error state. Any response from the integration other than `200 OK` is treated as an error and returned to the caller (client or Graph).

###### Make Shifts read-only for one-way sync

To do this, return a failure response for all requests from Shifts.

For example, if you don't want users making changes to shifts in Shifts, the endpoint must return a failure response whenever it receives a request regarding a shift entity.

###### Example

**Request**<br>
WfiRequestContainer

The following example shows a request that asks whether a shift entity (a shift with ID SHFT_12345678-1234-1234-1234-1234567890ab) with the properties outlined in "body" can be saved in Shifts. This request was triggered when a user created a shift in Shifts.

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
            "displayName": "Adele Vance"
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

The endpoint approved the request. The shift is saved in Shifts, and the user can see the shift in the schedule.

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

The endpoint denied the request. The user receives a “Could not add the shift” error message in Shifts.

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

### Sync data from your WFM system to Shifts

Use Shifts APIs in Microsoft Graph to read schedule data from your WFM system and write the data to Shifts.

For example, to add a shift to Shifts, use the [Create shift](/graph/api/schedule-post-shifts?view=graph-rest-1.0) API.

See the [Microsoft Graph API v1.0 reference](/graph/api/resources/shift?view=graph-rest-1.0) and [Microsoft Graph API beta reference](/graph/api/resources/shift?view=graph-rest-beta) for Shifts APIs, which are listed under **Shift management**.

> [!NOTE]
> The `MS-APP-ACT-AS` header is required in requests and must contain the ID (GUID) of the user your app is acting on behalf of. We recommend you use the user ID of a team owner when updating the schedule.

#### Initial sync

For the first sync, the service should read data in your WFM system and write the data to Shifts. We recommend you sync two weeks of future data.

#### After the initial sync

After the first sync, you can choose to:

- **Synchronously update Shifts with changes in your WFM system**: Send an update to Shifts for every change made in your WFM system.
- **Asynchronously update Shifts with changes in your WFM system**: Perform a periodic sync by writing all changes that occurred in your WFM system within a certain timeframe (for example, 30 seconds, 10 minutes) to Shifts.

    All write operations to Shifts, including write operations initiated by the connector, trigger a call to the connector’s /update endpoint. We recommend you include the `X-MS-WFMPassthrough: workforceIntegratonId` header to all write calls so the connector can identify and handle them appropriately. For example, if the change was initiated by your WFM system, approve it without applying an update to your WFM system.

  > [!NOTE]
  > If you're configuring the connector to sync data bidirectionally between your WFM system and Shifts, exclude changes initiated from Shifts in the periodic sync. These changes are already written in Shifts.

## Register an app in the Microsoft Entra admin center

Follow these steps to register an app for your connector in the Microsoft identity platform, configure permissions for the app to access Microsoft Graph, and get an access token.

1. Sign in to the Microsoft Entra admin center as at least a [Cloud Application Administrator](/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator).
1. Register your app. For steps, see [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).
1. Assign the *Schedule.ReadWrite.All* [application permissions](/graph/permissions-overview?tabs=http#application-permissions) to the app for app-only access and get an access token.

      For step-by-step guidance, see [Get access without a user](/graph/auth-v2-service?view=graph-rest-1.0).

      The access token verifies that your app is authorized to [call Microsoft Graph using its own identity](/graph/auth/auth-concepts#access-scenarios) using the *Schedule.ReadWrite.All* permission. It must be included in the Authorization header of requests.

## Register and enable the workforce integration

### Register your workforce integration in your tenant

Use the [Create workforceIntegration](/graph/api/workforceintegration-post?view=graph-rest-1.0&tabs=http) API to register your workforce integration in your tenant. Registering your workforce integration defines the Shifts entities to support for synchronous change notifications, the URL for callbacks from Shifts, and the encryption settings for communication between Shifts and the connector.

Here's an example request.

```http
POST https://graph.microsoft.com/v1.0/teamwork/workforceIntegrations/
{ 
  "displayName": "Contoso integration", 
  "apiVersion": 1, 
  "encryption": { 
    "protocol": "sharedSecret", 
    "secret": "secret-value" 
  }, 
  "isActive": true, 
  "url": "https://contosoconnector.com/wfi", 
  "supportedEntities": "shift,swapRequest,userShiftPreferences,openshift,openShiftRequest,offerShiftRequest”,
}
```

|Property  |More information  |
|---------|---------|-
|encryption|Set **protocol** to `sharedSecret`. The **secret** value is generated by your app and shared with Shifts during registration. It has a 64-character limit, and should be exactly 64 characters. Use the secret to decrypt the encrypted JSON payloads that are sent to your connector's endpoint from Shifts. The payload is encrypted using AES-256-CBC-HMAC-SHA256. Your app should safely persist this secret. For example, in a key vault.|
|supportedEntities |Specify the Shifts entities to sync. Shifts will make a call back to your connector's /update endpoint when any of these entities change so that you can approve or reject the change. Possible values are: `none`, `shift`, `swapRequest`, `userShiftPreferences`, `openshift`, `openShiftRequest`, `offerShiftRequest`<br><br>**Note** This list is an [evolvable enumeration](/graph/best-practices-concept#handling-future-members-in-evolvable-enumerations). You must use the `Prefer: include-unknown-enum-members` request header to get all the values.|
|Row3     |         |

To learn more, see [workforceIntegration resource type](/graph/api/resources/workforceintegrationencryption?view=graph-rest-1.0)
<!-- The shared secret for encryption should be generated by your app and shared with Shifts during registration. The secret has a 64-character limit, and should be exactly 64 characters. Use it to decrypt the encrypted JSON payloads that are sent to your connector's endpoint from Shifts. The payload is encrypted using AES-256-CBC-HMAC-SHA256. Your app should safely persist this secret. For example, in a key vault.
- Specify the entities to sync. Shifts will call your connector's /update endpoint when any of these entities change so you can approve or reject the change. For a list of these entities, see [workforceIntegration resource type](/graph/api/resources/workforceintegration?view=graph-rest-1.0).

    > [!NOTE]
    > This list is an [evolvable enumeration](/graph/best-practices-concept#handling-future-members-in-evolvable-enumerations). You must use the `Prefer: include-unknown-enum-members` request header to get all the values.

- Specify the entities for eligibility filtering. Options are:
  - `None`: Empty list
  - `SwapRequests`: Get a filtered list of shifts a user can choose in a swap request.
  - `TimeOffReasons`: Get a filtered list of time off reasons a user can select when they request time off.

    > [!NOTE]
    > This list is an [evolvable enumeration](/graph/best-practices-concept#handling-future-members-in-evolvable-enumerations). You must use the `Prefer: include-unknown-enum-members` request header to get all the values.-->

### Set up teams in Teams

1. Create teams in Teams that match the teams and locations in your WFM system, and add people to each team:

    - Add your frontline managers as team owners. Make sure you add the user in the `MS-APP-ACT-AS` header as the team owner of each respective team.
    - Add your frontline workers as team members.
1. Create a schedule for each team.
1. Create schedule groups, and add people to each schedule group. 
  
For guidance on creating frontline teams, see [How to find the best frontline team solution for your organization](frontline-team-options.md). To create teams at scale, see [Deploy frontline dynamic teams at scale](deploy-dynamic-teams-at-scale.md) and [Deploy frontline static teams at scale](deploy-teams-at-scale.md).

### Enable your workforce integration for a team schedule

Enable your workforce integration on the schedules you want to manage. This is done when you create or update the schedule on the team.

Here's an example of a request.

```http
POST teams/{teamId}/schedule
{
  enabled: true,
  timezone: “America/New_York”,
  workforceIntegrationIds: [ “workforceIntegrationId”]
}
```

- The workforceIntegrationId is obtained when you registered your app.
- You can enable a maximum of one workforce integration on a schedule. If you include multiple workforce integration Ids, the first one is used.

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

Maybe you haven't enabled the workforce integration for your team, or you registered the wrong WFI ID with a different callback URL.

## Related articles

- [Shifts for your frontline organization](shifts-for-teams-landing-page.md)
- [Shifts connectors](shifts-connectors.md)

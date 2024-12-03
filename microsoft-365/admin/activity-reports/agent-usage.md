---
title: "Agent usage in Microsoft 365 Copilot"
ms.author: camillepack
author: camillepack
manager: scotv
ms.date: 10/02/2024
audience: Admin
ms.topic: concept-article
ms.service: microsoft-365-copilot
ms.localizationpriority: medium
ms.collection: 
- Tier2
- scotvorg
- M365-subscription-management
- Adm_O365
- Adm_NonTOC
- m365copilot
- magic-ai-copilot
ms.custom: AdminSurgePortfolio
search.appverid:
- BCS160
- MST160
- MET150
- MOE150
description: "Learn about agent usage in Microsoft 365 copilot and gain insights into the Microsoft 365 Copilot activity in your organization."
---

# Microsoft 365 reports in the admin center – Agent usage in Microsoft 365 Copilot

Admins can manage agents in the same way as they manage any other app in the Integrated apps section of the Microsoft 365 admin center. Learn more in [Manage Copilot agents in Integrated Apps](/microsoft-365/admin/manage/manage-copilot-agents-integrated-apps). In the Microsoft 365 Copilot agent report, you can view the adoption of Copilot agents in your org. For agent activity on a given day, the report becomes available within 72 hours of the end of that day (in UTC).

> [!NOTE]
> The report is limited to agents built by your org through Microsoft Copilot Studio or Teams Tool Kit and is limited to usage of agents in Business chat (work) and Copilot in Word, Excel and PowerPoint. SharePoint agents and usage of standalone Graph connector is not included.

## How do I get to the agent usage in Microsoft 365 Copilot report?

1. In the admin center, go to Reports > Usage.
1. Select the Microsoft 365 Copilot page.
1. Select the Agent tab to view adoption and usage metrics.

## Interpret the Microsoft 365 Copilot agent report

You can use this report to see the usage of Copilot agents in your organization that were built by your organization and include agents that are approved by an admin and agents created via [agent builder](/microsoft-365-copilot/extensibility/copilot-studio-agent-builder) and [shared with users in your org](/microsoft-365-copilot/extensibility/copilot-studio-agent-builder-publish#share-the-agent).

At the top, you can filter by different periods. The Microsoft 365 Copilot agent report can be viewed over the last 7 days, 30 days, 90 days, or 180 days:

> [!NOTE]
> Copilot agent data is only available starting Nov 1, 2024.

:::image type="content" source="{source}" alt-text="{alt-text}":::

**Active agents** shows the distinct number of apps with a declarative agent element in that app with at least one active user over the selected time period. For more information, see [Declarative agents FAQ](/microsoft-365/admin/manage/manage-copilot-agents-integrated-apps). As defined earlier, only agents that have been created by your org including both admin approved and shared by users in your org are included.  

End users can interact with agents in two ways: either by at-mentioning the agent or selecting the agent from the side panel to the right in Business chat, or from the hamburger menu on the top left corner in Copilot in Word, Excel or PowerPoint. An active user of an agent, is a user who received a response from Microsoft 365 Copilot, after interacting with the agent as previously described, followed by the user sending a prompt.  

In Recommendations, the recommended action card highlights where Admins can go to, to manage Copilot agents as apps in the Integrated apps section of the Microsoft 365 admin center and enable agents for users in their org.

:::image type="content" source="{source}" alt-text="{alt-text}":::

To learn more about managing and enabling agents in your org, see [Manage Copilot agents in Integrated Apps](/microsoft-365/admin/manage/manage-copilot-agents-integrated-apps).

You can see the following summary charts in this report as default view:

:::image type="content" source="{source}" alt-text="{alt-text}":::

The definition of active agents is the same as provided earlier.

You can switch between Summary view and Trend view.

**Summary view** shows you the total number of agents that are actively used in the time frame.

**Trend view** shows you the daily time trend of agents in the time frame.

:::image type="content" source="{source}" alt-text="{alt-text}":::

## Agent details table

:::image type="content" source="{source}" alt-text="{alt-text}":::

| Item | Description |
| --- | --- |
| Agent ID | An agent is an element of an app. The ID is the app identifier as present in the app manifest. |
| Agent name | The name of the app as present in the app manifest. |
| Active users in Copilot | The number of distinct users in your organization that are using the agent. |
| Last activity date (UTC) | The date when that agent was last used by anyone in your organization. |

> [!NOTE]
> The agent metrics on the Usage page and Agents page include both admin approved and user-created agents, the table in the Agents details only shows agents that were admin approved. The breakout of agents created and shared by users in your org are now displayed in the table.

## FAQ 

### Are agents created from Microsoft Copilot Studio and Teams Tool Kit included?  

Yes. These are the agents that usage is reported for:

- Agents created in Microsoft Copilot studio by users in your org and approved by admin.
- Agents created in Teams Tool kit by users in your org and approved by admin.
- Agents created by users through agent builder for users that have this feature enabled and shared with other users in your org.

### Are agents published by Microsoft or Microsoft Partners included?

No. Currently, the report does not include the usage of agents built by Microsoft or Partners.  

### Why am I not seeing all the active agents in the Agent details table?  

Information about user-created agents through agent builder such as name, is not available currently and are not displayed in the table. However, usage of these agents is included in the report. Additionally, the agents built by users in your org that have been admin approved are shown in the table.  

### How can I see which users can see which agents?

Not available at this time.  

### How does agent usage impact overall Microsoft 365 Copilot usage?

Agent usage is already included in the top line Microsoft 365 Copilot usage number and does not have any impact. This is because users need to use Microsoft 365 Copilot to be able to interact with agents.  
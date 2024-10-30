---
title: Compare Microsoft Copilot features in E3 and E5 licenses
description: Lists and compares the features available in Microsoft 365 E3 and E5 licenses that can help you get your data ready for Microsoft 365 Copilot.
f1.keywords:
- NOCSH
ms.author: mandia
author: MandiOhlinger
manager: laurawi
ms.date: 10/30/2024
audience: Admin
ms.topic: 
ms.service: microsoft-365-copilot
ms.localizationpriority: medium
ms.collection: 
- scotvorg
- m365copilot
- magic-ai-copilot
- essentials-overview
ms.custom: [copilot-learning-hub]
appliesto:
  - ✅ Microsoft 365 Copilot
---

# Microsoft 365 E3 and E5 feature comparison list for Microsoft 365 Copilot

> [!WARNING]
> This article is a work in progress for Ignite. Do not publish.

[Microsoft 365 Copilot](microsoft-365-copilot-overview.md) is an AI-powered productivity assistant that can help users with different tasks, like finding information and creating content. You can use Copilot in your Microsoft 365 apps, like Word, Outlook, and Teams.

Since Copilot accesses the data your users have access to, it's important to make sure your data is ready for Copilot. This task includes making sure your data is shared with only the users who need access and is labeled for sensitivity.

There are different features in the Microsoft 365 E3 and E5 licenses that can help you get your data ready for Copilot. These features:

- Help prevent oversharing
- Declutter data sources
- Identify and label sensitive data in your Microsoft 365 and Office files

Use the information in this article to know the features available to you based on your license. It can also help you decide which license is right for you based on the features your organization wants and needs.

If you're currently [licensed for Copilot](microsoft-365-copilot-licensing.md) or plan to get it, this article can help.

This article applies to:

- Microsoft 365 Copilot
- Microsoft SharePoint Premium - SharePoint Advanced Management (SAM)
- Microsoft Purview

## Microsoft 365 E3 and E5 feature table

The following table lists some of the features that can help with Copilot.

| &nbsp; | E3 license | E5 license |
| --- | --- | --- |
| License requirements | - Microsoft 365 E3 or Office 365 E3 <br/>- Microsoft 365 Copilot (includes SharePoint Advanced Management (SAM)) | - Microsoft 365 E5 or Office 365 E5 <br/>- Microsoft 365 Copilot (includes SharePoint Advanced Management (SAM)) |
| Restricted SharePoint Search (RSS) | ✅  | ✅  |
| &nbsp; | &nbsp; | &nbsp; |
| **Microsoft Purview features** | &nbsp; | &nbsp; |
| Sensitivity labels |  ✅ <br/><br/> You can: <br/><br/>- Create custom labels. <br/> - Use default labels *except* on SharePoint document libraries. Must use custom label. <br/> - Manually apply labels. | ✅ <br/><br/> You can: <br/><br/> - Create custom labels. <br/> - Use default labels. <br/> - Manually apply labels. <br/> - Auto-apply labels. |
| Data loss prevention (DLP)| ✅ <br/><br/>Policies can target: <br/><br/>- SharePoint <br/> - Exchange <br/> - OneDrive | ✅ <br/><br/> Policies can target: <br/><br/>- SharePoint <br/> - Exchange <br/> - OneDrive <br/> - Teams <br/> - Endpoints |
| Adaptive Protection | n/a | ✅ |
| Data lifecycle management  | ✅ <br/><br/> You can: <br/><br/> - Create retention policies<br/> - Manually apply retention labels<br/> - Use Content explorer | ✅ <br/><br/> You can: <br/><br/> - Create retention policies<br/> - Manually apply retention labels<br/> - Auto-apply retention labels <br/> - Use Content explorer <br/> - Use Activity explorer |
| Communication Compliance | n/a | ✅ |
| eDiscovery | ✅ <br/><br/>eDiscovery (Standard) for sites, files, email; search | ✅ <br/><br/> search and delete |
| AI Hub |  ✅ | ✅ |
| &nbsp; | &nbsp; | &nbsp; |
| **SharePoint Advanced Management (SAM) features** | &nbsp; | &nbsp; |
| Data access governance (DAG) reports | ✅ | ✅ |
| Restricted access control (RAC) | ✅ | ✅ |
| Site lifecycle management | ✅ | ✅ |
| Change history report | ✅ | ✅ |

To learn more about these features and how they affect Copilot, see:

- [Microsoft 365 Copilot E3 deployment - admin guide](microsoft-365-copilot-e3-guide.md)
- [Microsoft 365 Copilot E5 deployment - admin guide](microsoft-365-copilot-e5-guide.md)

To learn more about licensing, see:

- [Microsoft 365 Copilot licensing](microsoft-365-copilot-licensing.md)
- [Microsoft Purview service description](/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-purview-service-description)
- [Microsoft SharePoint Premium - SharePoint Advanced Management licensing](/sharepoint/advanced-management#licensing)

## More features to help you get ready for Copilot

Microsoft continues to invest in features that help you get ready for Copilot. This section describes some more services and features that are available to you.

### AI Hub in Microsoft Purview

[AI Hub](/purview/ai-microsoft-purview) is a central location that helps you secure data for AI apps and proactively monitor AI use. It has preconfigured policies that focus on AI and reports that give information into AI use within your organization. It also includes eDiscovery and you can use it to analyze Copilot prompts and responses.

If your focus is on Copilot, then use AI Hub.

1. Sign into the [Microsoft Purview portal](https://purview.microsoft.com/) as an admin in one of the groups listed at [Microsoft Purview AI Hub - permissions](/purview/ai-microsoft-purview-permissions).
1. Select **Solutions** > **AI Hub** > **Recommendations**.
1. Create the recommended policies.

To learn more about these policies, see [AI Hub - one-click policies](/purview/ai-microsoft-purview-considerations#one-click-policies-from-the-ai-hub).

### Copilot dashboard in Viva Insights

Viva Insights provides actionable insights to help your organization get ready to deploy AI, drive adoption, and measure the effect of Copilot.

The dashboard shows metrics on readiness, adoption, impact, and sentiment.

1. Open the Teams app.
2. In the Teams vertical toolbar, select the ellipses > **Viva Insights**.
3. On the navigation panel, select **Copilot Dashboard**.

To learn more, see [Microsoft Copilot Dashboard for Microsoft 365 customers](/viva/insights/org-team-insights/copilot-dashboard).

## Get started with your E3 or E5 features

The next step is to start using the features in your Microsoft 365 license:

- [Microsoft 365 Copilot E3 deployment - admin guide](microsoft-365-copilot-e3-guide.md)
- [Microsoft 365 Copilot E5 deployment - admin guide](microsoft-365-copilot-e5-guide.md)

## Related content

- [Microsoft 365 Copilot licensing](microsoft-365-copilot-licensing.md)
- [Microsoft 365 Copilot E3 deployment - admin guide](microsoft-365-copilot-e3-guide.md)
- [Microsoft 365 Copilot E5 deployment - admin guide](microsoft-365-copilot-e5-guide.md)

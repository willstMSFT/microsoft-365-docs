---
title: "Microsoft 365 Copilot baseline deployment and readiness guide"
f1.keywords:
- NOCSH
ms.author: camillepack
author: camillepack
manager: scotv
ms.date: 10/22/2024
audience: Admin
ms.topic: get-started
ms.service: microsoft-365-copilot
ms.localizationpriority: medium
ms.collection: 
- scotvorg
- m365copilot
- magic-ai-copilot
- essentials-get-started
description: Learn how administrators can prepare their organization for Microsoft 365 Copilot. Admin cans assign licenses, optimize SharePoint search, give enough access, prevent oversharing, use sensitivity labels, create a pilot group, and more.
---

# Preparing for Microsoft 365 Copilot - admin guide

[**this is a draft that will replace the current set up guide, I think. work in progress**]


[Microsoft 365 Copilot](microsoft-365-copilot-overview.md) is an AI-powered productivity tool that uses large language models (LLMs). It integrates with your data, with Microsoft Graph, and with Microsoft 365 Apps.

It works alongside popular Microsoft 365 Apps, like Word, Excel, PowerPoint, Outlook, Teams, and more. Copilot provides real-time intelligent assistance, enabling users to enhance their creativity, productivity, and skills.

This article provides guidance for administrators on preparing their organization for Microsoft 365 Copilot. It covers baseline implementation and readiness activities, required licenses, and steps to ensure a secure and compliant deployment.

## Prerequisites

- This article uses the following admin centers. These admin centers require a specific role to complete the tasks in the article.

  - **[Microsoft 365 admin center](https://admin.microsoft.com)**: There are different roles, depending on the task you need to complete. To learn more about roles, see [Commonly used Microsoft 365 admin center roles](/microsoft-365/admin/add-users/about-admin-roles#commonly-used-microsoft-365-admin-center-roles).
  - **[SharePoint admin center](https://go.microsoft.com/fwlink/?linkid=2185219)**: Sign in as the [SharePoint administrator](/sharepoint/sharepoint-admin-role).
  - **[Microsoft Purview portal](https://purview.microsoft.com)**: There are different roles, depending on the task you need to complete. To learn more, see:

    - [Permissions required to create and manage sensitivity labels](/purview/get-started-with-sensitivity-labels#permissions-required-to-create-and-manage-sensitivity-labels)
    - [Roles and role groups in Microsoft Defender for Office 365 and Microsoft Purview](/defender-office-365/scc-permissions)

- You must have an appropriate **subscription plan to purchase Microsoft 365 Copilot**.

  You can purchase Microsoft 365 Copilot licenses through the [Microsoft 365 admin center](https://admin.microsoft.com) (**Billing** > **Purchase services**), Microsoft partners, or your Microsoft account team.

  Microsoft 365 Copilot licenses are available as an add-on to other licensing plans. To learn more, see [Understand licensing for Microsoft 365 Copilot](microsoft-365-copilot-licensing.md).

- More licenses might be required to use some of the features describes in this article, like Microsoft Purview and SharePoint Advanced Management.

  To learn more, see:

  - [Microsoft Purview service description](/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-purview-service-description)
  - [Microsoft SharePoint Premium - SharePoint Advanced Management overview](/sharepoint/advanced-management#licensing)

- To view Microsoft 365 app requirements, see [Microsoft 365 Copilot requirements](microsoft-365-copilot-requirements.md).

## Readiness activities

[**work in progress**]

To ensure a smooth transition to Microsoft 365 Copilot, administrators should undertake the following readiness activities:

- **Set up a test environment**: Establish a test environment with necessary licenses to validate configurations and test scenarios.
- **Conduct pilot testing**: Perform pilot testing with a select group of users to identify any issues and gather feedback.
- **Develop a communication plan**: Create a communication plan to inform users about the upcoming changes and provide them with the necessary resources and support.
- **Review Conditional Access policies**: Ensure that conditional access policies are appropriately configured. Microsoft 365 Copilot supports tenant-level Conditional Access Policies (CAP) in SharePoint Online.
- **Review Restricted Access Control and Information Barrier Policies**: Microsoft 365 Copilot does not currently support Restricted Access Control (RAC) and Microsoft 365 Information Barriers. Plan to extend support to both policies by December.
- **Ensure network compliance**: Review and ensure that your network meets the requirements for Microsoft 365 Copilot services.

## Security measures for Microsoft 365 Copilot

To ensure a secure and compliant environment for Microsoft 365 Copilot, it is crucial to implement robust security measures. Two key components of this are Multi-Factor Authentication (MFA) and audit logging. These measures help protect against unauthorized access and provide visibility into user and admin activities.

### Multi-Factor Authentication (MFA)

Multi-factor authentication (MFA) is a critical security measure that requires users to provide two or more verification factors to gain access to a resource such as an application or online account. Implementing MFA helps protect against unauthorized access and enhances the security of your organization's data.

#### Steps to implement MFA

- **Enable MFA for all users**: Ensure that MFA is enabled for all users in your organization. This can be done through the Microsoft 365 admin center.
- **Configure Conditional Access policies**: Set up conditional access policies to enforce MFA based on user risk, location, and device compliance.
- **Educate users**: Provide training and resources to help users understand the importance of MFA and how to use it effectively.

### Audit logging

Audit logging is essential for tracking and monitoring activities within your Microsoft 365 environment. It helps administrators detect and respond to potential security incidents and ensures compliance with regulatory requirements.

#### Steps to implement audit logging

- **Enable unified audit logging**: Turn on unified audit logging in the Microsoft 365 compliance center to capture all user and admin activities.
- **Configure audit log retention**: Set up retention policies to ensure that audit logs are retained for the required period based on your organization's compliance needs.
- **Monitor and review logs**: Regularly monitor and review audit logs to identify any suspicious activities or potential security threats.

## Get started and deploy

### Step 1 - Review app privacy

✅ **Review your Microsoft 365 apps privacy settings**

The privacy settings in your Microsoft 365 apps can affect the availability of Microsoft 365 Copilot features. To ensure that users can access Copilot features, review the privacy settings in your Microsoft 365 apps.

To learn more, see [Microsoft 365 Copilot and privacy controls for connected experiences](microsoft-365-copilot-privacy.md#microsoft-365-copilot-and-privacy-controls-for-connected-experiences).

### Step 2 - Evaluate data governance maturity and data security controls

✅ **[need to add a line here]**

Before deploying Microsoft 365 Copilot, it is essential to evaluate your organization's data governance maturity and data security controls. This can be achieved by completing the Microsoft 365 Copilot Optimization Assessment. Based on the outcomes of the assessment, determine your path forward to ensure that your organization is ready for Copilot deployment.

### Step 3 - Update channels

✅ **Use the Current Channel or Monthly Enterprise Channel to update apps**

Microsoft 365 Copilot follows the Microsoft 365 Apps standard practice for deployment and updates. It's available in all update channels, *except* for Semi-Annual Enterprise Channel.

Your options:

- **Production** channels include **Current Channel** and **Monthly Enterprise Channel**.

  - **Current Channel** provides your users with the newest Microsoft 365 app features as soon as they're ready. It provides the best experience for a fast-moving product, like Copilot.

  - **Monthly Enterprise Channel** gives more predictability of when these new Microsoft 365 app features are released each month. It's a good option for organizations that want to validate the new features before they're released to the Current Channel.

- **Preview** channels include **Current Channel (Preview)** and **Beta Channel**.

  Preview channels are a great option to validate the product before rolling out to the rest of organization. To learn more, see [Overview of update channels](/deployoffice/updates/overview-update-channels) and [Microsoft 365 Insider channels](/deployoffice/insider/compare-channels).

There are multiple ways you can manage channels for user devices. To learn more, see [Change update channel of Microsoft 365 to enable Copilot](/deployoffice/updates/change-channel-for-copilot).

### Step 4 - Provision Microsoft 365 Copilot licenses

✅ **Assign Copilot licenses using the Microsoft 365 admin center**

The next step is to assign licenses so users can start using Copilot. You can manage Microsoft 365 Copilot licenses in the Microsoft 365 admin center. You can assign to individual users or to groups of users, and also reassign licenses to other users.

- To access license management in the [Microsoft 365 admin center](https://admin.microsoft.com), select **Billing** > **Licenses**.

When licenses are assigned, Copilot shows up in the Microsoft 365 apps, like Word and Excel. To use Copilot, users sign into the app with their work or school account and the file must be editable (not read only).

To learn more, see:

- Enable Copilot in your organization at [Enable users for Microsoft 365 Copilot](microsoft-365-copilot-enable-users.md).
- You can assign licenses in bulk to [groups of users through the Azure admin center](/entra/identity/users/licensing-groups-assign) or [assign licenses to users with PowerShell](/microsoft-365/enterprise/assign-licenses-to-user-accounts-with-microsoft-365-powershell). For more information, see [Assign Microsoft 365 licenses to users](/microsoft-365/admin/manage/assign-licenses-to-users).

### Step 5 - Configure settings for Copilot

✅ **Configure more Copilot features**

In the [Microsoft 365 admin center](https://admin.microsoft.com) > **Copilot**, there are more Copilot features that benefit admins and settings you can configure that benefit your organization.

You can:

- View the status of Copilot license assignments
- Access the latest information on Copilot
- Manage data security and compliance controls
- Submit feedback on behalf of users
- Configure plugins and permissions
- Enable the use of web data as grounding data in Copilot

To learn more, see [Manage Microsoft 365 Copilot with the Copilot page](microsoft-365-copilot-page.md).

### Step 6 - Deploy to some users and measure adoption

✅ **Create a group of early adopters**

There are many uses of Microsoft 365 Copilot across the various Microsoft 365 productivity apps. And, there are opportunities for users to find value in different ways.

To help drive adoption, create a group of early adopters. This group can help you understand how users are using Copilot and how it's valuable to them.

1. Identify users across various business groups in your organization, ideally with high usage of existing Microsoft 365 features. You can identify these users by [reviewing usage metrics](/microsoft-365/admin/activity-reports/microsoft365-apps-usage-ww) in the [Microsoft 365 admin center](https://admin.microsoft.com).

2. Assign these users Microsoft 365 Copilot licenses and onboard them using the resources available at the [Microsoft 365 Copilot adoption hub](https://adoption.microsoft.com/), including the [user onboarding kit](https://adoption.microsoft.com/copilot/user-onboarding-toolkit/).

3. As these users get more comfortable with using Copilot, they can speak to how they use it best, and where it's most valuable for them. This information provides you with product champions that can help other users adopt and use Copilot across your organization.

    With your established community of early adopters or Champions, they can better speak to their peers within their organization and contextualize the value of Copilot to best suit their needs. This framework also provides IT departments with a scalable way to handle questions through Champions, developing a team of experts across your organization.

    To learn more about driving adoption, visit the [Microsoft 365 Copilot adoption hub](https://adoption.microsoft.com/Copilot/).

✅ **Get insights and user sentiment**

To measure the impact of Copilot on your organization, use the [Copilot Dashboard from Viva Insights](/viva/insights/org-team-insights/copilot-dashboard). Viva Insights gives organizational leaders and IT decision makers insights into readiness, adoption, impact, and user sentiment.

To learn more, see:

- [Open the Microsoft Copilot Dashboard (Preview) from Viva Insights](https://aka.ms/copilotdashboard)
- [Learn more about the Microsoft Copilot Dashboard (Preview) from Viva Insights](/viva/insights/org-team-insights/copilot-dashboard)

## Copilot with Commercial Data Protection

To enhance data security, enable commercial data protection in Copilot for all users in your organization. Follow these steps:

- **Log into Copilot**: Access Copilot on copilot.microsoft.com and flip the Work/Web toggle to Web. Check if commercial data protection is enabled by looking for the green Protected pill by the user profile.
- **Review documentation**: Review the Copilot with commercial data protection documentation to ensure that commercial data protection is available for your users.

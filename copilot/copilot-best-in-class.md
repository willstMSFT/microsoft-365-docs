---
title: Get your data ready for Microsoft 365 Copilot with E5 license
description: The Best in Class deployment for Microsoft 365 Copilot uses a E5 license, SharePoint Advanced Management, and Microsoft Purview. These services help your organization get ready for Copilot. This IT admin guide helps you prevent oversharing, declutter data sources, and monitor site changes. Get your organization and data ready for Copilot by following the steps in this article.
f1.keywords:
- NOCSH
ms.author: mandia
author: MandiOhlinger
manager: dougeby
ms.date: 10/28/2024
audience: Admin
ms.topic: get-started
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

# Microsoft 365 Copilot best in class deployment - admin guide

> [!WARNING]
> This article is a work in progress for Ignite. Do not publish.

[Microsoft 365 Copilot](microsoft-365-copilot-overview.md) is an AI-powered productivity tool that uses large language models (LLMs).

This article provides prescriptive guidance on how IT admins can prepare their organization and their data for Copilot.

When getting your organization and your data for Copilot, there are three options:

- **[Baseline](need link)**
- **[Core](copilot-core.md)**
- **Best in Class (this article)** - Microsoft 365 E5 + SharePoint Advanced Management (SAM)

To learn more about these options, including the different license options, see [Overview](new article / need link).

In the **Best in Class** Microsoft 365 Copilot deployment, you use the features included with your Microsoft 365 E5 and Microsoft 365 Copilot licenses. With these features, you:

- Use SAM to help prevent oversharing, declutter data sources, and monitor SharePoint site changes.
- Use Microsoft Purview to apply sensitivity labels, detect sensitive info & restrict endpoints, and keep necessary content (or delete the content you don't need).

When you use the features described in this article, your organization is better prepared for Copilot, including getting accurate results from Copilot.

This article applies to:

- Microsoft 365 Copilot
- Microsoft SharePoint Premium - SharePoint Advanced Management (SAM)
- Microsoft Purview

## Before you begin

- Microsoft recommends you start with the steps in [Baseline](need link). In Baseline, you optimize your search in SharePoint, update sharing settings in SharePoint & OneDrive, and check permissions & site access on your SharePoint sites.

  To learn more, see [Baseline](need link).

- The following licenses are required to use the features in this article:

  - [Microsoft 365 E5](https://www.microsoft.com/microsoft-365/enterprise/e5) or [Office 365 E5](https://www.microsoft.com/microsoft-365/enterprise/office-365-e5)
    - [Microsoft Purview](/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-purview-service-description) - Included with your E5 license

  > [!TIP]
  > For a list of the features and services you get with your license, see [Microsoft 365, Office 365, Enterprise Mobility + Security, and Windows 11 Subscriptions](https://aka.ms/M365EnterprisePlans).

  - [Microsoft 365 Copilot](microsoft-365-copilot-licensing.md)

    - [Microsoft SharePoint Premium - SharePoint Advanced Management](/sharepoint/advanced-management#licensing) - Included with your Copilot license

    Depending on your subscription plan, you might be able purchase Microsoft 365 Copilot licenses through the [Microsoft 365 admin center](https://admin.microsoft.com) (**Billing** > **Purchase services**), Microsoft partners, or your Microsoft account team.

    Microsoft 365 Copilot licenses are available as an add-on to other licensing plans. To learn more, see [Understand licensing for Microsoft 365 Copilot](microsoft-365-copilot-licensing.md).

- This article uses the following admin centers. These admin centers require a specific role to complete the tasks in the article.

  - **[SharePoint admin center](https://go.microsoft.com/fwlink/?linkid=2185219)**: Sign in as the [SharePoint administrator](/sharepoint/sharepoint-admin-role).
  - **[Microsoft Purview portal](https://purview.microsoft.com)**: There are different roles, depending on the task you need to complete. To learn more, see:

    - [Permissions required to create and manage sensitivity labels](/purview/get-started-with-sensitivity-labels#permissions-required-to-create-and-manage-sensitivity-labels)
    - [Roles and role groups in Microsoft Defender for Office 365 and Microsoft Purview](/defender-office-365/scc-permissions)

## Step 1 - Use SharePoint Advanced Management (SAM) features

In addition to the SharePoint steps you completed in [Baseline](add link), there are more features in [SharePoint Advanced Management (SAM)](/sharepoint/get-ready-copilot-sharepoint-advanced-management) that can help you get ready for Copilot.

✅ **Copilot goals with SAM**:

[!div class="checklist"]

- Declutter data sources by finding and removing inactive SharePoint sites.
- Identify SharePoint sites with overshared or sensitive content.
- Use policy to restrict access to SharePoint sites that are business critical or have sensitive content.
- Monitor site changes.

This section walks you through different SAM features that can help you get your organization and your data ready for Copilot.

To learn more about SAM + Copilot, see [Get ready for Copilot with SharePoint Advanced Management](/sharepoint/get-ready-copilot-sharepoint-advanced-management).

### Ensure all sites have valid owners

✅ **Run a [Site Ownership policy](/sharepoint/tbd) that finds any sites that don't have at least two owners**

A Site ownership policy automatically detects sites that don't have at least two owners and help to find potential owners. Set up the policy in simulation mode to identify owners based on your desired criteria. Then upgrade the policy to Active mode to enable notifications to site owner candidates.

You need site owners to help confirm the site is still active, perform [Site access review](/sharepoint/site-access-review#review-everyone-except-external-users-site-access-review-requests-for-site-owners), update content permissions and control access when needed.

To learn more about this policy and report, see [Site ownership policy](/sharepoint/tbd).

### Find and cleanup inactive sites

✅ **Create a [site lifecycle management policy](/sharepoint/site-lifecycle-management#create-an-inactive-site-policy) that finds inactive sites**

A [site lifecycle management policy](/sharepoint/site-lifecycle-management#create-an-inactive-site-policy) automatically detects inactive sites and sends a notification email to the site owners. When you use the email, the site owners can confirm that the site is still active.

Copilot can show data from these inactive sites in user prompts, which can lead to inaccurate and cluttered Copilot results.

The policy also creates a report that you can download and review. The report shows the inactive sites, the last activity date, and the email notification status.

1. Sign in to the [SharePoint admin center](https://go.microsoft.com/fwlink/?linkid=2185219) as a SharePoint administrator.
2. Expand **Policies** > select **Site lifecycle management**.
3. Select **Create a policy**, enter your parameters, and finish your policy.
4. When the policy runs and finds inactive sites, the policy automatically emails the site owners. The site owners should confirm if the site is still active.
1. If the site owners confirm the sties aren't needed, you need to put inactive sites either in read-only mode with SAM [Inactive Sites - Read only capability](/sharepoint/tbd), or move the sites to Microsoft 365 Archive with SAM [Inactive Sites - Archive capability](/sharepoint/tbd).

To learn more about this policy and report, see [site lifecycle management policy](/sharepoint/site-lifecycle-management#create-an-inactive-site-policy).

#### Best practices for managing inactive SharePoint sites

- [**Use the policy execution report**](/sharepoint/site-lifecycle-management) to keep track on site owner action status in response to the notifications.
- Select the Get AI insights button to [**get AI insights**](/sharepoint/advanced-management#ai-insights) generated for the report to help you identify issues with the sites and possible actions to address these issues.
- **Give the site owners a timeline** to complete these tasks. If they don't complete the task within the timeframe, you can move the sites to [Microsoft 365 Archive](/microsoft-365/archive/archive-overview) using SAM [Inactive Sites - Archive capability](/sharepoint/tbd) so that you can reactive them later if needed.

> [!TIP]
> Sites moved to Microsoft 365 Archive are no longer accessible by anyone in the organization outside of Microsoft Purview or admin search. This means Copilot won't include content from these sites when responding to user prompts.

This action helps reduce outdated content that clutters Copilot's data source, which improves the accuracy of Copilot responses.

### Identify sites with overshared or sensitive content

✅ **Run [Data access governance (DAG) reports](/SharePoint/data-access-governance-reports) in the SharePoint admin center**

The [DAG reports](/SharePoint/data-access-governance-reports) give more detailed information about site sharing links, sensitivity labels, and the **`Everyone except external users`** (EEEU) permissions on your SharePoint sites. Use these reports to find overshared sites.

Overshared sites are sites that are shared with more people than needed. Copilot can show data from these sites in user prompts.

1. Sign in to the [SharePoint admin center](https://go.microsoft.com/fwlink/?linkid=2185219) as a SharePoint administrator.
2. Select **Reports** > **Data access governance**. Your report options:

    | Report | Description | Task |
    | --- | --- | --- |
    | **Sharing links** | Shows the sites that have sharing links, including links shared with **Anyone**, shared with **People in your organization**, and shared with **Specific people** outside of your work or school. | Review these sites. <br/><br/>Make sure the sites are shared with only the users or groups that need access. Remove sharing for unneeded users and groups. |
    | **Sensitivity labels applied to files** | Shows sites with Office files that have sensitivity labels. | Review these sites.<br/><br/> Make sure the correct labels are applied. Update the labels as needed. To learn more, see [Identify and label sensitive data](#identify-and-label-sensitive-data) (in this article). |
    | **Shared with `Everyone except external users` (EEEU)** | Shows the sites that are shared with everyone in your organization except external users. | Review these sites. <br/><br/> Determine if EEEU permissions are appropriate. Many sites with EEEU are overshared. Remove the EEEU permission and assign to the users or groups as needed. |
    |**Oversharing Baseline Report for Sites, OneDrives and Files**|Scans all sites in your tenant, and lists sites that share content with more than a specified number of users (you specify the number).|Sort, filter or download the report, and identify the sites with potentially overshared content.|

You can run any of these reports individually or run all of them together. To learn more about these reports, see [Data access governance (DAG) reports](/sharepoint/data-access-governance-reports).

#### Best practices for managing the DAG reports

- **Run these reports weekly**, especially in the beginning stages of adopting Copilot. As you become more familiar with the reports and the data, you can adjust the frequency.

  If you have an admin team, create an admin task to run these reports and review the data.

  Your organization is paying for the license to run these reports and use the data to make decisions. Make sure you're getting the most out of it.

- Select the Get AI insights button to [**get AI insights**](/sharepoint/advanced-management#ai-insights) generated for the report to help you identify issues with the sites and possible actions to address these issues.

### Control access to overshared SharePoint sites

✅ **Initiate [Site access reviews](/sharepoint/site-access-review) by site owners**

From a Data access governance (DAG) report, you can select sites with oversharing risks, then initiate site access reviews. Site Owners receive notification for each site that requires attention. They can use the Site reviews page to track and manage multiple review requests.

The site owner reviews access in two main areas: SharePoint groups and individual items to determine whether the broad sharing is appropriate, or it's indeed oversharing and requires remediation.

If the site owner determines that the content is indeed overshared, they can take easy remediation actions by using the Access Review dashboard to update permissions.

✅ **Use [restricted access control policy (RAC)](/sharepoint/restricted-access-control) in the SharePoint admin center**

A [restricted access control policy](/sharepoint/restricted-access-control) restricts access to SharePoint sites and content to users in a specific group. Users not in the group can't access the site or its content, even if they previously had permissions or a shared link.

When users in the group have permissions to the content, then that content can show in Copilot results. Users not in the group don't see this info in their Copilot results. You can set up restricted access control for individual sites or OneDrive.

✅ **Use [restricted content discoverability policy (RCD)](/sharepoint/tbd) in the SharePoint admin center**

Different from RAC, the restricted content discoverability policy leaves site access unchanged but prevents the site's content from being surfaced in Microsoft 365 Copilot or organization-wide Search for all users. 

The SharePoint Admin can set restricted content discoverability on individual sites.

#### Best practices for control access to overshared SharePoint sites

- If your organization has a [Zero Trust](/security/zero-trust/copilots/zero-trust-microsoft-365-copilot) mindset, then you can apply RAC to all sites. Then, adjust the permissions as needed. If you have many sites, this action can help you quickly secure your sites. But, it can cause disruptions to users.

- If you use RAC or RCD, make sure you communicate the changes and the reasons for the changes.

> [!TIP]
> For business-critical sites, you can also:
>
> - When you create new sites, configure a RAC or RCD policy as part of your custom site provisioning process. This step proactively avoids oversharing.
> - Consider blocking downloads from selected sites using a block download policy. For example, [block the download of Teams meeting recordings and transcripts](/microsoftteams/block-download-meeting-recording).
> - Apply encryption with "extract rights" enforced on business-critical office documents. To learn more, see [Microsoft Purview data security and compliance protections for generative AI apps](/purview/ai-microsoft-purview).

### Monitor changes

✅ **Run the [change history report](/sharepoint/change-history-report) in the SharePoint admin center**

The [change history report](/sharepoint/change-history-report) tracks and monitor changes, including what changed, when the change happened, and who initiated the change. The intent is to identify recent changes that could lead to oversharing, which impacts Copilot results.

Use this report to review the changes made to your SharePoint sites and organization settings.

1. Sign in to the [SharePoint admin center](https://go.microsoft.com/fwlink/?linkid=2185219) as a SharePoint administrator.
2. Expand **Reports** > select **Change history** > **New report**.
3. Your report options:

    | Report | Description | Task |
    | --- | --- | --- |
    | **Site settings report** | Shows the site property changes and actions ran by Site Administrators and SharePoint Administrators. | Review the changes and actions. Make sure the actions meet your security requirements. |
    | **Organization settings report** | Shows changes made to organization settings, like when a site is created and if external sharing is enabled. | Review the changes and actions. Make sure the changes meet your security requirements. |

#### Best practices for managing the change history reports

- **Run these reports weekly**, especially in the beginning stages of adopting Copilot. As you become more familiar with the reports and the data, you can adjust the frequency.

  If you have an admin team, create an admin task to run these reports and review the data.

  Your organization is paying for the license to run these reports and use the data to make decisions. Make sure you're getting the most out of it.

- Create a report for the **site level changes and the organization level changes**. The site level reports show changes made to the site properties and actions. The organization level reports show changes made to the organization settings.

- **Review the sharing settings and access control settings**. Make sure the changes align with your security requirements. If they don't align, then work with the site owners to correct the settings.

- **Apply [restricted access control (RAC)](/SharePoint/restricted-access-control)** to sites that appear to be overshared. Inform the site owners of the changes and why.

  If your organization has a [Zero Trust](/security/zero-trust/copilots/zero-trust-microsoft-365-copilot) mindset, then you can apply RAC to all sites. Then, adjust the permissions as needed. If you have many sites, this action can help you quickly secure your sites. But, it can also cause disruptions to users. Make sure you communicate the changes and the reasons for the changes.

## Step 2 - Restrict SharePoint Search (RSS)

✅ **Copilot goal: Disable RSS**

As you get ready for Copilot, you review and configure the correct permissions on your SharePoint sites. In [Baseline](need link), you might have enabled Restricted SharePoint Search (RSS).

RSS is a temporary solution that gives you time to review and configure the correct permissions on your SharePoint sites. You add the reviewed & corrected sites to an allowed list.

- If your SharePoint site permissions are set correctly, then disable RSS.

  When disabled, SharePoint search accesses all your SharePoint sites. When users enter prompts, Copilot can show data from all your sites, which shows more relevant and complete information in the response.

  The goal is to disable RSS and allow SharePoint search to access all your sites. This action gives Copilot more data to work with, which can improve the accuracy of the responses.

  **OR**

- If you enabled RSS, then add more sites to the allowed list. You can add up to 100 sites to the allowed list. Copilot can show data from the allowed list sites in user prompts.

  Remember, your goal is to review & configure the correct permissions on your SharePoint sites, and disable RSS.

To learn more, see:

- [Restricted SharePoint Search](/sharepoint/restricted-sharepoint-search)
- [Curate the allowed list for Restricted SharePoint Search](/sharepoint/restricted-sharepoint-search-allowed-list)
- [Blog - Introducing Restricted SharePoint Search to help you get started with Copilot for Microsoft 365](https://techcommunity.microsoft.com/t5/microsoft-365-copilot/introducing-restricted-sharepoint-search-to-help-you-get-started/ba-p/4071060)

### Disable RSS and remove sites from the allowed list

1. Use the `Set-SPOTenantRestrictedSearchMode` PowerShell cmdlet to disable RSS.
1. Use the `Remove-SPOTenantRestrictedSearchAllowedSite` PowerShell cmdlet to remove sites from the allowed list.

To learn more about these cmdlets, see [Use PowerShell Scripts for Restricted SharePoint Search](/sharepoint/restricted-sharepoint-search-admin-scripts).

### Add sites to the RSS allowed list

1. Get a list of the sites that you want to add to the allowed list.

    - **Option 1 - Use the Sharing links report**

      1. Sign in to the [SharePoint admin center](https://go.microsoft.com/fwlink/?linkid=2185219) as a SharePoint administrator.
      1. Select **Reports** > **Data access governance** > **Sharing links** > **View reports**.
      1. Select one of the reports, like **"Anyone" links**. This report shows a list of sites with the highest number of **Anyone** links created. These links let anyone access files and folders without signing in. These sites are candidates to allow in tenant/org wide search.

    - **Option 2 - Use the sort and filter options for Active sites**

      1. Sign in to the [SharePoint admin center](https://go.microsoft.com/fwlink/?linkid=2185219) as a SharePoint administrator.
      1. Select **Sites** > **Active sites**.
      1. Use the sort and filter options to find the most active site, including page views. These sites are candidates to allow in a tenant/organization wide search.

          :::image type="content" source="media/copilot-best-in-class/sharepoint-active-sites-filter.png" alt-text="In SharePoint admin center, select active sites and then use the All sites filter.":::

2. Use the `Add-SPOTenantRestrictedSearchAllowedList` PowerShell cmdlet to add the sites to the allowed list.

    To learn more about this cmdlet, see [Use PowerShell Scripts for Restricted SharePoint Search](/sharepoint/restricted-sharepoint-search-admin-scripts).


## Step 3 - Use Microsoft Purview features

In addition to the SharePoint steps you completed in [Baseline](add link), there are more features in [Microsoft Purview](/purview/copilot-in-purview-overview) that can help you get ready for Copilot.

✅ **Copilot goals with Purview**:

[!div class="checklist"]

- Identify and label sensitive data in your Microsoft 365 and Office files.
- Detect and protect sensitive information from unauthorized sharing or leakage.
- Delete the content you don't need.
- Detect sensitive data and noncompliant content in Copilot prompts and responses.
- Review and analyze Copilot prompts and responses.

To learn more about Microsoft Purview, see [Microsoft 365 Copilot in Microsoft Purview Overview](/purview/copilot-in-purview-overview).

### Identify and label sensitive data

✅ **Create and apply [sensitivity labels](/purview/get-started-with-sensitivity-labels) to your documents, emails, and meetings**

[Sensitivity labels](/purview/sensitivity-labels) are a way to identify and classify the sensitivity of your organization's data. When they're applied to items, like documents and emails, the labels add an extra layer of protection.

The sensitivity labels can also affect Copilot results, including:

- The label settings include protection actions, like access to sites, customizable headers and footers, and encryption.
- If the label applies encryption, Copilot checks the usage rights for the user. For Copilot to return data from that item, the user must be granted permissions to copy from it.
- In Copilot Business Chat that can reference data from different types of items, sensitivity labels are visible in returned results. The latest response displays the sensitivity label with the [highest priority](/purview/sensitivity-labels#label-priority-order-matters).
- If Copilot creates new content from labeled items, the sensitivity label from the source item is automatically inherited.
- Sensitivity labels go with the content, even if the content moves outside Microsoft 365.

This section walks you through the steps to create and use the default sensitivity labels from Microsoft Purview. If you need to use your own label names and configurations, then create the labels manually or edit the default labels. If you already created your own sensitivity labels, then you can't create the default labels. To learn more about sensitivity labels, see:

- [Get started with sensitivity labels](/purview/get-started-with-sensitivity-labels)
- [Default labels and policies to protect your data](/purview/mip-easy-trials)
- [Microsoft Purview strengthens information protection for Copilot](/purview/ai-microsoft-purview#microsoft-purview-strengthens-information-protection-for-copilot)

> [!NOTE]
> You can enable sensitivity labels at the container-level, like SharePoint sites. When sensitivity labels are configured for groups and sites, items in the container don't inherit the sensitivity label. So, there isn't a direct impact to Copilot responses.
>
> However, the label settings can restrict access to the container, which provides an extra layer of security, like enforcing Conditional Access and setting the default sharing link for a site. As a result, if a user can't access the site, Copilot can't access the site on behalf of that user.
>
> To learn more, see [Use sensitivity labels to protect content in Microsoft Teams, Microsoft 365 groups, and SharePoint sites](/purview/sensitivity-labels-teams-groups-sites).

#### 1. Create the default sensitivity labels

1. Sign into the [Microsoft Purview portal](https://purview.microsoft.com/) as an admin in one of the groups listed at [Sensitivity labels - permissions](/purview/get-started-with-sensitivity-labels#permissions-required-to-create-and-manage-sensitivity-labels).

2. Select **Solutions** > **AI Hub** > **Overview**.
3. In the **Recommendations** section, select **Fortify your data security for AI**. This step creates the default labels and their policies.
4. To see or edit the default labels, or to create your own labels, select **Information protection** > **Sensitivity labels**. You might have to select **Refresh**.

When you have sensitivity labels:

- The labels help protect your data and can affect Copilot results.
- Your users can start manually applying published labels to their files and emails.
- Admins can start creating policies and configuring features that automatically apply labels to files and emails.

#### 2. Publish your labels and educate your users

1. If you're using the default sensitivity labels, the labels are automatically published to all users, even if you edit the labels.

    If you created your own sensitivity labels, then add your labels to a publishing policy. When they're published, users can manually apply the labels in their Office apps. These publishing policies also have settings that you need to consider, like a default label and requiring users to label their data.

    To learn more, see [Publish sensitivity labels by creating a label policy](/purview/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy).

2. Educate your users and provide guidance on when to apply the correct sensitivity label.

    In addition to manually applying labels, the default label policy includes applying the **General \ All Employees (unrestricted)** label as the default label. This label offers a base layer of protection. But, users should change the label if needed, especially for more sensitive content that requires encryption.

    To help you with this step, see [End-user documentation for sensitivity labels](/purview/get-started-with-sensitivity-labels#end-user-documentation-for-sensitivity-labels).

3. Monitor your labels. Select **Information protection** > **Reports**. You can see the usage of your labels.

#### 3. Enable sensitivity labels for files in SharePoint and OneDrive

This step is a one-time configuration that's required to enable sensitivity labels for SharePoint and OneDrive. It's also required for Microsoft 365 Copilot to access encrypted files stored in these locations.

As with all tenant-level configuration changes for SharePoint and OneDrive, it takes about 15 minutes for the change to take effect. Then users can select sensitivity labels in Office on the web and you can create policies that automatically label files in these locations.

You have two options:

- **Option 1**: Select **Information Protection** > **Sensitivity labels**. If you see the following message, select **Turn on now**:

  :::image type="content" source="media/copilot-best-in-class/purview-sensitivity-labels-prompt.png" alt-text="In Microsoft Purview Information Protection, turn on sensitivity labels for SharePoint and OneDrive." lightbox="media/copilot-best-in-class/purview-sensitivity-labels-prompt.png":::

- **Option 2**: Use the `[Set-SPOTenant](/powershell/module/sharepoint-online/set-spotenant)` Windows PowerShell cmdlet.

To learn more about this configuration, see [Enable sensitivity labels for files in SharePoint and OneDrive](/purview/sensitivity-labels-sharepoint-onedrive-files).

> [!TIP]
> Although not related to Copilot, now is a good time to [enable co-authoring for encrypted files](/purview/sensitivity-labels-coauthoring), if it's not already enabled. This setting ensures the best user experience for collaboration.

#### 4. Set default sensitivity labels for your SharePoint document libraries

This configuration is appropriate when your document libraries store files with the same level of sensitivity.

The SharePoint site admin can do this task.

1. In your SharePoint site, select **Documents** > **Settings** icon > **Library settings** > **More library settings**.
2. In **Default sensitivity labels** (Apply label to items in this list or library), select a sensitivity label from the drop-down list, like **Confidential**
3. **Save** your changes.

When set:

- SharePoint automatically applies the label to the files, which can include [files with a lower sensitivity label](/purview/sensitivity-labels-sharepoint-default-label#will-an-existing-label-be-overridden).
- It provides a baseline level of protection that's specific to the document library. It doesn't require content inspection and doesn't rely on end users.

To learn more, see:

- [Overview - Default sensitivity labels for SharePoint document libraries](/purview/sensitivity-labels-sharepoint-default-label)
- [Steps - Add a sensitivity label to SharePoint document library](https://support.microsoft.com/office/add-a-sensitivity-label-to-sharepoint-document-library-54b1602b-db0a-4bcb-b9ac-5e20cbc28089)

#### 5. Automatically apply sensitivity labels to files and emails

You can automatically apply labels to files in SharePoint sites, OneDrive accounts, Exchange emails, and Office files. Automatic labeling helps to identify a higher priority label for more sensitive information that might need a more restrictive setting than a default label.

- For the specific steps and information that you need to know, including learning about simulation mode for auto-labeling policies, see [Apply a sensitivity label to content automatically](/purview/apply-sensitivity-label-automatically).

**Client-side auto-labeling vs. service-side auto-labeling**:

- When you auto-label documents and emails in use by Word, Excel, PowerPoint, and Outlook, it's using client-side auto-labeling. Users see the label automatically applied in their Office apps, or you can recommend the appropriate label to the user.
- When you auto-label documents stored in all SharePoint or OneDrive sites, and all emails sent using Exchange Online, it's using service-side auto-labeling. There isn't any user interaction. You can label at scale for files at rest in OneDrive and SharePoint, and all emails that are sent and received.

If you created the default sensitivity labels and policies, they include both [client-side auto-labeling](/purview/mip-easy-trials#client-side-auto-labeling) and [service-side auto-labeling](/purview/mip-easy-trials#service-side-auto-labeling) to detect credit card numbers and personal data. These default settings make it easy for you to test the auto-labeling functionality.

You can edit or create your own auto-labeling settings to help identify your organization data that needs a specific sensitivity label to apply protection actions, like encryption.

### Detect and protect sensitive information from unauthorized sharing or leakage

✅ **Use [data loss prevention (DLP) policies](/purview/dlp-learn-about-dlp) to detect sensitive info**

[Data loss prevention (DLP)](/purview/dlp-learn-about-dlp) helps organizations protect sensitive information and prevent unauthorized sharing or leakage. Basically, it helps prevent users from sharing sensitive data with people who shouldn't have it.

The intent is to dynamically protect sensitive information, like financial data, social security numbers, and health records, from being overshared.

When DLP policies find this data, it can act and help prevent the data from showing up in Copilot results.

With DLP policies, you can also use the [trainable classifier tool](/purview/trainable-classifiers-get-started-with) to identify categories of content, like source code, financial documents, and HR.

This section walks you through the steps to create DLP policies for Microsoft Teams & your Windows and macOS endpoints, and use Adaptive Protection policies integrated with **Insider Risk Management** and DLP.

To learn more about DLP, see [Learn about data loss prevention in Microsoft Purview](/purview/dlp-learn-about-dlp).

#### 1. Open the Microsoft Purview portal

1. Sign into the [Microsoft Purview portal](https://purview.microsoft.com/) as one of the admins listed at [Create and deploy DLP policies - Permissions](/purview/dlp-create-deploy-policy).
2. Select **Solutions** > **Data Loss Prevention**.

#### 2. Create the default DLP policies

For Exchange Online, SharePoint Online, and OneDrive, you can use DLP to identify, monitor, and automatically protect sensitive information across emails and files, including files stored in Microsoft Teams file repositories.

Specifically, you configure DLP to inspect emails and files for sensitive information.

1. In **Data Loss Prevention**, select **Overview**.
2. In **Protect sensitive info**, you might see a list of sensitive information types that DLP already detected in your organization:

    :::image type="content" source="media/copilot-best-in-class/purview-dlp-protect-sensitive-info.png" alt-text="In Microsoft Purview Data Loss Prevention, go to protect sensitive info and view the sensitive information detected by DLP." lightbox="media/copilot-best-in-class/purview-dlp-protect-sensitive-info.png":::

3. Select **Get started** > **Create selected policies**. This step creates the default policies:

    :::image type="content" source="media/copilot-best-in-class/purview-dlp-create-default-policies.png" alt-text="In Microsoft Purview Data Loss Prevention, go to protect sensitive info and create the default policies." lightbox="media/copilot-best-in-class/purview-dlp-create-default-policies.png":::

    By default, Exchange Online emails, SharePoint sites, and OneDrive accounts are automatically enabled locations for all users within the tenant. So when you create a DLP policy, the policy automatically applies to these locations.

4. To create a new DLP policy, select **Policies** > **Create policy**.

    When you create your own policy, you can choose the category, like Financial or Medical. If your organization has sensitive information in these areas, then you should create a custom DLP policy.

    To learn more, see:

    - [Design a DLP policy](/purview/dlp-policy-design)
    - [Create and Deploy DLP policies](/purview/dlp-create-deploy-policy)

#### 3. Create a DLP policy for Teams

These policies can detect when sensitive info, like bank account numbers or passport numbers, are shared in Teams messages. Then, you can create policy tips to educate users or add actions that control sharing.

By default, Purview includes some policies for Teams that you can enable.

1. In **Data Loss Prevention**, select **Overview**.
2. Scroll down to see the following policies:

    - Start monitoring unprotected sensitive info in Teams
    - Automatically configure Teams DLP policies to protect files shared in team messages

    You can turn on these policies and also review the settings in the policy:

    :::image type="content" source="media/copilot-best-in-class/purview-dlp-default-policy-teams.png" alt-text="In Microsoft Purview Data Loss Prevention (DLP), turn on the unprotected sensitive info in Teams policy.":::

3. If you're getting started with DLP policies, then enable these default policies. If you're more experienced or want to create your own policies, then you can.

To learn more, see:

- [Create and Deploy data loss prevention policies](/purview/dlp-create-deploy-policy)
- [Teams DLP Policies](/purview/dlp-teams-default-policy)
- [Data loss prevention and Microsoft Teams](/purview/dlp-microsoft-teams)

#### 4. Create an endpoint DLP policy for your Windows and macOS devices

On the devices (also called endpoints), these policies can block specific apps, apply different restrictions to a specific group of printers, and block specific browsers from accessing files.

1. In **Data Loss Prevention**, select **Overview**.
2. Select **Turn on advanced classification**. This action enables the endpoint DLP policies:

    :::image type="content" source="media/copilot-best-in-class/purview-dlp-endpoint-enable.png" alt-text="In Microsoft Purview Data Loss Prevention (DLP), select the turn on advanced classification setting to enables DLP policies." lightbox="media/copilot-best-in-class/purview-dlp-endpoint-enable.png":::

3. In **Overview**, select the settings icon (top right corner) > **Data Loss Prevention**:

    :::image type="content" source="media/copilot-best-in-class/purview-dlp-solution-settings.png" alt-text="In Microsoft Purview Data Loss Prevention (DLP), select settings and then select Data Loss Prevention.":::

4. In **Endpoint DLP settings**, you can see all the different type of settings you can configure. To learn more about these policy settings, see [Configure endpoint data loss prevention settings](/purview/dlp-configure-endpoint-settings).

To learn more about DLP policies for endpoints, see:

- [Get started with endpoint data loss prevention](/purview/endpoint-dlp-getting-started)
- [Configure endpoint data loss prevention settings](/purview/dlp-configure-endpoint-settings)
- [Use Endpoint data loss prevention](/purview/endpoint-dlp-using)

> [!NOTE]
> If you use a mobile device managment (MDM) service to manage and help protect you devices, like [Microsoft Intune](/mem/intune/fundamentals/what-is-intune), then keep using your MDM provider. The endpoint DLP policies focus on data loss prevention with your Microsoft 365 data. MDM focuses on device management. You use them simulatenously.

#### 5. Create Adaptive Protection policies

[Adaptive Protection](/purview/dlp-adaptive-protection-learn) policies integrate **Insider Risk Management** with DLP. When [insider risk](/purview/insider-risk-management-adaptive-protection) identifies a user that's engaging in risky behavior, the user is dynamically assigned an [insider risk level](/purview/insider-risk-management-adaptive-protection#insider-risk-levels), like **Elevated**.

Adaptive Protection can automatically create DLP policies that help protect the organization against the risky behavior associated with the insider risk level. As the insider risk level changes for users, the DLP policies applied to users can also adjust.

**Turn on Adaptive Protection**:

1. Sign into the [Microsoft Purview portal](https://purview.microsoft.com/) as one of the admins listed at [Adaptive Protection - Permissions](/purview/insider-risk-management-adaptive-protection#permissions-for-adaptive-protection).
2. Select **Solutions** > **Insider Risk Management** > **Adaptive Protection**.
3. In **Dashboard**, select **Quick setup**.

    - [Adaptive Protection - Quick Setup](/purview/insider-risk-management-adaptive-protection) is the easiest and fastest way to get started with Adaptive Protection. It automatically creates and dynamically assigns the insider risk policies, DLP policies, and a Conditional Access policy.

      When the risk level is met, the policies automatically adjust to match the new risk level.

    - You can also create a [custom policy](/purview/insider-risk-management-adaptive-protection#custom-setup) instead of using the quick setup. If you create a custom policy, then you must also create the DLP and Conditional Access policies.

To learn more, see [Adaptive Protection policies](/purview/insider-risk-management-adaptive-protection).

#### 6. Test and monitor your policies

- For DLP policies, you can:

  - **Test your policies** using [simulation mode](/purview/dlp-test-dlp-policies). Simulation mode allows you to see the effect of an individual policy without enforcing the policy. Use it to find the items that match your policy.

  - **Monitor your policies** with alerts and built-in reports, including risky user activities outside of DLP policies.

    To learn more, see:

    - [Viewing policy application results](/purview/insider-risk-management-activities)
    - [Get started with the data loss prevention analytics](/purview/dlp-analytics-get-started)

- When you enable Adaptive Protection and your policies are configured, you can get policy metrics, users with an assigned risk level, and the policies currently in-scope for the user.

  To learn more, see:

  - [Help dynamically mitigate risks with Adaptive Protection](/purview/insider-risk-management-adaptive-protection)
  - [Investigate insider risk management activities](/purview/insider-risk-management-activities)

### Delete the content you don't need

✅ **Use [data lifecycle management](/purview/data-lifecycle-management) for automatic data retention or deletion**

[Data lifecycle management](/purview/data-lifecycle-management) uses retention policies and optionally, retention labels. They're typically used to retain content for compliance reasons and can also automatically delete stale information.

For example, your organization might have regulatory requirements that require you to keep content for a certain period of time. Or, you might have content that you want to delete because it's old, outdated, or no longer needed.

If you have stale data in your organization, then create and use retention policies. These policies help Copilot return more accurate information from your documents and emails.

Retention policies can also retain Copilot prompts and responses for compliance requirements, even if [users delete their Copilot activity](https://support.microsoft.com/office/delete-your-microsoft-365-copilot-activity-history-76de8afa-5eaf-43b0-bda8-0076d6e0390f). To learn more, see [Learn about retention for Copilot](/purview/retention-policies-copilot).

Settings in a retention policy apply at the container level, like a SharePoint site or an Exchange mailbox. These settings are automatically inherited by the data in that container. If you need [exceptions for individual emails or documents](/purview/create-retention-labels-data-lifecycle-management), then use retention labels. For example, you have a retention policy to delete data in OneDrive if the data is older than one year. But, users can apply retention labels to keep specific documents from automatic deletion.

1. To create retention policies, sign into the [Microsoft Purview portal](https://purview.microsoft.com/) as a Compliance Administrator.

    To learn more about the permissions, see [Data Lifecycle Management - Permissions](/purview/get-started-with-data-lifecycle-management#permissions-for-retention-policies-and-retention-labels).

2. Select **Solutions** > **Data Lifecycle Management** > **Policies** > **Retention policies**.

3. Select **New retention policy** and follow the instructions. For more specific information, see [Create and configure retention policies](/purview/create-retention-policies).

4. If needed, create and apply retention labels.

   You can use either **Data Lifecycle Management** or **Records Management** to create the labels. Records management includes more configuration options, like a [disposition review process](/purview/disposition). A disposition review is helpful if you need manual confirmation before items are automatically deleted.
  
    # [Data Lifecycle Management](#tab/dlm)

    Use [Data Lifecycle Management](/purview/data-lifecycle-management) for retention policies that manage automatic retention and deletion for Microsoft 365 workloads & Microsoft 365 Copilot interactions, and retention labels for any exceptions.

    - From **Data Lifecycle Management**, select **Retention labels** > **Create a label**.

    Follow the configuration instructions and if you need more help, see [How to create retention labels for data lifecycle management](/purview/create-retention-labels-data-lifecycle-management#how-to-create-retention-labels-for-data-lifecycle-management).

     # [Records Management](#tab/rm)

    Use [Records Management](/purview/records-management) for retention labels that provide more configuration options for high-value documents and emails that typically have stricter compliance requirements. If you want to use a disposition review, then you must use Records Management.

    1. Sign in to the [Microsoft Purview portal](https://purview.microsoft.com/) as a member of the Records Management admin role group.

        To learn more about the permissions, see [Records management - Permissions](/purview/get-started-with-records-management#permissions)

    2. Select **Solutions** > **Records Management**.

    3. Select **File plan** > **Create a label** > **Retention label**.

        Follow the configuration instructions and if you need more help, see [Use file plan to create and manage retention labels](/purview/file-plan-manager).

    ---

    After you've created the retention labels, you can then apply the labels to documents and emails:

    - [Publish retention labels and apply them in apps](/purview/create-apply-retention-labels)
    - [Automatically apply a retention label to retain or delete content](/purview/apply-retention-labels-automatically)

5. If you applied retention labels, monitor them to see how they're being used.

    1. Sign into the [Microsoft Purview portal](https://purview.microsoft.com/) as one of the admins listed at:

        - [Content explorer - Permissions](/purview/data-classification-content-explorer)
        - [Activity explorer - Permissions](/purview/data-classification-activity-explorer#permissions)

    2. Use [Content explorer](/purview/data-classification-content-explorer) to get information on the items using retention labels.

        There are a few ways to open Content Explorer:

        - **Data Loss Prevention** > **Explorers**
        - **Records Management** > **Explorers**
        - **Information protection** > **Explorers**

    3. Use [Activity explorer](/purview/data-classification-activity-explorer) to get a historical view of activities on your content that has retention labels. There are different filters you can use.

        There are a few ways to open Activity Explorer:

        - **AI Hub**
        - **Data Loss Prevention** > **Explorers**
        - **Records Management** > **Explorers**
        - **Information protection** > **Explorers**

To learn more, see:

- [Learn about retention policies and retention labels](/purview/retention)
- [Common settings for retention policies and retention label policies](/purview/retention-settings)

### Detect sensitive data and noncompliant content in Copilot interactions

✅ **Create [Communication Compliance policies](/purview/communication-compliance) to monitor interactions with Microsoft 365 Copilot**

[Communication Compliance](/purview/communication-compliance) can detect, capture, and act on potentially inappropriate messages in your organization. The inappropriate content includes sensitive or confidential information, harassing or threatening language, and sharing of adult content.

Communication Compliance comes with some predefined policies that help you get started. We recommend you use these predefined templates. You can also create your own custom policies.

These policies monitor and evaluate prompts and responses with Copilot.

1. Sign into the [Microsoft Purview portal](https://purview.microsoft.com/) as one of the admins listed at [Communication Compliance - Permissions](/purview/communication-compliance-configure#step-1-required-enable-permissions-for-communication-compliance).

2. Select **Solutions** > **Communication Compliance** > **Overview**.

    If there are some required steps listed, then complete them. To learn more about these steps, see [Set up and create communication compliance policy](/purview/communication-compliance-configure).

3. For the predefined policies, select **Create policy** > **Detect Microsoft 365 Copilot interactions**:

    :::image type="content" source="media/copilot-best-in-class/purview-communication-compliance-default-policy.png" alt-text="In Microsoft Purview Communication Compliance, create the detect Microsoft 365 Copilot interactions policy.":::

    This Copilot policy helps you get started. There are also other predefined templates you can use. At any time, you can also create your own custom policies.

    To learn more, see:

    - [Configure a communication compliance policy to detect for Copilot interactions](/purview/communication-compliance-copilot)
    - [Create and manage communication compliance policies](/purview/communication-compliance-policies)

4. Monitor your policies. Regularly review the policy reports and audit logs to see any policy matches & resolved items, including activity by users.

    To learn more, see [Use communication compliance reports and audits](/purview/communication-compliance-reports-audits).

To learn more, see:

- [Learn about communication compliance](/purview/communication-compliance)
- [Get started with communication compliance](/purview/communication-compliance-configure)
- [Create Communication Compliance policies](/purview/communication-compliance-policies)

### Review and analyze Copilot prompts and responses

✅ **Use [AI Hub](/purview/ai-microsoft-purview) or [eDiscovery](/purview/edisc) to analyze Copilot user prompts and responses**

When users enter a prompt and get a response from Copilot, you can view and search these interactions. Specifically, these features help you:

- Find sensitive information or inappropriate content included in Copilot activities.
- Respond to a data spillage incident when confidential or malicious information is released through Copilot-related activity.
- With eDiscovery, you can remove sensitive information or inappropriate content included in Copilot activities.

There are two ways to review and analyze Copilot prompts and responses - **AI Hub** and **eDiscovery**.

# [AI Hub](#tab/aihub)

[AI Hub](/purview/ai-microsoft-purview#microsoft-purview-ai-hub-provides-insights-policies-and-controls-for-ai-apps) is a central location in the Microsoft Purview portal that proactively monitors AI use. It includes eDiscovery and you can use it to analyze and review Copilot prompts and responses.

1. Sign into the [Microsoft Purview portal](https://purview.microsoft.com/) as an admin in one of the groups listed at [AI Hub - Permissions](/purview/ai-microsoft-purview-permissions).
2. Select **Solutions** > **AI Hub** > **Activity Explorer**.
3. Select an existing activity in the list. For example, if there's a **Sensitive info types detected** activity, select it.
4. Select **View related AI interaction activity**. In **Interaction details**, you can see the app, and the prompt & response. You can also export an activity.

To learn more, see:

- [Microsoft Purview AI Hub](/purview/ai-microsoft-purview-considerations)
- [AI Hub - Activity explorer events](/purview/ai-microsoft-purview-considerations#activity-explorer-events)

# [eDiscovery](#tab/edisc)

[eDiscovery](/purview/edisc) uses cases to identify, hold, export, and analyze content found in mailboxes and sites. You can this feature to analyze Copilot prompts and responses, and delete Copilot data.

1. Sign into the [Microsoft Purview portal](https://purview.microsoft.com/) as an admin in one of the groups [eDiscovery - Permissions](/purview/ediscovery-assign-permissions).
2. Select **Solutions** > **eDiscovery** > **Cases**.
3. Create a **case** and a **search** query. A search query searches in-place content, like email, documents, and instant messaging conversations.

    When you create a search query, you enter the [Data sources that have Copilot data](/purview/edisc-search-copilot-data#data-sources-for-copilot-data).

4. The data returned is the Copilot prompts and responses. You can review and export this information. If the data contains sensitive information, you can also delete it.

To learn more, see [Search for and optionally delete Copilot interactions in eDiscovery](/purview/edisc-search-copilot-data).

---

## Related content

- [Microsoft 365 Copilot requirements and prerequisites](/copilot/microsoft-365/microsoft-365-copilot-requirements)
- [Provision Microsoft 365 Copilot](/copilot/microsoft-365/microsoft-365-copilot-setup)

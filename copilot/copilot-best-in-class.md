---
title: Get your data ready for Microsoft 365 Copilot with E5 license
description: The Best in Class deployment for Microsoft 365 Copilot uses a E5 license, SharePoint Advanced Management, and Microsoft Purview. These services help your organization get ready for Copilot. This IT admin guide helps you prevent oversharing, declutter data sources, and monitor site changes. Get your organization and data ready for Copilot by following the steps in this article.
f1.keywords:
- NOCSH
ms.author: mandia
author: MandiOhlinger
manager: dougeby
ms.date: 10/14/2024
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
  - ✅ Microsoft SharePoint Premium Advanced Management
  - ✅ Microsoft Purview
---

# Microsoft 365 Copilot - Best in class deployment

> [!WARNING]
> This article is a work in progress for Ignite. Do not publish or share with anyone.

This article builds on what you did in [Baseline](need link??). In the **Best in Class** Microsoft 365 Copilot deployment, you use the features included with your Microsoft 365 E5 license and SharePoint Advanced Management (SAM). When you use these features, you can help prevent oversharing, declutter data sources, and monitor site changes. You also use Purview to enable sensitivity labels for files in SharePoint and OneDrive.

Get your organization and data ready for Copilot by following the steps in this article. You can use Copilot to its full potential and get the best results.

??Mention difference between Microsoft Copilot vs Microsoft 365 COpilot

This article applies to:

- Microsoft 365 Copilot
- Microsoft SharePoint Premium - SharePoint Advanced Management (SAM)
- Microsoft Purview

## Before you begin

- License requirements

  - Microsoft 365 E5
  - [Microsoft SharePoint Premium - SharePoint Advanced Management](/sharepoint/advanced-management)
  - Microsoft Purview (included with Microsoft 365 E5)
    - eDiscovery Premium
    - Microsoft Purview Information Protection

    [Microsoft Purview service description and licensing info](/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-purview-service-description)

- Role requirements

  - SharePoint administrator


## Features

- Conditional Access based on identity risk
- Detect noncompliant usage

## Step 1 - Restrict SharePoint Search (RSS) (introduced in Baseline)

✅ **Copilot goal: Disable RSS**

In the **get-ready for Copilot phase**, you review and configure the correct permissions on your SharePoint sites. As a temporary solution, you can use Restricted SharePoint Search. RSS allows you to restrict search results to a specific set of sites that you allow, called the allowlist.

RSS is a temporary solution that gives you time to review and configure the corrections permissions on your SharePoint sites.

- If your site permissions are set correctly, then disable RSS. When disabled, SharePoint search accesses all your sites. When users enter prompts, Copilot can show data from all your sites, which shows more relevant and complete information in the response.

  The goal is to disable RSS and allow SharePoint search to access all your sites. This action gives Copilot more data to work with, which can improve the accuracy of the responses.

  OR

- If you enabled RSS, add more sites to the allowlist. You can add up to 100 sites to the allowlist. Copilot can show data from the allowlist sites in user prompts.

  Remember, your goal is to review & configure the correct permissions on your SharePoint sites, and disable RSS. ??ADD: What about new sites, and automatically creating them w/the correct permissions??

### Steps to disable RSS

??Add steps

### Steps to add sites to the RSS allowlist

??Add steps

## Step 2 - Use SharePoint Advanced Management (SAM) features

In addition to the SharePoint steps you completed in [Baseline](add link), there are more features in [SharePoint Advanced Management (SAM)](/sharepoint/get-ready-copilot-sharepoint-advanced-management) that can help you with Copilot.

**Copilot goals with SAM**:

[!div class="checklist"]

- Prevent oversharing.
- Declutter data sources.
- Monitor site changes.

To learn more about SAM, see [Get ready for Copilot with SharePoint Advanced Management](/sharepoint/get-ready-copilot-sharepoint-advanced-management).

### Identify sites with overshared or sensitive content

✅ **Run [Data access governance (DAG) reports](/SharePoint/data-access-governance-reports) in the SharePoint admin center**

The DAG reports give more detailed information about site sharing link, sensitivity labels, and the **`Everyone except external users`** (EEEU) permissions on your SharePoint sites. Use these reports to find overshared sites.

1. Sign in to the [SharePoint admin center](https://go.microsoft.com/fwlink/?linkid=2185219) as a SharePoint administrator.
2. Select **Reports** > **Data access governance**.
3. Your report options:

    | Report | Description | Task |
    | --- | --- | --- |
    | **Sharing links reports** | Shows the sites that have sharing links, including links shared with anyone, shared with people in your organization, and shared with specific people outside of your work or school. | Review these sites. <br/><br/>Make sure the sites are shared with only the users or groups that need access. Remove sharing for unneeded users and groups. |
    | **Sensitivity labels applied to files** | Shows sites with  Office files that have sensitivity labels. | Review these sites.<br/><br/> Make sure the correct labels are applied. Update the labels as needed. |
    | **Shared with `Everyone except external users` (EEEU)** | Shows the sites that are shared with everyone in your organization except external users. | Review these sites. <br/><br/> Determine if EEEU permissions are appropriate. Many sites with EEEU are overshared. Remove the EEEU permission and assign to the users or groups as needed. |

You can run any of these reports individually or run all of them together.

To learn more about these reports, see [Data access governance (DAG) reports](/SharePoint/data-access-governance-reports).

#### Best practices for managing the DAG reports

- **Run these reports weekly**, especially in the beginning stages of adopting Copilot. As you become more familiar with the reports and the data, you can adjust the frequency.

  If you have an admin team, create an admin task to run these reports and review the data.

  Your organization is paying for the license to run these reports and use the data to make decisions. Make sure you're getting the most out of it.

- **Share the report data with site owners**. The site owners should:

  - Update or remove unneeded shared links. The goal is to only allow access to the users that need it.
  - Review and update the sensitivity labels. Make sure the correct labels are applied.
  - Determine if EEEU permissions are needed. If the permission isn't needed, then remove the EEEU permission and assign to individual users or groups as needed.

  ??Bulk action to update??

- **Give the site owners a timeline** to complete these tasks. If they don't complete the task within the timeframe, admins can restrict access using [restricted access control (RAC)](/SharePoint/restricted-access-control).

- **Apply [restricted access control (RAC)](/SharePoint/restricted-access-control)** to sites that appear to be overshared. Inform the site owners of the changes and why.

  If your organization has a [Zero Trust](/security/zero-trust/copilots/zero-trust-microsoft-365-copilot) mindset, then you can apply RAC to all sites. Then, adjust the permissions as needed. If you have many sites, this action can help you quickly secure your sites. But, it can also cause disruptions to users. Make sure you communicate the changes and the reasons for the changes.

### Find and cleanup inactive sites

✅ **Create a site lifecycle management policy that finds inactive sites**

A [site lifecycle management policy](/sharepoint/site-lifecycle-management#create-an-inactive-site-policy) automatically detects inactive sites and sends a notification email to the site owners. When you use the email, the site owners can confirm that the site is still active.

The policy also creates a report that you can download and review. The report shows the inactive sites, the last activity date, and the email notification status.

1. Sign in to the [SharePoint admin center](https://go.microsoft.com/fwlink/?linkid=2185219) as a SharePoint administrator.
2. Expand **Policies** > select **Site lifecycle management**.
3. Select **Create a policy**, enter your parameters, and finish your policy.
4. When the policy runs and finds inactive sites, the policy automatically emails the site owners. It also creates the report. Use this report to work with the site owners to determine the next steps, like deleting the site.

To learn more about this policy and report, see [site lifecycle management policy](/sharepoint/site-lifecycle-management#create-an-inactive-site-policy).

#### Best practices for managing inactive SharePoint sites

- **Use the inactive sites policy report** and work with the site owners on the future of their site. The site owners should confirm if the site is still active:

  - If the site isn't active, the owner can move any files they want to keep, and then delete the site.
  - If the site is still active, the owner can review the files, and update the data so it's still accurate.

  This action helps reduce outdated content that clutters Copilot's data source, which improves the accuracy of Copilot responses.

- **Give the site owners a timeline** to complete these tasks. If they don't complete the task within the timeframe, admins can [delete the inactive site](/sharepoint/delete-site-collection).

- **[Delete the inactive site](/sharepoint/delete-site-collection)**. Before you delete a site, inform the site owners and subsite owners of the changes, why the site is being deleted, and when it'll be deleted.

  ??Bulk action to delete? Does the site lifecycle management policy email give the delete option??

**??Site access review (Add to existing task)??**

### Monitor changes

✅ **Run the [change history report](/sharepoint/change-history-report) in the SharePoint admin center**

The [change history report](/sharepoint/change-history-report) tracks and monitor changes, including what changed, when the change happened, and who initiated the change. The intent is to identify recent changes that could lead to oversharing.

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

## Step 3 - Use Microsoft Purview features

In addition to the steps you completed in [Baseline](add link), there are more features in [Microsoft Purview](/purview/copilot-in-purview-overview) that can help you with Copilot.

**Copilot goals with Purview**:

[!div class="checklist"]

- Enable and use sensitivity labels to label your Microsoft 365 and Office files.
- DLP something
- Retention something
- Compliance something

To learn more about Purview, see [Microsoft 365 Copilot in Microsoft Purview Overview](/purview/copilot-in-purview-overview).

### Classify and identify sensitive data

✅ **Enable and use sensitivity labels on your documents, emails, and meetings**

Sensitivity labels are a way to classify and identify the sensitivity of your organization's files and meetings. When they're applied to items, like documents and emails, the labels add an extra layer of protection. They can also affect Copilot results, including:

- Copilot Business Chat can reference data from different types of items. The sensitivity label with the [highest priority](/purview/sensitivity-labels#label-priority-order-matters) is visible to users.
- If the label applies encryption, Copilot checks the usage rights for the user. For Copilot to return data from that item, the user must be granted permissions to copy from it.
- Sensitivity labels go with the content, even if the content is moved outside Microsoft 365.

When you apply sensitivity labels to your files and meetings, there's an order that you should follow. The order helps you start labeling at the top, and working your way down to individual files. The order:

1. Apply sensitivity labels at the container level (Microsoft Teams sites, Microsoft 365 Groups, and SharePoint sites).
2. Set the default sensitivity label for all your SharePoint document libraries. When you set the default, SharePoint can automatically apply the label to the files.
3. Enable sensitivity labels for files in SharePoint and OneDrive.
4. Automatically apply sensitivity labels to unlabeled files in SharePoint sites, OneDrive accounts, Exchange emails, and Office files.

This section walks you through the steps to enable and use sensitivity labels. To learn more about sensitivity labels, see:

- [Default labels and policies to protect your data](/purview/mip-easy-trials)
- [Automatically apply sensitivity labels](/purview/apply-sensitivity-label-automatically)

> [!NOTE]
> This section uses the default sensitivity labels included with Microsoft Purview. At anytime, you can create your own custom sensitivity labels, and use your custom labels instead.
>
> To learn more, see [Create and configure sensitivity labels and their policies](/purview/create-sensitivity-labels).

1. Sign into the [Microsoft Purview portal](https://purview.microsoft.com/) as an admin in one of the groups listed at [Sensitivity labels - permissions](/purview/get-started-with-sensitivity-labels#permissions-required-to-create-and-manage-sensitivity-labels)
2. **Turn on the default sensitivity labels**:

    1. Select **Solutions** > **AI Hub** > **Policies**.
    1. Select **Fortify your data security for AI** > **Get started** > **Create policies**.

        :::image type="content" source="media/copilot-best-in-class/purview-ai-hub-enable-default-labels.png" alt-text="In Microsoft Purview portal, open the AI Hub and create the Fortify your data security for AI policies to turn on sensitivity labels." lightbox="media/copilot-best-in-class/purview-ai-hub-enable-default-labels.png":::

    1. To see the default labels, select **Information protection** > **Sensitivity labels**. You might have to select **Refresh**.

    When the default labels are turned on:

    - Your users can start manually applying labels to their files and emails.
    - Admins can start creating policies and configuring features that automatically apply labels to files and emails.
    - The labels help protect your data and can affect Copilot results.

3. **Automatically apply a sensitivity label** to the following containers:

    - Microsoft Teams sites
    - Microsoft 365 Groups
    - SharePoint sites

    **Steps**:

    1. At the container level, there's a set of one-time steps you need to complete, including [enabling sensitivity labels in Microsoft Entra ID and syncing the labels using Windows PowerShell](/purview/sensitivity-labels-teams-groups-sites#how-to-enable-sensitivity-labels-for-containers-and-synchronize-labels).

        After you complete these one-time steps, you can apply sensitivity labels to the groups and sites. More built-in sensitivity labels also become available.

    2. In **Information protection** > **Sensitivity labels**, select an existing label > **Edit label**. When you enable the default sensitivity labels, the label settings are automatically configured for you.

        - **Scope** - Make no changes, unless you want to. The scope of each default label is automatically set to **File** (applies to Office apps, like Word and Excel) and **Emails** (applies to Outlook and Outlook on the web).

          Optionally, you can add **Meetings** (applies to Teams and Outlook). Or, you can create your own custom label and set the scope to include Meetings. It's your choice.

        - **Groups & sites** - Select this option. This setting allows the label to apply to Microsoft Teams, Microsoft 365 Groups, and SharePoint sites containers.

          If **Groups & sites** is grayed out, then you didn't complete the [one-time steps in Microsoft Entra ID and Windows PowerShell](/purview/sensitivity-labels-teams-groups-sites#how-to-enable-sensitivity-labels-for-containers-and-synchronize-labels) in the previous step.

        - **Define protection settings for groups and sites** - This option is available when you select **Groups & sites**. Select the protection settings that you want to apply to the groups and sites. To help you determine the best option for your organization, see [How to configure groups and site settings](/purview/sensitivity-labels-teams-groups-sites#how-to-configure-groups-and-site-settings).

          :::image type="content" source="media/copilot-best-in-class/purview-sensitivity-label-groups-sites.png" alt-text="When you create a sensitivity label in Microsoft Purview, select groups and sites, and then define the protection settings." lightbox="media/copilot-best-in-class/purview-sensitivity-label-groups-sites.png":::

          If you [created your own custom labels](/purview/create-sensitivity-labels), then you set the label properties. You can edit your custom labels and change the scope to include **Groups & sites**.

          To learn more, see [Use sensitivity labels to protect content in Microsoft Teams, Microsoft 365 groups, and SharePoint sites](/purview/sensitivity-labels-teams-groups-sites)

    3. **Publish your labels**. For the steps, see [Publish sensitivity labels by creating a label policy](/purview/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy).
    4. **Monitor your labels**. Select **Information protection** > **Reports**. You can see the usage of your labels, including the usage of your sensitivity labels.

4. **Set a default sensitivity label** for all your SharePoint document libraries. The SharePoint site admin can do this task.

    1. In SharePoint, go to the document library > **Settings** > **Library settings**.
    2. In **Default sensitivity labels**, select the label in the drop-down list, like Confidential.
    3. **Save** your changes.

    When set:

    - SharePoint automatically applies the label to the files, including files with a lower sensitivity label.
    - It helps protect your documents without requiring anyone to review the content.

    To learn more, see:

    - [Overview - Default sensitivity labels for SharePoint document libraries](/purview/sensitivity-labels-sharepoint-default-label)
    - [Steps - Add a sensitivity label to SharePoint document library](https://support.microsoft.com/office/add-a-sensitivity-label-to-sharepoint-document-library-54b1602b-db0a-4bcb-b9ac-5e20cbc28089)

    ??Set this via policy instead of relying on site admins??

5. **Enable sensitivity labels for files in SharePoint and OneDrive**. When enabled, users can manually apply labels to Office files stored in SharePoint and OneDrive, and change any existing label. Admins can create policies that automatically apply labels.

    You have two options:

    - **Option 1**: Select **Information Protection** > **Sensitivity labels**. If you see the following message, select **Turn on now**:

      :::image type="content" source="media/copilot-best-in-class/purview-sensitivity-labels-prompt.png" alt-text="In Microsoft Purview Information Protection, turn on sensitivity labels for SharePoint and OneDrive." lightbox="media/copilot-best-in-class/purview-sensitivity-labels-prompt.png":::

    - **Option 2**: Use the `[Set-SPOTenant](/powershell/module/sharepoint-online/set-spotenant)` Windows PowerShell cmdlet

      To learn more about these options, see [Enable sensitivity labels for files in SharePoint and OneDrive](/purview/sensitivity-labels-sharepoint-onedrive-files).

6. **Automatically apply sensitivity labels to unlabeled files** in SharePoint sites, OneDrive accounts, Exchange emails, and Office files. When they're automatically applied, you don't have to rely on end users to apply labels to their files.

    1. Automatically label unlabeled files in SharePoint sites & OneDrive accounts, and unlabeled emails in Exchange:

        - For the specific steps and information that you need to know, including learning about simulation mode, see [How to configure autolabeling policies for SharePoint, OneDrive, and Exchange](/purview/apply-sensitivity-label-automatically#how-to-configure-auto-labeling-policies-for-sharepoint-onedrive-and-exchange).

        - When creating the policy, make sure you select all the locations you want to autolabel. For example, if you don't want to autolabel emails, then don't select Exchange. You can also create separate policies for each location type.

          :::image type="content" source="media/copilot-best-in-class/purview-sensitivity-labels-auto-label-policy.png" alt-text="In Microsoft Purview, select Exchange email, SharePoint sites, and OneDrive accounts to automatically apply sensitivity labels to unlabeled files." lightbox="media/copilot-best-in-class/purview-sensitivity-labels-auto-label-policy.png":::

        - When creating the policy, you must create at least one rule. These rules must have a [sensitive info type](/purview/sit-sensitive-information-type-learn-about) condition. You can also use [Trainable classifiers](/purview/trainable-classifiers-learn-about). Be familiar with these features before you create the autolabeling policy.

        - Know the existing label you want to automatically apply. You can only select one label for each autolabel policy.

    2. Automatically label Office files & emails, and require users to apply labels on their Office files. When you publish a sensitivity label, the label shows up in your Office apps. At any time, users can also manually apply the label to their files and emails.

        - When you add the default label or create your own (**Information Protection** > **Sensitivity labels** > select a label > **Edit label**), enable the **Auto-labeling for files and emails** setting. This setting automatically applies the sensitivity label to the files and emails that match the conditions you set.

          :::image type="content" source="media/copilot-best-in-class/purview-edit-sensitivity-label-auto-label.png" alt-text="In Microsoft Purview Information Protection, edit an existing sensitivity label and select the autolabeling for files and emails setting." lightbox="media/copilot-best-in-class/purview-edit-sensitivity-label-auto-label.png":::

        - When you publish the label (**Information Protection** > **Sensitivity labels** > **Policies** > **Publishing policies**), enable the **Require users to apply a label to their email and documents** setting. This setting forces users to apply the label to their files and emails.

          :::image type="content" source="media/copilot-best-in-class/purview-sensitivity-labels-publish-require-users.png" alt-text="In Microsoft Purview Information Protection, publish a label and select the require users to apply a label to their email and documents setting." lightbox="media/copilot-best-in-class/purview-sensitivity-labels-publish-require-users.png":::

        To learn more about sensitivity labels in Office apps, see [Manage sensitivity labels in Office apps](/purview/sensitivity-labels-office-apps).

### Detect and protect sensitive information

✅ **Use data loss prevention (DLP) policies to detect sensitive info and restrict endpoints**

DLP is a security feature in Microsoft Purview. It can help organizations protect sensitive information and prevent unauthorized sharing or leakage. Basically, it helps prevent users from inappropriately sharing sensitive data with people who shouldn't have it.

The intent is to dynamically protect sensitive information from being overshared and reduce the risk of oversharing across instant messages and user endpoints.

For example, you can create a DLP policy that ??

With DLP policies, you can also:

- Use the [trainable classifier tool](/purview/trainable-classifiers-get-started-with) to identify categories of content, like source code, financial documents, and HR.
- ??Mention something about sensitivity labels??

This section walks you through the steps to create DLP policies for Microsoft Teams & your Windows and macOS endpoints, and use Adaptive Protection policies integrated with **Insider Risk Management** and DLP.

To learn more about DLP, see [Learn about data loss prevention in Microsoft Purview](/purview/dlp-learn-about-dlp).

1. Sign into the [Microsoft Purview portal](https://purview.microsoft.com/) as one of the admins listed at [Create and deploy DLP policies - Permissions](/purview/dlp-create-deploy-policy).
2. Select **Solutions** > **Data Loss Prevention**.
3. **Create a DLP policy for Teams**. These policies can detect when sensitive info, like bank account numbers or passport numbers, are shared in Teams messages. Then, you can create policy tips to educate users or add actions that control sharing.

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

4. **Create an endpoint DLP policy** for your Windows and macOS devices (called endpoints). On the devies, these policies can block specific apps, apply different restrictions to a specific group of printers, and block specific browsers from accessing files.

    1. In **Data Loss Prevention**, select **Overview**.
    1. Select **Turn on advanced classification**. This action enables the endpoint DLP policies:

        :::image type="content" source="media/copilot-best-in-class/purview-dlp-endpoint-enable.png" alt-text="In Microsoft Purview Data Loss Prevention (DLP), select the turn on advanced classification setting to enables DLP policies." lightbox="media/copilot-best-in-class/purview-dlp-endpoint-enable.png":::

        In **Overview**, select the settings gear icon (top right corner) > **Data Loss Prevention**:

        :::image type="content" source="media/copilot-best-in-class/purview-dlp-solution-settings.png" alt-text="In Microsoft Purview Data Loss Prevention (DLP), select settings and then select Data Loss Prevention.":::

        In **Endpoint DLP settings**, you can see all the different type of settings you can configure. To learn more about these policy settings, see [Configure endpoint data loss prevention settings](/purview/dlp-configure-endpoint-settings).

    To learn more about DLP policies for endpoints, see:

    - [Get started with endpoint data loss prevention](/purview/endpoint-dlp-getting-started)
    - [Configure endpoint data loss prevention settings](/purview/dlp-configure-endpoint-settings)
    - [Use Endpoint data loss prevention](/purview/endpoint-dlp-using)

    ??Why use this instead of Intune? Or, maybe add some info about Intune providing more features admins can control??

5. **Create Adaptive Protection policies** and [automatically assign DLP policies](/purview/dlp-adaptive-protection-learn) based on the user's identified risk level.

    Adaptive Protection policies integrate **Insider Risk Management** with DLP. When [insider risk](/purview/insider-risk-management-adaptive-protection) identifies a user that's engaging in risky behavior, the user is dynamically assigned an [insider risk level](/purview/insider-risk-management-adaptive-protection#insider-risk-levels), like **Elevated**.

    Adaptive Protection can automatically create a DLP policy that helps protect the organization against the risky behavior associated with the insider risk level. As the insider risk level changes for users, the DLP policies applied to users can also adjust.

    **Turn on Adaptive Protection**:

    1. Sign into the [Microsoft Purview portal](https://purview.microsoft.com/) as one of the admins listed at [Adaptive Protection - Permissions](/purview/insider-risk-management-adaptive-protection#permissions-for-adaptive-protection).
    1. Select **Solutions** > **Insider Risk Management** > **Adaptive Protection**.
    1. In **Dashboard**, select **Quick setup**.

        [Adaptive Protection - Quick Setup](/purview/insider-risk-management-adaptive-protection) is the easiest and fastest way to get started with Adaptive Protection. It automatically creates the insider risk policies, DLP policies, and a Conditional Access policy.

        You can also create a [custom policy](/purview/insider-risk-management-adaptive-protection#custom-setup) instead of using the quick setup. The choice is yours.

    1. [automatically assign DLP policies](/purview/dlp-adaptive-protection-learn) based on the user's identified risk level.

        ??How to do this??

    To learn more, see [Adaptive Protection policies](/purview/insider-risk-management-adaptive-protection).

6. Deploy your policies (??) and regularly review your policies.

    - [Test your Data Loss Prevention policies](/purview/dlp-test-dlp-policies)
    - [Get started with the data loss prevention analytics](/purview/dlp-analytics-get-started)
    - [Investigate insider risk management activities](/purview/insider-risk-management-activities)

### ✅ Retention policies and labels

Retention labels help you retain necessary content and delete the content you don't need.

For example, there are regulations that might require you to keep content for a certain period of time. Or, you might have content that you want to delete after a certain period of time.

As admin, you can automatically apply retention labels that keep (or dispose) of content that match specific conditions, like keep documents based on their content. When the labels are created, at any time users can manually apply retention labels to their content.

- Retention labels don't persist if the content is moved outside Microsoft 365.

??How does this impact Copilot results??

1. To manage retention labels in Microsoft Purview, you have two options - **Records Management** or **Data Lifecycle Management**. Decide which option is best for your content:

    | Records management | Data Lifecycle Management |
    | --- | --- |
    | [Records management](/purview/records-management) helps you manage regulatory, legal, and business-critical records, which typically have strict compliance requirements. | [Data Lifecycle Management](/purview/data-lifecycle-management) is best for general and broader data management needs that don't have stringent requirements. It also has flexible retention and deletion policies. |

    You can use both options and create separate retention policies depending on the type of data you need to keep (or delete).

2. Create the policy and/or labels. When you create the policy and/or labels, you can set the retention period, the actions to take when the retention period expires, and the conditions that must be met for the policy to apply.

    # [Data Lifecycle Management](#tab/dlm)

    1. Sign into the [Microsoft Purview portal](https://purview.microsoft.com/) as a Compliance Administrator.

        To learn more, see [Data Lifecycle Management - Permissions](/purview/get-started-with-data-lifecycle-management#permissions-for-retention-policies-and-retention-labels).

    2. Create a **retention policy** and/or a **retention label**. Decide which option is best for your content:

        - **Retention policies** (**Data Lifecycle Management** > **Policies** > **Retention policies**) apply to the container level, like a SharePoint site or an Exchange mailbox. Content in the container automatically inherits the retention settings.
        - **Retention labels** (**Data Lifecycle Management** > **Retention labels**) apply to the file level, like a specific document or email.

        To learn more, see:

        - [Create and configure retention labels](/purview/create-retention-labels-data-lifecycle-management)
        - [Create and configure retention policies](/purview/create-retention-policies)
        - [Compare capabilities for retention policies and retention labels](/purview/retention#compare-capabilities-for-retention-policies-and-retention-labels)

    # [Records management](#tab/rm)

    1. Sign into the [Microsoft Purview portal](https://purview.microsoft.com/) as a member of the Records Management admin role group.

        To learn more, see [Records management - Permissions](/purview/get-started-with-records-management#permissions)

    2. Create a **File plan** and/or a **Label policy**. Decide which option is best for your content:

        - **File plan** (**Records Management** > **File plan**) applies item-level retention settings.
        - **Label policies** (**Records Management** > **Policies** > **Label policies**) automatically labels content based on conditions you define. Users can also manually apply in specific locations.

        To learn more, see:

        - [Use file plan to create and manage retention labels](/purview/file-plan-manager)
        - [Create an autoapply retention label policy](/purview/apply-retention-labels-automatically#how-to-create-an-auto-apply-retention-label-policy)
        - [Manually apply retention labels](/purview/create-apply-retention-labels#manually-apply-retention-labels)

    ---

3. Monitor the retention labels to see how they're being used.

    1. Sign into the [Microsoft Purview portal](https://purview.microsoft.com/) as a ??.
    2. Use [Content explorer](/purview/data-classification-content-explorer) to get information on the items using retention labels.

        There are a few ways to open Content Explorer:

        - **Data Loss Prevention** > **Explorers**
        - **Records Management** > **Explorers**

    3. Use [Activity explorer](/purview/data-classification-activity-explorer) to get a historical view of activities on your content that has retention labels. There are different filters you can use.

      There are a few ways to open Activity Explorer:

      - **AI Hub**
      - **Data Loss Prevention** > **Explorers**
      - **Records Management** > **Explorers**

To learn more, see:

- [Learn about retention policies and retention labels](/purview/retention)
- [Common settings for retention policies and retention label policies](/purview/retention-settings)
- [Publish retention labels and apply them in apps](/purview/create-apply-retention-labels)

### Detect sensitive data and noncompliant content in Copilot interactions

✅ **Create Communication Compliance policies to monitor interactions with Microsoft 365 Copilot**

Communication Compliance can detect, capture, and act on potentially inappropriate messages in your organization. This information includes sensitive or confidential information, harassing or threatening language, and sharing of adult content.

Communication Compliance comes with some predefined that help you get started. We recommend you use these predefined templates. You can also create your own custom policies.

These policies monitor and evaluate interactions with Copilot.

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

### Preserve, collect, review, analyze, and export Copilot interactions

✅ Use eDiscovery to analyze Copilot user prompts and responses

eDiscovery policies can search for Copilot activity data and delete it.

When you use Copilot, this feature helps you:

- Find and remove sensitive information or inappropriate content included in Copilot activities.
- Respond to a data spillage incident when content containing confidential or malicious information is released through Copilot-related activity.

1. Sign into the [Microsoft Purview portal](https://purview.microsoft.com/) as one of the admins listed at [Communication Compliance - Permissions]().

2. Select **Solutions** > **eDiscovery** > **Cases** > **Create Case**.
3. ?? Select **Add data sources**, and add the sources you want to search for Copilot activity data.

    For a list of data sources you can add, see [Data sources for Copilot data](/purview/ediscovery-search-and-delete-copilot-data#data-sources-for-copilot-data)

To learn more, see:

- [Search for and optionally delete Copilot interactions in eDiscovery](/purview/ediscovery-search-and-delete-copilot-data)
- [eDiscovery Premium](/purview/ediscovery-premium-get-started)


AI Hub
Search for Copilot in Purview TOC

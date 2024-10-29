---
title: "Overview of permissions in Microsoft 365 Lighthouse"
f1.keywords: CSH
ms.author: sharik
author: SKjerland
manager: scotv
ms.reviewer: taylorau
ms.date: 10/28/2024
audience: Admin
ms.topic: concept-article
ms.service: microsoft-365-lighthouse
ms.localizationpriority: medium
ms.collection:
- Tier1
- scotvorg
- M365-subscription-management
- Adm_O365
- essentials-get-started
ms.custom:
- AdminSurgePortfolib
- M365-Lighthouse                         
search.appverid: MET150
description: "For Managed Service Providers (MSPs) using Microsoft 365 Lighthouse, learn more about Lighthouse permission requirements."
---

# Overview of permissions in Microsoft 365 Lighthouse

Microsoft 365 Lighthouse permissions are primarily managed by the following:

- Lighthouse role-based access control (RBAC) in the partner tenant
- Granular delegated administrative privileges (GDAP) in the customer tenant

To use Lighthouse, you need a combination of roles assigned via RBAC and GDAP.

## Manage Lighthouse RBAC permissions in the partner tenant

Lighthouse permissions in the partner tenant are managed by assigning RBAC roles in Lighthouse. Each role has a set of permissions that determines which data users can access and change within the partner tenant.    

RBAC roles are managed from the Lighthouse permissions page in Lighthouse. To access the Lighthouse permissions page and manage permissions, you must hold one of the following roles:

- Privileged Role Administrator in Microsoft Entra ID
- Administrator in Lighthouse

To learn more, see [Manage Lighthouse RBAC permissions in Microsoft 365 Lighthouse](m365-lighthouse-manage-lighthouse-rbac-permissions.md).

The following table provides an overview of each Lighthouse RBAC role. For a list of actions each role can perform in the partner tenant, see [Lighthouse RBAC roles and capabilities](#lighthouse-rbac-roles-and-capabilities). 

| Lighthouse&nbsp;RBAC&nbsp;role | Overview |
|---|---|
| Account Manager | Account Managers have full access to Sales Advisor pages and data across the entire partner tenant. Lighthouse Account Managers can export Sales Advisor data. |
| Administrator<sup>1</sup> | Administrators have full administrative permissions in Lighthouse. Lighthouse Administrators can manage RBAC and GDAP permissions and can create baselines, tags, and alerts.<br><br>Lighthouse Administrators are automatically assigned the Privileged Role Administrator, User Administrator, and Group Administrator roles in Microsoft Entra ID and the Admin Agent role in Partner Center. |
| Operator | Operators manage customer tenants in Lighthouse based on the GDAP permissions assigned to them for each customer tenant that they manage. Lighthouse Operators can also view high-level customer tenant status and manage alerts.<br><br>**Note:** Lighthouse Administrators can use templates on the Delegated access page to assign GDAP permissions to Lighthouse users. This automatically assigns the Operator role to users for the tenants for which they have GDAP permissions.<br><br>Users in a Just-in-Time (JIT) agent support role who have no other GDAP permissions are assigned the Lighthouse Operator role only when they have elevated JIT permissions. |
| Reader<sup>1</sup> | Readers have read-only access to data in Lighthouse. Lighthouse Readers can view high-level customer tenant status and alerts. |

<sup>1</sup> Lighthouse Administrator and Lighthouse Reader roles don't provide access to customer data. Access to customer data is governed by the Lighthouse user's GDAP permissions. We recommend that you use GDAP reader roles across customer tenants to give Lighthouse users an aggregate view across all customer tenants. 

## Lighthouse RBAC roles and capabilities

The following table describes the actions that each Lighthouse RBAC role can perform in Lighthouse. For some actions, you need to hold a Microsoft Entra role in addition to a Lighthouse RBAC role. For other actions, only a Microsoft Entra role is required. Microsoft Entra role requirements are indicated in the last column of the table. For a complete list of Microsoft Entra roles and the actions they can perform, see [Microsoft Entra built-in roles](/azure/active-directory/roles/permissions-reference).

> [!NOTE]
> Users with the Microsoft Entra Global Reader role are automatically assigned the Lighthouse Reader role. Users with the Microsoft Entra Global Administrator role are automatically assigned the Lighthouse Administrator role.

| Area | Actions | Account&nbsp;Manager | Administrator | Operator | Reader | Need Entra&nbsp;role? |
|---|---|:---:|:---:|:---:|:---:|:---:|
| **Home page** | View data on cards |  |  |  |  | Yes |
|  | Add users |  |  |  |  | Yes |
|  | Reset password |  |  |  |  | Yes |
|  | Offboard users |  |  |  |  | Yes |
| **Alerts** | View alerts and alert rules | &check; | &check; |  | &check; | No |
|  | Manage alerts (change severity, status, or assignment) |  | &check; |  |  | No |
|  | Create, edit, and delete alert rules |  | &check; |  |  | No |
| **Copilot insights** | View opportunites and adoption data |  |  |  |  | Yes|
| **Tenants** | View the Tenants page | &check; | &check; | &check; | &check; | No |
|  | View tenant details |  |  |  |  | Yes |
|  | Export data | &check; | &check; | &check; | &check; | No |
|  | View tags | &check; | &check; | &check; | &check; | No |
|  | Create, update, and delete tags in Lighthouse |  | &check; |  |  | No |
|  | Assign and remove tags from tenants |  | &check; |  |  | No |
|  | Activate and inactivate a tenant |  | &check; |  |  | No |
|  | View delegated access status | &check; | &check; | &check; | &check; | No |
|  | View Microsoft Secure Score |  |  |  |  | Yes |
|  | View baseline assignments | &check; | &check; | &check; | &check; | No |
|  | View deployment status |  |  | &check; |  | Yes |
|  | View apps and services usage |  |  | &check; |  | Yes |
|  | View and edit customer contact and website info | &check; | &check; | &check; | &check; | No |
| **Users** | Search for users | | | | | Yes |
|  | View user metrics | | | | | Yes |
|  | Onboard new users | | | | | Yes |
|  | Offboard users | | | | | Yes |
|  | View inactive users | | | | | Yes |
|  | View shared mailboxes | | | | | Yes |
|  | View and manage risky users | | | | | Yes |
|  | View and manage multifactor authentication | | | | | Yes |
|  | View and manage self-service password reset | | | | | Yes |
| **Devices** | View device security data | | | | | Yes |
|  | View vulnerability management data | | | | | Yes |
|  | View device comliance data | | | | | Yes |
|  | View threat management data | | | | | Yes |
|  | View device health data | | | | | Yes |
|  | View Windows 365 data | | | | | Yes |
|  | View Windows event logs | | | | | Yes |
| **Apps** | View app performance and app management data | | | | | Yes |
| **Data protection** | View protected data | | | | | Yes | 
| **Baselines** | View baselines (default, custom) and task details |  | &check; | &check; | &check; | No|
|  | Create, clone, edit, and assign baselines | |  &check; |  |  | No |
|  | View deployment insights | | | | | Yes |
| **Service&nbsp;health** | Monitor service health<sup>1</sup> |  | &check; | &check; |  | Yes |
| **Support** | Create and manage service requests<sup>2</sup> |  | &check; |  |  | Yes |
| **Audit logs** | View audit logs |  | &check; |  |  | Yes
| **Permissions** | View the Lighthouse Permissions page | |  &check; |  |  | No|
|  | Set up and manage Lighthouse permissions |  | &check; |  |  | No |
|  | View, set up, and manage GDAP on the Delegated access page |  | &check; |  |  | No |
| **Sales Advisor** | View opportunities | &check; | &check; |  |  | No |
|  | View subscription renewals | &check; | &check; |  |  | No |
|  | View license requests | &check; | &check; |  |  | No |

<sup>1</sup> To monitor service health, Lighthouse users must have at least one Microsoft Entra role assigned to them with the following property set: **microsoft.office365.serviceHealth/allEntities/allTasks**. The users must also have at least the Admin Agent role or Helpdesk Agent role assigned to them in Partner Center. 

<sup>2</sup> To create and manage service requests, Lighthouse users must have at least one Microsoft Entra role assigned to them with the following property set: **microsoft.office365.supportTickets/allEntities/allTasks**.

## Manage GDAP in the customer tenant

GDAP gives you a high level of control and flexibility by providing access to customer tenants through [Microsoft Entra built-in roles](/azure/active-directory/roles/permissions-reference). Assigning the least-privileged roles by task to MSP technicians through GDAP reduces security risk for both MSPs and customers.  

For more information about setting up a GDAP relationship with a customer tenant in Lighthouse, see [Obtain granular admin permissions to manage a customer's service - Partner Center](/partner-center/gdap-obtain-admin-permissions-to-manage-customer). 

For more information about least-privileged roles by task, see [Least-privileged roles - Partner Center](/partner-center/gdap-least-privileged-roles-by-task) and [Least privileged roles by task in Microsoft Entra ID](/azure/active-directory/roles/delegate-by-task).  

For more information about GDAP or delegated administrative privileges (DAP) deprecation, see [GDAP frequently asked questions - Partner Center](/partner-center/gdap-faq), or search the [Partner Center announcements](/partner-center/announcements/) for dates and timelines.

For a complete list of Microsoft Entra roles and the actions they can perform, see [Microsoft Entra built-in roles](/azure/active-directory/roles/permissions-reference). For information on how to assign roles, see [Assign Microsoft Entra roles to users](/azure/active-directory/roles/manage-roles-portal).

## Related content

[Requirements for Microsoft 365 Lighthouse](m365-lighthouse-requirements.md) (article)  
[View your Microsoft Entra roles in Microsoft 365 Lighthouse](m365-lighthouse-view-your-roles.md) (article)  
[Assign roles and permissions to users - Partner Center](/partner-center/permissions-overview) (article)  
[Overview of Microsoft 365 Lighthouse](m365-lighthouse-overview.md) (article)  
[Sign up for Microsoft 365 Lighthouse](m365-lighthouse-sign-up.md) (article)  
[GDAP frequently asked questions - Partner Center](/partner-center/gdap-faq) (article)  
[Microsoft 365 Lighthouse FAQ](m365-lighthouse-faq.yml) (article)

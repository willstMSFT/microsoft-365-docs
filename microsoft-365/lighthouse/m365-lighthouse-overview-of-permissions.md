---
title: "Overview of permissions in Microsoft 365 Lighthouse"
f1.keywords: CSH
ms.author: sharik
author: SKjerland
manager: scotv
ms.reviewer: taylorau
ms.date: 01/26/2024
audience: Admin
ms.topic: article
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
- Granular Delegated Admin Privileges (GDAP) in the customer tenant

To use Lighthouse, you need a combination of roles assigned via RBAC and GDAP.

## Managing Lighthouse RBAC permissions in the partner tenant

Lighthouse permissions in the partner tenant are managed by assigning RBAC roles. Each role has a set of permissions that determines which data users can access and change within the partner tenant. Administrators in Lighthouse should use a combination of RBAC and GDAP to provide least-privileged access to data based on the tasks each user needs to perform.   

RBAC roles are managed from the Lighthouse permissions page in Lighthouse. To access the Lighthouse permissions page and manage permissions, you must have one of the following roles:

- Global Administrator in Microsoft Entra ID
- Lighthouse Administrator in Microsoft 365 Lighthouse

To learn more, see [Manage Lighthouse RBAC permissions in Microsoft 365 Lighthouse](m365-lighthouse-manage-lighthouse-rbac-permissions.md).

The following table provides an overview of the different RBAC roles. For a list of actions each role can perform in the partner tenant, see [Lighthouse RBAC roles and capabilities](#lighthouse-rbac-roles-and-capabilities). 

| Lighthouse&nbsp;RBAC&nbsp;role | Overview |
|---|---|
| Lighthouse Administrator<sup>1</sup> | Assign the Lighthouse Administrator role to users who manage the Microsoft 365 Lighthouse service, including customer tenant management, deployment plans, and alerts configuration.<br><br>Lighthouse Administrators are automatically assigned the Privileged Role Administrator role in Microsoft Entra ID, which allows them to assign Lighthouse RBAC roles. They're also automatically added to the Admin Agent group in Partner Center which, along with having the Privileged Role Administrator role, allows them to manage GDAP permissions. |
| Lighthouse Account Manager | Assign the Lighthouse Account Manager role too users who need full access to Sales Advisor pages and data. Lighthouse Account Managers can export Sales Advisor data. |
| Lighthouse Operator | The Lighthouse Operator role is automatically assigned to users with GDAP permissions in a customer tenant. A user's permissions and management capabilities are defined by the associated GDAP permissions for each customer tenant that they manage.<br><br>Users in a Just-in-Time (JIT) agent support role who have no other GDAP permissions are assigned the Lighthouse Operator role only when they have elevated JIT permissions. |
| Lighthouse Reader<sup>1</sup> | Assign the Lighthouse Reader role to users who need read-only access to data in Lighthouse, including read-only access to the Alerts, Baseline, and Tenants pages.<br><br>**Note:**GDAP permissions control which customer tenant information is viewable in Lighthouse (not including the Tenants page). |

<sup>1</sup> Lighthouse Administrator and Lighthouse Reader roles only manage Lighthouse workloads.

## Lighthouse RBAC roles and capabilities

The following table describes the actions that Lighthouse Account Managers can perform in Lighthouse.

| Area | Actions | Lighthouse&nbsp;Administrator | Lighthouse&nbsp;Account&nbsp;Manager | Lighthouse&nbsp;Operator | Lighthouse&nbsp;Reader |
|---|---|:---:|:---:|:---:|:---:|
| **Tenants** | View the Tenants page | &check; | &check; | &check; | &check; |
|  | Manage tags | &check; |  |  |  |
|  | Activate and inactivate a tenant | &check; |  |  |  |
|  | View delegated status | &check; | &check; | &check; | &check; |
|  | View baseline assignment | &check; | &check; | &check; | &check; |
|  | View deployment status | &check; | &check; | &check; | &check; |
|  | View and edit customer contact and website information | &check; | &check; | &check; | &check; |
| **Baselines** | View baselines (default, custom) | &check; |  | &check; | &check; |
|  | Create, edit, and assign baselines | &check; |  |  |  |
| **Alerts** | View alerts | &check; | &check; | &check; | &check; |
|  | Manage alerts (change severity, status, or assignment) | &check; |  | &check; |  |
|  | Create, edit, and delete alert rules | &check; |  |  |  |
| **Permissions** | Set up and manage Lighthouse permissions | &check; |  |  |  |
|  | Set up and manage GDAP | &check; |  |  |  |
|  | View GDAP status detail | &check; |  |  |  |
| **Audit logs** | View audit logs | &check; |  | &check; |  |
| **Sales Advisor** | View Sales Advisor reports and manage data | &check; | &check; |  |  |
| **Support** | Create and manage service requests<sup>1</sup> | &check; |  |  |  |
| **Service&nbsp;health** | Monitor service health<sup>2</sup> | &check; |  | &check; |  |

<sup>1</sup> To create and manage service requests, Lighthouse users must have at least one Microsoft Entra role assigned to them with the following property set: **microsoft.office365.supportTickets/allEntities/allTasks**. For a complete list of Microsoft Entra roles, see [Microsoft Entra built-in roles](/entra/identity/role-based-access-control/permissions-reference).

<sup>2</sup> To monitor service health, Lighthouse users must have at least one Microsoft Entra role in the partner tenant with the following property set: **microsoft.office365.serviceHealth/allEntities/allTasks**. For a complete list of Microsoft Entra roles, see [Microsoft Entra built-in roles](/entra/identity/role-based-access-control/permissions-reference).

## Managing GDAP in the customer tenant

GDAP gives you a high level of control and flexibility by providing access to customer tenants through [Microsoft Entra built-in roles](/azure/active-directory/roles/permissions-reference). Assigning the least-privileged roles by task through GDAP to MSP technicians reduces security risk for both MSPs and customers.  

For more information about setting up a GDAP relationship with a customer tenant in Lighthouse, see [Obtain granular admin permissions to manage a customer's service - Partner Center](/partner-center/gdap-obtain-admin-permissions-to-manage-customer).   

For more information about least-privileged roles by task, see [Least-privileged roles - Partner Center](/partner-center/gdap-least-privileged-roles-by-task) and [Least privileged roles by task in Microsoft Entra ID](/azure/active-directory/roles/delegate-by-task).  

For more information about GDAP or Delegated Admin Privileges (DAP) deprecation, see [GDAP frequently asked questions - Partner Center](/partner-center/gdap-faq), [Delegated administration privileges (DAP) FAQ - Partner Center](/partner-center/dap-faq), or search the [Partner Center announcements](/partner-center/announcements/) for dates and timelines.

## Related content

[Assign roles and permissions to users](/partner-center/permissions-overview) (article)
[Manage Lighthouse RBAC permissions in Microsoft 365 Lighthouse](m365-lighthouse-manage-lighthouse-rbac-permissions.md) (article) 
[Requirements for Microsoft 365 Lighthouse](m365-lighthouse-requirements.md) (article)
[View your Microsoft Entra roles in Microsoft 365 Lighthouse](m365-lighthouse-view-your-roles.md) (article)   
[Delegated administration privileges (DAP) FAQ](/partner-center/dap-faq) (article)  
[Overview of Microsoft 365 Lighthouse](m365-lighthouse-overview.md) (article)  
[Microsoft 365 Lighthouse FAQ](m365-lighthouse-faq.yml) (article)
[Sign up for Microsoft 365 Lighthouse](m365-lighthouse-sign-up.md) (article) 

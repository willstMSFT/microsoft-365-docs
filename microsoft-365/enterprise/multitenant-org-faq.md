---
# Required metadata
# For more information, see https://review.learn.microsoft.com/en-us/help/platform/learn-editor-add-metadata?branch=main
# For valid values of ms.service, ms.prod, and ms.topic, see https://review.learn.microsoft.com/en-us/help/platform/metadata-taxonomies?branch=main

title: Multitenant orgs FAQ
description: Frequently asked questions regarding multitenant organizations
author:      jakeost-msft # GitHub alias
ms.author:   jacob.osterloh # Microsoft alias
ms.service: microsoft-365-enterprise
ms.topic: faq
ms.date:     11/01/2024
ms.subservice: multi-tenant
---

# Multitenant org FAQ

Read about frequently asked questions for Microsoft multitenant organizations. These frequently asked questions (FAQs) are periodically updated to include new topics.

## MTO lifecycle

### How is a multitenant organization (MTO) set up?

Administrators create an [MTO ](https://techcommunity.microsoft.com/blog/microsoft_365blog/multi-tenant-organization-capabilities-now-available-in-microsoft-365/4122812)in the Microsoft 365 admin center and configure collaboration capabilities for users across the tenants. [MTO configuration](/microsoft-365/enterprise/plan-multi-tenant-org-overview?view=o365-worldwide) includes the creation of cross-tenant sync jobs. 

### Are cross tenant sync jobs auto generated when an MTO is created?

When an MTO is created or a tenant joins an MTO, cross tenant sync jobs are auto generated to enable sync between any existing tenants and the new one. However, these jobs start executing only once administrators adds specific users to the sync.  

### Can existing cross tenant sync jobs created in the EntraID portal be used?

Existing cross-tenant sync jobs with B2B collaboration member users can be used instead of auto generated ones created on MTO formation. Existing B2B members will be able to leverage MTO features once it is set up.  

### Can I delete the auto-generated MTO_Sync job created during MTO setup?  

Currently, while auto-generated MTO_Sync jobs can be deleted, they might be automatically recreated. However, you can safely ignore them.  

### What happens to the cross-tenant sync jobs when a tenant leaves an MTO? 

Cross-tenant sync jobs are unaffected when leaving an MTO. We recommend that administrators review their cross-tenant syncs, [cross-tenant sync setting](/entra/identity/multi-tenant-organizations/cross-tenant-synchronization-overview), and [automatic redemption setting](/entra/identity/multi-tenant-organizations/cross-tenant-synchronization-overview) when a tenant leaves an MTO. 

### What happens when a synced user already exists on as a B2B user on the target tenant? 

If a user exists as a B2B guest, they will not be affected by the MTO creation, and their experience will not change. If you would like existing guests to experience the MTO features, they will need to be [converted](/entra/external-id/user-properties) to member users.  

If the user exists as a B2B member, they will automatically start to experience MTO capabilities. 

### What happens when a synced user already exists as a contact on the target tenant? 

The contact objects will remain unaffected by the creation of an MTO or cross tenant sync jobs. Cross-tenant sync will create B2B member objects which might cause duplicate entries to show when the user is searched for. We recommend cleaning up main contacts before implementing MTO. [Common considerations for multitenant user management in Microsoft Entra ID - Microsoft Entra | Microsoft Learn](/entra/architecture/multi-tenant-common-considerations) 

### Can security groups be synced across tenants? 

While groups can be used to sync users across tenants via Entra CTS, the security groups themselves cannot be synced across tenants. 

### Can source attributes be mapped to different attributes on the target tenant?



Yes, you can [customize](/entra/identity/multi-tenant-organizations/cross-tenant-synchronization-configure) your attribute mappings. 

### How should ‘Visible to Users’ property be set for the cross-tenant sync jobs? 

This setting is available in the cross-tenant sync job properties in the Entra ID portal. The property determines if the app shows up on end user portals like myapps.microsoft.com. It is recommended that ‘Visible to Users’ is set to No for sync jobs.  

### Can MTO users register applications in Entra ID in other tenants? 

This would depend on what roles can register apps. A recommendation would be to restrict this to the app developer role.

### Can the access permissions of the MTO user be restricted? 

Use [Conditional Access](/entra/identity/conditional-access/overview) policies to restrict access to MTO users similar to other provisioned users.   

### Can an MTO be created across worldwide geographies?  

An MTO can span tenants in multiple locations if they are in the same cloud. However, an MTO cannot be set up between tenants that are located in different cloud environments.  For instance, if you have a tenant in the commercial cloud and another in GCCH, creating an MTO between them is not supported yet. 

### Is MTO available in special clouds? And can I set up MTO between my cloud tenants? 

MTO is available on GCC and GCC-H clouds. However, note that the MTO tenants can ONLY have tenants which are within the same cloud. 

### What is the MTO licensing requirement?

Use of the multitenant organization feature requires Microsoft Entra ID P1 licenses or above in all multitenant organization tenants. For additional details, see [Entra multitenant organization licensing requirements](/entra/identity/multi-tenant-organizations/multi-tenant-organization-overview). If you plan on utilizing [Entra cross-tenant sync](/entra/identity/multi-tenant-organizations/cross-tenant-synchronization-overview) via the Microsoft 365 admin center or Microsoft Entra ID, also see [Entra cross-tenant sync licensing requirements](/entra/identity/multi-tenant-organizations/cross-tenant-synchronization-overview). 

## Teams

### Is cross tenant sync setup sufficient to leverage MTO functionality on Teams?

MTO specific Teams functionality requires an MTO to be set up. [Here](/microsoft-365/enterprise/plan-multi-tenant-org-overview?view=o365-worldwide) is the detailed guide to setup MTO. [External access](/microsoft-365/enterprise/plan-multi-tenant-org-overview?view=o365-worldwide) policy setup and [B2B direct connect](/microsoft-365/enterprise/plan-multi-tenant-org-overview?view=o365-worldwide) policy setup that is part of the MTO setup is essential to leverage MTO functionality on Teams. Learn more about Teams multi-tenant capabilities [here](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/announcing-more-seamless-collaboration-in-microsoft-teams-for/ba-p/3901092). It is important to keep in mind that these capabilities are only available in the new Teams desktop client and the customers using web client would not see any benefits or optimized experience for MTO. 

### Do old chats get merged when a user is converted from a B2B guest to a member? 

Old chats are not merged when a user is converted from a guest to a member. The user will still see the chat thread with B2B members, however, sending new chat messages in that thread is blocked. All search entry points will redirect the user to chat with home tenant ID of the user from broader MTO group and chats going forward will not fragment.

### Can MTO users create Teams and invite guests on other tenants? 

MTO users can create teams and invite guests from other tenants. 

### Does MTO work when using Teams on the web? 

Microsoft Teams on the web is not currently supported in an MTO. However, a version of the Teams web app is being optimized for MTO features in the future. 

### A few users are unable to see all MTO tenants in the drop down. Is this expected?

It is possible that some users won’t see all MTO tenants in the account picker dropdown. This can happen when users have not been added or invited to any team in the MTO tenant that is missing from the dropdown. 

### Is the org chart and profile picture visible for MTO users? 

The org chart and profile picture are available for MTO users and can be viewed in Teams. We do recommend leveraging cross-tenant sync to sync all user properties. Users may receive inconsistent experience in Teams if expected user properties are not synced or modified during the sync. 

### Can Teams rooms be used in an MTO? 

Teams Rooms are not supported in an MTO. This means that if your organization operates in a multitenant environment, you won't be able to access Teams Rooms for your meetings and collaborations that are hosted in another tenant.

### Can an MTO user book a conference room in another tenant? 

MTO users cannot book a conference room in another tenant. 

### Can I still use Teams Federation with MTO?

There is no impact on Teams Federation. Customers will still be able to chat via that method. MTO would make Teams chat easier by providing a more seamless People search and centralized chat notification experience within the MTO group. 

## SharePoint Online (SPO)

## Viva Engage

## Security and Compliance










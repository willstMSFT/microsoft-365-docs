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

## Are cross tenant sync jobs auto generated when an MTO is created?

When an MTO is created or a tenant joins an MTO, cross tenant sync jobs are auto generated to enable sync between any existing tenants and the new one. However, these jobs start executing only once administrators adds specific users to the sync.  

## How can existing cross tenant sync jobs created in the EntraID portal be used?  

Existing cross tenant sync jobs with B2B collaboration member users will automatically have MTO features enabled upon MTO setup.

## Can I delete the auto-generated MTO_Sync job created during MTO setup?  

Currently, auto-generated MAC created MTO_Sync jobs will be recreated when visiting the MAC MTO portal. So, while they can be deleted, they will be refreshed. These jobs are safe to ignore if you do not plan to use them as they act as a placeholder for sharing users via the MAC MTO portal.

## What happens to the cross-tenant sync jobs when a tenant leaves an MTO? 

Cross-tenant sync jobs are unaffected when leaving an MTO. We recommend all admins to review their CTS jobs and policies when a tenant leaves an MTO. 

## What happens when a synced user already exists on as a B2B user on the target tenant? 

This is not recommended, as the user may have an inconsistent experience based on the differences in the various syncs. 

## What happens when a synced user already exists as a contact on the target tenant? 

Removing on-prem GAL sync and cleaning up mail contacts and distribution lists is a significant effort before implementing MTO. 

## Will users who are already present as guests be automatically converted to members? 

No, admins must convert guest users into members users if they want to enable the MTO capabilities. 

## Can security groups be synced across tenants? 

While groups can be used to sync users across tenants via Entra CTS, the security groups themselves cannot be synced across tenants. 

## How should ‘Visible to Users’ property be set for the cross-tenant sync jobs? 

This setting is available in the cross-tenant sync job properties in the Entra ID portal. The property determines if the app shows up on end user portals like myapps.microsoft.com. It is recommended that ‘Visible to Users’ is set to No for sync jobs.  

## Can MTO users register applications in Entra ID in other tenants? 

This would depend on what roles can register apps. A recommendation would be to restrict this to the app developer role.

## Can the access permissions of the MTO user be restricted? 

Use Conditional Access policies to restrict access to MTO users similar to other provisioned users.  

### Is MTO supported in special clouds?

1. Multitenant organizations is supported in GCC, GCCH and DoD  

1. Multitenant organizations is not available in Microsoft 365 China (operated by 21Vianet). 

### Cross cloud MTO?

MTO cannot be established between tenants that are located in different cloud environments.  For instance, if you have a tenant in the commercial cloud and another in GCCH, creating an MTO between them is not possible. 

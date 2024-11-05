---
title: "Understand Copilot Prompt Gallery"
f1.keywords:
- NOCSH
ms.author: camillepack
author: camillepack
manager: scotv
ms.date: 10/20/2024
audience: Admin
ms.topic: how-to
ms.service: microsoft-365-copilot
ms.localizationpriority: medium
ms.collection: 
- scotvorg
- m365copilot
- magic-ai-copilot
description: "Learn about the Copilot Prompt Gallery and how it works with your organization."
---

# Understand Copilot Prompt Gallery - admin guide

Copilot Prompt Library is a resource of Microsoft-created prompts, videos, and articles that help users understand and use Microsoft Copilot effectively. Copilot Prompt Library is available within Microsoft Copilot and online at [Copilot Prompt Library](https://copilot.cloud.microsoft/prompts).

As an admin, you can support Copilot Prompt Library adoption and success within your organization. This article covers Copilot Prompt Library architecture, data flows, security, and privacy.

## Overview

**[image pending]**

Copilot Prompt Library is a comprehensive repository that provides users with access to a catalog of Copilot prompts. The catalog includes prompts created by Microsoft that highlight key scenarios and capabilities of Microsoft Copilot, designed to help users understand and use Microsoft Copilot more effectively.

Copilot Prompt Library features videos and articles to help users get started with Copilot and maximize productivity through effective prompting. Users can save and share successful prompts, facilitating collaboration and knowledge sharing within the organization.

Each suggested prompt in the prompt library includes additional information about how to personalize it and ways to extend the prompt for even more value. This makes Copilot Prompt Library a single resource to help your users use Copilot confidently and effectively.

## Data flow and compliance

Copilot Prompt Library processes and manages data in a structured manner to ensure compliance and security. The following are key data flows and compliance considerations:

**[diagram pending]**

- Copilot Prompt Library is both a website and a feature of Copilot that allows users to discover, manage, use, and share Copilot prompts.
- A user accesses Copilot Prompt Library, either via the Copilot Prompt Library website or in Copilot through an app.
- Copilot Prompt Library accesses Microsoft-authored prompts from the public catalog.
- Copilot Prompt Library accesses user-created prompts from user, group, and tenant collections in the Microsoft 365 Substrate data store.
- The prompts are stored in collections within the Substrate Data Store, which is a storage type that allows applications to store files and data and enables efficient indexing and search. There are collections for users, groups, and tenants, all of which are within the tenant boundary. All data is encrypted, transported via a secure pipeline, and is accessible only via Substrate APIs.

---
layout: Conceptual
title: Microsoft Entra synchronization protocol overview - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/auth-prov-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Architectural guidance on integrating Microsoft Entra ID with legacy synchronization protocols
ms.topic: concept-article
ms.date: 2023-02-08T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 3e7706e4-c054-02f9-a293-ea2b5f41ee32
document_version_independent_id: a23c3b0a-edc5-2b33-e576-eb786987c52c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/auth-prov-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/auth-prov-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/auth-prov-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 2681751d-1b5e-89c7-9a82-3407f8b31921
---

# Microsoft Entra synchronization protocol overview - Microsoft Entra | Microsoft Learn

Microsoft Entra ID enables integration with many synchronization protocols. The synchronization integrations enable you to sync user and group data to Microsoft Entra ID, and then user Microsoft Entra management capabilities. Some sync patterns also enable automated provisioning.

## Synchronization patterns

The following table presents Microsoft Entra integration with synchronization patterns and their capabilities. Select the name of a pattern to see

- A detailed description
- When to use it
- Architectural diagram
- Explanation of system components
- Links for how to implement the integration

| Synchronization pattern | Directory synchronization | User provisioning |
| --- | --- | --- |
| [Directory synchronization](sync-directory) | ![check mark](media/authentication-patterns/check.png) |  |
| [LDAP Synchronization](sync-ldap) | ![check mark](media/authentication-patterns/check.png) |  |
| [System for Cross-Domain Identity Management (SCIM) synchronization](sync-scim) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) |
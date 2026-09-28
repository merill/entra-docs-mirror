---
layout: Conceptual
title: Plan a Microsoft Entra B2B collaboration deployment - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/secure-external-access-resources
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: A guide for architects and IT administrators on securing and governing external access to internal resources
ms.topic: concept-article
ms.date: 2023-04-28T00:00:00.0000000Z
ms.reviewer: gasinh
ms.subservice: architecture
locale: en-us
document_id: 9af16781-e8ef-5202-a63c-33acaaa96be9
document_version_independent_id: bf8fec1f-0582-d4d2-16ac-f692de145b88
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/secure-external-access-resources.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/secure-external-access-resources
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/secure-external-access-resources.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 203fe561-e1f7-66d2-4537-ce5d6fb81110
---

# Plan a Microsoft Entra B2B collaboration deployment - Microsoft Entra | Microsoft Learn

Secure collaboration with your external partners ensures they have correct access to internal resources, and for the expected duration. Learn about governance practices to reduce security risks, meet compliance goals, and ensure accurate access.

## Governance benefits

Governed collaboration improves clarity of ownership of access, reduces exposure of sensitive resources, and enables you to attest to access policy.

- Manage external organizations, and their users who access resources
- Ensure access is correct, reviewed, and time bound
- Empower business owners to manage collaboration with delegation

## Collaboration methods

Traditionally, organizations use one of two methods to collaborate:

- Create locally managed credentials for external users, or
- Establish federations with partner identity providers (IdP)

Both methods have drawbacks. For more information, see the following table.

| Area of concern | Local credentials | Federation |
| --- | --- | --- |
| Security | - Access continues after external user terminates - UserType is Member by default, which grants too much default access | - No user-level visibility  - Unknown partner security posture |
| Expense | - Password and multi-factor authentication (MFA) management - Onboarding process - Identity cleanup - Overhead of running a separate directory | Small partners can't afford the infrastructure, lack expertise, and might use consumer email |
| Complexity | Partner users manage more credentials | Complexity grows with each new partner, and increased for partners |

Microsoft Entra B2B integrates with other tools in Microsoft Entra ID, and Microsoft 365 services. Microsoft Entra B2B simplifies collaboration, reduces expense, and increases security.

## Microsoft Entra B2B benefits

- If the home identity is disabled or deleted, external users can't access resources
- User home IdP handles authentication and credential management
- Resource tenant controls guest-user access and authorization
- Collaborate with users who have an email address, but no infrastructure
- IT departments don't connect out-of-band to set up access or federation
- Guest user access is protected by the same security processes as internal users
- Clear end-user experience with no extra credentials required
- Users collaborate with partners without IT department involvement
- Guest default permissions in the Microsoft Entra directory aren't limited or highly restricted
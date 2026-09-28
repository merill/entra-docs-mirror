---
layout: Conceptual
title: License self-service password reset - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-sspr-licensing
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about the difference Microsoft Entra self-service password reset licensing requirements
ms.topic: concept-article
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: tilarso
locale: en-us
document_id: 650b028a-16b9-f560-a2aa-8613d85ffce6
document_version_independent_id: 0e2c2f6b-65bd-4dc8-1a45-956d20bf8a9b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-sspr-licensing.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-sspr-licensing
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-sspr-licensing.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/82f69bd7-5cb0-4163-9fd6-9103bb1a8352
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/f003597a-dab2-429a-8639-1d2acd9c0371
platformId: d61193bc-3fd2-a422-585e-ee15664e48fc
---

# License self-service password reset - Microsoft Entra ID | Microsoft Learn

To reduce help desk calls and loss of productivity when a user can't sign in to their device or an application, user accounts in Microsoft Entra ID can be enabled for self-service password reset (SSPR). Features that make up SSPR include password change, reset, unlock, and writeback to an on-premises directory. Basic SSPR features are available in Microsoft 365 Business Standard or higher and all Microsoft Entra ID P1 or P2 SKUs at no cost.

This article details the different ways that self-service password reset can be licensed and used. For specific details about pricing and billing, see the [Microsoft Entra pricing page](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).

Although some unlicensed users may technically be able to access SSPR, a license is required for any user that you intend to benefit from the service.

Note

Some tenant services are not currently capable of limiting benefits to specific users. Efforts should be taken to limit the service benefits to licensed users. This helps avoid potential service disruption to your organization once targeting capabilities are available.

## Compare editions and features

The following table outlines the different SSPR scenarios for password change, reset, or on-premises writeback, and which SKUs provide the feature.

| Feature | Microsoft Entra ID Free | Microsoft 365 Business Standard | Microsoft 365 Business Premium | Microsoft Entra ID P1 or P2 |
| --- | --- | --- | --- | --- |
| **Cloud-only user password change**When a user in Microsoft Entra ID knows their password and wants to change it to something new. | ● | ● | ● | ● |
| **Cloud-only user password reset**When a user in Microsoft Entra ID forgets their password and needs to reset it. |  | ● | ● | ● |
| **Hybrid user password change or reset with on-prem writeback**When a user in Microsoft Entra synchronized from an on-premises directory using Microsoft Entra Connect wants to change or reset their password and also write the new password back to on-premises. |  |  | ● | ● |

Warning

Standalone Microsoft 365 Basic and Standard licensing plans don't support SSPR with on-premises writeback. The on-premises writeback feature requires Microsoft Entra ID P1, Premium P2, or Microsoft 365 Business Premium.

For additional licensing information, including costs, see the following pages:

- [Microsoft 365 licensing guidance for security & compliance](/en-us/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-365-security-compliance-licensing-guidance)
- [Microsoft Entra pricing](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing)
- [Microsoft Entra features and capabilities](https://www.microsoft.com/cloud-platform/azure-active-directory-features)
- [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
- [Microsoft 365 Enterprise](https://www.microsoft.com/microsoft-365/enterprise)
- [Microsoft 365 Business](/en-us/office365/servicedescriptions/office-365-service-descriptions-technet-library)
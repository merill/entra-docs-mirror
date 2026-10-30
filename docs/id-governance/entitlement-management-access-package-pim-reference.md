---
layout: Conceptual
title: Using groups managed by Privileged Identity Management with access packages - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-access-package-pim-reference
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This article serves as a reference for Microsoft Entra ID behavior when assignment periods of an access package and PIM policy don't align.
ms.topic: concept-article
ms.date: 2025-06-26T00:00:00.0000000Z
locale: en-us
document_id: 67ea7fe3-b0a1-a8fc-8e67-6d03c9973a52
document_version_independent_id: 67ea7fe3-b0a1-a8fc-8e67-6d03c9973a52
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-access-package-pim-reference.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-access-package-pim-reference
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-access-package-pim-reference.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 71ef2ff7-7a81-6cbb-c814-f974e7b57c97
---

# Using groups managed by Privileged Identity Management with access packages - Microsoft Entra ID Governance | Microsoft Learn

This article contains information about Microsoft Entra ID behavior in scenarios where a group managed by PIM, and the access package expiration periods, differ. By assigning a group managed by PIM to an access package, you're able to assign eligible roles when an access package is requested. If you’re looking for a guide on setting up a group to assign eligible roles via access packages, see: [Assign eligible group membership and ownership in access packages via Privileged Identity Management for Groups (Preview)](entitlement-management-access-package-eligible).

## Shorter access package expiration

When an access package's expiration date is shorter than PIM's "*Expire eligible assignments after*" duration, then the PIM assignment expires when the access package expires.

### Example

| Access package policy assignment expiration | PIM policy max assignment duration | Microsoft Entra ID behavior |
| --- | --- | --- |
| 30 days | 365 days | Entitlement management sets a 365 day expiration on the PIM assignment when the access policy assignment is created, but removes the PIM assignment after the access policy assignment expires after 30 days. |

## Shorter PIM duration

When the PIM "*Expire eligible assignments after*" duration expires before the access package assignment, access is revoked when the PIM assignment expires irrespective of the access package's expiration date.

### Example

| Access package policy assignment expiration | PIM policy max assignment duration | Microsoft Entra ID behavior |
| --- | --- | --- |
| 180 days | 40 days | Entitlement management sets a 40 day expiration on the PIM assignment when the access policy assignment is created. On day 41, although the access package is still assigned, access is revoked. |

## Permanent access package assignment

If the Access package assignment is permanent, access is revoked based on when the PIM "*Expire eligible assignments after*" assignment expires.

### Example

| Access package policy assignment expiration | PIM Policy Max Assignment Duration | Microsoft Entra ID behavior |
| --- | --- | --- |
| None (permanent allowed) | 40 days | Entitlement management sets a 40 day expiration on the PIM assignment when the access policy assignment is created. On day 41, although the access package is still assigned, access is revoked. |

## Permanent PIM assignment

When the PIM "*Expire eligible assignments after*" assignment is permanent, it's removed only when the access package assignment expires.

### Example

| Access package policy assignment expiration | PIM Policy Max Assignment Duration | Microsoft Entra ID behavior |
| --- | --- | --- |
| 60 days | None (permanent allowed) | Entitlement management creates the PIM assignment and sets it to permanent on the access package policy assignment. Access is revoked on day 61 after the access package policy assignment expires. |

## Permanent access package and PIM assignment

If both the access package and PIM "*Expire eligible assignments after*" assignments are permanent, the PIM assignment remains as long as the access package assignment.

### Example

| Access package policy assignment expiration | PIM Policy Max Assignment Duration | Microsoft Entra ID behavior |
| --- | --- | --- |
| None (permanent allowed) | None (permanent allowed) | Entitlement management creates and sets the PIM assignment to permanent. The PIM assignment is only removed if the access package assignment is removed by other ways such as a removal request. |
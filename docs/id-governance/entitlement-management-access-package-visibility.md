---
layout: Conceptual
title: Understand access package visibility in the My Access portal - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-access-package-visibility
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: A conceptual article describing access package visibility in the My Access portal.
ms.subservice: lifecycle-workflows
ms.topic: concept-article
ms.date: 2025-06-12T00:00:00.0000000Z
locale: en-us
document_id: 7bfd127d-9018-6042-957d-8718ba02e439
document_version_independent_id: 7bfd127d-9018-6042-957d-8718ba02e439
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-access-package-visibility.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-access-package-visibility
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-access-package-visibility.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: cbe4067b-a79a-9683-fa47-87e3f1dc597f
---

# Understand access package visibility in the My Access portal - Microsoft Entra ID Governance | Microsoft Learn

Important

In July 2025, we announced that the visibility behavior for access packages scoped to "Specific users and groups" would be changing. The previously announced changes to access package visibility have been cancelled. No action is required at this time.

The [My Access portal](https://myaccess.microsoft.com) is the central place for users to request, approve, and review their access to resources within Microsoft Entra. For administrators, the Microsoft Entra admin center provides extra functionalities, enabling configuration of access packages and the ability to conduct access reviews.

When you manage access to resources in Microsoft Entra, understanding how access packages appear to users in the [My Access portal](https://myaccess.microsoft.com) is essential. Access package visibility determines which packages users can discover and request, and is influenced by several configuration settings and planned changes. This article provides a detailed overview of the factors that control access package visibility in the My Access portal, explains how it currently works, and highlights important changes effective October 10, 2025.

## Discover requestable access packages

When a user lands on the "*Available*" tab, searches for requestable packages, or selects "*View all*," Microsoft Entra evaluates which access packages they should be able to see and potentially request. This visibility is determined by a specific sequence of checks.

The following flow diagram, which can be selected to enlarge, illustrates the current logic used to determine if an access package appears in the browse/search view for a specific user:

[![Diagram of access package visibility before October changes.](media/entitlement-management-access-package-visibility/visibility-diagram-small.png)](media/entitlement-management-access-package-visibility/visibility-diagram.png#lightbox)

**Explaining the current visibility flow**

The logic of this diagram is as follows:

1. **Is the catalog enabled?** The system first checks if the catalog containing the access package is enabled. If the entire catalog is disabled, none of its packages are visible for discovery.
2. **Is the end-user an external user?** The system checks if the user is an external user or an internal user. This affects the next step.

    - **(If external user) Is the catalog enabled for external users?** For external users, the catalog must **also** be enabled for external users in its settings. If not, external users don't see packages from this catalog. Internal users skip this check.
3. **Is the access package hidden?** This checks the specific "hidden" setting directly on the access package's properties (under "Edit"). If set to "Yes," the package is hidden from the browse/search view, regardless of policies.
4. **Does at least one enabled policy exist for the access package where 'Who can request' matches the end-user?** This is the final, crucial policy check. The system looks for *at least one policy* associated with the access package that meets ALL these criteria:

    1. The policy's "*Who can get access*" setting logically includes the current user based on their identity, group memberships, or connected organization affiliation. Policies set to "None (Administrator direct assignments only)" don't make a package visible in the My Access portal.
    2. The policy's '*Who can request access*' setting must have the 'Self' option checked so users can request access for themselves. If a manager is trying to request access for one of their direct reports the 'Manager' option must be checked.

If **all** these checks pass, then the access package is Visible in the user's browse/search view. Otherwise, it's not visible.
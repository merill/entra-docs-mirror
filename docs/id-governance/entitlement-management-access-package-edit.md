---
layout: Conceptual
title: Hide or delete access package in entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-access-package-edit
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to hide or delete an access package in Microsoft Entra entitlement management.
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2024-07-15T00:00:00.0000000Z
locale: en-us
document_id: 0e33a67a-85e2-a48f-b5c8-e316e37f134b
document_version_independent_id: 57c90bb3-0a8b-f016-e2f6-69a861ef87ad
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-access-package-edit.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-access-package-edit
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-access-package-edit.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: b4060476-3dbb-8eb8-80e4-1dfe334ea914
---

# Hide or delete access package in entitlement management - Microsoft Entra ID Governance | Microsoft Learn

When you create access packages, they're discoverable by default. This means that if a policy allows a user to request the access package, they'll automatically see the access package listed in their My Access portal. However, you can change the **Hidden** setting so that the access package isn't listed in the user's My Access portal. A user will only see the access packages from a given tenant in their My Access portal. Users can either use the organization/tenant switcher which is located on the top right of the My Access portal or a My Access portal link which includes a tenant hint. For more information, see [Share link to request an access package](entitlement-management-access-package-settings).

This article describes how to hide or delete an access package.

## Change the Hidden setting

Follow these steps to change the **Hidden** setting for an access package.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner and Access Package manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the Access packages page, open an access package.
4. On the Overview page, select **Edit**.
5. Set the **Hidden** setting.

    If set to **No**, the access package is listed in the user's My Access portal.

    If set to **Yes**, the access package won't be listed in the user's My Access portal. The only way a user can view the access package is if they have the direct **My Access portal link** to the access package. For more information, see [Share link to request an access package](entitlement-management-access-package-settings).

## Delete an access package

An access package can only be deleted if it has no active user assignments. Follow these steps to delete an access package.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner and Access Package manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the Access packages page, open the access package.
4. In the left menu, select **Assignments** and remove access for all users.
5. In the left menu, select **Overview** and then select **Delete**.
6. In the delete message that appears, select **Yes**.
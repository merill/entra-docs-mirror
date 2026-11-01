---
layout: Conceptual
title: Include access packages in catalog access reviews (preview) - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/catalog-access-reviews-access-packages
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to include access packages in Microsoft Entra catalog access reviews, assign reviewers, and understand the effect of denying an access package.
ms.subservice: access-reviews
ms.topic: how-to
ms.date: 2026-10-29T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1026
ai-usage: ai-generated
locale: en-us
document_id: a6c22c35-a1a9-b3ee-6166-c85dfa91b127
document_version_independent_id: a6c22c35-a1a9-b3ee-6166-c85dfa91b127
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/catalog-access-reviews-access-packages.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/catalog-access-reviews-access-packages
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/catalog-access-reviews-access-packages.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: 19e259f3-c2b9-c68b-e486-cbaab9c2a976
---

# Include access packages in catalog access reviews (preview) - Microsoft Entra ID Governance | Microsoft Learn

Microsoft Entra ID Governance now supports including access packages in catalog access reviews (preview). When a user has access to Microsoft Entra applications or Microsoft Entra groups through an access package, reviewers see the access package instead of separate entries for each resource it contains.

This article explains how to enable access packages in a catalog access review, who reviews them, and what happens when a reviewer denies an access package.

## Prerequisites

- A Microsoft Entra ID Governance or Microsoft Entra Suite subscription. For more information, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).
- At least the [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator) role to create the catalog access review.
- A catalog that contains the access packages you want to review.

## Include access packages in a review

Enable the access package preview option when you create the catalog access review.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **ID Governance** &gt; **Access reviews** &gt; **New access review**.
3. Select **Review users access across multiple resource types within a catalog**.
4. Enter the basic information for the review, and then select **Next**.
5. On the **Resources** tab, use **Select Catalog** to select the catalog that contains the access packages you want to review.
6. Select **Include access packages (Preview)**.

    ![Screenshot of the Resources tab with the Include access packages (Preview) checkbox selected beneath Select Catalog.](media/catalog-access-reviews/include-access-packages.png)
7. Select **Next**. On the **Reviewers and schedule** tab, choose the reviewers and configure the schedule.

    If you choose resource owners as reviewers, the access package assignment manager for each specific access package reviews that package.
8. Configure the reviewer experience and completion settings, and then select **Create**.

For more information about the review settings, see [Create a catalog access review](catalog-access-reviews#create-a-catalog-access-review).

## Review access package assignments

Reviewers review an access package as a single item, rather than deciding separately on each Microsoft Entra group or application granted through that package.

Note

Only Microsoft Entra applications and Microsoft Entra groups delivered through access packages are consolidated under the access package in the review.

1. Sign in to the [My Access portal](https://myaccess.microsoft.com) as a reviewer.
2. Select **Access reviews**, and then select the **Multi-resource** tab.
3. Open the catalog access review.
4. For each access package, select **Approve** or **Deny**, and provide a justification if required.
5. Select **Submit** to record your decisions.

When a reviewer denies an access package, the user's access package assignment is removed on the review end date. Removing the assignment removes the user's access to all resources granted through that package, not just the Microsoft Entra applications and Microsoft Entra groups consolidated in the review.
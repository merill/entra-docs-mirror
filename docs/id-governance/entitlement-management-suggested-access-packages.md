---
layout: Conceptual
title: Show suggested access packages for My Access in entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-suggested-access-packages
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to show suggested access packages to users in My Access so they can quickly find the most relevant access packages.
editor: markwahl-msft
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2025-01-09T00:00:00.0000000Z
ms.reviewer: myra-ramdenbourg
locale: en-us
document_id: 96c2247d-afea-67d7-dd4e-bee20e827d1c
document_version_independent_id: 96c2247d-afea-67d7-dd4e-bee20e827d1c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-suggested-access-packages.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-suggested-access-packages
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-suggested-access-packages.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ef2ef207-f6ce-b0cb-dce0-20d074c228e5
---

# Show suggested access packages for My Access in entitlement management - Microsoft Entra ID Governance | Microsoft Learn

In My Access, Microsoft Entra ID Governance users can see a curated list of suggested access packages in My Access. This capability allows users to quickly view the most relevant access packages for them based off their peers' access packages and previous assignments without scrolling through all their available access packages.

The suggested access packages list is created by finding people related to the user (manager, direct reports, organization, team members) and recommending access packages based on what the users’ peers have. The user is also suggested access packages that were previously assigned to them.

## Settings for end users to see their suggested access packages in My Access

Follow these steps to enable suggested access packages in My Access.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Control configurations** &gt; **My Access settings for end users**.

    [![Screenshot of opt-in feature selection option.](media/entitlement-management-suggested-access-packages/opt-in-features-selection.png)](media/entitlement-management-suggested-access-packages/opt-in-features-selection.png#lightbox)
3. For Show insights for suggested access packages in My Access, select *Past assignments, Past assignments and peers without names*, or *Past assignments and peers with names*.
4. Select **Save**.
5. Sign in to the My Access portal at https://myaccess.microsoft.com. Select **Access packages** to see your suggested access packages.[![Screenshot of suggested access packages.](media/entitlement-management-suggested-access-packages/suggested-access-packages.png)](media/entitlement-management-suggested-access-packages/suggested-access-packages.png#lightbox)
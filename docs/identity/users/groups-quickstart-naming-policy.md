---
layout: Conceptual
title: Group naming policy quickstart - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-quickstart-naming-policy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Explains how to add new users or delete existing users in Microsoft Entra ID
ms.topic: quickstart
ms.date: 2024-12-16T00:00:00.0000000Z
ms.reviewer: yukarppa
ms.custom: it-pro, mode-other
ms.collection: M365-identity-device-management
locale: en-us
document_id: aa84f24e-7d01-85fa-4927-d38fea6c49f8
document_version_independent_id: 3a79d18a-54b0-4c9a-a2cf-a01eae627b9f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-quickstart-naming-policy.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-quickstart-naming-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-quickstart-naming-policy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 4e1534da-8708-1b78-ee3e-324195e9d0dc
---

# Group naming policy quickstart - Microsoft Entra ID | Microsoft Learn

## Overview

In this quickstart, in Microsoft Entra ID, part of Microsoft Entra, you set up naming policy in your Microsoft Entra organization for user-created Microsoft 365 groups, to help you sort and search your groups. For example, you could use the naming policy to:

- Communicate the function of a group, membership, geographic region, or who created the group.
- Help categorize groups in the address book.
- Block specific words from being used in group names and aliases.

If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Configure the group naming policy

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](../role-based-access-control/permissions-reference#groups-administrator).
2. Select **Microsoft Entra ID**.
3. Select **Groups** &gt; **All groups**, then select **Naming policy** to open the **Naming policy** page.

    ![Screenshot of the Naming policy page in the admin center.](media/groups-quickstart-naming-policy/policy.png)

### View or edit the Prefix-suffix naming policy

1. On the **Naming policy** page, select **Group naming policy**.
2. You can view or edit the current prefix or suffix naming policies individually by selecting the attributes or strings you want to enforce as part of the naming policy.
3. To remove a prefix or suffix from the list, select the prefix or suffix, then select **Delete**. Multiple items can be deleted at the same time.
4. Select **Save** for your changes to the policy to go into effect.

### View or edit the custom blocked words

1. On the **Naming policy** page, select **Blocked words**.

    ![Screenshot of editing and uploading blocked words list for naming policy.](media/groups-quickstart-naming-policy/blockedwords.png)
2. View or edit the current list of custom blocked words by selecting **Download**.
3. Upload the new list of custom blocked words by selecting the file icon.
4. Select **Save** for your changes to the policy to go into effect.

That's it. You've set up your naming policy and added your custom blocked words.

## Clean up resources

To remove the naming policy, use the following steps.

### Remove the naming policy

1. On the **Naming policy** page, select **Delete policy**.
2. After you confirm the deletion, the naming policy is removed, including all prefix-suffix naming policy and any custom blocked words.
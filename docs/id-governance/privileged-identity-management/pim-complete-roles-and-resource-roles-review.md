---
layout: Conceptual
title: Complete an access review of Azure resource and Microsoft Entra roles in PIM - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-complete-roles-and-resource-roles-review
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Learn how to complete an access review of Azure resource and Microsoft Entra roles in Privileged Identity Management.
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: shaunliu
ms.custom: pim, sfi-image-nochange
locale: en-us
document_id: 4e7c597e-fd50-d008-76c5-1647203465d2
document_version_independent_id: b18d388f-4a09-3ff9-f21c-e98c38d90a78
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-complete-roles-and-resource-roles-review.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-complete-roles-and-resource-roles-review
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-complete-roles-and-resource-roles-review.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 7c32da8e-8cef-973f-66f4-b751add34452
---

# Complete an access review of Azure resource and Microsoft Entra roles in PIM - Microsoft Entra ID Governance | Microsoft Learn

## Overview

Privileged Role Administrators can review privileged access once an [access review starts](pim-create-roles-and-resource-roles-review). Privileged Identity Management (PIM) in Microsoft Entra ID automatically sends an email that prompts users to review their access. If a user doesn't receive an email, you can send them the instructions for [how to perform an access review](pim-perform-roles-and-resource-roles-review).

Once the review has been created, follow the steps in this article to complete the review and see the results.

## Complete access reviews

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a user that is assigned to one or more prerequisite roles.
2. Browse to **ID Governance** &gt; **Privileged Identity Management**.
3. For **Microsoft Entra roles**, select **Microsoft Entra roles**. For **Azure resources**, select **Azure resources**.
4. Select the access review that you want to manage. Below is a sample screenshot of the **Review Access** overview for both **Azure resources** and **Microsoft Entra roles**.

    [![Access reviews list showing role, owner, start date, end date, and status screenshot.](media/pim-complete-azure-ad-roles-and-resource-roles-review/rbac-azure-ad-roles-home-list.png)](media/pim-complete-azure-ad-roles-and-resource-roles-review/rbac-azure-ad-roles-home-list.png#lightbox)

On the detail page, the following options are available for managing the review of **Azure resources** and **Microsoft Entra roles**:

![Options for managing a review in Azure resources - Stop, Reset, Apply, Delete screenshot.](media/pim-complete-azure-ad-roles-and-resource-roles-review/rbac-access-review-menu.png)

### Stop an access review

All access reviews have an end date, but you can use the **Stop** button to finish it early. The **Stop** button is only selectable when the review instance is active. You can't restart a review after it's been stopped.

### Reset an access review

When the review instance is active and at least one decision has been made by reviewers, you can reset the access review by selecting the **Reset** button to remove all decisions that were made on it. After you've reset an access review, all users are marked as not reviewed again.

### Apply an access review

After an access review is completed, either because you've reached the end date or stopped it manually, the **Apply** button removes denied users' access to the role. If a user's access was denied during the review, this is the step that removes their role assignment. If the **Auto apply** setting is configured on review creation, this button is always disabled because the review will be applied automatically instead of manually.

### Delete an access review

If you aren't interested in the review any further, delete it. To remove the access review from the Privileged Identity Management service, select the **Delete** button.

Important

You aren't required to confirm this destructive change, so verify that you want to delete that review.

## Results

On the **Results** page, you can view and download a list of your review results.

[![Results page listing users, outcome, reason, reviewed by, applied by, and apply result for Microsoft Entra roles screenshot.](media/pim-complete-azure-ad-roles-and-resource-roles-review/rbac-access-review-azure-ad-results.png)](media/pim-complete-azure-ad-roles-and-resource-roles-review/rbac-access-review-azure-ad-results.png#lightbox)

Note

**Microsoft Entra roles** have a concept of role-assignable groups, where a group can be assigned to the role. When this happens, the group will show up in the review instead of expanding the members of the group, and a reviewer will either approve or deny the entire group.

[![Results page listing users, outcome, reason, reviewed by, applied by, and apply result for Azure resource roles screenshot.](media/pim-complete-azure-ad-roles-and-resource-roles-review/rbac-access-review-azure-resource-results.png)](media/pim-complete-azure-ad-roles-and-resource-roles-review/rbac-access-review-azure-resource-results.png#lightbox)

Note

If a group is assigned to **Azure resource roles**, the reviewer of the Azure resource role will see the expanded list of the users in a nested group. Should a reviewer deny a member of a nested group, that deny result won't be applied successfully because the user will not be removed from the nested group.

## Reviewers

On the **Reviewers** page, you can view and add reviewers to your existing access review. You can also remind reviewers to complete their reviews here.

Note

If the reviewer type selected is user or group, you can add more users or groups as the primary reviewers at any point. You can also remove primary reviewers at any point. If the reviewer type is manager, you can add users or groups as the fallback reviewers to complete reviews on users who don't have managers. Fallback reviewers cannot be removed.

[![Reviewers page listing name and user principal name for Azure resource roles screenshot.](media/pim-complete-azure-ad-roles-and-resource-roles-review/rbac-access-review-azure-resource-reviewers.png)](media/pim-complete-azure-ad-roles-and-resource-roles-review/rbac-access-review-azure-resource-reviewers.png#lightbox)
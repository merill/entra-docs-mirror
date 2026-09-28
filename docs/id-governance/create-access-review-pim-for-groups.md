---
layout: Conceptual
title: Create an access review of PIM for Groups (preview) - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/create-access-review-pim-for-groups
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to create an access review of PIM for Groups in Microsoft Entra ID.
editor: markwahl-msft
ms.subservice: access-reviews
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
ms.reviewer: jgangadhar
locale: en-us
document_id: 4d92b9bc-a958-6e68-9755-b46229ea0d53
document_version_independent_id: f8e2091a-81f6-606d-eb5c-5838fa809302
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/create-access-review-pim-for-groups.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/create-access-review-pim-for-groups
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/create-access-review-pim-for-groups.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3da1a4d0-618e-3b86-b415-b0a9b4d2048f
---

# Create an access review of PIM for Groups (preview) - Microsoft Entra ID Governance | Microsoft Learn

This article describes how to create one or more access reviews for PIM for Groups, including the active and eligible members of the group. Reviews can be performed on both active members of the group, who are active at the time the review is created, and the eligible members of the group.

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Create a PIM for Groups access review

### Scope

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Access Reviews**.
3. Select **New access review** to create a new access review.

    ![Screenshot that shows the Access reviews pane in Identity Governance.](media/create-access-review/access-reviews.png)
4. On the Access reviews template screen, select **Review access to a resource type**. ![Screenshot of the access review templates page.](media/catalog-access-reviews/access-review-templates.png)
5. In the **Select what to review** box, select **Teams + Groups**.

    ![Screenshot that shows creating an access review.](media/create-access-review/select-what-review.png)
6. Select **Teams + Groups** and then select **Select Teams + groups** under **Review Scope**. A list of groups to choose from appears on the screen.

    ![Screenshot that shows selecting Teams + Groups.](media/create-access-review/create-pim-review.png)

Note

When a PIM for Groups is selected, the users under review for the group include all eligible users and active users in that group.

1. Now you can select a scope for the review. Your options are:

    - **Guest users only**: This option limits the access review to only the Microsoft Entra B2B guest users in your directory.
    - **Everyone**: This option scopes the access review to all user objects associated with the resource.
2. If you're conducting group membership review, you can create access reviews for only the inactive users in the group. In the *Users scope* section, check the box next to **Inactive users (on tenant level)**. If you check the box, the scope of the review focuses on inactive users only, users who haven't signed in either interactively or non-interactively to the tenant. Then, specify **Days inactive** with the number of days inactive, up to 730 days (two years). Users in the group inactive for the specified number of days are the only users in the review.

Note

Recently created users aren't affected when configuring the inactivity time. The access review checks if a user has been created in the time frame configured and disregards users who haven’t existed for at least that amount of time. For example, if you set the inactivity time as 90 days and a guest user was created or invited less than 90 days ago, the guest user won't be in scope of the Access Review. This ensures that a user can sign in at least once before being removed.

1. Select **Next: Reviews**.

After you reach this step, you can follow the instructions outlined under **Next: Reviews** in the [Create an access review of groups or applications](create-access-review#next-reviews) article to complete your access review.

Note

For access reviews of PIM for Groups (preview), when selecting the group owner as the reviewer, you must assign at least one fallback reviewer. The review will only assign active owner(s) as the reviewer(s). Eligible owners aren't included. If there are no active owners when the review begins, the fallback reviewer(s) will be assigned to the review.
---
layout: Conceptual
title: Create an access review of an access package in entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-access-reviews-create
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to set up an access review in a policy for entitlement management access packages in Microsoft Entra ID part of Microsoft Entra.
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: c5c9f9a3-867d-70e7-ba99-8a10786e7929
document_version_independent_id: eb5672e0-967d-6b7b-5b78-f6aa4102c568
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-access-reviews-create.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-access-reviews-create
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-access-reviews-create.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: cbabc1ca-e7e6-2639-e5ad-b9ab2df1edc1
---

# Create an access review of an access package in entitlement management - Microsoft Entra ID Governance | Microsoft Learn

To reduce the risk of stale access, you should enable periodic reviews of users who have active assignments to an access package in entitlement management. You can enable reviews when you create a new access package or edit an existing access package assignment policy. This article describes how to enable access reviews of access packages.

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Create an access review of an access package

You can enable access reviews when [creating a new access package](entitlement-management-access-package-create) or [editing an existing access package assignment policy](entitlement-management-access-package-lifecycle-policy) policy. If you have multiple policies, for different communities of users to request access, you can have independent access review schedules for each policy. Follow these steps to enable access reviews of an access package's assignments:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Access reviews** &gt; **Access package**.
3. To create a new access package, select **New access package**.
4. To edit an existing access policy, in the left menu, select **Access packages** and open the access package you want to edit. Then, in the left menu, select **Policies**, and select the policy that has the lifecycle settings you want to edit.
5. Open the **Lifecycle** tab for an access package assignment policy to specify when a user's assignment to the access package expires. You can also specify whether users can extend their assignments.
6. In the **Expiration** section, set Access package assignments expires to **On date**, **Number of days**, **Number of hours**, or **Never**.

    For **On date**, select an expiration date in the future.

    For **Number of days**, specify a number between 0 and 3660 days.

    For **Number of hours**, specify the number of hours.

    Based on your selection, a user's assignment to the access package expires on a certain date, a specific number of days after they're approved, or never.

    ![Access package - Lifecycle Expiration settings](media/entitlement-management-access-reviews/expiration.png)
7. Select **Show advanced expiration settings** to show other settings.
8. To allow users to extend their assignments, set **Allow users to extend access** to **Yes**.

    If extensions are allowed in the policy, the user receives an email 14 days and one day before their access package assignment is set to expire, prompting them to extend the assignment. The user must still be in the scope of the policy at the time they request an extension. Also, if the policy has an explicit end date for assignments, and a user submits a request to extend access, the extension date in the request must be at or before when assignments expire, as defined in the policy that was used to grant the user access to the access package. For example, if the policy indicates that assignments are set to expire on June 30, the maximum extension a user can request is June 30.

    If a user's access is extended, they won't be able to request the access package after the specified extension date (date set in the time zone of the user who created the policy).
9. To require approval to grant an extension, set **Require approval to grant extension** to **Yes**.

    The same approval settings that were specified on the Requests tab will be used.
10. Next, move the **Require access reviews** toggle to **Yes**.

    ![Add the access review](media/entitlement-management-access-reviews/access-reviews-pane.png)
11. Specify the date the reviews start next to **Starting on**.
12. Next, set the **Review frequency** to **Annually**, **Bi-annually**, **Quarterly** or **Monthly**. This setting determines how often access reviews occur.
13. Set the **Duration** to define how many days each review of the recurring series is open for input from reviewers. For example, you might schedule an annual review that starts on January 1 and is open for review for 30 days so that reviewers have until the end of the month to respond.
14. Next to **Reviewers**, select **Self-review** if you want users to perform their own access review or select **Specific reviewer(s)** if you want to designate a reviewer. You can also select **Manager** if you want to designate the reviewer’s manager to be the reviewer. If you select this option, you need to add a **fallback** to forward the review to in case the manager can't be found in the system.
15. If you selected **Specific reviewer(s)**, specify which users do the access review:

    ![Select Add reviewers](media/entitlement-management-access-reviews/access-reviews-add-reviewer.png)

    1. Select **Add reviewers**.
    2. In the **Select reviewers** pane, search for and select the user(s) you want to be a reviewer.
    3. When you've selected your reviewer(s), select the **Select** button.

    ![Specify the reviewers](media/entitlement-management-access-reviews/access-reviews-select-reviewer.png)
16. If you selected **Manager**, specify the fallback reviewer:

    1. Select **Add fallback reviewers**.
    2. In the Select fallback reviewers pane, search for and select the user(s) you want to be fallback reviewer(s) for the reviewer's manager.
    3. When you've selected your fallback reviewer(s), select the **Select** button.

    ![Add the fallback reviewers](media/entitlement-management-access-reviews/access-reviews-select-manager.png)
17. There are other advanced settings you can configure. To configure other advanced access review settings, select **Show advanced access review settings**:

    1. If you want to specify what happens to users' access when a reviewer doesn't respond, select **If reviewers don't respond**, and then select one of the following:

        - **No change** if you don't want a decision made on the users' access.
        - **Remove access** if you want the users' access removed.
        - **Take recommendations** if you want a decision to be made based on recommendations from MyAccess.

        ![Add advanced access review settings](media/entitlement-management-access-reviews/advanced-access-reviews.png)
    2. If you want to see system recommendations, select **Show reviewer decision helpers**. The system's recommendations are based on the users' activity. The reviewers see one of the following recommendations:

        - **approve** the review if the user has signed-in at least once during the last 30 days.
        - **deny** the review if the user hasn't signed-in during the last 30 days.
    3. If you want the reviewer to share their reasons for their approval decision, select **Require reviewer justification**. Their justification is visible to other reviewers and the requestor.
18. Select **Review + Create** or select **next** if you're creating a new access package. Select **Update** if you're editing an access package, at the bottom of the page.

## View the status of the access review

After the start date, an access review will be listed in the **Access reviews** section. Follow these steps to view the status of an access review:

1. In **Identity Governance**, select **Access packages** then select the access package with the access review status you'd like to check.
2. Once you are on the access package overview, select **Access reviews** on the left menu.

    ![Select access reviews](media/entitlement-management-access-reviews/access-review-status-access-package-overview.png)
3. A list appears that contains all of the policies that have access reviews associated with them. Select the review to see its report.

    ![List of access reviews](media/entitlement-management-access-reviews/access-review-status-select-access-reviews.png)
4. When you view the report, it shows the number of users reviewed and the actions taken by the reviewer on them.

    ![View review status](media/entitlement-management-access-reviews/access-review-status.png)

## Access reviews email notifications

You can designate reviewers, or users can review their access themselves. By default, Microsoft Entra ID will send an email to reviewers or self-reviewers shortly after the review starts.

The email includes instructions on how to review access to access packages. If the review is for users to review their own access, show them the instructions on how to perform a self-review of their access packages.

If you've assigned guest users as reviewers, and they haven't accepted their Microsoft Entra guest invitation, they won't receive emails from access reviews. They must first accept the invite and create an account with Microsoft Entra ID before they can receive the emails.

Note

While the review cycle is open, reviewers can always change their access review decisions. At the midpoint of your access review, even if the reviewer has previously made a decision, a reminder email is still sent to reviewers notifying them that the access review cycle is still open.
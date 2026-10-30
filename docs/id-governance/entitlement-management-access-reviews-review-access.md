---
layout: Conceptual
title: Review access of an access package in entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-access-reviews-review-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to complete an access review of entitlement management access packages in access reviews.
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
locale: en-us
document_id: 7d804752-4802-b615-c269-fab8231d1970
document_version_independent_id: a18f2b1c-1632-4644-047d-506e2339537b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-access-reviews-review-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-access-reviews-review-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-access-reviews-review-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
platformId: 48296e14-7de7-8ada-5b05-158dc9755418
---

# Review access of an access package in entitlement management - Microsoft Entra ID Governance | Microsoft Learn

Entitlement management simplifies how enterprises manage access to groups, applications, and SharePoint sites. This article describes how designated reviewers can review user assignments to access packages.

## Perform access review by using the My Access portal

The [My Access portal](https://myaccess.microsoft.com/) is a user-friendly portal for manually granting, approving, and reviewing access needs.

### Open the access review

Use the following steps to find and open the access review:

1. You might receive an email from Microsoft that asks you to review access. Locate the email to open the access review. Here's an example email to review access:

    ![Access review reviewer email](media/entitlement-management-access-reviews-review-access/review-access-reviewer-email.png)
2. Select the **Review user access** link to open the access review.
3. If you don’t have the email, you can find your pending access reviews by navigating directly to https://myaccess.microsoft.com. (For US Government, use `https://myaccess.microsoft.us` instead.)
4. Select **Access reviews** on the left navigation bar to see a list of pending access reviews assigned to you.

    ![Select access reviews on My Access](media/entitlement-management-access-reviews-review-access/review-access-myaccess-select-access-review.png)
5. Select the review that you’d like to begin.

    ![Select the access review](media/entitlement-management-access-reviews-review-access/review-access-select-access-review.png)

### Manually approve or deny access for one or more users using the My Access portal

1. Review the list of users and determine which users need to continue to have access.

    ![List of users to review](media/entitlement-management-access-reviews-review-access/review-access-list-of-users.png)
2. To approve or deny access, select the radio button to the left of the user’s name.
3. Select **Approve** or **Deny** in the bar above the user names.

    ![Select the user](media/entitlement-management-access-reviews-review-access/review-access-select-users.png)
4. If you aren't sure, you can select the **Don’t know** button.

    If you make the **Don't know** selection, the user maintains access, and this selection goes in the audit logs. The log shows any other reviewers that you still completed the review.
5. You might be required to provide a reason for your decision. Type in a reason and select **Submit**.

    ![Approve or deny access](media/entitlement-management-access-reviews-review-access/review-access-decision-approve.png)
6. You can change your decision at any time before the end of the review. To do so, select the user from the list and change the decision. For example, you can approve access for a user you previously denied.

If there are multiple reviewers, the last submitted response is recorded. Consider an example where an administrator designates two reviewers – Alice and Bob. Alice opens the review first and approves access. Before the review ends, Bob opens the review and denies access. In this case, the last deny access decision gets recorded.

Note

If a user is denied access in the review, they aren't removed from the access package immediately. The user is removed from the access package when the review results are applied after the review is closed. The review closes automatically at the end of the review duration or earlier if an administrator manually stops the review.

### Approve or deny access using the system-generated recommendations

To review access for multiple users more quickly, you can use the system-generated recommendations, accepting the recommendations with a single select. The recommendations are generated based on the user's sign-in activity.

1. In the bar at the top of the page, select **Accept recommendations**.

    ![Select Accept recommendations](media/entitlement-management-access-reviews-review-access/review-access-use-recommendations.png)

    You see a summary of the recommended actions.
2. Select **Submit** to accept the recommendations.
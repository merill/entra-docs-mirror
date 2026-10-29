---
layout: Conceptual
title: Review your access to resources in access reviews - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/self-access-review
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to review your own access to resources in access reviews.
editor: markwahl-msft
ms.subservice: access-reviews
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
ms.reviewer: mwahl
locale: en-us
document_id: 0a5bd9a9-aa36-0421-ad5e-fff837aa8a9c
document_version_independent_id: 7dab64b0-ef51-73bd-f463-8ba62a33b107
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/self-access-review.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/self-access-review
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/self-access-review.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: 238ef8fc-5490-8fa8-f50f-0defc6c3974f
---

# Review your access to resources in access reviews - Microsoft Entra ID Governance | Microsoft Learn

Microsoft entitlement management simplifies how enterprises manage access to groups, applications, and SharePoint sites. This article describes how you can do a self-review of your assigned access packages.

## Review your own access by using My Access

You can review your own access to a group, application, or access package in two ways.

### Use email

Important

There could be delays in receiving email, and in some cases it could take up to 24 hours. Add azure-noreply@microsoft.com to your safe recipients list to make sure you receive all emails.

1. Look for an email from Microsoft that asks you to review access. Here's an example email message.

    ![Screenshot that shows an example email from Microsoft that asks you to review access to a group.](media/self-access-review/access-review-email-preview.png)
2. Select **Review access** to open the access review.
3. Continue in the section **Perform the access review**.

### Use My Access

You can also view your pending access reviews by using your browser to open **My Access**.

1. Sign in to [My Access](https://myaccess.microsoft.com/).
2. On the menu on the left, select **Access reviews** to see a list of pending access reviews assigned to you.

    ![Screenshot that shows Access reviews on the menu.](media/self-access-review/access-review-menu.png)

## Do the access review

1. Under **Groups and Apps**, you can see:

    - **Name**: The name of the access review.
    - **Due**: The due date for the review. After this date, denied users might be removed from the group or app being reviewed.
    - **Resource**: The name of the resource under review.
    - **Progress**: The number of users reviewed out of the total number of users who are part of this access review.
2. Select the name of an access review to get started.

    ![Screenshot that shows a pending access reviews list for apps and groups.](media/self-access-review/access-reviews-list-preview.png)
3. Review your access and decide if you still need access.

    If the request is to review access for others, the page looks different. For more information, see [Review access to groups or applications](perform-access-review).

    ![Screenshot that shows an open access review that asks if you still need access to a group.](media/self-access-review/review-access-preview.png)
4. Select **Yes** to keep your access, or select **No** to remove your access.
5. If you select **Yes**, you might need to specify a justification in the **Reason** box.

    ![Screenshot that shows selecting Yes to keep access to a group.](media/self-access-review/review-access-yes-preview.png)
6. Select **Submit**.

    Your selection is submitted, and you're returned to the **My Access** page.

    If you want to change your response, reopen the **Access reviews** page and update your response. You can change your response at any time until the access review has ended.

    Note

    If you indicated that you no longer need access, the system doesn't remove you immediately. You're removed when the review has ended or when an administrator stops the review.
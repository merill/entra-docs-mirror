---
layout: Conceptual
title: Manage user access with access reviews - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/manage-user-access-with-access-reviews
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to manage users' access as membership of a group or assignment to an application with Microsoft Entra access reviews
editor: markwahl-msft
ms.subservice: access-reviews
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
ms.reviewer: mwahl
ms.custom: sfi-ga-nochange
locale: en-us
document_id: e1a0ff03-4368-38c8-70e6-b41b6f79051c
document_version_independent_id: 31491ee3-751f-ccf7-8d54-049065bfba20
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/manage-user-access-with-access-reviews.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/manage-user-access-with-access-reviews
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/manage-user-access-with-access-reviews.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 69d17cda-b2d7-f218-48e7-911b4db42ff9
---

# Manage user access with access reviews - Microsoft Entra ID Governance | Microsoft Learn

With Microsoft Entra, you can easily ensure that users have appropriate access. You can ask the users themselves or a decision maker to participate in an access review and recertify or attest to users' access. The reviewers can give their input on each user's need for continued access based on suggestions from Microsoft Entra. When an access review is finished, you can then make changes and remove access from users who no longer need it.

Note

If you want to review only guest users' access and not review all types of users' access, see [Manage guest user access with access reviews](manage-guest-access-with-access-reviews). If you want to review users' membership in administrative roles such as Global Administrator, see [Start an access review in Microsoft Entra Privileged Identity Management](privileged-identity-management/pim-create-roles-and-resource-roles-review).

## Prerequisites

- Microsoft Entra ID P2 or Microsoft Entra ID Governance

For more information, see [License requirements](access-reviews-overview#license-requirements).

If you're reviewing access to an application, then before creating the review, see the article on how to [prepare for an access review of users' access to an application](access-reviews-application-preparation) to ensure the application is integrated with Microsoft Entra ID.

## Create and perform an access review

You can have one or more users as reviewers in an access review.

1. Select a group in Microsoft Entra ID that has one or more members. Or select an application connected to Microsoft Entra ID that has one or more users assigned to it.
2. Decide whether to have each user review their own access or to have one or more users review everyone's access in that group or application.
3. As at least a User Administrator, or (Preview) an owner of a Microsoft 365 group or Microsoft Entra security group to be reviewed, go to the [Identity Governance page](https://portal.azure.com/#blade/Microsoft_AAD_ERM/DashboardBlade/).
4. Create the access review. For more information, see [Create an access review of groups or applications](create-access-review).
5. When the access review starts, ask the reviewers to give input. By default, they each receive an email from Microsoft Entra ID with a link to the access panel, where they [review access to groups or applications](perform-access-review).
6. If the reviewers haven't given input, you can configure Microsoft Entra ID to send them a reminder. By default, Microsoft Entra ID automatically sends a reminder halfway to the end date to reviewers who haven't yet responded.
7. After the reviewers give input, stop the access review and apply the changes. For more information, see [Complete an access review of groups or applications](complete-access-review).
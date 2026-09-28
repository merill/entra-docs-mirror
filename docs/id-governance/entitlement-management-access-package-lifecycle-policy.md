---
layout: Conceptual
title: Change lifecycle settings for an access package in entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-access-package-lifecycle-policy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to change requestor information & lifecycle settings for an access package in entitlement management.
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2025-06-26T00:00:00.0000000Z
locale: en-us
document_id: ab023b28-8e4a-4963-9dfa-e05b4771d795
document_version_independent_id: 74351a4c-4366-ece3-10cb-18962f84b7d7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-access-package-lifecycle-policy.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-access-package-lifecycle-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-access-package-lifecycle-policy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 6ea2a6f4-cd6e-7de6-9752-009adc7027e0
---

# Change lifecycle settings for an access package in entitlement management - Microsoft Entra ID Governance | Microsoft Learn

As an access package manager, you can change the lifecycle settings for assignments in an access package at any time by editing an existing policy. If you change the expiration date for assignments on a policy, the expiration date for requests that are already in a pending approval or approved state won't change.

This article describes how to change the lifecycle settings for an existing access package assignment policy.

## Open requestor information

To ensure identities have the right access to an access package, custom questions can be configured to ask identities requesting access to certain access packages. Configuration options include: localization, required/optional, and text/multiple choice answer formats. Requestors see the questions when they request the package and approvers see the answers to the questions to help them make their decision. Use the following steps to configure questions in an access package:

## Open lifecycle settings

To change the lifecycle settings for an access package, you need to open the corresponding policy. Follow these steps to open the lifecycle settings for an access package.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner and the Access package manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the Access packages page, open the access package that you want to edit.
4. Select **Policies** and then select the policy that has the lifecycle settings you want to edit.

    The Policy details pane opens at the bottom of the page.

    ![Access package - Policy details pane](media/entitlement-management-shared/policy-details.png)
5. Select **Edit** to edit the policy.

    ![Access package - Edit policy](media/entitlement-management-shared/policy-edit.png)
6. Select the **Lifecycle** tab to open the lifecycle settings.

## Specify a lifecycle

On the **Lifecycle** tab, you specify when an identity's assignment to the access package expires. You can also specify whether identities can extend their assignments.

1. In the **Expiration** section, set **Access package assignments expire** to **On date**, **Number of days**, **Number of hours**, or **Never**.

    - For **On date**, select an expiration date in the future.
    - For **Number of days**, specify a number from 0 to 3660 days.
    - For **Number of hours**, specify how many hours.

    Based on your selection, a user's assignment to the access package expires on a certain date, some days after they're approved, or never.
2. If you want the user to request a specific start and end date for their access, select **Yes** for the **Users can request specific timeline** toggle.
3. Select **Show advanced expiration settings** to show more settings.

    ![Screenshot that shows lifecycle expiration settings for an access package.](../includes/media/entitlement-management-lifecycle-policy/expiration.png)
4. To allow the user to extend their assignments, set **Allow users to extend access** to **Yes**.

    If extensions are allowed in the policy, the user receives an email 14 days before, and then one day before, their access package assignment is set to expire. The email prompts the user to extend the assignment. The user must still be in the scope of the policy at the time that they request an extension.

    Also, if the policy has an explicit end date for assignments, and a user submits a request to extend access, the extension date in the request must be at or before when assignments expire. The policy that you used to grant the user access to the access package defines whether the extension date is at or before the assignment expiration. For example, if the policy indicates that assignments are set to expire on June 30, the maximum extension that a user can request is June 30.

    If a user's access is extended, they won't be able to request the access package after the specified extension date (the date set in the time zone of the user who created the policy).
5. To require approval to grant an extension, set **Require approval to grant extension** to **Yes**.

    This approval will use the same approval settings that you specified on the **Requests** tab.
6. If you want to **Require an access review** for this access package, move the toggle to **Yes**. Refer to the [detailed article on configuring the access review](/en-us/entra/id-governance/entitlement-management-access-reviews-create) and then return back here to finish setting up the access package.
7. If you didn't require an access review, or once you have configured it, select **Next** or **Update**.
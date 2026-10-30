---
layout: Conceptual
title: Manage guest access with access reviews - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/manage-guest-access-with-access-reviews
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Manage guest users as members of a group or assigned to an application with Microsoft Entra access reviews.
editor: markwahl-msft
ms.subservice: access-reviews
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
ms.reviewer: mwahl
locale: en-us
document_id: 94205933-3124-b7ee-c1f1-cd9cc44e439d
document_version_independent_id: c7c22007-3d50-f273-53a1-0cafd6da0737
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/manage-guest-access-with-access-reviews.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/manage-guest-access-with-access-reviews
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/manage-guest-access-with-access-reviews.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 2a0878dc-c45c-b11f-c0fb-a714e850b452
---

# Manage guest access with access reviews - Microsoft Entra ID Governance | Microsoft Learn

With access reviews, you can easily enable collaboration across organizational boundaries by using the [Microsoft Entra B2B feature](../external-id/what-is-b2b). Guest users from other tenants can be [invited by administrators](../external-id/add-users-administrator) or by [other users](../external-id/what-is-b2b). This capability also applies to social identities such as Microsoft accounts.

You also can easily ensure that guest users have appropriate access. You can ask the guests themselves or a decision maker to participate in an access review and re-certify (or attest) to the guests' access. The reviewers can give their input on each user's need for continued access, based on suggestions from Microsoft Entra ID. When an access review is finished, you can then make changes and remove access for guests who no longer need it.

Note

This document focuses on reviewing guest users' access. If you want to review all users' access, not just guests, see [Manage user access with access reviews](manage-user-access-with-access-reviews). If you want to review users' membership in administrative roles, such as Global Administrator, see [Start an access review in Microsoft Entra Privileged Identity Management](privileged-identity-management/pim-create-roles-and-resource-roles-review).

## Prerequisites

- Microsoft Entra ID P2 or Microsoft Entra ID Governance

For more information, see [License requirements](access-reviews-overview#license-requirements).

## Create and perform an access review for guests

First, you must be assigned as at least one of the following roles:

- User Administrator
- (Preview) Microsoft 365 or Microsoft Entra Security Group owner of the group to be reviewed

Then, go to the [Identity Governance page](https://portal.azure.com/#blade/Microsoft_AAD_ERM/DashboardBlade/) to ensure that access reviews is ready for your organization.

Microsoft Entra ID enables several scenarios for reviewing guest users.

You can review either:

- A group in Microsoft Entra ID that has one or more guests as members.
- An application connected to Microsoft Entra ID that has one or more guest users assigned to it.

When reviewing guest user access to Microsoft 365 groups, you can either create a review for each group individually, or turn on automatic, recurring access reviews of guest users across all Microsoft 365 groups. The following video provides more information on recurring access reviews of guest users:

You can then decide whether to ask each guest to review their own access or to ask one or more users to review every guest's access.

These scenarios are covered in the following sections.

### Ask guests to review their own membership in a group

You can use access reviews to ensure that users who were invited and added to a group continue to need access. You can easily ask guests to review their own membership in that group.

1. To create an access review for the group, select the review to include guest user members only and that members review themselves. For more information, see [Create an access review of groups or applications](create-access-review).
2. Ask each guest to review their own membership. By default, each guest who accepted an invitation receives an email from Microsoft Entra ID with a link to the access review. Microsoft Entra ID has instructions for guests on how to [review access to groups or applications](perform-access-review).
3. After the reviewers give input, stop the access review and apply the changes. For more information, see [Complete an access review of groups or applications](complete-access-review).
4. In addition to those users who denied their own need for continued access, you can also remove users who didn't respond. Non-responding users potentially no longer receive email.
5. If the group isn't used for access management, you also can remove users who weren't selected to participate in the review because they didn't accept their invitation. Not accepting might indicate that the invited user's email address had a typo. If a group is used as a distribution list, perhaps some guest users weren't selected to participate because they're contact objects.

### Ask an authorized user to review a guest's membership in a group

You can ask an authorized user, such as the owner of a group, to review a guest's need for continued membership in a group.

1. To create an access review for the group, select the review to include guest user members only. Then specify one or more reviewers. For more information, see [Create an access review of groups or applications](create-access-review).
2. Ask the reviewers to give input. By default, they each receive an email from Microsoft Entra ID with a link to the access panel, where they [review access to groups or applications](perform-access-review).
3. After the reviewers give input, stop the access review and apply the changes. For more information, see [Complete an access review of groups or applications](complete-access-review).

### Ask guests to review their own access to an application

You can use access reviews to ensure that users who were invited for a particular application continue to need access. You can easily ask the guests themselves to review their own need for access.

1. To create an access review for the application, select the review to include guests only and that users review their own access. For more information, see [Create an access review of groups or applications](create-access-review).
2. Ask each guest to review their own access to the application. By default, each guest who accepted an invitation receives an email from Microsoft Entra ID. That email has a link to the access review in your organization's access panel. Microsoft Entra ID has instructions for guests on how to [review access to groups or applications](perform-access-review).
3. After the reviewers give input, stop the access review and apply the changes. For more information, see [Complete an access review of groups or applications](complete-access-review).
4. In addition to users who denied their own need for continued access, you also can remove guest users who didn't respond. Non-responding users potentially no longer receive email. You also can remove guest users who weren't selected to participate, especially if they weren't recently invited. Those users didn't accept their invitation and so didn't have access to the application.

### Ask an authorized user to review a guest's access to an application

You can ask an authorized user, such as the owner of an application, to review a guest's need for continued access to the application.

1. To create an access review for the application, select the review to include guests only. Then specify one or more users as reviewers. For more information, see [Create an access review of groups or applications](create-access-review).
2. Ask the reviewers to give input. By default, they each receive an email from Microsoft Entra ID with a link to the access panel, where they [review access to groups or applications](perform-access-review).
3. After the reviewers give input, stop the access review and apply the changes. For more information, see [Complete an access review of groups or applications](complete-access-review).

### Ask guests to review their need for access, in general

In some organizations, guests might not be aware of their group memberships.

Note

Earlier versions of the portal didn't permit administrative access by users with the UserType of Guest. In some cases, an administrator in your directory might have changed a guest's UserType value to Member by using PowerShell. If this change previously occurred in your directory, the previous query might not include all guest users who historically had administrative access rights. In this case, you need to either change the guest's UserType or manually include the guest in the group membership.

1. Create a security group in Microsoft Entra ID with the guests as members, if a suitable group doesn't already exist. For example, you can create a group with a manually maintained membership of guests. Or, you can create a dynamic group with a name such as "Guests of Contoso" for users in the Contoso tenant who have the UserType attribute value of Guest. For efficiency, ensure the group is predominately guests - don't select a group that has member users, as member users don't need to be reviewed. Also, keep in mind that a guest user who is a member of the group can see the other members of the group.

Note

Guest users who are members of Microsoft Entra groups can see other members of the same group when viewing **My profile &gt; Groups I’m in**. This behavior is independent of access reviews. If your organization wants to prevent guest users from seeing other guest accounts, you can update **Guest user access restrictions** in Microsoft Entra ID. For example, you can restrict guests to view only their own profile information. To configure this setting, go to **Entra ID &gt; External Identities &gt; External collaboration settings**, and adjust the **Guest user access restrictions** accordingly.

1. To create an access review for that group, select the reviewers to be the members themselves. For more information, see [Create an access review of groups or applications](create-access-review).
2. Ask each guest to review their own membership. By default, each guest who accepted an invitation receives an email from Microsoft Entra ID with a link to the access review in your organization's access panel. Microsoft Entra ID has instructions for guests on how to [review access to groups or applications](perform-access-review). Those guests who didn't accept their invite appear in the review results as "Not Notified".
3. After the reviewers give input, stop the access review. For more information, see [Complete an access review of groups or applications](complete-access-review).
4. You can automatically delete the guest users Microsoft Entra B2B accounts as part of an access review when you're configuring an Access review for **Select Team + Groups**. This option isn't available for **All Microsoft 365 groups with guest users**.

![Screenshot showing page to create access review.](media/manage-guest-access-with-access-reviews/new-access-review.png)

To do so, select **Auto apply results to resource** as this will automatically remove the user from the resource. **If reviewers don't respond** should be set to **Remove access**, and **Action to apply on denied guest users** should also be set to **Block from signing in for 30 days then remove user from the tenant**.

This will immediately block sign in to the guest user account and then automatically delete their Microsoft Entra B2B account after 30 days.
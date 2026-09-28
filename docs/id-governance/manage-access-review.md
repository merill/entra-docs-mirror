---
layout: Conceptual
title: Manage access with access reviews - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/manage-access-review
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to manage user and guest access as membership of a group or assignment to an application with Microsoft Entra access reviews.
editor: markwahl-msft
ms.subservice: access-reviews
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
ms.reviewer: mwahl
locale: en-us
document_id: 46039141-8208-37da-08a6-b5268d020679
document_version_independent_id: 57386fcf-186b-e5fb-32bf-b84710673041
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/manage-access-review.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/manage-access-review
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/manage-access-review.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: fd3f0b4d-ed38-0707-f58d-17aaf76970d5
---

# Manage access with access reviews - Microsoft Entra ID Governance | Microsoft Learn

With access reviews, you can easily ensure that users or guests have appropriate access. You can ask the users themselves or a decision maker to participate in an access review and recertify (or attest) to users' access. The reviewers can give their input on each user's need for continued access based on suggestions from Microsoft Entra ID. When an access review is finished, you can then make changes and remove access from users who no longer need it.

Note

This article discusses conducting access reviews for users and applications. To see information on conducting an access review for multiple resources in access packages see here [Review access of an access package in Microsoft Entra entitlement management](entitlement-management-access-reviews-review-access). If you want to review user or service principal access to Microsoft Entra ID or Azure resource roles, see [Start an access review in Microsoft Entra Privileged Identity Management](privileged-identity-management/pim-create-roles-and-resource-roles-review).

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Create and perform an access review for users

First, you must be assigned as at least one of the following roles:

- User Administrator
- Identity Governance Administrator
- Privileged Role Administrator (for reviews of role-assignable groups only)
- (Preview) Microsoft 365 or Microsoft Entra Security Group owner of the group to be reviewed

Then, go to the [Identity Governance page](https://portal.azure.com/#blade/Microsoft_AAD_ERM/DashboardBlade/) to ensure that access reviews are ready for your organization.

You can have one or more users as reviewers in an access review.

1. Select a group in Microsoft Entra ID that has one or more members. Or select an application connected to Microsoft Entra ID that has one or more users assigned to it.
2. Decide whether to have each user review their own access or to have one or more users review everyone's access.
3. In one of the previously listed roles, go to the [Identity Governance page](https://portal.azure.com/#blade/Microsoft_AAD_ERM/DashboardBlade/).
4. Create the access review. For more information, see [Create an access review of groups or applications](create-access-review).
5. When the access review starts, ask the reviewers to give input. By default, they each receive an email from Microsoft Entra ID with a link to the access panel, where they [review access to groups or applications](self-access-review).
6. If the reviewers haven't given input, you can ask Microsoft Entra ID to send them a reminder. By default, Microsoft Entra ID automatically sends a reminder halfway to the end date to all reviewers.
7. After the reviewers give input, stop the access review and apply the changes. For more information, see [Complete an access review of groups or applications](complete-access-review).

## Manage guest access with Microsoft Entra access reviews

With Microsoft Entra ID, you can easily enable collaboration across organizational boundaries by using the [Microsoft Entra B2B feature](../external-id/what-is-b2b). Guest users from other tenants can be [invited by administrators](../external-id/add-users-administrator) or by [other users](../external-id/what-is-b2b). This capability also applies to social identities such as Microsoft accounts.

## Create and perform an access review for guests

The same roles required to create an access review for users are also required to create an access review for guests. For more information, see [Create and perform an access review for users](manage-access-review#create-and-perform-an-access-review-for-users).

Microsoft Entra ID enables several scenarios for reviewing guest users.

You can review either:

- A group in Microsoft Entra ID that has one or more guests as members.
- An application connected to Microsoft Entra ID that has one or more guest users assigned to it.

When reviewing guest user access to Microsoft 365 groups, you can either create a review for each group individually or turn on automatic, recurring access reviews of guest users across all Microsoft 365 groups. The following video provides more information on recurring access reviews of guest users:

You can then decide whether to ask each guest to review their own access or to ask one or more users to review every guest's access.

These scenarios are covered in the following sections.

### Ask guests to review their own membership in a group

You can use access reviews to ensure that users who were invited and added to a group continue to need access. You can easily ask guests to review their own membership in that group.

1. To create an access review for the group, select the review to include guest user members only and that members review themselves. For more information, see [Create an access review of groups or applications](create-access-review).
2. Ask each guest to review their own membership. By default, each guest who accepted an invitation receives an email from Microsoft Entra ID with a link to the access review. Microsoft Entra ID has instructions for guests on how to [review access to groups or applications](self-access-review).
3. After the reviewers give input, stop the access review and apply the changes. For more information, see [Complete an access review of groups or applications](complete-access-review).
4. In addition to those users who denied their own need for continued access, you can also remove users who didn't respond.
5. If the group isn't used for access management, you also can remove users who weren't selected to participate in the review because they didn't accept their invitation. Not accepting might indicate that the invited user's email address had a typo. If a group is used as a distribution list, perhaps some guest users weren't selected to participate because they're contact objects.

### Ask a sponsor to review a guest's membership in a group

You can ask a sponsor, such as the owner of a group, to review a guest's need for continued membership in a group.

1. To create an access review for the group, select the review to include guest user members only. Then specify one or more reviewers. For more information, see [Create an access review of groups or applications](create-access-review).
2. Ask the reviewers to give input. By default, they each receive an email from Microsoft Entra ID with a link to the access panel, where they [review access to groups or applications](self-access-review).
3. After the reviewers give input, stop the access review and apply the changes. For more information, see [Complete an access review of groups or applications](complete-access-review).

Note

You can block external identities from signing-in to your tenant and delete the external identities from your tenant after 30 days. During this period, settings, results, reviewers or Audit logs under the current review won't be viewable or configurable. For more information, see [Disable and delete external identities with Microsoft Entra access reviews](access-reviews-external-users#disable-and-delete-external-identities-with-azure-ad-access-reviews).

### Ask guests to review their own access to an application

You can use access reviews to ensure that users who were invited for a particular application continue to need access. You can easily ask the guests themselves to review their own need for access.

1. To create an access review for the application, select the review to include guests only and that users review their own access. For more information, see [Create an access review of groups or applications](create-access-review).
2. Ask each guest to review their own access to the application. By default, each guest who accepted an invitation receives an email from Microsoft Entra ID. That email has a link to the access review in your organization's access panel. Microsoft Entra ID has instructions for guests on how to [review access to groups or applications](self-access-review).
3. After the reviewers give input, stop the access review and apply the changes. For more information, see [Complete an access review of groups or applications](complete-access-review).
4. In addition to users who denied their own need for continued access, you also can remove guest users who didn't respond or who weren't selected to participate, especially if they weren't recently invited. Those users didn't accept their invitation and so didn't have access to the application.

### Ask a sponsor to review a guest's access to an application

You can ask a sponsor, such as the owner of an application, to review a guest's need for continued access to the application.

1. To create an access review for the application, select the review to include guests only. Then specify one or more users as reviewers. For more information, see [Create an access review of groups or applications](create-access-review).
2. Ask the reviewers to give input. By default, they each receive an email from Microsoft Entra ID with a link to the access panel, where they [review access to groups or applications](self-access-review).
3. After the reviewers give input, stop the access review and apply the changes. For more information, see [Complete an access review of groups or applications](complete-access-review).

### Ask guests to review their need for access, in general

In some organizations, guests might not be aware of their group memberships.

1. Create a security group in Microsoft Entra ID with the guests as members, if a suitable group doesn't already exist. For example, you can create a group with a manually maintained membership of guests. Or, you can create a dynamic group with a name such as "Guests of Contoso" for users in the Contoso tenant who have the UserType attribute value of Guest. Keep in mind that a guest user who is a member of the group can see the other members of the group.
2. To create an access review for that group, select the reviewers to be the members themselves. For more information, see [Create an access review of groups or applications](create-access-review).
3. Ask each guest to review their own membership. By default, each guest who accepted an invitation receives an email from Microsoft Entra ID with a link to the access review in your organization's access panel. Microsoft Entra ID has instructions for guests on how to [review access to groups or applications](perform-access-review).
4. After the reviewers give input, stop the access review. For more information, see [Complete an access review of groups or applications](complete-access-review).
5. Remove guest access for guests who were denied, didn't complete the review, or didn't previously accept their invitation. If some of the guests are contacts who were selected to participate in the review or they didn't previously accept an invitation, you can disable their accounts by using the Microsoft Entra admin center or PowerShell. If the guest no longer needs access and isn't a contact, you can remove their user object from your directory by using the Microsoft Entra admin center or PowerShell to delete the guest user object.
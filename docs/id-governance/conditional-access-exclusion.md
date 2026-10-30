---
layout: Conceptual
title: Manage users excluded from Conditional Access policies - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/conditional-access-exclusion
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to use access reviews to manage users that have been excluded from Conditional Access policies
editor: markwahl-msft
ms.subservice: access-reviews
ms.topic: how-to
ms.date: 2025-06-18T00:00:00.0000000Z
ms.reviewer: mwahl
locale: en-us
document_id: 3533f84b-34f4-df67-748f-2e45f1ce82be
document_version_independent_id: bb6e0bad-d77a-297b-e9c7-1de07fdac696
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/conditional-access-exclusion.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/conditional-access-exclusion
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/conditional-access-exclusion.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: e0a9d6ff-48ce-f647-c63c-297c455983c4
---

# Manage users excluded from Conditional Access policies - Microsoft Entra ID Governance | Microsoft Learn

In an ideal world, all users follow the access policies to secure access to your organization's resources. However, sometimes there are business cases that require you to make exceptions. This article goes over some examples of situations where exclusions could be necessary. You, as the IT administrator, can manage this task, avoid oversight of policy exceptions, and provide auditors with proof that these exceptions are reviewed regularly using Microsoft Entra access reviews.

Note

A valid Microsoft Entra ID P2 or Microsoft Entra ID Governance, Enterprise Mobility + Security E5 paid, or trial license is required to use Microsoft Entra access reviews. For more information, see [Microsoft Entra editions](../fundamentals/licensing).

## Why would you exclude users from policies?

Let's say that as the administrator, you decide to use [Microsoft Entra Conditional Access](../identity/conditional-access/concept-conditional-access-policy-common) to require multifactor authentication (MFA) and limit authentication requests to specific networks or devices. During deployment planning, you realize that not all users can meet these requirements. For example, you could have users who work from remote offices, not part of your internal network. You could also have to accommodate users connecting using unsupported devices while waiting for those devices to be replaced. In short, the business needs these users to sign in and do their job so you exclude them from Conditional Access policies.

As another example, you might be using [named locations](../identity/conditional-access/concept-assignment-network#countries) in Conditional Access to specify a set of countries and regions from which you don't want to allow users to access their tenant.

Unfortunately, some users might still have a valid reason to sign in from these blocked countries/regions. For example, users could be traveling for work and need to access corporate resources. In this case, the Conditional Access policy to block these countries/regions could use a cloud security group for the excluded users from the policy. Users who need access while traveling, can add themselves to the group using [Microsoft Entra self-service Group management](../identity/users/groups-self-service-management).

Another example might be that you have a Conditional Access policy [blocking legacy authentication for most of your users](../identity/conditional-access/policy-block-legacy-authentication). However, if you have some users that need to use legacy authentication methods to access specific resources, then you can exclude these users from the policy that blocks legacy authentication methods.

Note

Microsoft strongly recommends that you block the use of legacy protocols in your tenant to improve your security posture.

## Why are exclusions challenging?

In Microsoft Entra ID, you can scope a Conditional Access policy to a set of users. You can also configure exclusions by selecting Microsoft Entra roles, individual users, or guests. You should keep in mind that when exclusions are configured, the policy intent can't be enforced on excluded users. If exclusions are configured using a list of users or using legacy on-premises security groups, you have limited visibility into the exclusions. As a result:

- Users might not know that they're excluded.
- Users can join the security group to bypass the policy.
- Excluded users could have qualified for the exclusion before but no longer qualify for it.

Frequently, when you first configure an exclusion, there's a shortlist of users who bypass the policy. Over time, more users get added to the exclusion, and the list grows. At some point, you need to review the list and confirm that each of these users is still eligible for exclusion. Managing the exclusion list, from a technical point of view, can be relatively easy, but who makes the business decisions, and how do you make sure it's all auditable? However, if you configure the exclusion using a Microsoft Entra group, you can use access reviews as a compensating control, to drive visibility, and reduce the number of excluded users.

## How to create an exclusion group in a Conditional Access policy

Follow these steps to create a new Microsoft Entra group and a Conditional Access policy that doesn't apply to that group.

### Create an exclusion group

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Groups** &gt; **All groups**.
3. Select **New group**.
4. In the **Group type** list, select **Security**. Specify a name and description.
5. Make sure to set the **Membership** type to **Assigned**.
6. Select the users that should be part of this exclusion group and then select **Create**.

![New group pane in Microsoft Entra ID](media/conditional-access-exclusion/new-group.png)

### Create a Conditional Access policy that excludes the group

Now you can create a Conditional Access policy that uses this exclusion group.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access**.
3. Select **Create new policy**.
4. Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.
5. Under Assignments select **Users and groups**.
6. On the **Include** tab, select **All Users**.
7. Under **Exclude**, select **Users and groups** and choose the exclusion group you created.

    Note

    As a best practice, it is recommended to exclude at least one administrator account from the policy when testing to make sure you are not locked out of your tenant.
8. Continue with setting up the Conditional Access policy based on your organizational requirements.

![Select excluded users pane in Conditional Access](media/conditional-access-exclusion/select-excluded-users.png)

Let's cover two examples where you can use access reviews to manage exclusions in Conditional Access policies.

## Example 1: Access review for users accessing from blocked countries/regions

Let's say you have a Conditional Access policy that blocks access from certain countries/regions. It includes a group that is excluded from the policy. Here's a recommended access review where members of the group are reviewed.

![Create an access review pane for example 1](media/conditional-access-exclusion/create-access-review-1.png)

Note

At least the Identity Governance Administrator, or User Administrator role, is required to create access reviews. For a step by step guide on creating an access review, see: [Create an access review of groups and applications](create-access-review).

1. The review happens every week.
2. The review never ends in order to make sure you're keeping this exclusion group most up to date.
3. All members of this group are in scope for the review.
4. Each user needs to self-attest that they still need access from these blocked countries/regions, therefore they still need to be a member of the group.
5. If the user doesn't respond to the review request, they're automatically removed from the group, and no longer has access to the tenant while traveling to these countries/regions.
6. Enable email notifications to let users know about the start and completion of the access review.

## Example 2: Access review for users accessing with legacy authentication

Let's say you have a Conditional Access policy that blocks access for users using legacy authentication and older client versions and it includes a group that is excluded from the policy. Here's a recommended access review where members of the group are reviewed.

![Create an access review pane for example 2](media/conditional-access-exclusion/create-access-review-2.png)

1. This review would need to be a recurring review.
2. Everyone in the group would need to be reviewed.
3. It could be configured to list the business unit owners as the selected reviewers.
4. Auto-apply the results and remove users that aren't approved to continue using legacy authentication methods.
5. It might be beneficial to enable recommendations so reviewers of large groups can easily make their decisions.
6. Enable mail notifications so users are notified about the start and completion of the access review.

Important

If you have many exclusion groups and therefore need to create multiple access reviews, Microsoft Graph allows you to create and manage them programmatically. To get started, see the [access reviews API reference](/en-us/graph/api/resources/accessreviewsv2-overview) and [tutorial using the access reviews API in Microsoft Graph](/en-us/graph/tutorial-accessreviews-securitygroup).

## Access review results and audit logs

Now that you have everything in place, group, Conditional Access policy, and access reviews, it's time to monitor and track the results of these reviews.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Access reviews**.
3. Select the Access review you're using with the group you created an exclusion policy for.
4. Select **Results** to see who was approved to stay on the list and who was removed.

    ![Access reviews results show who was approved](media/conditional-access-exclusion/access-reviews-results.png)
5. Select **Audit logs** to see the actions that were taken during this review.

As an IT administrator, you know that managing exclusion groups to your policies is sometimes inevitable. However, maintaining these groups, reviewing them regularly by the business owner or the users themselves, and auditing these changes can be made easier with access reviews.
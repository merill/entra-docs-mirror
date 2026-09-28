---
layout: Conceptual
title: Delegate approvals and access reviews in My Access (Preview) - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/delegate-approvals-my-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to delegate approvals and access reviews to another user in My Access.
ms.topic: how-to
ms.date: 2026-06-03T00:00:00.0000000Z
locale: en-us
document_id: 3b1745f2-215a-be13-6271-d426245fcfe7
document_version_independent_id: 3b1745f2-215a-be13-6271-d426245fcfe7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/delegate-approvals-my-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/delegate-approvals-my-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/delegate-approvals-my-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7e43c33f-44e4-255c-03f3-2ece1191dd0a
---

# Delegate approvals and access reviews in My Access (Preview) - Microsoft Entra ID Governance | Microsoft Learn

Approval delegation in My Access allows approvers to assign another individual to respond to access package approval requests and multi-resource access reviews on their behalf. This feature helps maintain productivity when approvers are unavailable due to leave, travel, or other commitments.

## License requirements

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## How delegation works

When an approver sets a delegate, the following happens:

- All approvals explicitly assigned to an approver (not through a group) after delegation are routed to the specified delegate.
- Multi-resource access reviews assigned after delegation are routed to the specified delegate.
- The original approver can still respond to approvals and access reviews during the delegation period.
- Delegations can be time-bound or indefinite.
- Delegates are notified when they're assigned.
- Requestors are notified when their request is approved by a delegate.
- Delegation is always bulk; approvers can't delegate specific approvals or reviews.

Note

Delegation for access reviews applies only to multi-resource (catalog) access reviews. Single-resource access reviews (such as those for a single group or application) aren't included in delegation.

### What delegates can see

**Delegates can**:

- View approvals and multi-resource access reviews assigned to them.
- See who delegated the items.
- Respond to approvals and access reviews during the specified time period.

**Delegates can't**:

- Redelegate approvals or access reviews.
- See items assigned before the delegation was set.

## Limitations

- Delegation is limited to one level. If User A delegates to User B, and User B delegates to User C, User C won't receive approvals from User A.
- Delegation only applies to approvals explicitly assigned to an approver, not those assigned through a group.
- Delegation applies only to items assigned after the delegation is configured.
- Access review delegation applies only to multi-resource access reviews.

## Enable delegate approvals preview

To enable approvers to delegate in My Access, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Entitlement Management** &gt; **Preview Features**.
3. Select **Allow users to delegate approvals and access reviews in My Access**.

## Restrict who users can delegate to

Administrators can control who users are allowed to select as a delegate. Configure these restrictions in the Microsoft Entra admin center.

| Restriction | Behavior |
| --- | --- |
| **Direct manager only** | Users can only delegate to their direct manager as defined in Microsoft Entra ID. |
| **Specific groups** | Users can only delegate to members of one or more administrator-defined groups. |
| **Unrestricted** | Users can delegate to any user in the directory. |
| **Limit delegation duration** | Administrators can set a maximum duration for new and updated delegations. Delegations without an expiration date are rejected. |

Note

When both a manager restriction and a group restriction are configured, a user can delegate to anyone who meets either restriction. For example, if an admin sets direct manager and a specific group, the user can delegate to their manager or to any member of that group.

To configure delegation restrictions:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Entitlement Management** &gt; **Settings**.
3. Under **Delegate restrictions**, choose the restriction type and configure the allowed groups if applicable.
4. Select **Save**.

## Set up a delegate

With the delegate option enabled, you can set up a delegate to approve access and respond to multi-resource access reviews on your behalf. To set up a delegate, follow these steps:

1. Sign in to the [My Access portal](https://myaccess.microsoft.com).
2. On the left menu, select **Approvals** or **Access reviews**.
3. Select **Delegate approvals and access reviews**.
4. In the dialog box that opens:

    1. In the **User** field, enter the name or email of the person you want to delegate to.
    2. Set the **Start date** for the delegation.
    3. Set the **End date** for the delegation, or select the **No end date** checkbox for an indefinite delegation.
5. Select **Delegate**.

The active delegation appears on both the **Approvals** page and the **Access reviews** page.

### Edit or remove a delegate

#### Edit the delegate

1. Sign in to the [My Access portal](https://myaccess.microsoft.com).
2. On the left menu, select **Approvals** or **Access reviews**.
3. Select the active delegate display that shows your current delegate's name.
4. In the **Edit delegate** dialog box, update the delegate, start date, or end date as needed.
5. Select **Save and apply**.

#### Remove the delegate

1. Sign in to the [My Access portal](https://myaccess.microsoft.com).
2. On the left menu, select **Approvals** or **Access reviews**.
3. Select the active delegate display that shows your current delegate's name.
4. In the **Edit delegate** dialog box, select **Remove delegate**.
5. Select **Confirm**.

After you confirm, the delegate can no longer respond to your approvals and access reviews.
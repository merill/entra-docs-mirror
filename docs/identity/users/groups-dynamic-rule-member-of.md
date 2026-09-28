---
layout: Conceptual
title: Configure dynamic membership groups with the memberOf operator in the Entra Admin Center (preview) - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-dynamic-rule-member-of
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Learn how to create a dynamic membership group that can contain members of other groups in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2026-08-04T00:00:00.0000000Z
ms.reviewer: mbhargav
ms.custom: it-pro
locale: en-us
document_id: a30c67d5-6cc0-16f3-db2a-8244d7344aa3
document_version_independent_id: ab230d40-68c6-3a1f-c4c3-12d4a76e42df
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-dynamic-rule-member-of.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-dynamic-rule-member-of
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-dynamic-rule-member-of.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: 0c7cfd28-27d2-eb3f-9eca-8e6024fad234
---

# Configure dynamic membership groups with the memberOf operator in the Entra Admin Center (preview) - Microsoft Entra ID | Microsoft Learn

## Overview

This feature preview in Microsoft Entra ID enables admins to create dynamic membership groups and administrative units that populate by adding members of other groups using the `memberOf` attribute. Apps that couldn't read group-based membership previously in Microsoft Entra ID can now read the entire membership of these new `memberOf` groups. Not only can these groups be used for apps but they can also be used for licensing assignments.

Important

The public preview of the `memberOf` rule operator is ending. After **November 3, 2026**, dynamic membership groups, dynamic administrative units, and entitlement management auto-assignment policies that use the `memberOf` operator stop updating and remain in their last known state. This can lead to stale access and enforcement gaps, including outdated Teams and SharePoint access, Conditional Access targeting, group-based licensing, and access package assignments.

Before November 3, 2026, review all uses of the `memberOf` operator and remove or replace those configurations. See Migrate before the preview ends. This is a preview feature that isn't intended for production use; review the Preview limitations.

The following diagram illustrates how you could create Dynamic-Group-A with members of Security-Group-X and Security-Group-Y. Members of the groups inside Security-Group-X and Security-Group-Y don't become members of Dynamic-Group-A.

![Diagram that shows how the memberOf attribute works.](media/groups-dynamic-rule-member-of/member-of-diagram.png)

With this preview, admins can configure dynamic membership groups with the `memberOf` attribute in the Azure portal, Microsoft Graph, and PowerShell. Security groups, Microsoft 365 groups, and groups that are synced from on-premises Active Directory can all be added as members of these dynamic membership groups. They can also all be added to a single group. For example, the dynamic group could be a security group, but you can use Microsoft 365 groups, security groups, and groups that are synced from on-premises to define its membership.

## Prerequisites

You must be at least a [User Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#user-administrator) to use the `memberOf` attribute to create a Microsoft Entra dynamic group. You must have a Microsoft Entra ID P1 or P2 license for the Microsoft Entra tenant.

## Preview limitations

- This preview should only be used in test environments as it can affect dynamic group processing in the tenant. These limitations are being addressed, and updates will be provided when they're available.
- Each Microsoft Entra tenant is limited to 500 dynamic groups using the `memberOf` attribute. The `memberOf` groups count toward the total dynamic group quota of 15,000.
- Each dynamic group can have up to 50 member groups.
- When you add members of security groups to `memberOf` dynamic membership groups, only direct members of the security group become members of the dynamic group.
- You can't use one `memberOf` dynamic group to define the membership of another `memberOf` dynamic group. For example, Dynamic Group A, with members of group B and C in it, can't be a member of Dynamic Group D.
- The `memberOf` attribute can't be used with other rules. For example, a rule that states dynamic group A should contain members of group B and also should contain only users located in Redmond will fail.
- The dynamic group rule builder and validate feature can't be used for `memberOf` at this time.
- The `memberOf` attribute can't be used with other operators. For example, you can't create a rule that states "Members Of group A can't be in Dynamic group B."
- Users included in `memberOf` dynamic membership groups might cause a slower processing time for your tenant, if the tenant has a large number of groups or frequent dynamic membership groups updates.
- Membership of a memberOf dynamic group doesn't automatically update when a child group is deleted or when members are removed from a child group. The affected users or devices remain members of the memberOf dynamic group until the rule is modified.
- Only available in public cloud.

## Get started

This feature is available in the Azure portal, Microsoft Graph, and PowerShell. However, the `memberOf` attribute isn’t currently supported in the rule builder UI. To use `memberOf` in the Azure portal, you must define the rule by using the rule editor (advanced syntax).

### Create a memberOf dynamic group

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Groups** &gt; **All groups**.
3. Select **New group**.
4. Fill in group details. The group type can be **Security** or **Microsoft 365**, and the membership type can be set to **Dynamic User** or **Dynamic Device**.
5. Select **Add dynamic query**.
6. MemberOf isn't yet supported in the rule builder UI. Select **Edit** to write the rule in the **Rule syntax** box.

    1. Example user rule: `user.memberof -any (group.objectId -in ['groupId'])`
    2. Example device rule: `device.memberof -any (group.objectId -in ['groupId'])`

    Note

    Replace `'groupId'` with the **object ID of the source group** whose members you want to include in the dynamic group.

    The two examples are alternatives:

    - Use the **user** rule when creating a **Dynamic user** group.
    - Use the **device** rule when creating a **Dynamic device** group.

    To include multiple source groups, specify multiple group object IDs. For example:

    ```text
    user.memberof -any (group.objectId -in ['<groupObjectId1>', '<groupObjectId2>'])
    ```
7. Select **OK**.
8. Select **Create group**.

## Migrate before the preview ends

As Microsoft continues to improve the scale and reliability of dynamic membership processing, the `memberOf` preview is ending. During preview, we observed that using `memberOf` can slow dynamic membership processing for all groups in a tenant. `memberOf` is a preview operator and isn't recommended for production use.

We recognize the importance of the customer scenarios that `memberOf` addresses, and we're continuing to develop an alternative solution that meets these needs with the right level of scalability and reliability. In the interim, identify and replace every configuration that uses the `memberOf` operator before November 3, 2026. After that date, configurations that still use `memberOf` stop updating and stay in their last known state, which can leave access stale and enforcement gaps in place.

**Dynamic membership groups**

- Export dynamic membership groups from the Microsoft Entra admin center and identify rules that contain `memberOf`.
- Replace `memberOf` with [supported rule operators](groups-dynamic-rule-more-efficient), or convert the group to assigned membership.
- Validate group membership after making changes. If the group is no longer needed, pause or delete it.

**Dynamic administrative units**

- Use Microsoft Graph PowerShell to identify [dynamic administrative units](../role-based-access-control/admin-units-members-dynamic) that use `memberOf` rules.
- Replace `memberOf`-based rules with supported logic, or convert the administrative unit to assigned membership.
- Validate both membership and administrative scope. If the administrative unit is no longer needed, delete it.

**Entitlement management auto-assignment policies**

- Use Microsoft Graph PowerShell to identify [auto-assignment policies](../../id-governance/entitlement-management-access-package-auto-assignment-policy) that use `memberOf`.
- Replace `memberOf`-based logic with supported attribute-based operators where possible. If no equivalent rule is available, plan an alternative assignment method before retirement.
- Validate access package assignments after making changes.
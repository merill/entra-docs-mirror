---
layout: Conceptual
title: Use Microsoft Entra groups to manage role assignments - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/groups-concept
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: Use Microsoft Entra groups to simplify role assignment management in Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2026-03-16T00:00:00.0000000Z
ms.reviewer: vincesm
ms.custom: it-pro
locale: en-us
document_id: c1414bc2-4151-b667-65f5-b44f2bf582a1
document_version_independent_id: b93aee66-1769-8d98-fea5-ebca3a12d5fc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/groups-concept.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/groups-concept
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/groups-concept.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 36bc0475-e9ce-fc3e-2232-8bbe455f5d2e
---

# Use Microsoft Entra groups to manage role assignments - Microsoft Entra ID | Microsoft Learn

With Microsoft Entra ID P1 or P2, you can create role-assignable groups and assign Microsoft Entra roles to these groups. This feature simplifies role management, ensures consistent access, and makes auditing permissions more straightforward. Assigning roles to a group instead of individuals allows for easy addition or removal of users from a role and creates consistent permissions for all members of the group. You can also create custom roles with specific permissions and assign them to groups.

## Why assign roles to groups?

Consider the example where the Contoso company has hired people across geographies to manage and reset passwords for employees in its Microsoft Entra organization. Instead of asking a Privileged Role Administrator to assign the Helpdesk Administrator role to each person individually, they can create a Contoso\_Helpdesk\_Administrators group and assign the role to the group. When people join the group, they're assigned the role indirectly. Your existing governance workflow can then take care of the approval process and auditing of the group's membership to ensure that only legitimate users are members of the group and are thus assigned the Helpdesk Administrator role.

## How role assignments to groups work

To assign a role to a group, you must create a new security or Microsoft 365 group with the `isAssignableToRole` property set to `true`. In the Microsoft Entra admin center, you set the **Microsoft Entra roles can be assigned to the group** option to **Yes**. Either way, you can then assign one or more Microsoft Entra roles to the group in the same way as you assign roles to users.

![Screenshot of the Roles and administrators page](media/groups-concept/role-assignable-group.png)

## Restrictions for role-assignable groups

Role-assignable groups have the following restrictions:

- You can only set the `isAssignableToRole` property or the **Microsoft Entra roles can be assigned to the group** option for new groups.
- The `isAssignableToRole` property is **immutable**. Once a group is created with this property set, it can't be changed.
- You can't make an existing group a role-assignable group.
- A maximum of 500 role-assignable groups can be created in a single Microsoft Entra organization (tenant).

## How are role-assignable groups protected?

If a group is assigned a role, any IT administrator who can manage dynamic membership groups could also indirectly manage the membership of that role. For example, assume that a group named Contoso\_User\_Administrators is assigned the User Administrator role. An Exchange administrator who can modify dynamic membership groups could add themselves to the Contoso\_User\_Administrators group and in that way become a User Administrator. As you can see, an administrator could elevate their privilege in a way you didn't intend.

Only groups that have the `isAssignableToRole` property set to `true` at creation time can be assigned a role. This property is immutable. Once a group is created with this property set, it can't be changed. You can't set the property on an existing group.

Role-assignable groups are designed to help prevent potential breaches by having the following restrictions:

- You must be assigned at least the Privileged Role Administrator role to create a role-assignable group.
- The membership type for role-assignable groups must be Assigned and can't be a Microsoft Entra dynamic group. Automated population of dynamic membership groups could lead to an unwanted account being added to the group and thus assigned to the role.
- By default, Privileged Role Administrators can manage the membership of a role-assignable group, but you can delegate the management of role-assignable groups by adding group owners.
- For Microsoft Graph, the *RoleManagement.ReadWrite.Directory* permission is required to be able to manage the membership of role-assignable groups. The *Group.ReadWrite.All* permission won't work.
- To prevent elevation of privilege, you must be assigned at least the Privileged Authentication Administrator role to change the credentials, reset MFA, or modify sensitive attributes for members and owners of a role-assignable group.
- Group nesting isn't supported. A group can't be added as a member of a role-assignable group.

## Delete and restore behavior

When a role-assignable group is deleted, it's soft-deleted and can be restored within 30 days. Group owners can restore a deleted role-assignable group. For information about how to restore a deleted group, see [Restore a deleted Microsoft 365 group or cloud security group in Microsoft Entra ID](../users/groups-restore-deleted).

## Use PIM to make a group eligible for a role assignment

If you don't want members of the group to have standing access to a role, you can use [Microsoft Entra Privileged Identity Management (PIM)](../../id-governance/privileged-identity-management/pim-configure) to make a group eligible for a role assignment. Each member of the group is then eligible to activate the role assignment for a fixed time duration.

Note

For groups used for elevating into Microsoft Entra roles, we recommend that you require an approval process for eligible member assignments. Assignments that can be activated without approval can leave you vulnerable to a security risk from less-privileged administrators, who might be able to reset a user's credentials and then activate the assignment on their behalf.

Confirm that groups used for role elevation are created as [role-assignable](groups-concept). You must be assigned at least the Privileged Authentication Administrator role to change the credentials of members and owners of a role-assignable group.

## Scenarios not supported

The following scenarios aren't supported:

- Assign Microsoft Entra roles (built-in or custom) to on-premises groups.

## Known issues

The following are known issues with role-assignable groups:

- *Microsoft Entra ID P2 licensed customers only*: Even after deleting the group, it's still shown as an eligible member of the role in PIM UI. Functionally there's no problem; it's just a cache issue in the Microsoft Entra admin center.
- Use the new [Exchange admin center](/en-us/exchange/exchange-admin-center) for role assignments via dynamic membership groups. The old Exchange admin center doesn't support this feature. If accessing the old Exchange admin center is required, assign the eligible role directly to the user (not via role-assignable groups). Exchange PowerShell cmdlets work as expected.
- If an administrator role is assigned to a role-assignable group instead of individual users, members of the group won't be able to access Rules, Organization, or Public Folders in the new [Exchange admin center](/en-us/exchange/exchange-admin-center). The workaround is to assign the role directly to users instead of the group.
- Azure Information Protection Portal (the classic portal) doesn't recognize role membership via group yet. You can [migrate to the unified sensitivity labeling platform](/en-us/azure/information-protection/configure-policy-migrate-labels) and then use the Microsoft Purview portal to use group assignments to manage roles.

## License requirements

Using this feature requires a Microsoft Entra ID P1 license. The Privileged Identity Management for just-in-time role activation requires a Microsoft Entra ID P2 license. To find the right license for your requirements, see [Comparing generally available features of the Free and Premium editions](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).
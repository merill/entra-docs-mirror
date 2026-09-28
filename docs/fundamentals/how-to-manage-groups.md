---
layout: Conceptual
title: How to manage groups - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/how-to-manage-groups
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Instructions about how to create and update Microsoft Entra groups, such as membership and settings.
ms.date: 2026-06-17T00:00:00.0000000Z
ms.topic: how-to
ms.custom:
- ge-structured-content-pilot
- sfi-image-nochange
locale: en-us
document_id: 21b5b297-ac9c-3b4d-ef17-4771050ff989
document_version_independent_id: 21b5b297-ac9c-3b4d-ef17-4771050ff989
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/how-to-manage-groups.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/how-to-manage-groups
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/how-to-manage-groups.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ea3b9ace-1e89-ae12-9ad8-ddf720d56bc1
---

# How to manage groups - Microsoft Entra | Microsoft Learn

Microsoft Entra groups are used to manage users that all need the same access and permissions to resources, such as potentially restricted apps and services. Instead of adding special permissions to individual users, you create a group that applies the special permissions to every member of that group.

This article covers basic group scenarios where a single group is added to a single resource and users are added as members to that group. For more complex scenarios like dynamic membership groups and rule creation, see the [Microsoft Entra user management documentation](../identity/users/).

Before adding groups and members, [learn about groups and membership types](concept-learn-about-groups) to help you decide which options to use when you create a group.

## Prerequisites

The following prerequisites are required to manage groups in Microsoft Entra:

- **[User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator)** or **[Groups Administrator](../identity/role-based-access-control/permissions-reference#groups-administrator)** role is required to manage group membership settings.
- An Azure subscription. If you don't have one, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Access to a Microsoft Entra tenant. For more information, see [Create a new tenant](create-new-tenant).

## Create a basic group and add members

You can create a basic group and add your members at the same time using the Microsoft Entra admin center. You must have at least the **Groups Administrator** or **User Administrator** role assigned to create groups. Review the [appropriate Microsoft Entra roles for managing groups](../identity/role-based-access-control/delegate-by-task#groups-least-privileged-roles).

Note

[Cross-tenant delegated administration](../id-governance/tenant-governance/cross-tenant-delegated-administration) uses granular delegated admin privileges (GDAP). Group creation by GDAP administrators isn't supported if the target tenant uses a group naming policy prefix or suffix that references attributes of the calling user, such as department or company name. Use an administrator account in the target tenant to create the group.

To create a basic group and add members:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](../identity/role-based-access-control/permissions-reference#groups-administrator).
2. Browse to **Entra ID** &gt; **Groups** &gt; **All groups**.
3. Select **New group**.

    ![Screenshot of the 'Microsoft Entra groups' page with 'New group' option highlighted.](media/how-to-manage-groups/new-group.png)
4. Select a **Group type**. For more information on group types, see the [learn about groups and membership types](concept-learn-about-groups) article.

    - Selecting the **Microsoft 365** Group type enables the **Group email address** option.
5. Enter a **Group name.** Choose a name that you'll remember and that makes sense for the group. A check will be performed to determine if the name is already in use. If the name is already in use, you'll be asked to change the name of your group.

    - The name of the group can't start with a space. Starting the name with a space prevents the group from appearing as an option for steps such as adding role assignments to group members.
6. **Group email address**: Only available for Microsoft 365 group types. Enter an email address manually or use the email address built from the Group name you provided.
7. **Group description.** Add an optional description to your group.
8. Switch the **Microsoft Entra roles can be assigned to the group** setting to yes to use this group to assign Microsoft Entra roles to members.

    - This option is only available with P1 or P2 licenses.
    - You must have at least the **Privileged Role Administrator** role.
    - Enabling this option automatically selects **Assigned** as the Membership type.
    - The ability to add roles while creating the group is added to the process.
    - [Learn more about role-assignable groups](../identity/role-based-access-control/groups-create-eligible).
9. Select a **Membership type.** For more information on membership types, see the [learn about groups and membership types](concept-learn-about-groups) article.
10. Optionally add **Owners** or **Members**. Members and owners can be added after creating your group.

    1. Select the link under **Owners** or **Members** to populate a list of every user in your directory.
    2. Choose users from the list and then select the **Select** button at the bottom of the window.

    ![Screenshot of selecting members for your group during the group creation process.](media/how-to-manage-groups/add-members.png)
11. Select **Create**. Your group is created and ready for you to manage other settings.

### Turn off group welcome email

    A welcome notification is sent to all users when they're added to a new Microsoft 365 group, regardless of the membership type. When an attribute of a user or device changes, all rules for dynamic membership groups in the organization are processed for potential membership changes. Users who are added then also receive the welcome notification. You can turn off this behavior in [Exchange PowerShell](/en-us/powershell/module/exchange/set-unifiedgroup).

## Add members or owners of a group

Members and owners can be added from existing groups. The process is the same for members and owners. You'll need the **Groups Administrator** or **User Administrator** role to add members and owners.

Note

Need to add multiple members at one time? Learn about the [add members in bulk](../identity/users/groups-bulk-import-members) option.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](../identity/role-based-access-control/permissions-reference#groups-administrator).
2. Browse to **Entra ID** &gt; **Groups** &gt; **All groups**.
3. Select the group you need to manage.
4. Select either **Members** or **Owners**.

    ![Screenshot of the Group overview page with Members and Owners menu options highlighted.](media/how-to-manage-groups/groups-members-owners.png)
5. Select **+ Add** (members or owners).
6. Scroll through the list or enter a name in the search box. You can choose multiple names at one time. When you're ready, select the **Select** button.

    The **Group Overview** page updates to show the number of members who are now added to the group.

## Remove members or owners of a group

Members and owners can be removed from existing groups. The process is the same for members and owners. You'll need the **Groups Administrator** or **User Administrator** role to remove members and owners.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](../identity/role-based-access-control/permissions-reference#groups-administrator).
2. Browse to **Entra ID** &gt; **Groups** &gt; **All groups**.
3. Select the group you need to manage.
4. Select either **Members** or **Owners**.
5. Check the box next to a name from the list and select the **Remove** button.

    ![Screenshot of group members with a name selected and the Remove button highlighted.](media/how-to-manage-groups/groups-remove-member.png)

## Edit group settings

You can edit a group's name, description, or membership type. You'll need the **Groups Administrator** or **User Administrator** role to edit a group's settings.

To edit your group settings:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](../identity/role-based-access-control/permissions-reference#groups-administrator).
2. Browse to **Entra ID** &gt; **Groups** &gt; **All groups**.
3. Scroll through the list or enter a group name in the search box. Select the group you need to manage.
4. Select **Properties** from the side menu.
5. Update the **General settings** information as needed, including:

    - **Group name.** Edit the existing group name.
    - **Group description.** Edit the existing group description.
    - **Group type.** You can't change the type of group after it's been created. To change the **Group type**, you must delete the group and create a new one.
    - **Membership type.** Change the membership type. If you enabled the **Microsoft Entra roles can be assigned to the group** option, you can't change the membership type. For more info about the available membership types, see the [learn about groups and membership types](concept-learn-about-groups) article.
    - **Object ID.** You can't change the Object ID, but you can copy it to use in your PowerShell commands for the group. For more info about using PowerShell cmdlets, see [Microsoft Entra cmdlets for configuring group settings](../identity/users/groups-settings-v2-cmdlets).

## Add a group to another group

For the security group type, you can add an existing group to another group (also known as nested groups). Depending on the group membership types, you can add a group as a member of another group. Nested groups can be used for membership and Conditional Access scopes. Nested groups don't gain access to shared resources and applications that are assigned to the parent group.

We currently don't support:

- Adding groups to a group synced with on-premises Active Directory.
- Adding security groups to Microsoft 365 groups.
- Adding Microsoft 365 groups to security groups or other Microsoft 365 groups.
- Assigned membership to shared resources and apps for nested security groups.
- Applying licenses to nested security groups.
- Adding distribution groups in nesting scenarios.
- Adding security groups as members of mail-enabled security groups.
- Adding groups as members of a role-assignable group.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](../identity/role-based-access-control/permissions-reference#groups-administrator).
2. Browse to **Entra ID** &gt; **Groups** &gt; **All groups**.
3. On the **All groups** page, search for and select the group you want to become a member of another group.

    Note

    You only can add your group as a member to one other group at a time. Wildcard characters aren't supported in the **Select Group** search box.
4. On the group Overview page, select **Group memberships** from the side menu.
5. Select **+ Add memberships**.
6. Locate the group you want your group to be a member of and choose **Select**.

    For this exercise, we're adding "MDM policy - West" to the "MDM policy - All org" group. The "MDM - policy - West" group will have the same access as the "MDM policy - All org" group.

    ![Screenshot of making a group the member of another group with Group membership from the side menu and 'Add membership' option highlighted.](media/how-to-manage-groups/nested-groups-selected.png)

    Now you can review the "MDM policy - West - Group memberships" page to see the group and member relationship.

    For a more detailed view of the group and member relationship, select the parent group name (MDM policy - All org) and take a look at the "MDM policy - West" page details.

## Remove a group from another group

You can remove an existing Security group from another Security group; however, removing the group also removes any inherited access for its members.

1. On the **All groups** page, search for and select the group you need to remove as a member of another group.
2. On the group Overview page, select **Group memberships**.
3. Select the parent group from the **Group memberships** page.
4. Select **Remove**.

    For this exercise, we're now going to remove "MDM policy - West" from the "MDM policy - All org" group.

    ![Screenshot of the 'Group membership' page showing both the member and the group details with 'Remove membership' option highlighted.](media/how-to-manage-groups/remove-nested-group.png)

## Delete a group

You can delete a group for any number of reasons, but typically it will be because you:

- Choose the incorrect **Group type** option.
- Created a duplicate group by mistake.
- No longer need the group.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](../identity/role-based-access-control/permissions-reference#groups-administrator).
2. Browse to **Entra ID** &gt; **Groups** &gt; **All groups**.
3. Search for and select the group you want to delete.
4. Select **Delete**.
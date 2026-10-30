---
layout: Conceptual
title: Add users, groups, or devices to an administrative unit - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/admin-units-members-add
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: Add users, groups, or devices to an administrative unit in Microsoft Entra ID
ms.topic: how-to
ms.date: 2026-03-04T00:00:00.0000000Z
ms.reviewer: anandy
ms.custom: oldportal;it-pro;, sfi-image-nochange
locale: en-us
document_id: 43480033-c11c-c89d-bbaf-7d9790000782
document_version_independent_id: 4ff490a6-474c-1305-29b7-d728de56d7b2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/admin-units-members-add.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/admin-units-members-add
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/admin-units-members-add.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 9f21e1d8-945f-ebb4-721a-3e32200641c7
---

# Add users, groups, or devices to an administrative unit - Microsoft Entra ID | Microsoft Learn

In Microsoft Entra ID, you can add users, groups, or devices to an administrative unit to limit the scope of role permissions. Adding a group to an administrative unit brings the group itself into the management scope of the administrative unit, but **not** the members of the group. For additional details on what scoped administrators can do, see [Administrative units in Microsoft Entra ID](administrative-units).

This article describes how to add users, groups, or devices to administrative units manually. For information about how to add users or devices to administrative units dynamically using rules, see [Manage users or devices for an administrative unit with rules for dynamic membership groups](admin-units-members-dynamic).

## Prerequisites

- Microsoft Entra ID P1 or P2 license for each administrative unit administrator
- Microsoft Entra ID Free licenses for administrative unit members
- To add existing users, groups, or devices:
    - Privileged Role Administrator
- To create new groups:
    - Groups Administrator (scoped to the administrative unit or entire directory)
- [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/installation) module when using PowerShell
- Admin consent when using Graph Explorer for Microsoft Graph API

For more information, see [Prerequisites to use PowerShell or Graph Explorer](prerequisites).

# [Admin center](#tab/admin-center)
You can add users, groups, or devices to administrative units using the Microsoft Entra admin center. You can also add users in a bulk operation or create a new group in an administrative unit.

### Add a single user, group, or device to administrative units

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID**.
3. Browse to one of the following:

    - **Users** &gt; **All users**
    - **Groups** &gt; **All groups**
    - **Devices** &gt; **All devices**
4. Select the user, group, or device you want to add to administrative units.
5. Select **Administrative units**.
6. Select **Assign to administrative unit**.
7. In the **Select** pane, select the administrative units and then select **Select**.

    [![Screenshot of the Administrative units page for adding a user to an administrative unit.](media/admin-units-members-add/assign-users-individually.png)](media/admin-units-members-add/assign-users-individually.png#lightbox)

### Add users, groups, or devices to a single administrative unit

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID** &gt; **Roles & admins** &gt; **Admin units**.
3. Select the administrative unit you want to add users, groups, or devices to.
4. Select one of the following:

    - **Users**
    - **Groups**
    - **Devices**
5. Select **Add member**, **Add**, or **Add device**.
6. In the **Select** pane, select the users, groups, or devices you want to add to the administrative unit and then select **Select**.

    [![Screenshot of adding multiple devices to an administrative unit.](media/admin-units-members-add/admin-unit-members-add.png)](media/admin-units-members-add/admin-unit-members-add.png#lightbox)

### Add users to an administrative unit in a bulk operation

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID** &gt; **Roles & admins** &gt; **Admin units**.
3. Select the administrative unit you want to add users to.
4. Select **Users** &gt; **Bulk operations** &gt; **Bulk add members**.

    [![Screenshot of the Users page for assigning users to an administrative unit as a bulk operation.](media/admin-units-members-add/bulk-assign-to-admin-unit.png)](media/admin-units-members-add/bulk-assign-to-admin-unit.png#lightbox)
5. In the **Bulk add members** pane, download the comma-separated values (CSV) template.
6. Edit the downloaded CSV template with the list of users you want to add.

    Add one user principal name (UPN) in each row. Don't remove the first two rows of the template.
7. Save your changes and upload the CSV file.

    [![Screenshot of an edited CSV file for adding users to an administrative unit in bulk.](media/admin-units-members-add/bulk-user-entries.png)](media/admin-units-members-add/bulk-user-entries.png#lightbox)
8. Select **Submit**.

### Create a new group in an administrative unit

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](permissions-reference#groups-administrator).
2. Browse to **Entra ID** &gt; **Roles & admins** &gt; **Admin units**.
3. Select the administrative unit you want to create a new group in.
4. Select **Groups**.
5. Select **New group** and complete the steps to create a new group.

    [![Screenshot of the Administrative units page for creating a new group in an administrative unit.](media/admin-units-members-add/admin-unit-create-group.png)](media/admin-units-members-add/admin-unit-create-group.png#lightbox)

# [PowerShell](#tab/ms-powershell)
Use the [New-MgDirectoryAdministrativeUnitMemberByRef](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/new-mgdirectoryadministrativeunitmemberbyref) command to add user, groups, or devices to an administrative unit or create a new group in an administrative unit.

### Add users to an administrative unit

```powershell
$adminUnitObj = Get-MgDirectoryAdministrativeUnit -Filter "DisplayName eq '{admin-unit-id}'"
$userObj = Get-MgUser -Filter "UserPrincipalName eq '{user-principal-name}'"
$odataId = "https://graph.microsoft.com/v1.0/users/" + $userObj.Id
New-MgDirectoryAdministrativeUnitMemberByRef -AdministrativeUnitId $adminUnitObj.Id -OdataId $odataId
```

### Add groups to an administrative unit

```powershell
$adminUnitObj = Get-MgDirectoryAdministrativeUnit -Filter "DisplayName eq '{admin-unit-id}'"
$groupObj = Get-MgGroup -Filter "DisplayName eq 'group-name'"
$odataId = "https://graph.microsoft.com/v1.0/groups/" + $groupObj.Id
New-MgDirectoryAdministrativeUnitMemberByRef -AdministrativeUnitId $adminUnitObj.Id -OdataId $odataId
```

### Add devices to an administrative unit

```powershell
$adminUnitObj = Get-MgDirectoryAdministrativeUnit -Filter "DisplayName eq '{admin-unit-id}'"
$odataId = "https://graph.microsoft.com/v1.0/devices/{device-id}"
New-MgDirectoryAdministrativeUnitMemberByRef -AdministrativeUnitId $adminUnitObj.Id -OdataId $odataId
```

### Create a new group in an administrative unit

```powershell
$adminUnitObj = Get-MgDirectoryAdministrativeUnit -Filter "DisplayName eq '{admin-unit-id}'"
$params = @{
    "@odata.type" = "#microsoft.graph.group"
    description = "{group-description}"
    displayName = "{group-name}"
    groupTypes = @(
        "Unified"
    )
    mailEnabled = $false
    mailNickname = "{group-name}"
    securityEnabled = $true
}
New-MgDirectoryAdministrativeUnitMember -AdministrativeUnitId $adminUnitObj.Id -BodyParameter $params
```

# [Graph API](#tab/ms-graph)
Use the [Add a member](/en-us/graph/api/administrativeunit-post-members) API to add users, groups, or devices to an administrative unit or create a new group in an administrative unit.

### Add users to an administrative unit

Request

```http
POST https://graph.microsoft.com/v1.0/directory/administrativeUnits/{admin-unit-id}/members/$ref
```

Body

```http
{
    "@odata.id":"https://graph.microsoft.com/v1.0/users/{user-id}"
}
```

Example

```http
{
    "@odata.id":"https://graph.microsoft.com/v1.0/users/john@example.com"
}
```

### Add groups to an administrative unit

Request

```http
POST https://graph.microsoft.com/v1.0/directory/administrativeUnits/{admin-unit-id}/members/$ref
```

Body

```http
{
    "@odata.id":"https://graph.microsoft.com/v1.0/groups/{group-id}"
}
```

Example

```http
{
    "@odata.id":"https://graph.microsoft.com/v1.0/groups/871d21ab-6b4e-4d56-b257-ba27827628f3"
}
```

### Add devices to an administrative unit

Request

```http
POST https://graph.microsoft.com/v1.0/directory/administrativeUnits/{admin-unit-id}/members/$ref
```

Body

```http
{
    "@odata.id":"https://graph.microsoft.com/v1.0/devices/{device-id}"
}
```

### Create a new group in an administrative unit

To create a new group directly in an administrative unit, use the following request. To add an existing group instead, see **Add groups to an administrative unit** earlier in this article.

Request

```http
POST https://graph.microsoft.com/v1.0/directory/administrativeUnits/{admin-unit-id}/members
```

Body

```http
{
    "@odata.type": "#Microsoft.Graph.Group",
    "description": "{Example group description}",
    "displayName": "{Example group name}",
    "groupTypes": [
        "Unified"
    ],
    "mailEnabled": true,
    "mailNickname": "{examplegroup}",
    "securityEnabled": false
}
```

---
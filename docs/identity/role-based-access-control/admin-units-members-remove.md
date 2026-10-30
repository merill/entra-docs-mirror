---
layout: Conceptual
title: Remove users, groups, or devices from an administrative unit - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/admin-units-members-remove
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: Remove users, groups, or devices from an administrative unit in Microsoft Entra ID
ms.topic: how-to
ms.date: 2025-01-03T00:00:00.0000000Z
ms.reviewer: anandy
ms.custom: oldportal, it-pro, has-azure-ad-ps-ref, azure-ad-ref-level-one-done, sfi-image-nochange
locale: en-us
document_id: 965c4dcf-866f-9df5-0a5b-4a015a6bc819
document_version_independent_id: fe06597f-9a91-8625-a8b8-30ae4bee7346
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/admin-units-members-remove.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/admin-units-members-remove
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/admin-units-members-remove.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: b61b726d-ca20-a41e-6a5b-0217d0f0ff6e
---

# Remove users, groups, or devices from an administrative unit - Microsoft Entra ID | Microsoft Learn

When users, groups, or devices in an administrative unit no longer need access, you can remove them.

## Prerequisites

- Microsoft Entra ID P1 or P2 license for each administrative unit administrator
- Microsoft Entra ID Free licenses for administrative unit members
- Privileged Role Administrator
- [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/installation) module when using PowerShell
- Admin consent when using Graph Explorer for Microsoft Graph API

For more information, see [Prerequisites to use PowerShell or Graph Explorer](prerequisites).

# [Admin center](#tab/admin-center)
You can remove users, groups, or devices from administrative units individually using the Microsoft Entra admin center. You can also remove users in a bulk operation.

### Remove a single user, group, or device from administrative units

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID**.
3. Browse to one of the following:

    - **Users** &gt; **All users**
    - **Groups** &gt; **All groups**
    - **Devices** &gt; **All devices**
4. Select the user, group, or device you want to remove from an administrative unit.
5. Select **Administrative units**.
6. Add check marks next to the administrative units you want to remove the user, group, or device from.
7. Select **Remove from administrative unit**.

    [![Screenshot of Devices and Administrative units page with Remove from administrative unit option.](media/admin-units-members-remove/device-admin-unit-remove.png)](media/admin-units-members-remove/device-admin-unit-remove.png#lightbox)

### Remove users, groups, or devices from a single administrative unit

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID** &gt; **Roles & admins** &gt; **Admin units**.
3. Select the administrative unit that you want to remove users, groups, or devices from.
4. Select one of the following:

    - **Users**
    - **Groups**
    - **Devices**
5. Add check marks next to the users, groups, or devices you want to remove.
6. Select **Remove member**, **Remove**, or **Remove device**.

    [![Screenshot showing a list of users in an administrative unit with check marks and a Remove member option.](media/admin-units-members-remove/admin-units-remove-user.png)](media/admin-units-members-remove/admin-units-remove-user.png#lightbox)

### Remove users from an administrative unit in a bulk operation

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID** &gt; **Roles & admins** &gt; **Admin units**.
3. Select the administrative unit that you want to remove users from.
4. Select **Users** &gt; **Bulk operations** &gt; **Bulk remove members**.

    [![Screenshot of Users page that shows the Bulk remove members link.](media/admin-units-members-remove/bulk-user-remove.png)](media/admin-units-members-remove/bulk-user-remove.png#lightbox)
5. In the **Bulk remove members** pane, download the comma-separated values (CSV) template.
6. Edit the downloaded CSV template with the list of users you want to remove.

    Add one user principal name (UPN) in each row. Don't remove the first two rows of the template.
7. Save your changes and upload the CSV file.
8. Select **Submit**.

# [PowerShell](#tab/ms-powershell)
Use the [Remove-MgDirectoryAdministrativeUnitMemberByRef](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/remove-mgdirectoryadministrativeunitmemberbyref) command to remove users, groups, or devices from an administrative unit.

### Remove users from an administrative unit

```powershell
$adminUnitObj = Get-MgDirectoryAdministrativeUnit -Filter "DisplayName eq 'Test administrative unit 2'"
$userObj = Get-MgUser -Filter "UserPrincipalName eq 'bill@example.com'"
Remove-MgDirectoryAdministrativeUnitMemberByRef -AdministrativeUnitId $adminUnitObj.Id -DirectoryObjectId $userObj.Id
```

### Remove groups from an administrative unit

```powershell
$adminUnitObj = Get-MgDirectoryAdministrativeUnit -Filter "DisplayName eq 'Test administrative unit 2'"
$groupObj = Get-MgGroup -Filter "DisplayName eq 'TestGroup'"
Remove-MgDirectoryAdministrativeUnitMemberByRef -AdministrativeUnitId $adminUnitObj.Id -DirectoryObjectId $groupObj.Id
```

### Remove devices from an administrative unit

```powershell
Remove-MgDirectoryAdministrativeUnitMemberByRef -AdministrativeUnitId $adminUnitObj.Id -DirectoryObjectId $deviceObj.Id
```

# [Graph API](#tab/ms-graph)
Use the [Remove a member](/en-us/graph/api/administrativeunit-delete-members) API to remove users, groups, or devices from an administrative unit. For `{member-id}`, specify the user, group, or device ID.

```http
DELETE https://graph.microsoft.com/v1.0/directory/administrativeUnits/{admin-unit-id}/members/{member-id}/$ref
```

---
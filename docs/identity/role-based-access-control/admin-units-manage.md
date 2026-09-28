---
layout: Conceptual
title: Create or delete administrative units - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/admin-units-manage
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: Create administrative units to restrict the scope of role permissions in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-01-03T00:00:00.0000000Z
ms.reviewer: anandy
ms.custom: oldportal, it-pro, no-azure-ad-ps-ref, sfi-image-nochange
locale: en-us
document_id: 10d0bacc-f835-c3d2-5b13-7491a190a3c3
document_version_independent_id: 2cfc9c21-b9b7-2a2c-348f-dd6fb2cdc9e8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/admin-units-manage.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/admin-units-manage
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/admin-units-manage.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: e8a0ee5c-9413-f79c-2241-5b613e9a51c0
---

# Create or delete administrative units - Microsoft Entra ID | Microsoft Learn

Administrative units let you subdivide your organization into any unit that you want, and then assign specific administrators that can manage only the members of that unit. For example, you could use administrative units to delegate permissions to administrators of each school at a large university, so they could control access, manage users, and set policies only in the School of Engineering.

This article describes how to create or delete administrative units to restrict the scope of role permissions in Microsoft Entra ID.

## Prerequisites

- Microsoft Entra ID P1 or P2 license for each administrative unit administrator
- Microsoft Entra ID Free licenses for administrative unit members
- Privileged Role Administrator role
- [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/installation) module when using PowerShell
- Admin consent when using Graph Explorer for Microsoft Graph API

For more information, see [Prerequisites to use PowerShell or Graph Explorer](prerequisites).

## Create an administrative unit

You can create a new administrative unit by using either the Microsoft Entra admin center, Microsoft Entra PowerShell, or Microsoft Graph.

# [Admin center](#tab/admin-center)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID** &gt; **Roles & admins** &gt; **Admin units**.

    [![Screenshot of the Administrative units page.](media/admin-units-manage/nav-to-admin-units.png)](media/admin-units-manage/nav-to-admin-units.png#lightbox)
3. Select **Add**.
4. In the **Name** box, enter the name of the administrative unit. Optionally, add a description of the administrative unit.
5. If you don't want tenant-level administrators to be able to access this administrative unit, set the **Restricted management administrative unit** toggle to **Yes**. For more information, see [Restricted management administrative units](admin-units-restricted-management).

    [![Screenshot showing the Add administrative unit page and the Name box for entering the name of the administrative unit.](media/admin-units-manage/add-new-admin-unit.png)](media/admin-units-manage/add-new-admin-unit.png#lightbox)
6. Optionally, on the **Assign roles** tab, select a role and then select the users to assign the role to with this administrative unit scope.

    [![Screenshot showing the Add assignments pane to add role assignments with this administrative unit scope.](media/admin-units-manage/assign-roles-admin-unit.png)](media/admin-units-manage/assign-roles-admin-unit.png#lightbox)
7. On the **Review + create** tab, review the administrative unit and any role assignments.
8. Select the **Create** button.

# [PowerShell](#tab/ms-powershell)
Use the [Connect-MgGraph](/en-us/powershell/microsoftgraph/authentication-commands#using-connect-mggraph) command to sign in to your tenant and consent to the required permissions.

```powershell
Connect-MgGraph -Scopes "AdministrativeUnit.ReadWrite.All"
```

Use the [New-MgDirectoryAdministrativeUnit](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/new-mgdirectoryadministrativeunit) command to create a new administrative unit.

```powershell
$params = @{
    DisplayName = "Seattle District Technical Schools"
    Description = "Seattle district technical schools administration"
    Visibility = "HiddenMembership"
}
$adminUnitObj = New-MgDirectoryAdministrativeUnit -BodyParameter $params
```

Use the [New-MgDirectoryAdministrativeUnit](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/new-mgdirectoryadministrativeunit) command to create a new restricted management administrative unit. Set the `IsMemberManagementRestricted` property to `$true`.

```powershell
$params = @{
    DisplayName = "Contoso Executive Division"
    Description = "Contoso Executive Division administration"
    Visibility = "HiddenMembership"
    IsMemberManagementRestricted = $true
}
$restrictedAU = New-MgDirectoryAdministrativeUnit -BodyParameter $params
```

# [Graph API](#tab/ms-graph)
Use the [Create administrativeUnit](/en-us/graph/api/directory-post-administrativeunits) API to create a new administrative unit.

Request

```http
POST https://graph.microsoft.com/v1.0/directory/administrativeUnits
```

Body

```http
{
  "displayName": "North America Operations",
  "description": "North America Operations administration"
}
```

Use the [Create administrativeUnit](/en-us/graph/api/directory-post-administrativeunits) API to create a new restricted management administrative unit. Set the `isMemberManagementRestricted` property to `true`.

Request

```http
POST https://graph.microsoft.com/v1.0/directory/administrativeUnits
```

Body

```http
{ 
  "displayName": "Contoso Executive Division",
  "description": "This administrative unit contains executive accounts of Contoso Corp.", 
  "isMemberManagementRestricted": true
}
```

---

## Delete an administrative unit

In Microsoft Entra ID, you can delete an administrative unit that you no longer need as a unit of scope for administrative roles. Before you delete the administrative unit, you should remove any role assignments with that administrative unit scope.

# [Admin center](#tab/admin-center)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID** &gt; **Roles & admins** &gt; **Admin units**.
3. Select the administrative unit you want to delete.
4. Select **Roles and administrators**, and then open a role to view the role assignments.
5. Remove all the role assignments with the administrative unit scope.
6. Browse to **Entra ID** &gt; **Roles & admins** &gt; **Admin units**.
7. Add a check mark next to the administrative unit you want to delete.
8. Select **Delete**.

    [![Screenshot of the administrative unit Delete button and confirmation window.](media/admin-units-manage/select-admin-unit-to-delete.png)](media/admin-units-manage/select-admin-unit-to-delete.png#lightbox)
9. To confirm that you want to delete the administrative unit, select **Yes**.

# [PowerShell](#tab/ms-powershell)
Use the [Remove-MgDirectoryAdministrativeUnit](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/remove-mgdirectoryadministrativeunit) command to delete an administrative unit.

```powershell
$adminUnitObj = Get-MgDirectoryAdministrativeUnit -Filter "DisplayName eq 'Seattle District Technical Schools'"
Remove-MgDirectoryAdministrativeUnit -AdministrativeUnitId $adminUnitObj.Id
```

# [Graph API](#tab/ms-graph)
Use the [Delete administrativeUnit](/en-us/graph/api/administrativeunit-delete) API to delete an administrative unit.

```http
DELETE https://graph.microsoft.com/v1.0/directory/administrativeUnits/{admin-unit-id}
```

---
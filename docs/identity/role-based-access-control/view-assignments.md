---
layout: Conceptual
title: List Microsoft Entra role assignments - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/view-assignments
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: Learn how to list Microsoft Entra role assignments using the Microsoft Entra admin center, Microsoft Graph PowerShell, or Microsoft Graph API.
ms.topic: how-to
ms.date: 2025-01-03T00:00:00.0000000Z
ms.reviewer: vincesm
ms.custom: it-pro, has-azure-ad-ps-ref, azure-ad-ref-level-one-done, sfi-ga-nochange, sfi-image-nochange
locale: en-us
document_id: 155c3c2e-5e09-4e36-32de-87d597a01fa2
document_version_independent_id: e69b2d78-7804-7f73-ff77-53a3923ca250
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/view-assignments.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/view-assignments
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/view-assignments.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: a18d0720-f20e-e0b9-0307-20de1abfaecc
---

# List Microsoft Entra role assignments - Microsoft Entra ID | Microsoft Learn

This article describes how to list roles you have assigned in Microsoft Entra ID using the Microsoft Entra admin center, Microsoft Graph PowerShell, or Microsoft Graph API.

Role assignments contain information linking a given security principal (a user, group, or application service principal) to a role definition. Listing users, groups, and assigned roles are default user permissions.

## Scopes

In Microsoft Entra ID, roles can be assigned at different scopes.

- Role assignments at tenant scope are added to and can be seen in the list of single application role assignments.
- Role assignments at the single application scope aren't added to and can't be seen in the list of tenant scoped assignments.

## Prerequisites

- [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/installation) module when using PowerShell
- Admin consent when using Graph explorer for Microsoft Graph API

For more information, see [Prerequisites to use PowerShell or Graph Explorer](prerequisites).

## List Microsoft Entra role assignments

# [Admin center](#tab/admin-center)
### List my role assignments

It's easy to list your own permissions as well. On the **Roles and administrators** page, select **Your Role** to see the roles that are currently assigned to you.

[![Screenshot of Roles and administrators page in Microsoft Entra admin center.](../../media/common/entra-roles-admins.png)](../../media/common/entra-roles-admins.png#lightbox)

### List role assignments for a user

Follow these steps to list Microsoft Entra roles for a user using the Microsoft Entra admin center. Your experience will be different depending on whether you have [Microsoft Entra Privileged Identity Management (PIM)](../../id-governance/privileged-identity-management/pim-configure) enabled.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Users**.
3. Select *user name* &gt; **Assigned roles**.

    You can see the list of roles assigned to the user at different scopes. Additionally, you can see whether the role has been assigned directly or via a group.

    [![Screenshot of roles assigned to a user.](media/view-assignments/user-role-assignments.png)](media/view-assignments/user-role-assignments.png#lightbox)

    If you have a Microsoft Entra ID P2 license, you'll see the PIM experience, which has eligible, active, and expired role assignment details.

    [![Screenshot of roles assigned to a user in PIM.](media/view-assignments/user-role-assignments-pim.png)](media/view-assignments/user-role-assignments-pim.png#lightbox)

### List role assignments for a group

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Groups** &gt; **All groups**.
3. Select a role-assignable group.

    To determine if a group is role-assignable, you can view the **Properties** for the group.
4. Select **Assigned roles**.

    You can now see all the Microsoft Entra roles assigned to this group. If you don't see the **Assigned roles** option, the group is not a role-assignable group.

    [![Screenshot of roles assigned to a group.](media/view-assignments/group-role-assignments.png)](media/view-assignments/group-role-assignments.png#lightbox)

### Download role assignments

To download all active role assignments across all roles, including built-in and custom roles, follow these steps.

Bulk operations can only run for up to 1 hour and has limitations in large tenants. For more information, see [Bulk operations](../../fundamentals/bulk-operations-service-limitations) and [Bulk create users in Microsoft Entra ID](https://go.microsoft.com/fwlink/?linkid=2103821).

1. On the **Roles and administrators** page, select **All roles**.
2. Select **Download assignments**.

    [![Screenshot of pane to download all role assignments.](media/view-assignments/download-role-assignments-all.png)](media/view-assignments/download-role-assignments-all.png#lightbox)
3. Specify a file name and select **Start bulk operation**.

    A CSV file that lists assignments at all scopes for all roles is downloaded.

To download role assignments for a specific role, follow these steps.

1. On the **Roles and administrators** page, select a role.
2. Select **Download assignments**.

    If you have a Microsoft Entra ID P2 license, you'll see the PIM experience. Select **Export** to download the role assignments.

    A CSV file that lists assignments at all scopes for that role is downloaded.

### List role assignments with tenant scope

This procedure describes how to list role assignments with tenant scope.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Roles & admins**.
3. Select a role name to open the role. Don't add a check mark next to the role.

    ![Screenshot of Roles and administrators page with mouse over role name.](../../media/common/entra-roles-admins-mouse.png)
4. Select **Assignments** to list the role assignments.

    [![Screenshot that lists role assignments with tenant scope.](media/view-assignments/role-assignments-tenant.png)](media/view-assignments/role-assignments-tenant.png#lightbox)
5. In the **Scope** column, see the role assignments with **Directory** scope.

### List role assignments with app registration scope

This section describes how to list role assignments with single-application scope.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **App registrations**.
3. Select an app registration for the list of role assignments you want to view.

    You might have to select **All applications** to see the complete list of app registrations in your Microsoft Entra organization.
4. Select **Roles and administrators**.
5. Select a role name to open the role.
6. Select **Assignments** to list the role assignments.

    Opening the assignments page from within the app registration shows you the role assignments that are scoped to this Microsoft Entra resource.

    [![Screenshot that lists role assignments with application registration scope.](media/view-assignments/role-assignments-app-registration.png)](media/view-assignments/role-assignments-app-registration.png#lightbox)
7. In the **Scope** column, see the role assignments with **This resource** scope.

### List role assignments with administrative unit scope

You can view all the role assignments created with an administrative unit scope in the **Admin units** section of the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Roles & admins** &gt; **Admin units**.
3. Select an administrative unit for the list of role assignments you want to view.
4. Select **Roles and administrators**.
5. Select a role name to open the role.
6. Select **Assignments** to list the role assignments.

    [![Screenshot that lists role assignments with administrative unit scope.](media/view-assignments/role-assignments-admin-unit.png)](media/view-assignments/role-assignments-admin-unit.png#lightbox)
7. In the **Scope** column, see the role assignments with **This resource** scope.

# [PowerShell](#tab/ms-powershell)
This section describes viewing assignments of a role with tenant scope. This section uses the [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/overview) module.

### Setup

1. Install the Microsoft Graph module using [Install-Module](/en-us/powershell/module/powershellget/install-module).

    ```powershell
    Install-Module -name Microsoft.Graph
    ```
2. Use the [Connect-MgGraph](/en-us/powershell/module/microsoft.graph.authentication/connect-mggraph) command to sign into and use Microsoft Graph PowerShell cmdlets.

    ```powershell
    Connect-MgGraph
    ```

### List role assignments with tenant scope

Use the [Get-MgRoleManagementDirectoryRoleDefinition](/en-us/powershell/module/microsoft.graph.identity.governance/get-mgrolemanagementdirectoryroledefinition) and [Get-MgRoleManagementDirectoryRoleAssignment](/en-us/powershell/module/microsoft.graph.identity.governance/get-mgrolemanagementdirectoryroleassignment) commands to list role assignments.

The following example shows how to list the role assignments for the [Groups Administrator](permissions-reference#groups-administrator) role.

```powershell
# Get a specific directory role by ID
$role = Get-MgRoleManagementDirectoryRoleDefinition -UnifiedRoleDefinitionId fdd7a751-b60b-444a-984c-02652fe8fa1c

# Get role assignments for a given role definition
Get-MgRoleManagementDirectoryRoleAssignment -Filter "roleDefinitionId eq '$($role.Id)'"
```

```Example
Id                                            PrincipalId                          RoleDefinitionId                     DirectoryScopeId AppScop
                                                                                                                                         eId
--                                            -----------                          ----------------                     ---------------- -------
lAPpYvVpN0KRkAEhdxReEH2Fs3EjKm1BvSKkcYVN2to-1 aaaaaaaa-bbbb-cccc-1111-222222222222 62e90394-69f5-4237-9190-012177145e10 /
lAPpYvVpN0KRkAEhdxReEMdXLf2tIs1ClhpzQPsutrQ-1 bbbbbbbb-cccc-dddd-2222-333333333333 62e90394-69f5-4237-9190-012177145e10 /
```

The following example shows how to list all active role assignments across all roles, including built-in and custom roles.

```powershell
$roles = Get-MgRoleManagementDirectoryRoleDefinition
foreach ($role in $roles)
{
  Get-MgRoleManagementDirectoryRoleAssignment -Filter "roleDefinitionId eq '$($role.Id)'"
}
```

```Example
Id                                            PrincipalId                          RoleDefinitionId                     DirectoryScopeId AppScop
                                                                                                                                         eId
--                                            -----------                          ----------------                     ---------------- -------
lAPpYvVpN0KRkAEhdxReEH2Fs3EjKm1BvSKkcYVN2to-1 aaaaaaaa-bbbb-cccc-1111-222222222222 62e90394-69f5-4237-9190-012177145e10 /
lAPpYvVpN0KRkAEhdxReEMdXLf2tIs1ClhpzQPsutrQ-1 bbbbbbbb-cccc-dddd-2222-333333333333 62e90394-69f5-4237-9190-012177145e10 /
4-PYiFWPHkqVOpuYmLiHa3ibEcXLJYtFq5x3Kkj2TkA-1 cccccccc-dddd-eeee-3333-444444444444 88d8e3e3-8f55-4a1e-953a-9b9898b8876b /
4-PYiFWPHkqVOpuYmLiHa2hXf3b8iY5KsVFjHNXFN4c-1 dddddddd-eeee-ffff-4444-555555555555 88d8e3e3-8f55-4a1e-953a-9b9898b8876b /
BSub0kaAukSHWB4mGC_PModww03rMgNOkpK77ePhDnI-1 eeeeeeee-ffff-aaaa-5555-666666666666 d29b2b05-8046-44ba-8758-1e26182fcf32 /
BSub0kaAukSHWB4mGC_PMgzOWSgXj8FHusA4iaaTyaI-1 ffffffff-aaaa-bbbb-6666-777777777777 d29b2b05-8046-44ba-8758-1e26182fcf32 /
```

### List role assignments for a principal

Use the [Get-MgRoleManagementDirectoryRoleAssignment](/en-us/powershell/module/microsoft.graph.identity.governance/get-mgrolemanagementdirectoryroleassignment) command to list the role assignments for a principal.

```powershell
# Get role assignments for a given principal
Get-MgRoleManagementDirectoryRoleAssignment -Filter "PrincipalId eq 'aaaaaaaa-bbbb-cccc-1111-222222222222'"
```

### List direct and transitive role assignments for a principal

Use the [List transitiveRoleAssignments](/en-us/graph/api/rbacapplication-list-transitiveroleassignments) API to get roles assigned directly and transitively to a user.

```powershell
$response = $null
$uri = "https://graph.microsoft.com/beta/roleManagement/directory/transitiveRoleAssignments?`$count=true&`$filter=principalId eq 'aaaaaaaa-bbbb-cccc-1111-222222222222'"
$method = 'GET'
$headers = @{'ConsistencyLevel' = 'eventual'}

$response = (Invoke-MgGraphRequest -Uri $uri -Headers $headers -Method $method -Body $null).value
```

### List role assignments for a group

Use the [Get-MgGroup](/en-us/powershell/module/microsoft.graph.groups/get-mggroup) command to get a group.

```powershell
Get-MgGroup -Filter "DisplayName eq 'Contoso_Helpdesk_Administrators'"
```

Use the [Get-MgRoleManagementDirectoryRoleAssignment](/en-us/powershell/module/microsoft.graph.identity.governance/get-mgrolemanagementdirectoryroleassignment) command to list the role assignments for the group.

```powershell
Get-MgRoleManagementDirectoryRoleAssignment -Filter "PrincipalId eq '<object id of group>'" 
```

### List role assignments with administrative unit scope

Use the [Get-MgDirectoryAdministrativeUnitScopedRoleMember](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/get-mgdirectoryadministrativeunitscopedrolemember) command to list role assignments with administrative unit scope.

```powershell
$adminUnit = Get-MgDirectoryAdministrativeUnit -Filter "displayname eq 'Example_admin_unit_name'"
Get-MgDirectoryAdministrativeUnitScopedRoleMember -AdministrativeUnitId $adminUnit.Id | FL *
```

# [Graph API](#tab/ms-graph)
This section describes how to list role assignments with tenant scope. Use the [List unifiedRoleAssignments](/en-us/graph/api/rbacapplication-list-roleassignments) API to get the role assignments.

### List role assignments for a principal

```http
GET https://graph.microsoft.com/v1.0/roleManagement/directory/roleAssignments?$filter=principalId+eq+'<object-id-of-principal>'
```

Response

```http
HTTP/1.1 200 OK
{
"value":[
            { 
                "id": "A1bC2dE3fH4iJ5kL6mN7oP8qR9sT0uIiSDKQoTVJrLE9etXyrY0-1"
                "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
                "roleDefinitionId": "10dae51f-b6af-4016-8d66-8c2a99b929b3",
                "directoryScopeId": "/"  
            } ,
            {
                "id": "C2dE3fH4iJ5kL6mN7oP8qR9sT0uV1wIiSDKQoTVJrLE9etXyrY0-1"
                "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
                "roleDefinitionId": "fe930be7-5e62-47db-91af-98c3a49a38b1",
                "directoryScopeId": "/"
            }
        ]
}
```

### List direct and transitive role assignments for a principal

Follow these steps to list Microsoft Entra roles assigned to a user using the Microsoft Graph API in [Graph Explorer](https://aka.ms/ge).

1. Sign in to the [Graph Explorer](https://aka.ms/ge).
2. Use the [List transitiveRoleAssignments](/en-us/graph/api/rbacapplication-list-transitiveroleassignments) API to get roles assigned directly and transitively to a user. Add following query to the URL.

    ```http
    GET https://graph.microsoft.com/beta/rolemanagement/directory/transitiveRoleAssignments?$count=true&$filter=principalId eq 'aaaaaaaa-bbbb-cccc-1111-222222222222'
    ```
3. Navigate to **Request headers** tab. Add `ConsistencyLevel` as key and `Eventual` as its value.
4. Select **Run query**.

### List role assignments for a group

Use the [Get group](/en-us/graph/api/group-get) API to get a group.

```http
GET https://graph.microsoft.com/v1.0/groups?$filter=displayName+eq+'Contoso_Helpdesk_Administrator'
```

Use the [List unifiedRoleAssignments](/en-us/graph/api/rbacapplication-list-roleassignments) API to get the role assignment.

```http
GET https://graph.microsoft.com/v1.0/roleManagement/directory/roleAssignments?$filter=principalId eq
```

### List role assignments for a role definition

The following example shows how to list the role assignments for a specific role definition.

```http
GET https://graph.microsoft.com/v1.0/roleManagement/directory/roleAssignments?$filter=roleDefinitionId eq '<template-id-of-role-definition>'
```

Response

```http
HTTP/1.1 200 OK
{
    "id": "C2dE3fH4iJ5kL6mN7oP8qR9sT0uV1wIiSDKQoTVJrLE9etXyrY0-1",
    "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
    "roleDefinitionId": "00000000-0000-0000-0000-000000000000",
    "directoryScopeId": "/"
}
```

### List a role assignment by ID

```http
GET https://graph.microsoft.com/v1.0/roleManagement/directory/roleAssignments/lAPpYvVpN0KRkAEhdxReEJC2sEqbR_9Hr48lds9SGHI-1
```

Response

```http
HTTP/1.1 200 OK
{ 
    "id": "A1bC2dE3fH4iJ5kL6mN7oP8qR9sT0uIiSDKQoTVJrLE9etXyrY0-1",
    "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
    "roleDefinitionId": "10dae51f-b6af-4016-8d66-8c2a99b929b3",
    "directoryScopeId": "/"
}
```

### List role assignments with app registration scope

```http
GET https://graph.microsoft.com/v1.0/roleManagement/directory/roleAssignments?$filter=directoryScopeId+eq+'/d23998b1-8853-4c87-b95f-be97d6c6b610'
```

Response

```http
HTTP/1.1 200 OK
{
"value":[
            { 
                "id": "A1bC2dE3fH4iJ5kL6mN7oP8qR9sT0uIiSDKQoTVJrLE9etXyrY0-1"
                "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
                "roleDefinitionId": "10dae51f-b6af-4016-8d66-8c2a99b929b3",
                "directoryScopeId": "/d23998b1-8853-4c87-b95f-be97d6c6b610"
            } ,
            {
                "id": "C2dE3fH4iJ5kL6mN7oP8qR9sT0uV1wIiSDKQoTVJrLE9etXyrY0-1"
                "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
                "roleDefinitionId": "00000000-0000-0000-0000-000000000000",
                "directoryScopeId": "/d23998b1-8853-4c87-b95f-be97d6c6b610"
            }
        ]
}
```

### List role assignments with administrative unit scope

Use the [List scopedRoleMembers](/en-us/graph/api/administrativeunit-list-scopedrolemembers) API to list role assignments with administrative unit scope.

Request

```http
GET /directory/administrativeUnits/{admin-unit-id}/scopedRoleMembers
```

Body

```http
{}
```

---
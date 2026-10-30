---
layout: Conceptual
title: Create a custom role with permissions to create unlimited app registrations - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/quickstart-app-registration-limits
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: Assign a custom role to grant unrestricted app registrations in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-01-03T00:00:00.0000000Z
ms.reviewer: vincesm
ms.custom: it-pro, mode-other, has-azure-ad-ps-ref, azure-ad-ref-level-one-done, sfi-image-nochange
locale: en-us
document_id: d59b2783-b3e8-1505-2cb2-ae0a3516e56f
document_version_independent_id: b265a449-4571-17c8-1acc-c3f20b6d093b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/quickstart-app-registration-limits.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/quickstart-app-registration-limits
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/quickstart-app-registration-limits.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 8be10fe5-866e-6d64-dba7-5e06567228e8
---

# Create a custom role with permissions to create unlimited app registrations - Microsoft Entra ID | Microsoft Learn

In this quick start guide, you create a custom role with permission to create an unlimited number of app registrations, and then assign that role to a user. The assigned user can then use the Microsoft Entra admin center, Microsoft Graph PowerShell, or Microsoft Graph API to create application registrations. Unlike the built-in Application Developer role, this custom role grants the ability to create an unlimited number of application registrations. The Application Developer role grants the ability, but the total number of created objects is limited to 250 to prevent hitting [the directory-wide object quota](../users/directory-service-limits-restrictions). The least privileged role required to create and assign Microsoft Entra custom roles is the Privileged Role Administrator.

If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

- Microsoft Entra ID P1 or P2 license
- Privileged Role Administrator
- [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/installation) module when using PowerShell
- Admin consent when using Graph explorer for Microsoft Graph API

For more information, see [Prerequisites to use PowerShell or Graph Explorer](prerequisites).

# [Admin center](#tab/admin-center)
### Create a custom role

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID** &gt; **Roles & admins**.
3. Select **New custom role**.

    [![Screenshot of Roles and administrators page in Microsoft Entra admin center.](../../media/common/entra-roles-admins.png)](../../media/common/entra-roles-admins.png#lightbox)
4. On the **Basics** tab, enter "Application Registration Creator" for the name of the role and "Can create an unlimited number of application registrations" for the role description, and then select **Next**.

    [![Screenshot of Basics tab to provide a name and description for a custom role.](media/quickstart-app-registration-limits/basics-tab.png)](media/quickstart-app-registration-limits/basics-tab.png#lightbox)
5. On the **Permissions** tab, enter "microsoft.directory/applications/create" in the search box, and then select the checkboxes next to the desired permissions, and then select **Next**.

    [![Screenshot of Permissions tab to select the permissions for a custom role.](media/quickstart-app-registration-limits/permissions-tab.png)](media/quickstart-app-registration-limits/permissions-tab.png#lightbox)
6. On the **Review + create** tab, review the permissions and select **Create**.

### Assign the role

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID** &gt; **Roles & admins**.
3. Select the Application Registration Creator role and select **Add assignment**.
4. Select the desired user and click **Select** to add the user to the role.

Done! In this quickstart, you successfully created a custom role with permission to create an unlimited number of app registrations, and then assign that role to a user.

Tip

To assign the role to an application using the Microsoft Entra admin center, enter the name of the application into the search box of the assignment page. Applications aren't shown in the list by default, but are returned in search results.

### App registration permissions

There are two permissions available for granting the ability to create application registrations, each with different behavior.

- microsoft.directory/applications/createAsOwner: Assigning this permission results in the creator being added as the first owner of the created app registration, and the created app registration counts against the creator's 250 created objects quota.
- microsoft.directory/applications/create: Assigning this permission results in the creator not being added as the first owner of the created app registration, and the created app registration won't count against the creator's 250 created objects quota. Use this permission carefully, because there's nothing preventing the assignee from creating app registrations until the directory-level quota is hit. If both permissions are assigned, this permission takes precedence.

# [PowerShell](#tab/ms-powershell)
### Create a custom role

Create a new role using the following PowerShell script:

```powershell
# Basic role information
$displayName = "Application Registration Creator"
$description = "Can create an unlimited number of application registrations."
$templateId = (New-Guid).Guid

# Set of permissions to grant
$allowedResourceAction =
@(
    "microsoft.directory/applications/create"
    "microsoft.directory/applications/createAsOwner"
)
$rolePermissions = @{'allowedResourceActions'= $allowedResourceAction}

# Create new custom admin role
$customRole = New-MgRoleManagementDirectoryRoleDefinition -DisplayName $displayName -Description $description -RolePermissions $rolePermissions -TemplateId $templateId -IsEnabled:$true
```

### Assign the role

Assign the role using the following PowerShell script:

```powershell
# Get the user and role definition you want to link
$user = Get-MgUser -Filter "UserPrincipalName eq 'Adam@contoso.com'"
$roleDefinition = Get-MgRoleManagementDirectoryRoleDefinition -Filter "DisplayName eq 'Application Registration Creator'"

# Get resource scope for assignment
$resourceScope = '/'

# Create a scoped role assignment
$roleAssignment = New-MgRoleManagementDirectoryRoleAssignment -DirectoryScopeId $resourceScope -RoleDefinitionId $roleDefinition.Id -PrincipalId $user.Id
```

# [Graph API](#tab/ms-graph)
### Create a custom role

Use the [Create unifiedRoleDefinition](/en-us/graph/api/rbacapplication-post-roledefinitions) API to create a custom role.

```http
POST https://graph.microsoft.com/v1.0/roleManagement/directory/roleDefinitions
```

Body

```http
{
    "description": "Can create an unlimited number of application registrations.",
    "displayName": "Application Registration Creator",
    "isEnabled": true,
    "rolePermissions":
    [
        {
            "allowedResourceActions":
            [
                "microsoft.directory/applications/create"
                "microsoft.directory/applications/createAsOwner"
            ]
        }
    ],
    "templateId": "<PROVIDE NEW GUID HERE>",
    "version": "1"
}
```

### Assign the role

Use the [Create unifiedRoleAssignment](/en-us/graph/api/rbacapplication-post-roleassignments) API to assign the custom role. The role assignment combines a security principal ID (which can be a user or service principal), a role definition (role) ID, and a Microsoft Entra resource scope.

```http
POST https://graph.microsoft.com/v1.0/roleManagement/directory/roleAssignments
```

Body

```http
{
    "@odata.type": "#microsoft.graph.unifiedRoleAssignment",
    "principalId": "<PROVIDE OBJECTID OF USER TO ASSIGN HERE>",
    "roleDefinitionId": "<PROVIDE OBJECTID OF ROLE DEFINITION HERE>",
    "directoryScopeId": "/"
}
```

---
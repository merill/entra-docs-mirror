---
layout: Conceptual
title: List Microsoft Entra role definitions - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/role-definitions-list
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: Learn how to list Microsoft Entra built-in and custom role definitions and their permissions using the Microsoft Entra admin center, Microsoft Graph PowerShell, or Microsoft Graph API.
ms.topic: how-to
ms.date: 2025-01-03T00:00:00.0000000Z
ms.reviewer: absinh
ms.custom: it-pro, has-azure-ad-ps-ref, azure-ad-ref-level-one-done, sfi-image-nochange
locale: en-us
document_id: 0c48d0c7-601d-29d1-f125-77bab25c8a4b
document_version_independent_id: 4f5af85e-ca7a-e0cf-ab9a-cc4d0b1b00ac
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/role-definitions-list.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/role-definitions-list
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/role-definitions-list.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: c8fa7c9f-107e-cb02-79ca-521fca7b7f9a
---

# List Microsoft Entra role definitions - Microsoft Entra ID | Microsoft Learn

This article describes how to list the Microsoft Entra built-in and custom role definitions and their permissions using the Microsoft Entra admin center, Microsoft Graph PowerShell, or Microsoft Graph API.

A role definition is a collection of permissions that can be performed, such as read, write, and delete. It's typically referred to as a role. Microsoft Entra ID has over 100 built-in roles or you can create your own custom roles. If you ever wondered "What do these roles really do?", you can access a detailed list of permissions for each of the roles.

## Prerequisites

- [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/installation) module when using PowerShell
- Admin consent when using Graph explorer for Microsoft Graph API

For more information, see [Prerequisites to use PowerShell or Graph Explorer](prerequisites).

## List Microsoft Entra role definitions

# [Admin center](#tab/admin-center)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Roles & admins**.

    [![Screenshot of Roles and administrators page in Microsoft Entra admin center.](../../media/common/entra-roles-admins.png)](../../media/common/entra-roles-admins.png#lightbox)
3. Select a role name to open the role. Don't add a check mark next to the role.

    ![Screenshot of Roles and administrators page with mouse over role name.](../../media/common/entra-roles-admins-mouse.png)
4. Select **Description** to see the summary and list of permissions for the role.

    The page includes links to relevant documentation to help guide you through managing roles.

    [![Screenshot of Roles and administrators page that shows role description.](media/role-definitions-list/roles-admins-description.png)](media/role-definitions-list/roles-admins-description.png#lightbox)

# [PowerShell](#tab/ms-powershell)
Follow these steps to list Microsoft Entra roles with PowerShell.

1. Open a PowerShell window. If necessary, use [Install-Module](/en-us/powershell/module/powershellget/install-module) to install Microsoft Graph PowerShell. For more information, see [Prerequisites to use PowerShell or Graph Explorer](prerequisites).

    ```powershell
    Install-Module Microsoft.Graph -Scope CurrentUser
    ```
2. In a PowerShell window, use [Connect-MgGraph](/en-us/powershell/microsoftgraph/authentication-commands#using-connect-mggraph) to sign in to your tenant.

    ```powershell
    Connect-MgGraph -Scopes "RoleManagement.Read.All"
    ```
3. Use [Get-MgRoleManagementDirectoryRoleDefinition](/en-us/powershell/module/microsoft.graph.identity.governance/get-mgrolemanagementdirectoryroledefinition) to get roles.

    ```powershell
    # Get all role definitions
    Get-MgRoleManagementDirectoryRoleDefinition
    
    # Get single role definition by ID
    Get-MgRoleManagementDirectoryRoleDefinition -UnifiedRoleDefinitionId 00000000-0000-0000-0000-000000000000
    
    # Get single role definition by templateId
    Get-MgRoleManagementDirectoryRoleDefinition -Filter "TemplateId eq 'c4e39bd9-1100-46d3-8c65-fb160da0071f'"
    
    # Get role definition by displayName
    Get-MgRoleManagementDirectoryRoleDefinition -Filter "displayName eq 'Helpdesk Administrator'"
    ```
4. To view the list of permissions of a role, use the following cmdlet.

    ```powershell
    # Do this avoid truncation of the list of permissions
    $FormatEnumerationLimit = -1
    
    (Get-MgRoleManagementDirectoryRoleDefinition -Filter "displayName eq 'Conditional Access Administrator'").RolePermissions | Format-list
    ```

# [Graph API](#tab/ms-graph)
Follow these instructions to list Microsoft Entra roles using the Microsoft Graph API in [Graph Explorer](https://aka.ms/ge).

1. Sign in to the [Graph Explorer](https://aka.ms/ge).
2. Select **GET** as the HTTP method from the dropdown.
3. Select the API version to **v1.0**.
4. Use the [List unifiedRoleDefinitions](/en-us/graph/api/rbacapplication-list-roledefinitions) API to list all role definitions.

    ```http
    GET https://graph.microsoft.com/v1.0/roleManagement/directory/roleDefinitions
    ```

    To list a specific role by displayName, use this format.

    ```http
    GET https://graph.microsoft.com/v1.0/roleManagement/directory/roleDefinitions?$filter = displayName eq 'Helpdesk Administrator'
    ```
5. Select **Run query** to list the roles.

    Here's an example of the response.

    ```http
    {
        "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#roleManagement/directory/roleDefinitions",
        "value": [
            {
                "id": "729827e3-9c14-49f7-bb1b-9608f156bbb8",
                "description": "Can reset passwords for non-administrators and Helpdesk Administrators.",
                "displayName": "Helpdesk Administrator",
                "isBuiltIn": true,
                "isEnabled": true,
                "resourceScopes": [
                    "/"
                ],
    
        ...
    
    ```
6. To view permissions of a role, use the following API.

    ```http
    GET https://graph.microsoft.com/v1.0/roleManagement/directory/roleDefinitions?$filter=DisplayName eq 'Conditional Access Administrator'&$select=rolePermissions
    ```

---
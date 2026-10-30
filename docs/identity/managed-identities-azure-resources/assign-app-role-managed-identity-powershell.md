---
layout: Conceptual
title: Assign a managed identity to an application role using PowerShell - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/assign-app-role-managed-identity-powershell
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Step-by-step instructions for assigning a managed identity access to another application's role using PowerShell.
ms.topic: how-to
ms.date: 2025-09-09T00:00:00.0000000Z
locale: en-us
document_id: 4913ca66-4b0e-1da5-cfd1-4ab7e006f97d
document_version_independent_id: 4913ca66-4b0e-1da5-cfd1-4ab7e006f97d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/assign-app-role-managed-identity-powershell.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/assign-app-role-managed-identity-powershell
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/assign-app-role-managed-identity-powershell.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 779f84ee-b58c-53c0-82d6-92717ffee0c1
---

# Assign a managed identity to an application role using PowerShell - Managed identities for Azure resources | Microsoft Learn

Managed identities for Azure resources provide Azure services with an identity in Microsoft Entra ID. They work without needing credentials in your code. Azure services use this identity to authenticate to services that support Microsoft Entra authentication. Application roles provide a form of role-based access control, and allow a service to implement authorization rules.

Note

The tokens your application receives are cached by the underlying infrastructure. This means that any changes to the managed identity's roles can take significant time to process. For more information, see [Limitation of using managed identities for authorization](managed-identity-best-practice-recommendations#limitation-of-using-managed-identities-for-authorization).

In this article, you'll learn how to assign a managed identity to an application role exposed by another application using the [Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/overview) or [Azure CLI](/en-us/cli/azure/what-is-azure-cli).

## Prerequisites

- If you're unfamiliar with managed identities for Azure resources, see [Managed identity for Azure resources overview](overview).
- Review the [difference between a system-assigned and user-assigned managed identity](/en-us/azure/logic-apps/authenticate-with-managed-identity).
- If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before continuing.

## Assign a managed identity access to another application's app role using PowerShell

To run the example scripts, you have two options:

- Use the [Azure Cloud Shell](/en-us/azure/cloud-shell/overview), which you can open using the **Try It** button on the top-right corner of code blocks.
- Run scripts locally by installing the latest version of the [Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/get-started).

1. Enable managed identity on an Azure resource, [such as an Azure VM](how-to-configure-managed-identities).
2. Find the object ID of the managed identity's service principal.

    **For a system-assigned managed identity**, you can find the object ID on the Azure portal on the resource's **Identity** page. You can also use the following PowerShell script to find the object ID. You'll need the resource ID of the resource you created in step 1, which is available in the Azure portal on the resource's **Properties** page.

    ```powershell
    $resourceIdWithManagedIdentity = '/subscriptions/{my subscription ID}/resourceGroups/{my resource group name}/providers/Microsoft.Compute/virtualMachines/{my virtual machine name}'
    (Get-AzResource -ResourceId $resourceIdWithManagedIdentity).Identity.PrincipalId
    ```

    **For a user-assigned managed identity**, you can find the managed identity's object ID on the Azure portal on the resource's **Overview** page. You can also use the following PowerShell script to find the object ID. You'll need the resource ID of the user-assigned managed identity.

    ```powershell
    $userManagedIdentityResourceId = '/subscriptions/{my subscription ID}/resourceGroups/{my resource group name}/providers/Microsoft.ManagedIdentity/userAssignedIdentities/{my managed identity name}'
    (Get-AzResource -ResourceId $userManagedIdentityResourceId).Properties.PrincipalId
    ```
3. [Create a new application registration](/en-us/entra/identity-platform/quickstart-register-app) to represent the service that you want your managed identity to send a request to.

    - If the API or service that exposes the app role grant to the managed identity already has a service principal in your Microsoft Entra tenant, skip this step. For example, in the case that you want to grant the managed identity access to the Microsoft Graph API.
4. Find the object ID of the service application's service principal. You can find this using the [Microsoft Entra admin center](https://entra.microsoft.com/).

    1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/).
    2. In the left nav blade, select **Entra ID** &gt; **Enterprise apps**. Then find the application and look for the **Object ID**.
    3. You can also find the service principal's object ID by its display name using the following PowerShell script:

    ```powershell
    $serverServicePrincipalObjectId = (Get-MgServicePrincipal -Filter "DisplayName eq '$applicationName'").Id
    ```

    Note

    Display names for applications aren't unique, so you should verify that you obtain the correct application's service principal.
5. Add an [app role](../../identity-platform/howto-add-app-roles-in-apps) to the application you created in the previous step. You can then create the role using the Azure portal or by using Microsoft Graph. For example, you could add an app role by running the following query in [Graph explorer](https://developer.microsoft.com/graph/graph-explorer):

    ```http
    PATCH /applications/{id}/
    
    {
        "appRoles": [
            {
                "allowedMemberTypes": [
                    "User",
                    "Application"
                ],
                "description": "Read reports",
                "id": "00001111-aaaa-2222-bbbb-3333cccc4444",
                "displayName": "Report reader",
                "isEnabled": true,
                "value": "report.read"
            }
        ]
    }
    ```
6. Assign the app role to the managed identity. You'll need the following information to assign the app role:

    - `managedIdentityObjectId`: the object ID of the managed identity's service principal, which you found in the previous step.
    - `serverServicePrincipalObjectId`: the object ID of the server application's service principal, which you found in step 4.
    - `appRoleId`: the ID of the app role exposed by the server app, which you generated in step 5 - in the example, the app role ID is `00000000-0000-0000-0000-000000000000`.
    - Execute the following PowerShell command to add the role assignment:

        ```powershell
        New-MgServicePrincipalAppRoleAssignment `
            -ServicePrincipalId $serverServicePrincipalObjectId `
            -PrincipalId $managedIdentityObjectId `
            -ResourceId $serverServicePrincipalObjectId `
            -AppRoleId $appRoleId
        ```

## Complete example script

This example script shows you how to assign an Azure web app's managed identity to an app role.

```powershell
# Install the module.
# Install-Module Microsoft.Graph -Scope CurrentUser

# Your tenant ID (in the Azure portal, under Microsoft Entra ID > Overview).
$tenantID = '<tenant-id>'

# The name of your web app, which has a managed identity that should be assigned to the server app's app role.
$webAppName = '<web-app-name>'
$resourceGroupName = '<resource-group-name-containing-web-app>'

# The name of the server app that exposes the app role.
$serverApplicationName = '<server-application-name>' # For example, MyApi

# The name of the app role that the managed identity should be assigned to.
$appRoleName = '<app-role-name>' # For example, MyApi.Read.All

# Look up the web app's managed identity's object ID.
$managedIdentityObjectId = (Get-AzWebApp -ResourceGroupName $resourceGroupName -Name $webAppName).identity.principalid

Connect-MgGraph -TenantId $tenantId -Scopes 'Application.Read.All','Application.ReadWrite.All','AppRoleAssignment.ReadWrite.All','Directory.AccessAsUser.All','Directory.Read.All','Directory.ReadWrite.All'

# Look up the details about the server app's service principal and app role.
$serverServicePrincipal = (Get-MgServicePrincipal -Filter "DisplayName eq '$serverApplicationName'")
$serverServicePrincipalObjectId = $serverServicePrincipal.Id
$appRoleId = ($serverServicePrincipal.AppRoles | Where-Object {$_.Value -eq $appRoleName }).Id

# Assign the managed identity access to the app role.
New-MgServicePrincipalAppRoleAssignment `
    -ServicePrincipalId $serverServicePrincipalObjectId `
    -PrincipalId $managedIdentityObjectId `
    -ResourceId $serverServicePrincipalObjectId `
    -AppRoleId $appRoleId
```
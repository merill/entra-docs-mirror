---
layout: Conceptual
title: Manage user-assigned managed identities using PowerShell - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-powershell
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Manage user-assigned managed identities using PowerShell.
ms.topic: how-to
ms.date: 2025-09-09T00:00:00.0000000Z
locale: en-us
document_id: 84513b6c-7041-8a25-3e8f-2de93eebb45e
document_version_independent_id: 84513b6c-7041-8a25-3e8f-2de93eebb45e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-powershell.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
interactive_type: azurepowershell
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-powershell
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-powershell.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/f7db5823-dfbf-4e94-9016-c24311b90d7e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/a5ab72d9-1367-4994-84a6-d9964cd9936d
platformId: a5c5568f-efff-8103-102a-c7524dfcd210
---

# Manage user-assigned managed identities using PowerShell - Managed identities for Azure resources | Microsoft Learn

Managed identities for Azure resources eliminate the need to manage credentials in code. You can use them to get a Microsoft Entra token for your applications. The applications can use the token when accessing resources that support Microsoft Entra authentication. Azure manages the identity so you don't have to.

There are two types of managed identities: system-assigned and user-assigned. System-assigned managed identities have their lifecycle tied to the resource that created them. This identity is restricted to only one resource, and you can grant permissions to the managed identity by using Azure role-based access control (RBAC). User-assigned managed identities can be used on multiple resources.

In this article, you learn how to create, list, delete, or assign a role to a user-assigned managed identity by using PowerShell. We use Azure Virtual Machine (AzureVM) as an example resource to which you can assign a user-assigned managed identity.

## Prerequisites

- If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview). *Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview#managed-identity-types)*.
- If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you continue.
- To run the example scripts, you have two options:
    - Use [Azure Cloud Shell](/en-us/azure/cloud-shell/overview), which you can open by using the **Try It** button in the upper-right corner of code blocks.
    - Run scripts locally with Azure PowerShell, as described in the next section.

### Configure Azure PowerShell locally

To use Azure PowerShell locally for this article instead of using Cloud Shell:

1. Install [the latest version of Azure PowerShell](/en-us/powershell/azure/install-azure-powershell) if you haven't already.
2. Sign in to Azure.

    ```azurepowershell
    Connect-AzAccount
    ```
3. Install the [latest version of PowerShellGet](/en-us/powershell/gallery/powershellget/install-powershellget).

    ```azurepowershell
    Install-Module -Name PowerShellGet -AllowPrerelease
    ```

    You might need to `Exit` out of the current PowerShell session after you run this command for the next step.
4. Install the prerelease version of the `Az.ManagedServiceIdentity` module to perform the user-assigned managed identity operations in this article.

    ```azurepowershell
    Install-Module -Name Az.ManagedServiceIdentity -AllowPrerelease
    ```

## Create a user-assigned managed identity

To create a user-assigned managed identity, your account needs the [Managed Identity Contributor](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role assignment.

1. To create a user-assigned managed identity, use the `New-AzUserAssignedIdentity` command. The `ResourceGroupName` parameter specifies the resource group where to create the user-assigned managed identity. The `-Name` parameter specifies its name.
2. Replace the `<RESOURCE GROUP>` and `<USER ASSIGNED IDENTITY NAME>` parameter values with your own values.

    Important

    When you create user-assigned managed identities, the name must start with a letter or number, and may include a combination of alphanumeric characters, hyphens (-) and underscores (\_). For the assignment to a virtual machine or virtual machine scale set to work properly, the name is limited to 24 characters. For more information, see [FAQs and known issues](known-issues).

    ```azurepowershell
    New-AzUserAssignedIdentity -ResourceGroupName <RESOURCEGROUP> -Name <USER ASSIGNED IDENTITY NAME>
    ```

## List user-assigned managed identities

To list or read a user-assigned managed identity, your account needs the [Managed Identity Operator](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-operator) or [Managed Identity Contributor](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role assignment.

1. To list user-assigned managed identities, use the `Get-AzUserAssignedIdentity` command. The `-ResourceGroupName` parameter specifies the resource group where the user-assigned managed identity was created.
2. Replace the `<RESOURCE GROUP>` value with your own value.

    ```azurepowershell
    Get-AzUserAssignedIdentity -ResourceGroupName <RESOURCE GROUP>
    ```

    In the response, user-assigned managed identities have the `"Microsoft.ManagedIdentity/userAssignedIdentities"` value returned for the key `Type`.

    `Type :Microsoft.ManagedIdentity/userAssignedIdentities`

## Delete a user-assigned managed identity

To delete a user-assigned managed identity, your account needs the [Managed Identity Contributor](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role assignment.

1. To delete a user-assigned managed identity, use the `Remove-AzUserAssignedIdentity` command. The `-ResourceGroupName` parameter specifies the resource group where the user-assigned identity was created. The `-Name` parameter specifies its name.
2. Replace the `<RESOURCE GROUP>` and the `<USER ASSIGNED IDENTITY NAME>` parameter values with your own values.

    ```azurepowershell
    Remove-AzUserAssignedIdentity -ResourceGroupName <RESOURCE GROUP> -Name <USER ASSIGNED IDENTITY NAME>
    ```

    Deleting a user-assigned managed identity won't remove the reference from any resource it was assigned to. Identity assignments must be removed separately.
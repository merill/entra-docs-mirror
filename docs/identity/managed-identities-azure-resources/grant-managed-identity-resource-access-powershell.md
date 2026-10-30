---
layout: Conceptual
title: Use PowerShell to grant a managed identity access to a resource - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/grant-managed-identity-resource-access-powershell
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Step-by-step instructions on using PowerShell to assign a managed identity access to an Azure resource or another resource.
ms.topic: how-to
ms.date: 2024-06-03T00:00:00.0000000Z
locale: en-us
document_id: e30e7f4c-4913-c3be-e937-881e0d8a7987
document_version_independent_id: e30e7f4c-4913-c3be-e937-881e0d8a7987
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/grant-managed-identity-resource-access-powershell.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
interactive_type: azurepowershell
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/grant-managed-identity-resource-access-powershell
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/grant-managed-identity-resource-access-powershell.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: cef8cddd-da2e-6a29-a61a-231c555f835b
---

# Use PowerShell to grant a managed identity access to a resource - Managed identities for Azure resources | Microsoft Learn

This article shows you how to use PowerShell to give a managed identity access to an Azure resource. In this article, we use the example of an Azure virtual machine (Azure VM) managed identity accessing an Azure storage account. Once you've configured an Azure resource with a managed identity, you can then give the managed identity access to another resource, similar to any security principal.

## Prerequisites

- Be sure you've enabled managed identity on an Azure resource, such as an [Azure virtual machine](how-to-configure-managed-identities).
- If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before continuing.

## Use Azure RBAC to assign a managed identity access to another resource using PowerShell

Note

We recommend that you use the Azure Az PowerShell module to interact with Azure. See [Install Azure PowerShell](/en-us/powershell/azure/install-azure-powershell) to get started. To learn how to migrate to the Az PowerShell module, see [Migrate Azure PowerShell from AzureRM to Az](/en-us/powershell/azure/migrate-from-azurerm-to-az).

To run the scripts in this example, you have two options:

- Use the [Azure Cloud Shell](/en-us/azure/cloud-shell/overview), which you can open using the **Try It** button on the top-right corner of code blocks.
- Run scripts locally by installing the latest version of [Azure PowerShell](/en-us/powershell/azure/install-azure-powershell), then sign in to Azure using `Connect-AzAccount`.

1. Enable managed identity on an Azure resource, [such as an Azure VM](how-to-configure-managed-identities).
2. Give the Azure virtual machine (VM) access to a storage account.

    1. Use [Get-AzVM](/en-us/powershell/module/az.compute/get-azvm) to get the service principal for the VM named `myVM`, which was created when you enabled managed identity.
    2. Use [New-AzRoleAssignment](/en-us/powershell/module/az.resources/new-azroleassignment) to give the VM **Reader** access to a storage account called `myStorageAcct`:

    ```azurepowershell
    $spID = (Get-AzVM -ResourceGroupName myRG -Name myVM).identity.principalid
    New-AzRoleAssignment -ObjectId $spID -RoleDefinitionName "Reader" -Scope "/subscriptions/<mySubscriptionID>/resourceGroups/<myResourceGroup>/providers/Microsoft.Storage/storageAccounts/<myStorageAcct>"
    ```
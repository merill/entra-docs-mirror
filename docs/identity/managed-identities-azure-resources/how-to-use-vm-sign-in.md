---
layout: Conceptual
title: Use managed identities on an Azure VM for sign-inV - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/how-to-use-vm-sign-in
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Step-by-step instructions and examples for using an Azure VM-managed identities for Azure resources service principal for script client sign-in and resource access.
ms.topic: how-to
ms.tgt_pltfrm: na
ms.date: 2022-01-11T00:00:00.0000000Z
ms.tool: azure-cli, azure-powershell
ms.devlang: azurecli
ms.custom: devx-track-azurepowershell, devx-track-azurecli
locale: en-us
document_id: 023e532d-35be-b17f-2928-f2710dd27f90
document_version_independent_id: 056b3221-b5f6-8ad7-76e8-6a39b5fac0d2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/how-to-use-vm-sign-in.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/how-to-use-vm-sign-in
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/how-to-use-vm-sign-in.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: d15c107e-8ada-b2d2-4818-761fd96877cd
---

# Use managed identities on an Azure VM for sign-inV - Managed identities for Azure resources | Microsoft Learn

This article provides PowerShell and CLI script examples for sign-in using managed identities for Azure resources service principal, and guidance on important topics such as error handling.

Note

We recommend that you use the Azure Az PowerShell module to interact with Azure. See [Install Azure PowerShell](/en-us/powershell/azure/install-azure-powershell) to get started. To learn how to migrate to the Az PowerShell module, see [Migrate Azure PowerShell from AzureRM to Az](/en-us/powershell/azure/migrate-from-azurerm-to-az).

## Prerequisites

- If you're not familiar with the managed identities for Azure resources feature, see this [overview](overview). If you don't have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you continue.

If you plan to use the Azure PowerShell or Azure CLI examples in this article, be sure to install the latest version of [Azure PowerShell](/en-us/powershell/azure/install-azure-powershell) or [Azure CLI](/en-us/cli/azure/install-azure-cli).

Important

- All sample script in this article assumes the command-line client is running on a VM with managed identities for Azure resources enabled. Use the VM "Connect" feature in the Azure portal, to remotely connect to your VM. For details on enabling managed identities for Azure resources on a VM, see [Configure managed identities for Azure resources on a VM using the Azure portal](qs-configure-portal-windows-vm), or one of the variant articles (using PowerShell, CLI, a template, or an Azure SDK).
- To prevent errors during resource access, the VM's managed identity must be given at least "Reader" access at the appropriate scope (the VM or higher) to allow Azure Resource Manager operations on the VM. See [Assign managed identities for Azure resources access to a resource using the Azure portal](grant-managed-identity-resource-access-azure-portal) for details.

## Overview

Managed identities for Azure resources provide a [service principal object](../../identity-platform/developer-glossary#service-principal-object) , which is [created upon enabling managed identities for Azure resources](overview) on the VM. The service principal can be given access to Azure resources, and used as an identity by script/command-line clients for sign-in and resource access. Traditionally, in order to access secured resources under its own identity, a script client would need to:

- be registered and consented with Microsoft Entra ID as a confidential/web client application
- sign in under its service principal, using the app's credentials (which are likely embedded in the script)

With managed identities for Azure resources, your script client no longer needs to do either, as it can sign in under the managed identities for Azure resources service principal.

## Azure CLI

The following script demonstrates how to:

1. Sign in to Microsoft Entra ID under the VM's managed identity for Azure resources service principal
2. Call Azure Resource Manager and get the VM's service principal ID. CLI takes care of managing token acquisition/use for you automatically. Be sure to substitute your virtual machine name for `<VM-NAME>`.

    ```azurecli
    az login --identity
    
    $spID=$(az resource list -n <VM-NAME> --query [*].identity.principalId --out tsv)
    echo The managed identity for Azure resources service principal ID is $spID
    ```

## Azure PowerShell

The following script demonstrates how to:

1. Sign in to Microsoft Entra ID under the VM's managed identity for Azure resources service principal
2. Call an Azure Resource Manager cmdlet to get information about the VM. PowerShell takes care of managing token use for you automatically.

    ```azurepowershell
    Add-AzAccount -identity
    
    # Call Azure Resource Manager to get the service principal ID for the VM's managed identity for Azure resources. 
    $vmInfoPs = Get-AzVM -ResourceGroupName <RESOURCE-GROUP> -Name <VM-NAME>
    $spID = $vmInfoPs.Identity.PrincipalId
    echo "The managed identity for Azure resources service principal ID is $spID"
    ```

## Resource IDs for Azure services

See [Azure services that support Microsoft Entra authentication](managed-identities-status) for a list of resources that support Microsoft Entra ID and have been tested with managed identities for Azure resources, and their respective resource IDs.

## Error handling guidance

Responses such as the following may indicate that the VM's managed identity for Azure resources has not been correctly configured:

- PowerShell: *Invoke-WebRequest : Unable to connect to the remote server*
- CLI: *MSI: Failed to retrieve a token from `http://localhost:50342/oauth2/token` with an error of 'HTTPConnectionPool(host='localhost', port=50342)*

If you receive one of these errors, return to the Azure VM in the [Azure portal](https://portal.azure.com) and go to the **Identity** page and ensure **System assigned** is set to "Yes."
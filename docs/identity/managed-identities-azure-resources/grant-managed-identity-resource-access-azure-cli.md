---
layout: Conceptual
title: Use Azure CLI to grant a managed identity access to a resource - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/grant-managed-identity-resource-access-azure-cli
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Step-by-step instructions on using Azure CLI to assign a managed identity access to an Azure resource or another resource.
ms.topic: how-to
ms.date: 2025-09-09T00:00:00.0000000Z
locale: en-us
document_id: 4693a6c3-1bef-3188-1bfc-6fd6a3167037
document_version_independent_id: 4693a6c3-1bef-3188-1bfc-6fd6a3167037
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/grant-managed-identity-resource-access-azure-cli.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
interactive_type: azurecli
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/grant-managed-identity-resource-access-azure-cli
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/grant-managed-identity-resource-access-azure-cli.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/089c8ba6-d135-43ff-bfaf-b8197fb72fb9
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/32516e21-6665-416f-be21-413febe47d91
platformId: fcd10361-e38b-0c68-2525-4eb1f6a966a8
---

# Use Azure CLI to grant a managed identity access to a resource - Managed identities for Azure resources | Microsoft Learn

This article shows you how to use the Azure CLI to give a managed identity access to an Azure resource. In this article, we use the example of an Azure virtual machine (Azure VM) managed identity accessing an Azure storage account. Once you've configured an Azure resource with a managed identity, you can then give the managed identity access to another resource, similar to any security principal.

## Prerequisites

- Be sure you've enabled managed identity on an Azure resource, such as an [Azure virtual machine](how-to-configure-managed-identities).
- If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before continuing.

## Prepare your environment

- Use the Bash environment in [Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see [Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).

    [![](../../reusable-content/azure-cli/media/hdi-launch-cloud-shell.png)](https://shell.azure.com)
- If you prefer to run CLI reference commands locally, [install](/en-us/cli/azure/install-azure-cli) the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see [How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).

    - If you're using a local installation, sign in to the Azure CLI by using the [az login](/en-us/cli/azure/reference-index#az-login) command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see [Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).
    - When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see [Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).
    - Run [az version](/en-us/cli/azure/reference-index?#az-version) to find the version and dependent libraries that are installed. To upgrade to the latest version, run [az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).

## Use Azure RBAC to assign a managed identity access to another resource

1. In this example, you give an Azure virtual machine (VM) managed access to a storage account. First use [az resource list](/en-us/cli/azure/resource#az-resource-list) to get the service principal for a VM named myVM:

    ```azurecli
    spID=$(az resource list -n myVM --query [*].identity.principalId --out tsv)
    ```

    For an Azure Virtual Machine (VM) scale set, the command is the same except here you get the service principal for the VM set named "DevTestVMSS":

    ```azurecli
    spID=$(az resource list -n DevTestVMSS --query [*].identity.principalId --out tsv)
    ```
2. Once you have the service principal ID, use [az role assignment create](/en-us/cli/azure/role/assignment#az-role-assignment-create) to give the virtual machine or virtual machine scale set **Reader** access to a storage account called "myStorageAcct":

    ```azurecli
    az role assignment create --assignee $spID --role 'Reader' --scope /subscriptions/<mySubscriptionID>/resourceGroups/<myResourceGroup>/providers/Microsoft.Storage/storageAccounts/myStorageAcct
    ```
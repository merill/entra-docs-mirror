---
layout: Conceptual
title: Manage user-assigned managed identities using the Azure CLI - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-azure-cli
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Manage user-assigned managed identities using the Azure CLI.
ms.topic: how-to
ms.date: 2025-09-09T00:00:00.0000000Z
locale: en-us
document_id: 3b4d5dd4-de86-8d54-de35-9655e21faa3e
document_version_independent_id: 3b4d5dd4-de86-8d54-de35-9655e21faa3e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-azure-cli.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
interactive_type: azurecli
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-azure-cli
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-azure-cli.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/089c8ba6-d135-43ff-bfaf-b8197fb72fb9
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/32516e21-6665-416f-be21-413febe47d91
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 6ad603d7-a4d0-da7d-960c-0af9b60d91f7
---

# Manage user-assigned managed identities using the Azure CLI - Managed identities for Azure resources | Microsoft Learn

Managed identities for Azure resources eliminate the need to manage credentials in code. You can use them to get a Microsoft Entra token for your applications. The applications can use the token when accessing resources that support Microsoft Entra authentication. Azure manages the identity so you don't have to.

There are two types of managed identities: system-assigned and user-assigned. System-assigned managed identities have their lifecycle tied to the resource that created them. This identity is restricted to only one resource, and you can grant permissions to the managed identity by using Azure role-based access control (RBAC). User-assigned managed identities can be used on multiple resources.

In this article, you learn how to create, list, delete, or assign a role to a user-assigned managed identity by using the Azure CLI.

## Prerequisites

- If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview). Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview#managed-identity-types).
- If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you continue.

## Prepare your environment

- Use the Bash environment in [Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see [Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).

    [![](../../reusable-content/azure-cli/media/hdi-launch-cloud-shell.png)](https://shell.azure.com)
- If you prefer to run CLI reference commands locally, [install](/en-us/cli/azure/install-azure-cli) the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see [How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).

    - If you're using a local installation, sign in to the Azure CLI by using the [az login](/en-us/cli/azure/reference-index#az-login) command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see [Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).
    - When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see [Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).
    - Run [az version](/en-us/cli/azure/reference-index?#az-version) to find the version and dependent libraries that are installed. To upgrade to the latest version, run [az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).

To modify user permissions when you use an app service principal by using the CLI, you must provide the service principal more permissions in the Azure Active Directory Graph API because portions of the CLI perform GET requests against the Graph API. Otherwise, you might end up receiving an "Insufficient privileges to complete the operation" message.

To do this step,

1. Go into the **App registration** in Microsoft Entra ID, select your app, select **API permissions**, and scroll down and select **Azure Active Directory Graph**.
2. Select **Application permissions**, and then add the appropriate permissions.

## Create a user-assigned managed identity

To create a user-assigned managed identity, your account needs the [Managed Identity Contributor](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role assignment.

1. Use the `az identity create` command to create a user-assigned managed identity. The `-g` parameter specifies the resource group where to create the user-assigned managed identity. The `-n` parameter specifies its name.
2. Replace the `<RESOURCE GROUP>` and `<USER ASSIGNED IDENTITY NAME>` parameter values with your own values.

    Important

    When you create user-assigned managed identities, the name must start with a letter or number, and may include a combination of alphanumeric characters, hyphens (-) and underscores (\_). For the assignment to a virtual machine or virtual machine scale set to work properly, the name is limited to 24 characters. For more information, see [FAQs and known issues](known-issues).

    ```azurecli
    az identity create -g <RESOURCE GROUP> -n <USER ASSIGNED IDENTITY NAME>
    ```

## List user-assigned managed identities

To list or read a user-assigned managed identity, your account needs the [Managed Identity Operator](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-operator) or [Managed Identity Contributor](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role assignment.

To list user-assigned managed identities, use the `az identity list` command. Replace the `<RESOURCE GROUP>` value with your own value.

```azurecli
az identity list -g <RESOURCE GROUP>
```

In the JSON response, user-assigned managed identities have the `"Microsoft.ManagedIdentity/userAssignedIdentities"` value returned for the key `type`.

`"type": "Microsoft.ManagedIdentity/userAssignedIdentities"`

## Delete a user-assigned managed identity

To delete a user-assigned managed identity, your account needs the [Managed Identity Contributor](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role assignment.

To delete a user-assigned managed identity,

1. use the `az identity delete` command. The `-n` parameter specifies its name. The `-g` parameter specifies the resource group where the user-assigned managed identity was created.
2. Replace the `<USER ASSIGNED IDENTITY NAME>` and `<RESOURCE GROUP>` parameter values with your own values.

    ```azurecli
    az identity delete -n <USER ASSIGNED IDENTITY NAME> -g <RESOURCE GROUP>
    ```

    Deleting a user-assigned managed identity won't remove the reference from any resource it was assigned to. Remove those from the resource itself. For example, for a VM or virtual machine scale set, use the `az vm/vmss identity remove` command.
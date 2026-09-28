---
layout: Conceptual
title: View service principal for a managed identity - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/how-to-view-managed-identity-service-principal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Step-by-step instructions for viewing the service principal of a managed identity.
ms.topic: how-to
ms.tgt_pltfrm: na
ms.date: 2025-03-14T00:00:00.0000000Z
ms.custom: devx-track-azurecli, devx-track-azurepowershell
zone_pivot_groups: identity-mi-service-principals
locale: en-us
document_id: e5a1ab2c-1e7a-646a-981d-56d653dd5e16
document_version_independent_id: e5a1ab2c-1e7a-646a-981d-56d653dd5e16
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/how-to-view-managed-identity-service-principal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
interactive_type: azurecli
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/how-to-view-managed-identity-service-principal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/how-to-view-managed-identity-service-principal.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/089c8ba6-d135-43ff-bfaf-b8197fb72fb9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/32516e21-6665-416f-be21-413febe47d91
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 4a352e9f-008a-3faa-cc67-88f6374f29f6
---

# View service principal for a managed identity - Managed identities for Azure resources | Microsoft Learn

Managed identities for Azure resources provide Azure services with an automatically managed identity in Microsoft Entra ID. You can use this identity to authenticate to any service that supports Microsoft Entra authentication without having credentials in your code.

In this article, you'll learn how to view the service principal of a managed identity.

Note

Service principals are enterprise applications.

## Prerequisites

- If you're unfamiliar with managed identities for Azure resources, see [What are managed identities for Azure resources?](overview).
- If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before continuing.
- Enable [system assigned identity on a virtual machine](qs-configure-portal-windows-vm#system-assigned-managed-identity) or [application](/en-us/azure/app-service/overview-managed-identity#add-a-system-assigned-identity).

::: zone pivot="identity-mi-service-principal-portal"

## View the service principal for a managed identity using the Azure portal

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. In the **Manage** section select **All applications**.
4. Set a filter for "Application type == Managed Identities" and select **Apply**.
5. (Optional) In the search filter box, enter the name of the Azure resource that has system managed identities enabled or the name of the user assigned managed identity.

    [![Screenshot of the View managed identity service principal.](media/how-to-view-managed-identity-service-principal-portal/view-managed-identity-service-principal-portal.png)](media/how-to-view-managed-identity-service-principal-portal/view-managed-identity-service-principal-portal.png#lightbox)

::: zone-end

::: zone pivot="identity-mi-service-principal-cli"

## View the service principal of a managed identity using Azure CLI

- Use the Bash environment in [Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see [Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).

    [![](../../reusable-content/azure-cli/media/hdi-launch-cloud-shell.png)](https://shell.azure.com)
- If you prefer to run CLI reference commands locally, [install](/en-us/cli/azure/install-azure-cli) the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see [How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).

    - If you're using a local installation, sign in to the Azure CLI by using the [az login](/en-us/cli/azure/reference-index#az-login) command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see [Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).
    - When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see [Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).
    - Run [az version](/en-us/cli/azure/reference-index?#az-version) to find the version and dependent libraries that are installed. To upgrade to the latest version, run [az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).

The following command demonstrates how to view the service principal of a virtual machine (VM) or application with managed identity enabled. Replace `<Azure resource name>` with your own values.

```azurecli
az ad sp list --display-name <Azure resource name>
```

::: zone-end

::: zone pivot="identity-mi-service-principal-powershell"

## View the service principal for a managed identity using PowerShell

To run the scripts for this example, you have two options:

- Use the [Azure Cloud Shell](/en-us/azure/cloud-shell/overview), which you can open using the **Try It** button on the top right corner of code blocks.
- Run scripts locally by installing the latest version of [Azure PowerShell](/en-us/powershell/azure/install-azure-powershell), then sign in to Azure using `Connect-AzAccount`.

The following command demonstrates how to view the service principal of a virtual machine (VM) or application with *system assigned identity* enabled. Replace `<Azure resource name>` with your own values.

```powershell
Get-AzADServicePrincipal -DisplayName <Azure resource name>
```

::: zone-end
---
layout: Conceptual
title: Get signed in identity - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/how-to-get-signed-in-identity
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Get the unique identifier for the currently signed in account for Azure CLI so that you can use this identity with role-based access control in Azure to connect to various Azure services.
ms.topic: how-to
ms.date: 2025-04-11T00:00:00.0000000Z
zone_pivot_groups: interface-portal-cli-powershell
locale: en-us
document_id: 6b7a21d6-6753-e321-1c85-bb772237dba8
document_version_independent_id: 6b7a21d6-6753-e321-1c85-bb772237dba8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/how-to-get-signed-in-identity.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
interactive_type: azurecli,azurepowershell
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/how-to-get-signed-in-identity
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/how-to-get-signed-in-identity.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/089c8ba6-d135-43ff-bfaf-b8197fb72fb9
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/cdc80360-921e-4b45-947f-2719acf06f23
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/32516e21-6665-416f-be21-413febe47d91
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/539badf0-028a-4e3e-bda6-770b2552b4d8
platformId: 08cebfd7-63d1-2555-3902-a7f1694afad8
---

# Get signed in identity - Microsoft Entra ID | Microsoft Learn

## Overview

This article gives simple steps to get the identity of the currently signed in account. You can use this identity information later to grant role-based access control access to the signed in account to either manage data or resources in Azure.

The current Azure CLI session could be signed in with a human identity (your account), a managed identity, a workload identity, or a service principal. No matter what type of identity you use with Azure CLI, to steps to get the details of the identity can be similar. For more information, see [Microsoft Entra identity fundamentals](/en-us/entra/fundamentals/identity-fundamental-concepts#identity).

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

::: zone pivot="interface-cli"

- Use the Bash environment in [Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see [Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).

    [![](../../reusable-content/azure-cli/media/hdi-launch-cloud-shell.png)](https://shell.azure.com)
- If you prefer to run CLI reference commands locally, [install](/en-us/cli/azure/install-azure-cli) the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see [How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).

    - If you're using a local installation, sign in to the Azure CLI by using the [az login](/en-us/cli/azure/reference-index#az-login) command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see [Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).
    - When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see [Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).
    - Run [az version](/en-us/cli/azure/reference-index?#az-version) to find the version and dependent libraries that are installed. To upgrade to the latest version, run [az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).

::: zone-end

::: zone pivot="interface-shell"

- If you choose to use Azure PowerShell locally:
    - [Install the latest version of the Az PowerShell module](/en-us/powershell/azure/install-azure-powershell).
    - Connect to your Azure account using the [Connect-AzAccount](/en-us/powershell/module/az.accounts/connect-azaccount) cmdlet.
- If you choose to use Azure Cloud Shell:
    - See [Overview of Azure Cloud Shell](/en-us/azure/cloud-shell/overview) for more information.

::: zone-end

## Get signed in account identity

Use the command line to query the graph for information about your account's unique identifier.

::: zone pivot="interface-cli"

1. Get the details for the currently logged-in account using [`az ad signed-in-user`](/en-us/cli/azure/ad/signed-in-user#az-ad-signed-in-user-show).

    ```azurecli
    az ad signed-in-user show
    ```
2. The command outputs a JSON response containing various fields.

    ```json
    {
      "@odata.context": "<https://graph.microsoft.com/v1.0/$metadata#users/$entity>",
      "businessPhones": [],
      "displayName": "Kai Carter",
      "givenName": "Kai",
      "id": "aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb",
      "jobTitle": "Senior Sales Representative",
      "mail": "<kai@adventure-works.com>",
      "mobilePhone": null,
      "officeLocation": "Redmond",
      "preferredLanguage": null,
      "surname": "Carter",
      "userPrincipalName": "<kai@adventure-works.com>"
    }
    ```

    Tip

    Record the value of the `id` field. In this example, that value would be `aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb`. This value can then be used in various scripts to grant your current account role-based access control permissions to Azure resources.

::: zone-end

::: zone pivot="interface-portal"

Use the in-portal panes for Microsoft Entra ID to get details of your currently signed-in user account.

1. Sign in to the Azure portal (https://portal.azure.com).
2. On the **Home** pane, locate and select the **Microsoft Entra ID** option.

    [![Screenshot of the Microsoft Entra ID option in the 'Home' page of the Azure portal.](media/get-signed-in-identity/home-entra-id-option.png)](media/get-signed-in-identity/home-entra-id-option-full.png#lightbox)

    Tip

    If this option isn't listed, select **More services** and then search for **Microsoft Entra ID** using the search term **"Entra"**.
3. Within the **Overview** pane for the Microsoft Entra ID tenant, select **Users** inside the **Manage** section of the service menu.

    ![Screenshot of the 'Users' option in the service menu for the Microsoft Entra ID tenant.](media/get-signed-in-identity/users-option-service-menu.png)
4. In the list of users, select the identity (user) that you want to get more details about.

    ![Screenshot of the list of users for a Microsoft Entra ID tenant with an example user highlighted.](media/get-signed-in-identity/users-list.png)

    Note

    This screenshot illustrates an example user named *"Kai Carter"* with a principal of `kai@adventure-works.com`.
5. On the details pane for the specific user, observe the value of the **Object ID** property.

    ![Screenshot of the details pane for a specific user in a Microsoft Entra ID tenant with their unique 'Object ID' highlighted.](media/get-signed-in-identity/user-details.png)

    Tip

    Record the value of the **Object ID** property. In this example, that value would be `aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb`. This value can then be used in various scripts to grant your current account role-based access control permissions to Azure resources.

::: zone-end

::: zone pivot="interface-shell"

1. Get the details for the currently logged-in account using [`Get-AzADUser`](/en-us/powershell/module/az.resources/get-azaduser).

    ```azurepowershell
    Get-AzADUser -SignedIn | Format-List `
        -Property Id, DisplayName, Mail, UserPrincipalName
    ```
2. The command outputs a list response containing various fields.

    ```output
    Id                : aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb
    DisplayName       : Kai Carter
    Mail              : kai@adventure-works.com
    UserPrincipalName : kai@adventure-works.com
    ```

    Tip

    Record the value of the `id` field. In this example, that value would be `aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb`. This value can then be used in various scripts to grant your current account role-based access control permissions to Azure resources.

::: zone-end
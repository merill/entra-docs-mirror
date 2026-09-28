---
layout: Conceptual
title: Assign a managed identity to an application role using Azure CLI - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/assign-app-role-managed-identity-azure-cli
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Step-by-step instructions for assigning a managed identity access to another application's role using Azure CLI.
ms.topic: how-to
ms.date: 2025-09-09T00:00:00.0000000Z
locale: en-us
document_id: 82ac8666-4ab3-5e63-2f5b-94d4b8137c99
document_version_independent_id: 82ac8666-4ab3-5e63-2f5b-94d4b8137c99
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/assign-app-role-managed-identity-azure-cli.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/assign-app-role-managed-identity-azure-cli
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/assign-app-role-managed-identity-azure-cli.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/089c8ba6-d135-43ff-bfaf-b8197fb72fb9
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/32516e21-6665-416f-be21-413febe47d91
platformId: 840da01f-1b3d-8020-f28b-3b75e2594550
---

# Assign a managed identity to an application role using Azure CLI - Managed identities for Azure resources | Microsoft Learn

Managed identities for Azure resources provide Azure services with an identity in Microsoft Entra ID. They work without needing credentials in your code. Azure services use this identity to authenticate to services that support Microsoft Entra authentication. Application roles provide a form of role-based access control, and allow a service to implement authorization rules.

Note

The tokens your application receives are cached by the underlying infrastructure. This means that any changes to the managed identity's roles can take significant time to process. For more information, see [Limitation of using managed identities for authorization](managed-identity-best-practice-recommendations#limitation-of-using-managed-identities-for-authorization).

In this article, you'll learn how to assign a managed identity to an application role exposed by another application using the [Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/overview) or [Azure CLI](/en-us/cli/azure/what-is-azure-cli).

## Prerequisites

- If you're unfamiliar with managed identities for Azure resources, see [Managed identity for Azure resources overview](overview).
- Review the [difference between a system-assigned and user-assigned managed identity](/en-us/azure/logic-apps/authenticate-with-managed-identity).
- If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before continuing.

## Assign a managed identity access to another application's app role using CLI

- Use the Bash environment in [Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see [Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).

    [![](../../reusable-content/azure-cli/media/hdi-launch-cloud-shell.png)](https://shell.azure.com)
- If you prefer to run CLI reference commands locally, [install](/en-us/cli/azure/install-azure-cli) the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see [How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).

    - If you're using a local installation, sign in to the Azure CLI by using the [az login](/en-us/cli/azure/reference-index#az-login) command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see [Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).
    - When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see [Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).
    - Run [az version](/en-us/cli/azure/reference-index?#az-version) to find the version and dependent libraries that are installed. To upgrade to the latest version, run [az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).

1. Enable managed identity on an Azure resource, [such as an Azure virtual machines](how-to-configure-managed-identities).
2. Find the object ID of the managed identity's service principal.

    - **For a system-assigned managed identity**, you can find the object ID on the Azure portal on the resource's **Identity** page. You can also use the following script to find the object ID. You'll need the resource ID of the resource you created in the previous step, which is available in the Azure portal on the resource's **Properties** page.

        ```azurecli
        resourceIdWithManagedIdentity="/subscriptions/{my subscription ID}/resourceGroups/{my resource group name}/providers/Microsoft.Compute/virtualMachines/{my virtual machine name}"
        
        oidForMI=$(az resource show --ids $resourceIdWithManagedIdentity --query "identity.principalId" -o tsv | tr -d '[:space:]')
        echo "object id for managed identity is: $oidForMI"
        ```
    - **For a user-assigned managed identity**, you can find the managed identity's object ID on the Azure portal on the resource's **Overview** page. You can also use the following script to find the object ID. You'll need the resource ID of the user-assigned managed identity.

        ```azurecli
        userManagedIdentityResourceId="/subscriptions/{my subscription ID}/resourceGroups/{my resource group name}/providers/Microsoft.ManagedIdentity/userAssignedIdentities/{my managed identity name}"
        
        oidForMI=$(az resource show --id $userManagedIdentityResourceId --query "properties.principalId" -o tsv | tr -d '[:space:]')
        echo "object id for managed identity is: $oidForMI"
        ```
3. [Create a new application registration](/en-us/entra/identity-platform/quickstart-register-app) to represent the service that your managed identity sends a request to.

    - If the API or service that exposes the app role grant to the managed identity already has a service principal in your Microsoft Entra tenant, skip this step.
4. Find the object ID of the service application's service principal. You can find this using the [Microsoft Entra admin center](https://entra.microsoft.com/).

    1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/).
    2. In the left nav blade, select **Entra ID** &gt; **Enterprise apps**. Then find the application and look for the **Object ID**.
    3. You can also find the service principal's object ID by its display name using the following script:

        ```azurecli
        appName="{name for your application}"
        serverSPOID=$(az ad sp list --filter "displayName eq '$appName'" --query '[0].id' -o tsv | tr -d '[:space:]')
        echo "object id for server service principal is: $serverSPOID"
        ```

        Note

        Display names for applications are not unique, so you should verify that you obtain the correct application's service principal.
    4. Or you can find the Object ID by the unique Application ID for your application registration:

        ```azurecli
        appID="{application id for your application}"
        serverSPOID=$(az ad sp list --filter "appId eq '$appID'" --query '[0].id' -o tsv | tr -d '[:space:]')
        echo "object id for server service principal is: $serverSPOID"
        ```
5. Add an [app role](../../identity-platform/howto-add-app-roles-in-apps) to the application you created in the previous step. You can create the role using the Azure portal or using Microsoft Graph. For example, you could add an app role like this:

    ```json
    {
        "allowedMemberTypes": [
            "Application"
        ],
        "displayName": "Read data from MyApi",
        "id": "00001111-aaaa-2222-bbbb-3333cccc4444",
        "isEnabled": true,
        "description": "Allow the application to read data as itself.",
        "value": "MyApi.Read.All"
    }
    ```
6. Assign the app role to the managed identity. You'll need the following information to assign the app role:

    - `managedIdentityObjectId`: the object ID of the managed identity's service principal, which you found in step 2.
    - `serverServicePrincipalObjectId`: the object ID of the server application's service principal, which you found in step 4.
    - `appRoleId`: the ID of the app role exposed by the server app, which you generated in step 5 - in the example, the app role ID is `00000000-0000-0000-0000-000000000000`.
7. Execute the following script to add the role assignment. This functionality isn't directly exposed on the Azure CLI and that a REST command is used here instead:

    ```azurecli
    roleguid="00000000-0000-0000-0000-000000000000"
    az rest -m POST -u https://graph.microsoft.com/v1.0/servicePrincipals/$oidForMI/appRoleAssignments -b "{\"principalId\": \"$oidForMI\", \"resourceId\": \"$serverSPOID\",\"appRoleId\": \"$roleguid\"}"
    ```
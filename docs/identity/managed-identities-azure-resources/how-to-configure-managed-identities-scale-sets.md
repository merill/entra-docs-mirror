---
layout: Conceptual
title: Configure managed identities for Azure resources on virtual machine scale set - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/how-to-configure-managed-identities-scale-sets
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Step-by-step instructions for configuring managed identities for Azure resources on a virtual machine scale set using the Azure portal.
ms.topic: quickstart
ms.date: 2025-01-16T00:00:00.0000000Z
ms.custom: mode-api, devx-track-azurecli, devx-track-linux, devx-track-arm-template, devx-track-azurepowershell
ms.devlang: azurecli
zone_pivot_groups: identity-mi-scaled-sets
locale: en-us
document_id: 05af5a98-d7e0-328e-9353-71fd0f07e0b8
document_version_independent_id: 05af5a98-d7e0-328e-9353-71fd0f07e0b8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/how-to-configure-managed-identities-scale-sets.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
interactive_type: azurecli,azurepowershell
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/how-to-configure-managed-identities-scale-sets
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/how-to-configure-managed-identities-scale-sets.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/96f6b0a2-2fd7-4de1-936d-89ad6e0eb7cc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ef8b0a5a-ba0a-4ec0-8636-48246ccd954f
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 81ca060b-d49c-b5fb-b73c-8c5d6187368f
---

# Configure managed identities for Azure resources on virtual machine scale set - Managed identities for Azure resources | Microsoft Learn

Managed identities for Azure resources provide Azure services with an automatically managed identity in Microsoft Entra ID. You can use this identity to authenticate to any service that supports Microsoft Entra authentication, without having credentials in your code.

For information about Azure Policy definition and details, see [Use Azure Policy to assign managed identities (preview)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F516187d4-ef64-4a1b-ad6b-a7348502976c).

::: zone pivot="identity-mi-methods-azp"

In this article, using the Azure portal, you learn how to perform the following managed identities for Azure resources operations on a virtual machine scale set:

- If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview).
- If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before continuing.
- To perform the management operations in this article, your account needs the following Azure role assignments:

    Note

    No additional Microsoft Entra directory role assignments required.

    - [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to enable and remove system-assigned managed identity from a virtual machine scale set.

## System-assigned managed identity

In this section, you will learn how to enable and disable the system-assigned managed identity using the Azure portal.

### Enable system-assigned managed identity during creation of a virtual machine scale set

Currently, the Azure portal does not support enabling system-assigned managed identity during the creation of a virtual machine scale set. First create a [Virtual Machine Scale Set](/en-us/azure/virtual-machine-scale-sets/quick-create-portal), then enable a system-assigned managed identity on the scale set:

- [Create a Virtual Machine Scale Set in the Azure portal](/en-us/azure/virtual-machine-scale-sets/quick-create-portal)

### Enable system-assigned managed identity on an existing virtual machine scale set

To enable the system-assigned managed identity on a virtual machine scale set that was originally provisioned without it:

1. Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the virtual machine scale set.
2. Navigate to the desired virtual machine scale set.
3. Under **System assigned**, **Status**, select **On** and then click **Save**:

    ![Screenshot shows &quot;Identity (preview)&quot; page with &quot;System assigned&quot; selected, the Status &quot;On&quot;, and the &quot;Save&quot; button highlighted.](media/msi-qs-configure-portal-windows-vmss/create-windows-vmss-portal-configuration-blade.png)

### Remove system-assigned managed identity from a virtual machine scale set

If you have a virtual machine scale set that no longer needs a system-assigned managed identity:

1. Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the virtual machine scale set. Also make sure your account belongs to a role that gives you write permissions on the virtual machine scale set.
2. Navigate to the desired virtual machine scale set.
3. Under **System assigned**, **Status**, select **Off** and then click **Save**:

    ![Screenshot showing the configuration page.](media/msi-qs-configure-portal-windows-vmss/disable-windows-vmss-portal-configuration-blade.png)

## User-assigned managed identity

In this section, you learn how to add and remove a user-assigned managed identity from a virtual machine scale set using the Azure portal.

### Assign a user-assigned managed identity during the creation of a virtual machine scale set

Currently, the Azure portal does not support assigning a user-assigned managed identity during the creation of a virtual machine scale set. First create a [Virtual Machine Scale Set](/en-us/azure/virtual-machine-scale-sets/quick-create-portal), then assign a user assigned managed identity to the scale set.

### Assign a user-assigned managed identity to an existing virtual machine scale set

1. Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the virtual machine scale set.
2. Navigate to the desired virtual machine scale set and click **Security** &gt; **Identity**, **User assigned** and then **+Add**.
3. Select the previously created [user assigned managed identity](how-manage-user-assigned-managed-identities#create-a-user-assigned-managed-identity) from the list.

    ![Screenshot that shows the Identity page with User assigned selected and the Add button highlighted.](media/msi-qs-configure-portal-windows-vmss/add-user-assigned-identity-vm-screenshot-1.png)

### Remove a user-assigned managed identity from a virtual machine scale set

Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the VM.

Navigate to the desired virtual machine scale set and click **Identity**, **User assigned**, the name of the user-assigned managed identity you want to delete and then click **Remove** (click **Yes** in the confirmation pane).

![A screenshot showing how to remove user-assigned identity from a virtual machine scale set.](media/msi-qs-configure-portal-windows-vmss/remove-user-assigned-identity-vmss-screenshot.png)

::: zone-end

::: zone pivot="identity-mi-methods-azcli"

In this article, you learn how to perform the following managed identities for Azure resources operations on an Azure virtual machine scale set, using the Azure CLI:

- Enable and disable the system-assigned managed identity on an Azure virtual machine scale set
- Add and remove a user-assigned managed identity on an Azure virtual machine scale set

If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before continuing.

## Prerequisites

- If you're unfamiliar with managed identities for Azure resources, see [What are managed identities for Azure resources?](overview). To learn about system-assigned and user-assigned managed identity types, see [Managed identity types](overview#managed-identity-types).
- To perform the management operations in this article, your account needs the following Azure role-based access control assignments:

    - [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to create a virtual machine scale set and enable and remove system and/or user-assigned managed identity from a virtual machine scale set.
    - [Managed Identity Contributor](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create a user-assigned managed identity.
    - [Managed Identity Operator](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to assign and remove a user-assigned managed identity from and to a virtual machine scale set.

    Note

    No additional Microsoft Entra directory role assignments required.

- Use the Bash environment in [Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see [Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).

    [![](../../reusable-content/azure-cli/media/hdi-launch-cloud-shell.png)](https://shell.azure.com)
- If you prefer to run CLI reference commands locally, [install](/en-us/cli/azure/install-azure-cli) the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see [How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).

    - If you're using a local installation, sign in to the Azure CLI by using the [az login](/en-us/cli/azure/reference-index#az-login) command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see [Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).
    - When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see [Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).
    - Run [az version](/en-us/cli/azure/reference-index?#az-version) to find the version and dependent libraries that are installed. To upgrade to the latest version, run [az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).

## System-assigned managed identity

In this section, you learn how to enable and disable the system-assigned managed identity for an Azure virtual machine scale set using Azure CLI.

### Enable system-assigned managed identity during creation of an Azure virtual machine scale set

To create a virtual machine scale set with the system-assigned managed identity enabled:

1. Create a [resource group](/en-us/azure/azure-resource-manager/management/overview#terminology) for containment and deployment of your virtual machine scale set and its related resources, using [az group create](/en-us/cli/azure/group/#az-group-create). You can skip this step if you already have a resource group you would like to use instead:

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```
2. [Create](/en-us/cli/azure/vmss/#az-vmss-create) a virtual machine scale set. The following example creates a virtual machine scale set named *myVMSS* with a system-assigned managed identity, as requested by the `--assign-identity` parameter, with the specified `--role` and `--scope`. The `--admin-username` and `--admin-password` parameters specify the administrative user name and password account for virtual machine sign-in. Update these values as appropriate for your environment:

    ```azurecli
    az vmss create --resource-group myResourceGroup --name myVMSS --image win2016datacenter --upgrade-policy-mode automatic --custom-data cloud-init.txt --admin-username azureuser --admin-password myPassword12 --assign-identity --generate-ssh-keys --role contributor --scope mySubscription
    ```

### Enable system-assigned managed identity on an existing Azure virtual machine scale set

If you need to [Enable](/en-us/cli/azure/vmss/identity#az-vmss-identity-assign) the system-assigned managed identity on an existing Azure virtual machine scale set:

```azurecli
az vmss identity assign -g myResourceGroup -n myVMSS
```

### Disable system-assigned managed identity from an Azure virtual machine scale set

If you have a virtual machine scale set that no longer needs the system-assigned managed identity, but still needs user-assigned managed identities, use the following command:

```azurecli
az vmss update -n myVM -g myResourceGroup --set identity.type='UserAssigned' 
```

If you have a virtual machine that no longer needs system-assigned managed identity and it has no user-assigned managed identities, use the following command:

Note

The value `none` is case sensitive. It must be lowercase.

```azurecli
az vmss update -n myVM -g myResourceGroup --set identity.type="none"
```

## User-assigned managed identity

In this section, you learn how to enable and remove a user-assigned managed identity using Azure CLI.

### Assign a user-assigned managed identity during the creation of a virtual machine scale set

This section walks you through creation of a virtual machine scale set and assignment of a user-assigned managed identity to the virtual machine scale set. If you already have a virtual machine scale set you want to use, skip this section and proceed to the next.

1. You can skip this step if you already have a resource group you would like to use. Create a [resource group](/en-us/azure/azure-resource-manager/management/overview#terminology) for containment and deployment of your user-assigned managed identity, using [az group create](/en-us/cli/azure/group/#az-group-create). Be sure to replace the `<RESOURCE GROUP>` and `<LOCATION>` parameter values with your own values. :

    ```azurecli
    az group create --name <RESOURCE GROUP> --location <LOCATION>
    ```
2. Create a user-assigned managed identity using [az identity create](/en-us/cli/azure/identity#az-identity-create). The `-g` parameter specifies the resource group where the user-assigned managed identity is created, and the `-n` parameter specifies its name. Be sure to replace the `<RESOURCE GROUP>` and `<USER ASSIGNED IDENTITY NAME>` parameter values with your own values:

    Important

    When you create user-assigned managed identities, the name must start with a letter or number, and may include a combination of alphanumeric characters, hyphens (-) and underscores (\_). For the assignment to a virtual machine or virtual machine scale set to work properly, the name is limited to 24 characters. For more information, see [FAQs and known issues](known-issues).

    ```azurecli
    az identity create -g <RESOURCE GROUP> -n <USER ASSIGNED IDENTITY NAME>
    ```

    The response contains details for the user-assigned managed identity created, similar to the following. The resource `id` value assigned to the user-assigned managed identity is used in the following step.

    ```json
    {
         "clientId": "00001111-aaaa-2222-bbbb-3333cccc4444",
         "clientSecretUrl": "https://control-westcentralus.identity.azure.net/subscriptions/<SUBSCRIPTON ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER ASSIGNED IDENTITY NAME>/credentials?tid=5678&oid=9012&aid=aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb",
         "id": "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER ASSIGNED IDENTITY NAME>",
         "location": "westcentralus",
         "name": "<USER ASSIGNED IDENTITY NAME>",
         "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
         "resourceGroup": "<RESOURCE GROUP>",
         "tags": {},
         "tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee",
         "type": "Microsoft.ManagedIdentity/userAssignedIdentities"    
    }
    ```
3. [Create](/en-us/cli/azure/vmss#az-vmss-create) a virtual machine scale set. The following example creates a virtual machine scale set associated with the new user-assigned managed identity, as specified by the `--assign-identity` parameter, with the specified `--role` and `--scope`. Be sure to replace the `<RESOURCE GROUP>`, `<VMSS NAME>`, `<USER NAME>`, `<PASSWORD>`, `<USER ASSIGNED IDENTITY>`, `<ROLE>`, and `<SUBSCRIPTION>` parameter values with your own values.

    ```azurecli
    az vmss create --resource-group <RESOURCE GROUP> --name <VMSS NAME> --image <SKU Linux Image> --admin-username <USER NAME> --admin-password <PASSWORD> --assign-identity <USER ASSIGNED IDENTITY> --role <ROLE> --scope <SUBSCRIPTION>
    ```

### Assign a user-assigned managed identity to an existing virtual machine scale set

1. Create a user-assigned managed identity using [az identity create](/en-us/cli/azure/identity#az-identity-create). The `-g` parameter specifies the resource group where the user-assigned managed identity is created, and the `-n` parameter specifies its name. Be sure to replace the `<RESOURCE GROUP>` and `<USER ASSIGNED IDENTITY NAME>` parameter values with your own values:

    ```azurecli
    az identity create -g <RESOURCE GROUP> -n <USER ASSIGNED IDENTITY NAME>
    ```

    The response contains details for the user-assigned managed identity created, similar to the following.

    ```json
    {
         "clientId": "00001111-aaaa-2222-bbbb-3333cccc4444",
         "clientSecretUrl": "https://control-westcentralus.identity.azure.net/subscriptions/<SUBSCRIPTON ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER ASSIGNED IDENTITY >/credentials?tid=5678&oid=9012&aid=aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb",
         "id": "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER ASSIGNED IDENTITY>",
         "location": "westcentralus",
         "name": "<USER ASSIGNED IDENTITY>",
         "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
         "resourceGroup": "<RESOURCE GROUP>",
         "tags": {},
         "tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee",
         "type": "Microsoft.ManagedIdentity/userAssignedIdentities"    
    }
    ```
2. [Assign](/en-us/cli/azure/vmss/identity) the user-assigned managed identity to your virtual machine scale set. Be sure to replace the `<RESOURCE GROUP>` and `<VIRTUAL MACHINE SCALE SET NAME>` parameter values with your own values. The `<USER ASSIGNED IDENTITY>` is the user-assigned identity's resource `name` property, as created in the previous step:

    ```azurecli
    az vmss identity assign -g <RESOURCE GROUP> -n <VIRTUAL MACHINE SCALE SET NAME> --identities <USER ASSIGNED IDENTITY>
    ```

### Remove a user-assigned managed identity from an Azure virtual machine scale set

To [remove](/en-us/cli/azure/vmss/identity#az-vmss-identity-remove) a user-assigned managed identity from a virtual machine scale set use `az vmss identity remove`. If this is the only user-assigned managed identity assigned to the virtual machine scale set, `UserAssigned` is removed from the identity type value. Be sure to replace the `<RESOURCE GROUP>` and `<VIRTUAL MACHINE SCALE SET NAME>` parameter values with your own values. The `<USER ASSIGNED IDENTITY>` is the user-assigned managed identity's `name` property, which can be found in the identity section of the virtual machine scale set using `az vmss identity show`:

```azurecli
az vmss identity remove -g <RESOURCE GROUP> -n <VIRTUAL MACHINE SCALE SET NAME> --identities <USER ASSIGNED IDENTITY>
```

If your virtual machine scale set doesn't have a system-assigned managed identity and you want to remove all user-assigned managed identities from it, use the following command:

Note

The value `none` is case sensitive. It must be lowercase.

```azurecli
az vmss update -n myVMSS -g myResourceGroup --set identity.type="none" identity.userAssignedIdentities=null
```

If your virtual machine scale set has both system-assigned and user-assigned managed identities, you can remove all the user-assigned identities by switching to use only system-assigned managed identity. Use the following command:

```azurecli
az vmss update -n myVMSS -g myResourceGroup --set identity.type='SystemAssigned' identity.userAssignedIdentities=null 
```

::: zone-end

::: zone pivot="identity-mi-methods-powershell"

In this article, using PowerShell, you learn how to perform the managed identities for Azure resources operations on a virtual machine scale set:

- Enable and disable the system-assigned managed identity on a virtual machine scale set
- Add and remove a user-assigned managed identity on a virtual machine scale set

Note

We recommend that you use the Azure Az PowerShell module to interact with Azure. See [Install Azure PowerShell](/en-us/powershell/azure/install-azure-powershell) to get started. To learn how to migrate to the Az PowerShell module, see [Migrate Azure PowerShell from AzureRM to Az](/en-us/powershell/azure/migrate-from-azurerm-to-az).

## Prerequisites

- If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview). **Be sure to review the [difference between a system-assigned and user managed assigned identity](overview#managed-identity-types)**.
- If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before continuing.
- To perform the management operations in this article, your account needs the following Azure role-based access control assignments:

    Note

    No additional Microsoft Entra directory role assignments required.

    - [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to create a virtual machine scale set and enable and remove system-assigned managed and/or user-assigned managed identity from a virtual machine scale set.
    - [Managed Identity Contributor](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create a user-assigned managed identity.
    - [Managed Identity Operator](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to assign and remove a user-assigned managed identity from and to a virtual machine scale set.
- To run the example scripts, you have two options:

    - Use the [Azure Cloud Shell](/en-us/azure/cloud-shell/overview), which you can open using the **Try It** button on the top-right corner of code blocks.
    - Run scripts locally by installing the latest version of [Azure PowerShell](/en-us/powershell/azure/install-azure-powershell), then sign in to Azure using `Connect-AzAccount`.

## System-assigned managed identity

In this section, you learn how to enable and remove a system-assigned managed identity using Azure PowerShell.

### Enable system-assigned managed identity during the creation of an Azure virtual machine scale set

To create a virtual machine scale set with the system-assigned managed identity enabled:

1. Refer to *Example 1* in the [New-AzVmssConfig](/en-us/powershell/module/az.compute/new-azvmssconfig) cmdlet reference article to create a virtual machine scale set with a system-assigned managed identity. Add the parameter `-IdentityType SystemAssigned` to the `New-AzVmssConfig` cmdlet:

    ```azurepowershell
    $VMSS = New-AzVmssConfig -Location $Loc -SkuCapacity 2 -SkuName "Standard_A0" -UpgradePolicyMode "Automatic" -NetworkInterfaceConfiguration $NetCfg -IdentityType SystemAssigned`
    ```

### Enable system-assigned managed identity on an existing Azure virtual machine scale set

If you need to enable a system-assigned managed identity on an existing Azure virtual machine scale set:

1. Make sure the Azure account you're using belongs to a role that gives you write permissions on the virtual machine scale set, such as "Virtual Machine Contributor".
2. Retrieve the virtual machine scale set properties using the [`Get-AzVmss`](/en-us/powershell/module/az.compute/get-azvmss) cmdlet. Then to enable a system-assigned managed identity, use the `-IdentityType` switch on the [Update-AzVmss](/en-us/powershell/module/az.compute/update-azvmss) cmdlet:

    ```azurepowershell
    Update-AzVmss -ResourceGroupName myResourceGroup -Name -myVmss -IdentityType "SystemAssigned"
    ```

### Disable the system-assigned managed identity from an Azure virtual machine scale set

If you have a virtual machine scale set that no longer needs the system-assigned managed identity but still needs user-assigned managed identities, use the following cmdlet:

1. Make sure your account belongs to a role that gives you write permissions on the virtual machine scale set, such as "Virtual Machine Contributor".
2. Run the following cmdlet:

    ```azurepowershell
    Update-AzVmss -ResourceGroupName myResourceGroup -Name myVmss -IdentityType "UserAssigned"
    ```
3. If you have a virtual machine scale set that no longer needs system-assigned managed identity and it has no user-assigned managed identities, use the following command:

    ```azurepowershell
    Update-AzVmss -ResourceGroupName myResourceGroup -Name myVmss -IdentityType None
    ```

## User-assigned managed identity

In this section, you learn how to add and remove a user-assigned managed identity from a virtual machine scale set using Azure PowerShell.

### Assign a user-assigned managed identity during creation of an Azure virtual machine scale set

Creating a new virtual machine scale set with a user-assigned managed identity isn't currently supported via PowerShell. See the next section on how to add a user-assigned managed identity to an existing virtual machine scale set. Check back for updates.

### Assign a user-assigned managed identity to an existing Azure virtual machine scale set

To assign a user-assigned managed identity to an existing Azure virtual machine scale set:

1. Make sure your account belongs to a role that gives you write permissions on the virtual machine scale set, such as "Virtual Machine Contributor".
2. Retrieve the virtual machine scale set properties using the `Get-AzVM` cmdlet. Then to assign a user-assigned managed identity to the virtual machine scale set, use the `-IdentityType` and `-IdentityID` switch on the [Update-AzVmss](/en-us/powershell/module/az.compute/update-azvmss) cmdlet. Replace `<VM NAME>`, `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>`, `<USER ASSIGNED ID1>`, `USER ASSIGNED ID2` with your own values.

    Important

    When you create user-assigned managed identities, the name must start with a letter or number, and may include a combination of alphanumeric characters, hyphens (-) and underscores (\_). For the assignment to a virtual machine or virtual machine scale set to work properly, the name is limited to 24 characters. For more information, see [FAQs and known issues](known-issues).

    ```azurepowershell
    Update-AzVmss -ResourceGroupName <RESOURCE GROUP> -Name <VMSS NAME> -IdentityType UserAssigned -IdentityID "<USER ASSIGNED ID1>","<USER ASSIGNED ID2>"
    ```

### Remove a user-assigned managed identity from an Azure virtual machine scale set

If your virtual machine scale set has multiple user-assigned managed identities, you can remove all but the last one using the following commands. Be sure to replace the `<RESOURCE GROUP>` and `<VIRTUAL MACHINE SCALE SET NAME>` parameter values with your own values. The `<USER ASSIGNED IDENTITY NAME>` is the user-assigned managed identity's name property, which should remain on the virtual machine scale set. This information can be found in the identity section of the virtual machine scale set using `az vmss show`:

```azurepowershell
Update-AzVmss -ResourceGroupName myResourceGroup -Name myVmss -IdentityType UserAssigned -IdentityID "<USER ASSIGNED IDENTITY NAME>"
```

If your virtual machine scale set doesn't have a system-assigned managed identity and you want to remove all user-assigned managed identities from it, use the following command:

```azurepowershell
Update-AzVmss -ResourceGroupName myResourceGroup -Name myVmss -IdentityType None
```

If your virtual machine scale set has both system-assigned and user-assigned managed identities, you can remove all the user-assigned managed identities by switching to use only system-assigned managed identity.

```azurepowershell
Update-AzVmss -ResourceGroupName myResourceGroup -Name myVmss -IdentityType "SystemAssigned"
```

::: zone-end

::: zone pivot="identity-mi-methods-arm"

In this article, you learn how to perform the following managed identities for Azure resources operations on an Azure virtual machine scale set, using Azure Resource Manager deployment template:

- Enable and disable the system-assigned managed identity on an Azure virtual machine scale set
- Add and remove a user-assigned managed identity on an Azure virtual machine scale set

## Prerequisites

- If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview). **Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview#managed-identity-types)**.
- If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before continuing.
- To perform the management operations in this article, your account needs the following Azure role-based access control assignments:

    Note

    No additional Microsoft Entra directory role assignments required.

    - [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to create a virtual machine scale set and enable and remove system and/or user-assigned managed identity from a virtual machine scale set.
    - [Managed Identity Contributor](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create a user-assigned managed identity.
    - [Managed Identity Operator](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to assign and remove a user-assigned managed identity from and to a virtual machine scale set.

## Azure Resource Manager templates

As with the Azure portal and scripting, [Azure Resource Manager](/en-us/azure/azure-resource-manager/management/overview) templates provide the ability to deploy new or modified resources defined by an Azure resource group. Several options are available for template editing and deployment, both local and portal-based, including:

- Using a [custom template from the Azure Marketplace](/en-us/azure/azure-resource-manager/templates/deploy-portal#deploy-resources-from-custom-template), which allows you to create a template from scratch, or base it on an existing common or [quickstart template](https://azure.microsoft.com/resources/templates/).
- Deriving from an existing resource group, by exporting a template from either [the original deployment](/en-us/azure/azure-resource-manager/templates/export-template-portal), or from the [current state of the deployment](/en-us/azure/azure-resource-manager/templates/export-template-portal).
- Using a local [JSON editor (such as VS Code)](/en-us/azure/azure-resource-manager/templates/quickstart-create-templates-use-the-portal), and then uploading and deploying by using PowerShell or CLI.
- Using the Visual Studio [Azure Resource Group project](/en-us/azure/azure-resource-manager/templates/create-visual-studio-deployment-project) to both create and deploy a template.

Regardless of the option you choose, template syntax is the same during initial deployment and redeployment. Enabling managed identities for Azure resources on a new or existing VM is done in the same manner. Also, by default, Azure Resource Manager does an [incremental update](/en-us/azure/azure-resource-manager/templates/deployment-modes) to deployments.

## System-assigned managed identity

In this section, you will enable and disable the system-assigned managed identity using an Azure Resource Manager template.

### Enable system-assigned managed identity during the creation of a virtual machines scale set or an existing virtual machine scale set

1. Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the virtual machine scale set.
2. To enable the system-assigned managed identity, load the template into an editor, locate the `Microsoft.Compute/virtualMachinesScaleSets` resource of interest within the resources section and add the `identity` property at the same level as the `"type": "Microsoft.Compute/virtualMachinesScaleSets"` property. Use the following syntax:

    ```JSON
    "identity": {
        "type": "SystemAssigned"
    }
    ```
3. When you're done, the following sections should be added to the resource section of your template and should resemble the example shown below:

    ```json
     "resources": [
         {
             //other resource provider properties...
             "apiVersion": "2018-06-01",
             "type": "Microsoft.Compute/virtualMachineScaleSets",
             "name": "[variables('vmssName')]",
             "location": "[resourceGroup().location]",
             "identity": {
                 "type": "SystemAssigned",
             },
            "properties": {
                 //other resource provider properties...
                 "virtualMachineProfile": {
                     //other virtual machine profile properties...
    
                 }
             }
         }
     ]
    ```

### Disable a system-assigned managed identity from an Azure virtual machine scale set

If you have a virtual machine scale set that no longer needs a system-assigned managed identity:

1. Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the virtual machine scale set.
2. Load the template into an editor and locate the `Microsoft.Compute/virtualMachineScaleSets` resource of interest within the `resources` section. If you have a VM that only has system-assigned managed identity, you can disable it by changing the identity type to `None`.

    **Microsoft.Compute/virtualMachineScaleSets API version 2018-06-01**

    If your apiVersion is `2018-06-01` and your VM has both system and user-assigned managed identities, remove `SystemAssigned` from the identity type and keep `UserAssigned` along with the userAssignedIdentities dictionary values.

    **Microsoft.Compute/virtualMachineScaleSets API version 2018-06-01**

    If your apiVersion is `2017-12-01` and your virtual machine scale set has both system and user-assigned managed identities, remove `SystemAssigned` from the identity type and keep `UserAssigned` along with the `identityIds` array of the user-assigned managed identities.

    The following example shows you how to remove a system-assigned managed identity from a virtual machine scale set with no user-assigned managed identities:

    ```json
    {
        "name": "[variables('vmssName')]",
        "apiVersion": "2018-06-01",
        "location": "[parameters(Location')]",
        "identity": {
            "type": "None"
         }
    
    }
    ```

## User-assigned managed identity

In this section, you assign a user-assigned managed identity to a virtual machine scale set using Azure Resource Manager template.

Note

To create a user-assigned managed identity using an Azure Resource Manager Template, see [Create a user-assigned managed identity](how-manage-user-assigned-managed-identities?pivots=identity-mi-methods-arm#create-a-user-assigned-managed-identity).

### Assign a user-assigned managed identity to a virtual machine scale set

1. Under the `resources` element, add the following entry to assign a user-assigned managed identity to your virtual machine scale set. Be sure to replace `<USERASSIGNEDIDENTITY>` with the name of the user-assigned managed identity you created.

    **Microsoft.Compute/virtualMachineScaleSets API version 2018-06-01**

    If your apiVersion is `2018-06-01`, your user-assigned managed identities are stored in the `userAssignedIdentities` dictionary format and the `<USERASSIGNEDIDENTITYNAME>` value must be stored in a variable defined in the `variables` section of your template.

    ```json
    {
        "name": "[variables('vmssName')]",
        "apiVersion": "2018-06-01",
        "location": "[parameters(Location')]",
        "identity": {
            "type": "userAssigned",
            "userAssignedIdentities": {
                "[resourceID('Microsoft.ManagedIdentity/userAssignedIdentities/',variables('<USERASSIGNEDIDENTITYNAME>'))]": {}
            }
        }
    
    }
    ```

    **Microsoft.Compute/virtualMachineScaleSets API version 2017-12-01**

    If your `apiVersion` is `2017-12-01` or earlier, your user-assigned managed identities are stored in the `identityIds` array and the `<USERASSIGNEDIDENTITYNAME>` value must be stored in a variable defined in the variables section of your template.

    ```json
    {
        "name": "[variables('vmssName')]",
        "apiVersion": "2017-03-30",
        "location": "[parameters(Location')]",
        "identity": {
            "type": "userAssigned",
            "identityIds": [
                "[resourceID('Microsoft.ManagedIdentity/userAssignedIdentities/',variables('<USERASSIGNEDIDENTITY>'))]"
            ]
        }
    }
    ```
2. When you are done, your template should look similar to the following:

    **Microsoft.Compute/virtualMachineScaleSets API version 2018-06-01**

    ```json
    "resources": [
         {
             //other resource provider properties...
             "apiVersion": "2018-06-01",
             "type": "Microsoft.Compute/virtualMachineScaleSets",
             "name": "[variables('vmssName')]",
             "location": "[resourceGroup().location]",
             "identity": {
                 "type": "UserAssigned",
                 "userAssignedIdentities": {
                     "[resourceID('Microsoft.ManagedIdentity/userAssignedIdentities/',variables('<USERASSIGNEDIDENTITYNAME>'))]": {}
                 }
             },
            "properties": {
                 //other virtual machine properties...
                 "virtualMachineProfile": {
                     //other virtual machine profile properties...
                 }
             }
         }
     ]
    ```

    **Microsoft.Compute/virtualMachines API version 2017-12-01**

    ```json
    "resources": [
         {
             //other resource provider properties...
             "apiVersion": "2017-12-01",
             "type": "Microsoft.Compute/virtualMachineScaleSets",
             "name": "[variables('vmssName')]",
             "location": "[resourceGroup().location]",
             "identity": {
                 "type": "UserAssigned",
                 "identityIds": [
                     "[resourceID('Microsoft.ManagedIdentity/userAssignedIdentities/',variables('<USERASSIGNEDIDENTITYNAME>'))]"
                 ]
             },
            "properties": {
                 //other virtual machine properties...
                 "virtualMachineProfile": {
                     //other virtual machine profile properties...
                 }
             }
         }
     ]
    ```

### Remove user-assigned managed identity from an Azure virtual machine scale set

If you have a virtual machine scale set that no longer needs a user-assigned managed identity:

1. Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the virtual machine scale set.
2. Load the template into an editor and locate the `Microsoft.Compute/virtualMachineScaleSets` resource of interest within the `resources` section. If you have a virtual machine scale set that only has user-assigned managed identity, you can disable it by changing the identity type to `None`.

    The following example shows you how to remove all user-assigned managed identities from a VM with no system-assigned managed identities:

    ```json
    {
        "name": "[variables('vmssName')]",
        "apiVersion": "2018-06-01",
        "location": "[parameters(Location')]",
        "identity": {
            "type": "None"
         }
    }
    ```

    **Microsoft.Compute/virtualMachineScaleSets API version 2018-06-01**

    To remove a single user-assigned managed identity from a virtual machine scale set, remove it from the `userAssignedIdentities` dictionary.

    If you have a system-assigned identity, keep it in the `type` value under the `identity` value.

    **Microsoft.Compute/virtualMachineScaleSets API version 2017-12-01**

    To remove a single user-assigned managed identity from a virtual machine scale set, remove it from the `identityIds` array.

    If you have a system-assigned managed identity, keep it in the `type` value under the `identity` value.

::: zone-end

::: zone pivot="identity-mi-methods-rest"

In this article, using CURL to make calls to the Azure Resource Manager REST endpoint, you learn how to perform the following managed identities for Azure resources operations on a virtual machine scale set:

- Enable and disable the system-assigned managed identity on an Azure virtual machine scale set
- Add and remove a user-assigned managed identity on an Azure virtual machine scale set

If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before continuing.

## Prerequisites

- If you're unfamiliar with managed identities for Azure resources, see [What are managed identities for Azure resources?](overview). To learn about system-assigned and user-assigned managed identity types, see [Managed identity types](overview#managed-identity-types).
- To perform the management operations in this article, your account needs the following Azure role assignments:

    - [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to create a virtual machine scale set and enable and remove system and/or user-assigned managed identity from a virtual machine scale set.
    - [Managed Identity Contributor](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create a user-assigned managed identity.
    - [Managed Identity Operator](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to assign and remove a user-assigned identity from and to a virtual machine scale set.

    Note

    No additional Microsoft Entra directory role assignments required.

- Use the Bash environment in [Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see [Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).

    [![](../../reusable-content/azure-cli/media/hdi-launch-cloud-shell.png)](https://shell.azure.com)
- If you prefer to run CLI reference commands locally, [install](/en-us/cli/azure/install-azure-cli) the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see [How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).

    - If you're using a local installation, sign in to the Azure CLI by using the [az login](/en-us/cli/azure/reference-index#az-login) command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see [Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).
    - When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see [Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).
    - Run [az version](/en-us/cli/azure/reference-index?#az-version) to find the version and dependent libraries that are installed. To upgrade to the latest version, run [az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).

## System-assigned managed identity

In this section, you learn how to enable and disable system-assigned managed identity on a virtual machine scale set using CURL to make calls to the Azure Resource Manager REST endpoint.

### Enable system-assigned managed identity during creation of a virtual machine scale set

To create a virtual machine scale set with system-assigned managed identity enabled, you need to create a virtual machine scale set and retrieve an access token to use CURL to call the Resource Manager endpoint with the system-assigned managed identity type value.

1. Create a [resource group](/en-us/azure/azure-resource-manager/management/overview#terminology) for containment and deployment of your virtual machine scale set and its related resources, using [az group create](/en-us/cli/azure/group/#az-group-create). You can skip this step if you already have resource group you would like to use instead:

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```
2. Create a [network interface](/en-us/cli/azure/network/nic#az-network-nic-create) for your virtual machine scale set:

    ```azurecli
     az network nic create -g myResourceGroup --vnet-name myVnet --subnet mySubnet -n myNic
    ```
3. Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your virtual machine scale set with a system-assigned managed identity.

    ```azurecli
    az account get-access-token
    ```
4. Using Azure Cloud Shell, create a virtual machine scale set using CURL to call the Azure Resource Manager REST endpoint. The following example creates a virtual machine scale set named *myVMSS* in the *myResourceGroup* with a system-assigned managed identity, as identified in the request body by the value `"identity":{"type":"SystemAssigned"}`. Replace `<ACCESS TOKEN>` with the value you received in the previous step when you requested a Bearer access token and the `<SUBSCRIPTION ID>` value as appropriate for your environment.

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01' -X PUT -d '{"sku":{"tier":"Standard","capacity":3,"name":"Standard_D1_v2"},"location":"eastus","identity":{"type":"SystemAssigned"},"properties":{"overprovision":true,"virtualMachineProfile":{"storageProfile":{"imageReference":{"sku":"2016-Datacenter","publisher":"MicrosoftWindowsServer","version":"latest","offer":"WindowsServer"},"osDisk":{"caching":"ReadWrite","managedDisk":{"storageAccountType":"StandardSSD_LRS"},"createOption":"FromImage"}},"osProfile":{"computerNamePrefix":"myVMSS","adminUsername":"azureuser","adminPassword":"myPassword12"},"networkProfile":{"networkInterfaceConfigurations":[{"name":"myVMSS","properties":{"primary":true,"enableIPForwarding":true,"ipConfigurations":[{"name":"myVMSS","properties":{"subnet":{"id":"/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"}}}]}}]}},"upgradePolicy":{"mode":"Manual"}}}' -H "Content-Type: application/json" -H "Authorization: Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PUT https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01 HTTP/1.1
    ```

    **Request headers**

    | Request header | Description |
    | --- | --- |
    | *Content-Type* | Required. Set to `application/json`. |
    | *Authorization* | Required. Set to a valid `Bearer` access token. |

    **Request body**

    ```JSON
     {
        "sku":{
           "tier":"Standard",
           "capacity":3,
           "name":"Standard_D1_v2"
        },
        "location":"eastus",
        "identity":{
           "type":"SystemAssigned"
        },
        "properties":{
           "overprovision":true,
           "virtualMachineProfile":{
              "storageProfile":{
                 "imageReference":{
                    "sku":"2016-Datacenter",
                    "publisher":"MicrosoftWindowsServer",
                    "version":"latest",
                    "offer":"WindowsServer"
                 },
                 "osDisk":{
                    "caching":"ReadWrite",
                    "managedDisk":{
                       "storageAccountType":"StandardSSD_LRS"
                    },
                    "createOption":"FromImage"
                 }
              },
              "osProfile":{
                 "computerNamePrefix":"myVMSS",
                 "adminUsername":"azureuser",
                 "adminPassword":"myPassword12"
              },
              "networkProfile":{
                 "networkInterfaceConfigurations":[
                    {
                       "name":"myVMSS",
                       "properties":{
                          "primary":true,
                          "enableIPForwarding":true,
                          "ipConfigurations":[
                             {
                                "name":"myVMSS",
                                "properties":{
                                   "subnet":{
                                      "id":"/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
                                   }
                                }
                             }
                          ]
                       }
                    }
                 ]
              }
           },
           "upgradePolicy":{
              "mode":"Manual"
           }
        }
     }  
    ```

### Enable system-assigned managed identity on an existing virtual machine scale set

To enable system-assigned managed identity on an existing virtual machine scale set, you need to acquire an access token and then use CURL to call the Resource Manager REST endpoint to update the identity type.

1. Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your virtual machine scale set with a system-assigned managed identity.

    ```azurecli
    az account get-access-token
    ```
2. Use the following CURL command to call the Azure Resource Manager REST endpoint to enable system-assigned managed identity on your virtual machine scale set as identified in the request body by the value `{"identity":{"type":"SystemAssigned"}` for a virtual machine scale set named *myVMSS*. Replace `<ACCESS TOKEN>` with the value you received in the previous step when you requested a Bearer access token and the `<SUBSCRIPTION ID>` value as appropriate for your environment.

    Important

    To ensure you don't delete any existing user-assigned managed identities that are assigned to the virtual machine scale set, you need to list the user-assigned managed identities by using this CURL command: `curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Compute/virtualMachineScaleSets/<VMSS NAME>?api-version=2018-06-01' -H "Authorization: Bearer <ACCESS TOKEN>"`. If you have any user-assigned managed identities assigned to the virtual machine scale set as identified in the `identity` value in the response, skip to step 3 that shows you how to retain user-assigned managed identities while enabling system-assigned managed identity on your virtual machine scale set.

    ```bash
     curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"SystemAssigned"}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01 HTTP/1.1
    ```

    **Request headers**

    | Request header | Description |
    | --- | --- |
    | *Content-Type* | Required. Set to `application/json`. |
    | *Authorization* | Required. Set to a valid `Bearer` access token. |

    **Request body**

    ```JSON
     {
        "identity":{
           "type":"SystemAssigned"
        }
     }
    ```
3. To enable system-assigned managed identity on a virtual machine scale set with existing user-assigned managed identities, you need to add `SystemAssigned` to the `type` value.

    For example, if your virtual machine scale set has the user-assigned managed identities `ID1` and `ID2` assigned to it, and you would like to add system-assigned managed identity to the virtual machine scale set, use the following CURL call. Replace `<ACCESS TOKEN>` and `<SUBSCRIPTION ID>` with values appropriate to your environment.

    API version `2018-06-01` stores user-assigned managed identities in the `userAssignedIdentities` value in a dictionary format as opposed to the `identityIds` value in an array format used in API version `2017-12-01`.

    **API VERSION 2018-06-01**

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"SystemAssigned,UserAssigned", "userAssignedIdentities":{"/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1":{},"/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID2":{}}}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01 HTTP/1.1
    ```

    **Request headers**

    | Request header | Description |
    | --- | --- |
    | *Content-Type* | Required. Set to `application/json`. |
    | *Authorization* | Required. Set to a valid `Bearer` access token. |

    **Request body**

    ```JSON
     {
        "identity":{
           "type":"SystemAssigned,UserAssigned",
           "userAssignedIdentities":{
              "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1":{
              },
              "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID2":{
    
              }
           }
        }
     }
    ```

    **API VERSION 2017-12-01**

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2017-12-01' -X PATCH -d '{"identity":{"type":"SystemAssigned,UserAssigned", "identityIds":["/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1","/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID2"]}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2017-12-01 HTTP/1.1
    ```

    **Request headers**

    | Request header | Description |
    | --- | --- |
    | *Content-Type* | Required. Set to `application/json`. |
    | *Authorization* | Required. Set to a valid `Bearer` access token. |

    **Request body**

    ```JSON
     {
        "identity":{
           "type":"SystemAssigned,UserAssigned",
           "identityIds":[
              "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1",
              "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID2"
           ]
        }
     }
    ```

### Disable system-assigned managed identity from a virtual machine scale set

To disable a system-assigned identity on an existing virtual machine scale set, you need to acquire an access token and then use CURL to call the Resource Manager REST endpoint to update the identity type to `None`.

1. Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your virtual machine scale set with a system-assigned managed identity.

    ```azurecli
    az account get-access-token
    ```
2. Update the virtual machine scale set using CURL to call the Azure Resource Manager REST endpoint to disable system-assigned managed identity. The following example disables system-assigned managed identity as identified in the request body by the value `{"identity":{"type":"None"}}` from a virtual machine scale set named *myVMSS*. Replace `<ACCESS TOKEN>` with the value you received in the previous step when you requested a Bearer access token and the `<SUBSCRIPTION ID>` value as appropriate for your environment.

    Important

    To ensure you don't delete any existing user-assigned managed identities that are assigned to the virtual machine scale set, you need to list the user-assigned managed identities by using this CURL command: `curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Compute/virtualMachineScaleSets/<VMSS NAME>?api-version=2018-06-01' -H "Authorization: Bearer <ACCESS TOKEN>"`. If you have any user-assigned managed identity assigned to the virtual machine scale set, skip to step 3 that shows you how retain the user-assigned managed identities while removing the system-assigned managed identity from your virtual machine scale set.

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"None"}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01 HTTP/1.1
    ```

    **Request headers**

    | Request header | Description |
    | --- | --- |
    | *Content-Type* | Required. Set to `application/json`. |
    | *Authorization* | Required. Set to a valid `Bearer` access token. |

    **Request body**

    ```JSON
     {
        "identity":{
           "type":"None"
        }
     }
    ```

    To remove system-assigned managed identity from a virtual machine scale set that has user-assigned managed identities, remove `SystemAssigned` from the `{"identity":{"type:" "}}` value while keeping the `UserAssigned` value and the `userAssignedIdentities` dictionary values if you are using **API version 2018-06-01**. If you are using **API version 2017-12-01** or earlier, keep the `identityIds` array.

## User-assigned managed identity

In this section, you learn how to add and remove user-assigned managed identity on a virtual machine scale set using CURL to make calls to the Azure Resource Manager REST endpoint.

### Assign a user-assigned managed identity during the creation of a virtual machine scale set

1. Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your virtual machine scale set with a system-assigned managed identity.

    ```azurecli
    az account get-access-token
    ```
2. Create a [network interface](/en-us/cli/azure/network/nic#az-network-nic-create) for your virtual machine scale set:

    ```azurecli
     az network nic create -g myResourceGroup --vnet-name myVnet --subnet mySubnet -n myNic
    ```
3. Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your virtual machine scale set with a system-assigned managed identity.

    ```azurecli
    az account get-access-token
    ```
4. Create a user-assigned managed identity using the instructions found here: [Create a user-assigned managed identity](how-manage-user-assigned-managed-identities?pivots=identity-mi-methods-rest#create-a-user-assigned-managed-identity).
5. Create a virtual machine scale set using CURL to call the Azure Resource Manager REST endpoint. The following example creates a virtual machine scale set named *myVMSS* in the resource group *myResourceGroup* with a user-assigned managed identity `ID1`, as identified in the request body by the value `"identity":{"type":"UserAssigned"}`. Replace `<ACCESS TOKEN>` with the value you received in the previous step when you requested a Bearer access token and the `<SUBSCRIPTION ID>` value as appropriate for your environment.

    **API VERSION 2018-06-01**

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01' -X PUT -d '{"sku":{"tier":"Standard","capacity":3,"name":"Standard_D1_v2"},"location":"eastus","identity":{"type":"UserAssigned","userAssignedIdentities":{"/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1":{}}},"properties":{"overprovision":true,"virtualMachineProfile":{"storageProfile":{"imageReference":{"sku":"2016-Datacenter","publisher":"MicrosoftWindowsServer","version":"latest","offer":"WindowsServer"},"osDisk":{"caching":"ReadWrite","managedDisk":{"storageAccountType":"StandardSSD_LRS"},"createOption":"FromImage"}},"osProfile":{"computerNamePrefix":"myVMSS","adminUsername":"azureuser","adminPassword":"myPassword12"},"networkProfile":{"networkInterfaceConfigurations":[{"name":"myVMSS","properties":{"primary":true,"enableIPForwarding":true,"ipConfigurations":[{"name":"myVMSS","properties":{"subnet":{"id":"/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"}}}]}}]}},"upgradePolicy":{"mode":"Manual"}}}' -H "Content-Type: application/json" -H "Authorization: Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PUT https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01 HTTP/1.1
    ```

    **Request headers**

    | Request header | Description |
    | --- | --- |
    | *Content-Type* | Required. Set to `application/json`. |
    | *Authorization* | Required. Set to a valid `Bearer` access token. |

    **Request body**

    ```JSON
     {
        "sku":{
           "tier":"Standard",
           "capacity":3,
           "name":"Standard_D1_v2"
        },
        "location":"eastus",
        "identity":{
           "type":"UserAssigned",
           "userAssignedIdentities":{
              "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1":{
    
              }
           }
        },
        "properties":{
           "overprovision":true,
           "virtualMachineProfile":{
              "storageProfile":{
                 "imageReference":{
                    "sku":"2016-Datacenter",
                    "publisher":"MicrosoftWindowsServer",
                    "version":"latest",
                    "offer":"WindowsServer"
                 },
                 "osDisk":{
                    "caching":"ReadWrite",
                    "managedDisk":{
                       "storageAccountType":"StandardSSD_LRS"
                    },
                    "createOption":"FromImage"
                 }
              },
              "osProfile":{
                 "computerNamePrefix":"myVMSS",
                 "adminUsername":"azureuser",
                 "adminPassword":"myPassword12"
              },
              "networkProfile":{
                 "networkInterfaceConfigurations":[
                    {
                       "name":"myVMSS",
                       "properties":{
                          "primary":true,
                          "enableIPForwarding":true,
                          "ipConfigurations":[
                             {
                                "name":"myVMSS",
                                "properties":{
                                   "subnet":{
                                      "id":"/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
                                   }
                                }
                             }
                          ]
                       }
                    }
                 ]
              }
           },
           "upgradePolicy":{
              "mode":"Manual"
           }
        }
     }
    ```

    **API VERSION 2017-12-01**

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2017-12-01' -X PUT -d '{"sku":{"tier":"Standard","capacity":3,"name":"Standard_D1_v2"},"location":"eastus","identity":{"type":"UserAssigned","identityIds":["/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1"]},"properties":{"overprovision":true,"virtualMachineProfile":{"storageProfile":{"imageReference":{"sku":"2016-Datacenter","publisher":"MicrosoftWindowsServer","version":"latest","offer":"WindowsServer"},"osDisk":{"caching":"ReadWrite","managedDisk":{"storageAccountType":"StandardSSD_LRS"},"createOption":"FromImage"}},"osProfile":{"computerNamePrefix":"myVMSS","adminUsername":"azureuser","adminPassword":"myPassword12"},"networkProfile":{"networkInterfaceConfigurations":[{"name":"myVMSS","properties":{"primary":true,"enableIPForwarding":true,"ipConfigurations":[{"name":"myVMSS","properties":{"subnet":{"id":"/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"}}}]}}]}},"upgradePolicy":{"mode":"Manual"}}}' -H "Content-Type: application/json" -H "Authorization: Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PUT https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2017-12-01 HTTP/1.1
    ```

    **Request headers**

    | Request header | Description |
    | --- | --- |
    | *Content-Type* | Required. Set to `application/json`. |
    | *Authorization* | Required. Set to a valid `Bearer` access token. |

    **Request body**

    ```JSON
     {
        "sku":{
           "tier":"Standard",
           "capacity":3,
           "name":"Standard_D1_v2"
        },
        "location":"eastus",
        "identity":{
           "type":"UserAssigned",
           "identityIds":[
              "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1"
           ]
        },
        "properties":{
           "overprovision":true,
           "virtualMachineProfile":{
              "storageProfile":{
                 "imageReference":{
                    "sku":"2016-Datacenter",
                    "publisher":"MicrosoftWindowsServer",
                    "version":"latest",
                    "offer":"WindowsServer"
                 },
                 "osDisk":{
                    "caching":"ReadWrite",
                    "managedDisk":{
                       "storageAccountType":"StandardSSD_LRS"
                    },
                    "createOption":"FromImage"
                 }
              },
              "osProfile":{
                 "computerNamePrefix":"myVMSS",
                 "adminUsername":"azureuser",
                 "adminPassword":"myPassword12"
              },
              "networkProfile":{
                 "networkInterfaceConfigurations":[
                    {
                       "name":"myVMSS",
                       "properties":{
                          "primary":true,
                          "enableIPForwarding":true,
                          "ipConfigurations":[
                             {
                                "name":"myVMSS",
                                "properties":{
                                   "subnet":{
                                      "id":"/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
                                   }
                                }
                             }
                          ]
                       }
                    }
                 ]
              }
           },
           "upgradePolicy":{
              "mode":"Manual"
           }
        }
     }
    ```

### Assign a user-assigned managed identity to an existing Azure virtual machine scale set

1. Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your virtual machine scale set with a system-assigned managed identity.

    ```azurecli
    az account get-access-token
    ```
2. Create a user-assigned managed identity using the instructions found here, [Create a user-assigned managed identity](how-manage-user-assigned-managed-identities?pivots=identity-mi-methods-rest#create-a-user-assigned-managed-identity).
3. To ensure you don't delete existing user or system-assigned managed identities that are assigned to the virtual machine scale set, you need to list the identity types assigned to the virtual machine scale set by using the following CURL command. If you have managed identities assigned to the virtual machine scale set, they are listed in the `identity` value.

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Compute/virtualMachineScaleSets/<VMSS NAME>?api-version=2018-06-01' -H "Authorization: Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    GET https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Compute/virtualMachineScaleSets/<VMSS NAME>?api-version=2018-06-01 HTTP/1.1
    ```

    **Request headers**

    | Request header | Description |
    | --- | --- |
    | *Authorization* | Required. Set to a valid `Bearer` access token. |
4. If you don't have any user or system-assigned managed identities assigned to your virtual machine scale set, use the following CURL command to call the Azure Resource Manager REST endpoint to assign the first user-assigned managed identity to the virtual machine scale set. If you have a user or system-assigned managed identity(s) assigned to the virtual machine scale set, skip to step 5 that shows you how to add multiple user-assigned managed identities to a virtual machine scale set while also maintaining the system-assigned managed identity.

    The following example assigns a user-assigned managed identity, `ID1` to a virtual machine scale set named *myVMSS* in the resource group *myResourceGroup*. Replace `<ACCESS TOKEN>` with the value you received in the previous step when you requested a Bearer access token and the `<SUBSCRIPTION ID>` value as appropriate for your environment.

    **API VERSION 2018-06-01**

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-12-01' -X PATCH -d '{"identity":{"type":"userAssigned", "userAssignedIdentities":{"/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1":{}}}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-12-01 HTTP/1.1
    ```

    **Request headers**

    | Request header | Description |
    | --- | --- |
    | *Content-Type* | Required. Set to `application/json`. |
    | *Authorization* | Required. Set to a valid `Bearer` access token. |

    **Request body**

    ```JSON
     {
        "identity":{
           "type":"userAssigned",
           "userAssignedIdentities":{
              "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1":{
    
              }
           }
        }
     }
    ```

    **API VERSION 2017-12-01**

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2017-12-01' -X PATCH -d '{"identity":{"type":"userAssigned", "identityIds":["/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1"]}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2017-12-01 HTTP/1.1
    ```

    **Request headers**

    | Request header | Description |
    | --- | --- |
    | *Content-Type* | Required. Set to `application/json`. |
    | *Authorization* | Required. Set to a valid `Bearer` access token. |

    **Request body**

    ```JSON
     {
        "identity":{
           "type":"userAssigned",
           "identityIds":[
              "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1"
           ]
        }
     }
    ```
5. If you have an existing user-assigned or system-assigned managed identity assigned to your virtual machine scale set:

    **API VERSION 2018-06-01**

    Add the user-assigned managed identity to the `userAssignedIdentities` dictionary value.

    For example, if you have system-assigned managed identity and the user-assigned managed identity `ID1` currently assigned to your virtual machine scale and would like to add the user-assigned managed identity `ID2` to it:

    ```bash
    curl  'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"SystemAssigned, UserAssigned", "userAssignedIdentities":{"/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1":{},"/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID2":{}}}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01 HTTP/1.1
    ```

    **Request headers**

    | Request header | Description |
    | --- | --- |
    | *Content-Type* | Required. Set to `application/json`. |
    | *Authorization* | Required. Set to a valid `Bearer` access token. |

    **Request body**

    ```JSON
     {
        "identity":{
           "type":"SystemAssigned, UserAssigned",
           "userAssignedIdentities":{
              "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1":{
    
              },
              "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID2":{
    
              }
           }
        }
     }
    ```

    **API VERSION 2017-12-01**

    Retain the user-assigned managed identities you would like to keep in the `identityIds` array value while adding the new user-assigned managed identity.

    For example, if you have system-assigned identity and the user-assigned managed identity `ID1` currently assigned to your virtual machine scale set and would like to add the user-assigned managed identity `ID2` to it:

    ```bash
    curl  'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2017-12-01' -X PATCH -d '{"identity":{"type":"SystemAssigned, UserAssigned", "identityIds":["/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1","/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID2"]}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2017-12-01 HTTP/1.1
    ```

    **Request headers**

    | Request header | Description |
    | --- | --- |
    | *Content-Type* | Required. Set to `application/json`. |
    | *Authorization* | Required. Set to a valid `Bearer` access token. |

    **Request body**

    ```JSON
     {
        "identity":{
           "type":"SystemAssigned, UserAssigned",
           "identityIds":[
              "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1",
              "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID2"
           ]
        }
     }
    ```

### Remove a user-assigned managed identity from a virtual machine scale set

1. Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your virtual machine scale set with a system-assigned managed identity.

    ```azurecli
    az account get-access-token
    ```
2. To ensure you don't delete any existing user-assigned managed identities that you would like to keep assigned to the virtual machine scale set or remove the system-assigned managed identity, you need to list the managed identities by using the following CURL command:

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Compute/virtualMachineScaleSets/<VMSS NAME>?api-version=2018-06-01' -H "Authorization: Bearer <ACCESS TOKEN>" 
    ```

    ```HTTP
    GET https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Compute/virtualMachineScaleSets/<VMSS NAME>?api-version=2018-06-01 HTTP/1.1
    ```

    **Request headers**

    | Request header | Description |
    | --- | --- |
    | *Authorization* | Required. Set to a valid `Bearer` access token. |

    If you have managed identities assigned to the VM, they are listed in the response in the `identity` value.

    For example, if you have user-assigned managed identities `ID1` and `ID2` assigned to your virtual machine scale set, and you only want to keep `ID1` assigned and retain the system-assigned managed identity:

    **API VERSION 2018-06-01**

    Add `null` to the user-assigned managed identity you would like to remove:

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"SystemAssigned, UserAssigned", "userAssignedIdentities":{"/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID2":null}}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01 HTTP/1.1
    ```

    **Request headers**

    | Request header | Description |
    | --- | --- |
    | *Content-Type* | Required. Set to `application/json`. |
    | *Authorization* | Required. Set to a valid `Bearer` access token. |

    **Request body**

    ```JSON
     {
        "identity":{
           "type":"SystemAssigned, UserAssigned",
           "userAssignedIdentities":{
              "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID2":null
           }
        }
     }
    ```

    **API VERSION 2017-12-01**

    Retain only the user-assigned managed identity(s) you would like to keep in the `identityIds` array:

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2017-12-01' -X PATCH -d '{"identity":{"type":"SystemAssigned,UserAssigned", "identityIds":["/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1"]}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2017-12-01 HTTP/1.1
    ```

    **Request headers**

    | Request header | Description |
    | --- | --- |
    | *Content-Type* | Required. Set to `application/json`. |
    | *Authorization* | Required. Set to a valid `Bearer` access token. |

    **Request body**

    ```JSON
     {
        "identity":{
           "type":"SystemAssigned,UserAssigned",
           "identityIds":[
              "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1"
           ]
        }
     }
    ```

If your virtual machine scale set has both system-assigned and user-assigned managed identities, you can remove all the user-assigned managed identities by switching to use only system-assigned using the following command:

```bash
curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"SystemAssigned"}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
```

```HTTP
PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01 HTTP/1.1
```

**Request headers**

| Request header | Description |
| --- | --- |
| *Content-Type* | Required. Set to `application/json`. |
| *Authorization* | Required. Set to a valid `Bearer` access token. |

**Request body**

```JSON
{
   "identity":{
      "type":"SystemAssigned"
   }
}
```

If your virtual machine scale set has only user-assigned managed identities and you would like to remove them all, use the following command:

```bash
curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"None"}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
```

```HTTP
PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01 HTTP/1.1
```

**Request headers**

| Request header | Description |
| --- | --- |
| *Content-Type* | Required. Set to `application/json`. |
| *Authorization* | Required. Set to a valid `Bearer` access token. |

**Request body**

```JSON
{
   "identity":{
      "type":"None"
   }
}
```

::: zone-end
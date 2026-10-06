---
layout: Conceptual
title: Configure managed identities on Azure virtual machines (VMs) - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/how-to-configure-managed-identities
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Step-by-step instructions for configuring system and user-assigned managed identities on an Azure VMs.
ms.topic: quickstart
ms.date: 2025-01-16T00:00:00.0000000Z
ms.custom: mode-api, devx-track-azurecli, devx-track-linux, devx-track-arm-template, devx-track-azurepowershell
ms.devlang: azurecli
zone_pivot_groups: identity-configure-mi-methods
locale: en-us
document_id: aa5bf9cf-3d6a-ecc4-7bbc-634ebf519c43
document_version_independent_id: aa5bf9cf-3d6a-ecc4-7bbc-634ebf519c43
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/how-to-configure-managed-identities.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
interactive_type: azurecli,azurepowershell
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/how-to-configure-managed-identities
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/how-to-configure-managed-identities.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/2ed91286-6cf7-4b83-810d-75d0ee3b09dd
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/6735bd7e-4f7b-457d-b58c-29e6f0198677
platformId: a5307446-c018-42df-b73a-0cdfdecb7e7e
---

# Configure managed identities on Azure virtual machines (VMs) - Managed identities for Azure resources | Microsoft Learn

Managed identities for Azure resources provide Azure services with an automatically managed identity in Microsoft Entra ID. You can use this identity to authenticate to any service that supports Microsoft Entra authentication, without having credentials in your code.

For information about Azure Policy definition and details, see [Use Azure Policy to assign managed identities (preview)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd367bd60-64ca-4364-98ea-276775bddd94).

::: zone pivot="qs-configure-portal-windows-vm"

In this article, you learn how to enable and disable system and user-assigned managed identities for an Azure Virtual Machine (VM), using the Azure portal.

## Prerequisites

- If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview).
- If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before continuing.

## System-assigned managed identity

In this section, you learn how to enable and disable the system-assigned managed identity for VM using the Azure portal.

### Enable system-assigned managed identity during creation of a VM

To enable system-assigned managed identity on a VM during its creation, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) role assignment. No other Microsoft Entra directory role assignments are required.

When creating a [Windows virtual machine](/en-us/azure/virtual-machines/windows/quick-create-portal#create-virtual-machine) or [Linux virtual machine](/en-us/azure/virtual-machines/linux/quick-create-portal#create-virtual-machine), select the **Management** tab.

In the **Identity** section, select the **Enable system assigned managed identity** check-box.

![Screenshot showing how to enable system-assigned identity during VM creation.](media/msi-qs-configure-portal-windows-vm/enable-system-assigned-identity-vm-creation.png)

### Enable system-assigned managed identity on an existing VM

To enable system-assigned managed identity on a VM that was originally provisioned without it, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) role assignment. No other Microsoft Entra directory role assignments are required.

1. Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the VM.
2. Navigate to the desired Virtual Machine and in the **Security** section select **Identity**.
3. Under **System assigned**, **Status**, select **On** and then click **Save**:

    ![Screenshot that shows the Identity page with the System assigned status set to On.](media/msi-qs-configure-portal-windows-vm/create-windows-vm-portal-configuration-blade.png)

### Remove system-assigned managed identity from a VM

To remove system-assigned managed identity from a VM, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) role assignment. No other Microsoft Entra directory role assignments are required.

If you have a Virtual Machine that no longer needs system-assigned managed identity:

1. Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the VM.
2. Navigate to the desired Virtual Machine and in the **Security** section select **Identity**.
3. Under **System assigned**, **Status**, select **Off** and then click **Save**:

    ![Screenshot of the configuration page.](media/msi-qs-configure-portal-windows-vm/create-windows-vm-portal-configuration-blade-disable.png)

## User-assigned managed identity

In this section, you learn how to add and remove a user-assigned managed identity from a VM using the Azure portal.

### Assign a user-assigned identity during the creation of a VM

To assign a user-assigned identity to a VM, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) and [Managed Identity Operator](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-operator) role assignments. No other Microsoft Entra directory role assignments are required.

Currently, the Azure portal does not support assigning a user-assigned managed identity during the creation of a VM. First create a [Windows virtual machine](/en-us/azure/virtual-machines/windows/quick-create-portal#create-virtual-machine) or [Linux virtual machine](/en-us/azure/virtual-machines/linux/quick-create-portal#create-virtual-machine), then assign a user-assigned managed identity to the VM.

### Assign a user-assigned managed identity to an existing VM

To assign a user-assigned identity to a VM, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) and [Managed Identity Operator](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-operator) role assignments. No other Microsoft Entra directory role assignments are required.

1. Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the VM.
2. Navigate to the desired VM and click **Security** &gt; **Identity**, **User assigned** and then **+Add**. Click the user-assigned identity you want to add to the VM and then click **Add**.
3. Select the previously created [user assigned managed identity](how-manage-user-assigned-managed-identities#create-a-user-assigned-managed-identity) from the list.

    ![Screenshot that shows the Identity page with User assigned selected and the Add button highlighted.](media/msi-qs-configure-portal-windows-vm/add-user-assigned-identity-vm-screenshot1.png)

### Remove a user-assigned managed identity from a VM

To remove a user-assigned identity from a VM, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) role assignment. No other Microsoft Entra directory role assignments are required.

Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the VM.

Navigate to the desired VM and select **Security** &gt; **Identity**, **User assigned**, the name of the user-assigned managed identity you want to delete and then click **Remove** (click **Yes** in the confirmation pane).

![Screenshot showing how to remove user-assigned managed identity from a VM.](media/msi-qs-configure-portal-windows-vm/remove-user-assigned-identity-vm-screenshot.png)

::: zone-end

::: zone pivot="qs-configure-cli-windows-vm"

In this article, using the Azure CLI, you learn how to perform the following managed identities for Azure resources operations on an Azure VM:

- Enable and disable the system-assigned managed identity on an Azure VM
- Add and remove a user-assigned managed identity on an Azure VM

If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before continuing.

## Prerequisites

- If you're unfamiliar with managed identities for Azure resources, see [What are managed identities for Azure resources?](overview). To learn about system-assigned and user-assigned managed identity types, see [Managed identity types](overview#managed-identity-types).

- Use the Bash environment in [Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see [Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).

    [![](../../reusable-content/azure-cli/media/hdi-launch-cloud-shell.png)](https://shell.azure.com)
- If you prefer to run CLI reference commands locally, [install](/en-us/cli/azure/install-azure-cli) the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see [How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).

    - If you're using a local installation, sign in to the Azure CLI by using the [az login](/en-us/cli/azure/reference-index#az-login) command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see [Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).
    - When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see [Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).
    - Run [az version](/en-us/cli/azure/reference-index?#az-version) to find the version and dependent libraries that are installed. To upgrade to the latest version, run [az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).

## System-assigned managed identity

In this section, you learn how to enable and disable the system-assigned managed identity on an Azure VM using Azure CLI.

### Enable system-assigned managed identity during creation of an Azure VM

To create an Azure VM with the system-assigned managed identity enabled, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) role assignment. No other Microsoft Entra directory role assignments are required.

1. Create a [resource group](/en-us/azure/azure-resource-manager/management/overview#terminology) for containment and deployment of your VM and its related resources, using [az group create](/en-us/cli/azure/group/#az-group-create). You can skip this step if you already have resource group you would like to use instead:

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```
2. Create a VM using [az vm create](/en-us/cli/azure/vm/#az-vm-create). The following example creates a VM named *myVM* with a system-assigned managed identity, as requested by the `--assign-identity` parameter, with the specified `--role` and `--scope`. The `--admin-username` and `--admin-password` parameters specify the administrative user name and password account for virtual machine sign-in. Update these values as appropriate for your environment:

    ```azurecli
    az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --generate-ssh-keys --assign-identity --role contributor --scope /Subscriptions/mySubscriptionId/resourceGroups/myResourceGroup --admin-username azureuser --admin-password myPassword12
    ```

### Enable system-assigned managed identity on an existing Azure VM

To enable system-assigned managed identity on a VM, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) role assignment. No other Microsoft Entra directory role assignments are required.

1. If you're using the Azure CLI in a local console, first sign in to Azure using [az login](/en-us/cli/azure/reference-index#az-login). Use an account that is associated with the Azure subscription that contains the VM.

    ```azurecli
    az login
    ```
2. Use [az vm identity assign](/en-us/cli/azure/vm/identity) with the `identity assign` command enable the system-assigned identity to an existing VM:

    ```azurecli
    az vm identity assign -g myResourceGroup -n myVm
    ```

### Disable system-assigned identity from an Azure VM

To disable system-assigned managed identity on a VM, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) role assignment. No other Microsoft Entra directory role assignments are required.

If you have a Virtual Machine that no longer needs the system-assigned identity, but still needs user-assigned identities, use the following command:

```azurecli
az vm update -n myVM -g myResourceGroup --set identity.type='UserAssigned'
```

If you have a virtual machine that no longer needs system-assigned identity and it has no user-assigned identities, use the following command:

Note

The value `none` is case sensitive. It must be lowercase.

```azurecli
az vm update -n myVM -g myResourceGroup --set identity.type="none"
```

## User-assigned managed identity

In this section, you will learn how to add and remove a user-assigned managed identity from an Azure VM using Azure CLI. If you create your user-assigned managed identity in a different RG than your VM. You'll have to use the URL of your managed identity to assign it to your VM. For example:

`--identities "/subscriptions/<SUBID>/resourcegroups/<RESOURCEGROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER_ASSIGNED_ID_NAME>"`

### Assign a user-assigned managed identity during the creation of an Azure VM

To assign a user-assigned identity to a VM during its creation, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) and [Managed Identity Operator](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-operator) role assignments. No other Microsoft Entra directory role assignments are required.

1. You can skip this step if you already have a resource group you would like to use. Create a [resource group](/en-us/azure/azure-resource-manager/management/overview#terminology) for containment and deployment of your user-assigned managed identity, using [az group create](/en-us/cli/azure/group#az-group-create). Be sure to replace the `<RESOURCE GROUP>` and `<LOCATION>` parameter values with your own values. :

    ```azurecli
    az group create --name <RESOURCE GROUP> --location <LOCATION>
    ```
2. Create a user-assigned managed identity using [az identity create](/en-us/cli/azure/identity#az-identity-create). The `-g` parameter specifies the resource group where the user-assigned managed identity is created, and the `-n` parameter specifies its name.

    Important

    When you create user-assigned managed identities, the name must start with a letter or number, and may include a combination of alphanumeric characters, hyphens (-) and underscores (\_). For the assignment to a virtual machine or virtual machine scale set to work properly, the name is limited to 24 characters. For more information, see [FAQs and known issues](known-issues).

    ```azurecli
    az identity create -g myResourceGroup -n myUserAssignedIdentity
    ```

    The response contains details for the user-assigned managed identity created, similar to the following. The resource ID value assigned to the user-assigned managed identity is used in the following step.

    ```json
    {
        "clientId": "00001111-aaaa-2222-bbbb-3333cccc4444",
        "clientSecretUrl": "https://control-westcentralus.identity.azure.net/subscriptions/<SUBSCRIPTON ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<myUserAssignedIdentity>/credentials?tid=5678&oid=9012&aid=aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb",
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
3. Create a VM using [az vm create](/en-us/cli/azure/vm#az-vm-create). The following example creates a VM associated with the new user-assigned identity, as specified by the `--assign-identity` parameter, with the specified `--role` and `--scope`. Be sure to replace the `<RESOURCE GROUP>`, `<VM NAME>`, `<USER NAME>`, `<PASSWORD>`, `<USER ASSIGNED IDENTITY NAME>`, `<ROLE>`, and `<SUBSCRIPTION>` parameter values with your own values.

    ```azurecli
    az vm create --resource-group <RESOURCE GROUP> --name <VM NAME> --image <SKU linux image>  --admin-username <USER NAME> --admin-password <PASSWORD> --assign-identity <USER ASSIGNED IDENTITY NAME> --role <ROLE> --scope <SUBSCRIPTION>
    ```

### Assign a user-assigned managed identity to an existing Azure VM

To assign a user-assigned identity to a VM, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) and [Managed Identity Operator](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-operator) role assignments. No other Microsoft Entra directory role assignments are required.

1. Create a user-assigned identity using [az identity create](/en-us/cli/azure/identity#az-identity-create). The `-g` parameter specifies the resource group where the user-assigned identity is created, and the `-n` parameter specifies its name. Be sure to replace the `<RESOURCE GROUP>` and `<USER ASSIGNED IDENTITY NAME>` parameter values with your own values:

    Important

    Creating user-assigned managed identities with special characters (that is, underscore) in the name is not currently supported. Please use alphanumeric characters. Check back for updates. For more information, see [FAQs and known issues](known-issues)

    ```azurecli
    az identity create -g <RESOURCE GROUP> -n <USER ASSIGNED IDENTITY NAME>
    ```

    The response contains details for the user-assigned managed identity created, similar to the following.

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
2. Assign the user-assigned identity to your VM using [az vm identity assign](/en-us/cli/azure/vm). Be sure to replace the `<RESOURCE GROUP>` and `<VM NAME>` parameter values with your own values. The `<USER ASSIGNED IDENTITY NAME>` is the user-assigned managed identity's resource `name` property, as created in the previous step. If you created your user-assigned managed identity in a different RG than your VM. You'll have to use the URL of your managed identity.

    ```azurecli
    az vm identity assign -g <RESOURCE GROUP> -n <VM NAME> --identities <USER ASSIGNED IDENTITY>
    ```

### Remove a user-assigned managed identity from an Azure VM

To remove a user-assigned identity to a VM, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) role assignment.

If this is the only user-assigned managed identity assigned to the virtual machine, `UserAssigned` will be removed from the identity type value. Be sure to replace the `<RESOURCE GROUP>` and `<VM NAME>` parameter values with your own values. The `<USER ASSIGNED IDENTITY>` will be the user-assigned identity's `name` property, which can be found in the identity section of the virtual machine using `az vm identity show`:

```azurecli
az vm identity remove -g <RESOURCE GROUP> -n <VM NAME> --identities <USER ASSIGNED IDENTITY>
```

If your VM does not have a system-assigned managed identity and you want to remove all user-assigned identities from it, use the following command:

Note

The value `none` is case sensitive. It must be lowercase.

```azurecli
az vm update -n myVM -g myResourceGroup --set identity.type="none" identity.userAssignedIdentities=null
```

If your VM has both system-assigned and user-assigned identities, you can remove all the user-assigned identities by switching to use only system-assigned. Use the following command:

```azurecli
az vm update -n myVM -g myResourceGroup --set identity.type='SystemAssigned' identity.userAssignedIdentities=null
```

::: zone-end

::: zone pivot="qs-configure-powershell-windows-vm"

In this article, using PowerShell, you learn how to perform the following managed identities for Azure resources operations on an Azure VM.

Note

We recommend that you use the Azure Az PowerShell module to interact with Azure. See [Install Azure PowerShell](/en-us/powershell/azure/install-azure-powershell) to get started. To learn how to migrate to the Az PowerShell module, see [Migrate Azure PowerShell from AzureRM to Az](/en-us/powershell/azure/migrate-from-azurerm-to-az).

## Prerequisites

- If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview). **Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview#managed-identity-types)**.
- If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before continuing.
- To run the example scripts, you have two options:
    - Use the [Azure Cloud Shell](/en-us/azure/cloud-shell/overview), which you can open using the **Try It** button on the top-right corner of code blocks.
    - Run scripts locally by installing the latest version of [Azure PowerShell](/en-us/powershell/azure/install-azure-powershell), then sign in to Azure using `Connect-AzAccount`.

## System-assigned managed identity

In this section, we go over how to enable and disable the system-assigned managed identity using Azure PowerShell.

### Enable system-assigned managed identity during creation of an Azure VM

To create an Azure VM with the system-assigned managed identity enabled, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) role assignment. No other Microsoft Entra directory role assignments are required.

1. Refer to one of the following Azure VM Quickstarts, completing only the necessary sections ("Sign in to Azure", "Create resource group", "Create networking group", "Create the VM").

    When you get to the "Create the VM" section, make a slight modification to the [New-AzVMConfig](/en-us/powershell/module/az.compute/new-azvm) cmdlet syntax. Be sure to add a `-IdentityType SystemAssigned` parameter to provision the VM with the system-assigned identity enabled, for example:

    ```azurepowershell
    $vmConfig = New-AzVMConfig -VMName myVM -IdentityType SystemAssigned ...
    ```

    - [Create a Windows virtual machine using PowerShell](/en-us/azure/virtual-machines/windows/quick-create-powershell)
    - [Create a Linux virtual machine using PowerShell](/en-us/azure/virtual-machines/linux/quick-create-powershell)

### Enable system-assigned managed identity on an existing Azure VM

To enable system-assigned managed identity on a VM that was originally provisioned without it, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) role assignment. No other Microsoft Entra directory role assignments are required.

1. Retrieve the VM properties using the `Get-AzVM` cmdlet. Then to enable a system-assigned managed identity, use the `-IdentityType` switch on the [Update-AzVM](/en-us/powershell/module/az.compute/update-azvm) cmdlet:

    ```azurepowershell
    $vm = Get-AzVM -ResourceGroupName myResourceGroup -Name myVM
    Update-AzVM -ResourceGroupName myResourceGroup -VM $vm -IdentityType SystemAssigned
    ```

### Add VM system assigned identity to a group

After you have enabled system assigned identity on a VM, you can add it to a group. The following procedure adds a VM's system assigned identity to a group.

1. Retrieve and note the `ObjectID` (as specified in the `Id` field of the returned values) of the VM's service principal:

    ```azurepowershell
    Get-AzADServicePrincipal -displayname "myVM"
    ```
2. Retrieve and note the `ObjectID` (as specified in the `Id` field of the returned values) of the group:

    ```azurepowershell
    Get-AzADGroup -searchstring "myGroup"
    ```
3. Add the VM's service principal to the group:

    ```azurepowershell
    New-MgGroupMember -GroupId "<Id of group>" -DirectoryObjectId "<Id of VM service principal>" 
    ```

## Disable system-assigned managed identity from an Azure VM

To disable system-assigned managed identity on a VM, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) role assignment. No other Microsoft Entra directory role assignments are required.

If you have a Virtual Machine that no longer needs the system-assigned managed identity but still needs user-assigned managed identities, use the following cmdlet:

1. Retrieve the VM properties using the `Get-AzVM` cmdlet and set the `-IdentityType` parameter to `UserAssigned`:

    ```azurepowershell
    $vm = Get-AzVM -ResourceGroupName myResourceGroup -Name myVM
    Update-AzVm -ResourceGroupName myResourceGroup -VM $vm -IdentityType "UserAssigned" -IdentityID "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER ASSIGNED IDENTITY NAME>..."
    ```

If you have a virtual machine that no longer needs system-assigned managed identity and it has no user-assigned managed identities, use the following commands:

```azurepowershell
$vm = Get-AzVM -ResourceGroupName myResourceGroup -Name myVM
Update-AzVm -ResourceGroupName myResourceGroup -VM $vm -IdentityType None
```

## User-assigned managed identity

In this section, you learn how to add and remove a user-assigned managed identity from a VM using Azure PowerShell.

### Assign a user-assigned managed identity to a VM during creation

To assign a user-assigned identity to a VM, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) and [Managed Identity Operator](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-operator) role assignments. No other Microsoft Entra directory role assignments are required.

1. Refer to one of the following Azure VM Quickstarts, completing only the necessary sections ("Sign in to Azure", "Create resource group", "Create networking group", "Create the VM").

    When you get to the "Create the VM" section, make a slight modification to the [`New-AzVMConfig`](/en-us/powershell/module/az.compute/new-azvm) cmdlet syntax. Add the `-IdentityType UserAssigned` and `-IdentityID` parameters to provision the VM with a user-assigned identity. Replace `<VM NAME>`,`<SUBSCRIPTION ID>`, `<RESOURCE GROUP>`, and `<USER ASSIGNED IDENTITY NAME>` with your own values. For example:

    ```azurepowershell
    $vmConfig = New-AzVMConfig -VMName <VM NAME> -IdentityType UserAssigned -IdentityID "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER ASSIGNED IDENTITY NAME>..."
    ```

    - [Create a Windows virtual machine using PowerShell](/en-us/azure/virtual-machines/windows/quick-create-powershell)
    - [Create a Linux virtual machine using PowerShell](/en-us/azure/virtual-machines/linux/quick-create-powershell)

### Assign a user-assigned managed identity to an existing Azure VM

To assign a user-assigned identity to a VM, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) and [Managed Identity Operator](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-operator) role assignments. No other Microsoft Entra directory role assignments are required.

1. Create a user-assigned managed identity using the [New-AzUserAssignedIdentity](/en-us/powershell/module/az.managedserviceidentity/new-azuserassignedidentity) cmdlet. Note the `Id` in the output because you'll need this information in the next step.

    Important

    Creating user-assigned managed identities only supports alphanumeric, underscore and hyphen (0-9 or a-z or A-Z, \_ or -) characters. Additionally, name should be limited from 3 to 128 character length for the assignment to VM/VMSS to work properly. For more information, see [FAQs and known issues](known-issues)

    ```azurepowershell
    New-AzUserAssignedIdentity -ResourceGroupName <RESOURCEGROUP> -Name <USER ASSIGNED IDENTITY NAME>
    ```
2. Retrieve the VM properties using the `Get-AzVM` cmdlet. Then to assign a user-assigned managed identity to the Azure VM, use the `-IdentityType` and `-IdentityID` switch on the [Update-AzVM](/en-us/powershell/module/az.compute/update-azvm) cmdlet. The value for the`-IdentityId` parameter is the `Id` you noted in the previous step. Replace `<VM NAME>`, `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>`, and `<USER ASSIGNED IDENTITY NAME>` with your own values.

    Warning

    To retain any previously user-assigned managed identities assigned to the VM, query the `Identity` property of the VM object (for example, `$vm.Identity`). If any user assigned managed identities are returned, include them in the following command along with the new user assigned managed identity you would like to assign to the VM.

    ```azurepowershell
    $vm = Get-AzVM -ResourceGroupName <RESOURCE GROUP> -Name <VM NAME>
    
    # Get the list of existing identity IDs and then append to it
    $identityIds = $vm.Identity.UserAssignedIdentities.Keys
    $uid = "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER ASSIGNED IDENTITY NAME>"
    $identityIds = $identityIds + $uid 
    
    # Update the VM with added identity IDs
    Update-AzVM -ResourceGroupName <RESOURCE GROUP> -VM $vm -IdentityType UserAssigned -IdentityID $uid 
    ```

### Remove a user-assigned managed identity from an Azure VM

To remove a user-assigned identity to a VM, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) role assignment.

If your VM has multiple user-assigned managed identities, you can remove all but the last one using the following commands. Be sure to replace the `<RESOURCE GROUP>` and `<VM NAME>` parameter values with your own values. The `<USER ASSIGNED IDENTITY NAME>` is the user-assigned managed identity's name property, which should remain on the VM. This information is discoverable using a query to search for the `Identity` property of the VM object. For example, `$vm.Identity`:

```azurepowershell
$vm = Get-AzVm -ResourceGroupName myResourceGroup -Name myVm
Update-AzVm -ResourceGroupName myResourceGroup -VirtualMachine $vm -IdentityType UserAssigned -IdentityID <USER ASSIGNED IDENTITY NAME>
```

If your VM doesn't have a system-assigned managed identity and you want to remove all user-assigned managed identities from it, use the following command:

```azurepowershell
$vm = Get-AzVm -ResourceGroupName myResourceGroup -Name myVm
Update-AzVm -ResourceGroupName myResourceGroup -VM $vm -IdentityType None
```

If your VM has both system-assigned and user-assigned managed identities, you can remove all the user-assigned managed identities by switching to use only system-assigned managed identities.

```azurepowershell
$vm = Get-AzVm -ResourceGroupName myResourceGroup -Name myVm
Update-AzVm -ResourceGroupName myResourceGroup -VirtualMachine $vm -IdentityType "SystemAssigned"
```

::: zone-end

::: zone pivot="qs-configure-template-windows-vm"

In this article, using the Azure Resource Manager deployment template, you learn how to perform the following managed identities for Azure resources operations on an Azure VM:

## Prerequisites

- If you're unfamiliar with using Azure Resource Manager deployment template, check out the [overview section](overview). **Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview#managed-identity-types)**.
- If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before continuing.

## Azure Resource Manager templates

As with the Azure portal and scripting, [Azure Resource Manager](/en-us/azure/azure-resource-manager/management/overview) templates allow you to deploy new or modified resources defined by an Azure resource group. Several options are available for template editing and deployment, both local and portal-based, including:

- Using a [custom template from the Azure Marketplace](/en-us/azure/azure-resource-manager/templates/deploy-portal#deploy-resources-from-custom-template), which allows you to create a template from scratch, or base it on an existing common or [quickstart template](https://azure.microsoft.com/resources/templates/).
- Deriving from an existing resource group, by exporting a template from either [the original deployment](/en-us/azure/azure-resource-manager/templates/export-template-portal), or from the [current state of the deployment](/en-us/azure/azure-resource-manager/templates/export-template-portal).
- Using a local [JSON editor (such as VS Code)](/en-us/azure/azure-resource-manager/templates/quickstart-create-templates-use-the-portal), and then uploading and deploying by using PowerShell or CLI.
- Using the Visual Studio [Azure Resource Group project](/en-us/azure/azure-resource-manager/templates/create-visual-studio-deployment-project) to both create and deploy a template.

Regardless of the option you choose, template syntax is the same during initial deployment and redeployment. Enabling a system or user-assigned managed identity on a new or existing VM is done in the same manner. Also, by default, Azure Resource Manager does an [incremental update](/en-us/azure/azure-resource-manager/templates/deployment-modes) to deployments.

## System-assigned managed identity

In this section, you will enable and disable a system-assigned managed identity using an Azure Resource Manager template.

### Enable system-assigned managed identity during creation of an Azure VM or on an existing VM

To enable system-assigned managed identity on a VM, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) role assignment. No other Microsoft Entra directory role assignments are required.

1. Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the VM.
2. To enable system-assigned managed identity, load the template into an editor, locate the `Microsoft.Compute/virtualMachines` resource of interest within the `resources` section and add the `"identity"` property at the same level as the `"type": "Microsoft.Compute/virtualMachines"` property. Use the following syntax:

    ```json
    "identity": {
        "type": "SystemAssigned"
    },
    ```
3. When you're done, the following sections should be added to the `resource` section of your template and it should resemble the following:

    ```json
     "resources": [
         {
             //other resource provider properties...
             "apiVersion": "2018-06-01",
             "type": "Microsoft.Compute/virtualMachines",
             "name": "[variables('vmName')]",
             "location": "[resourceGroup().location]",
             "identity": {
                 "type": "SystemAssigned",
                 }                        
         }
     ]
    ```

### Assign a role the VM's system-assigned managed identity

After you enable a system-assigned managed identity on your VM, you may want to grant it a role such as **Reader** access to the resource group in which it was created. You can find detailed information to help you with this step in the [Assign Azure roles using Azure Resource Manager templates](/en-us/azure/role-based-access-control/role-assignments-template) article.

### Disable a system-assigned managed identity from an Azure VM

To remove system-assigned managed identity from a VM, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) role assignment. No other Microsoft Entra directory role assignments are required.

1. Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the VM.
2. Load the template into an editor and locate the `Microsoft.Compute/virtualMachines` resource of interest within the `resources` section. If you have a VM that only has system-assigned managed identity, you can disable it by changing the identity type to `None`.

    **Microsoft.Compute/virtualMachines API version 2018-06-01**

    If your VM has both system and user-assigned managed identities, remove `SystemAssigned` from the identity type and keep `UserAssigned` along with the `userAssignedIdentities` dictionary values.

    **Microsoft.Compute/virtualMachines API version 2018-06-01**

    If your `apiVersion` is `2017-12-01` and your VM has both system and user-assigned managed identities, remove `SystemAssigned` from the identity type and keep `UserAssigned` along with the `identityIds` array of the user-assigned managed identities.

The following example shows you how to remove a system-assigned managed identity from a VM with no user-assigned managed identities:

```json
{
    "apiVersion": "2018-06-01",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[parameters('vmName')]",
    "location": "[resourceGroup().location]",
    "identity": {
        "type": "None"
    }
}
```

## User-assigned managed identity

In this section, you assign a user-assigned managed identity to an Azure VM using Azure Resource Manager template.

Note

To create a user-assigned managed identity using an Azure Resource Manager Template, see [Create a user-assigned managed identity](how-manage-user-assigned-managed-identities?pivots=identity-mi-methods-arm#create-a-user-assigned-managed-identity).

### Assign a user-assigned managed identity to an Azure VM

To assign a user-assigned identity to a VM, your account needs the [Managed Identity Operator](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-operator) role assignment. No other Microsoft Entra directory role assignments are required.

1. Under the `resources` element, add the following entry to assign a user-assigned managed identity to your VM. Be sure to replace `<USERASSIGNEDIDENTITY>` with the name of the user-assigned managed identity you created.

    **Microsoft.Compute/virtualMachines API version 2018-06-01**

    If your `apiVersion` is `2018-06-01`, your user-assigned managed identities are stored in the `userAssignedIdentities` dictionary format and the `<USERASSIGNEDIDENTITYNAME>` value must be stored in a variable defined in the `variables` section of your template.

    ```json
     {
         "apiVersion": "2018-06-01",
         "type": "Microsoft.Compute/virtualMachines",
         "name": "[variables('vmName')]",
         "location": "[resourceGroup().location]",
         "identity": {
             "type": "userAssigned",
             "userAssignedIdentities": {
                 "[resourceID('Microsoft.ManagedIdentity/userAssignedIdentities/',variables('<USERASSIGNEDIDENTITYNAME>'))]": {}
             }
         }
     }
    ```

    **Microsoft.Compute/virtualMachines API version 2017-12-01**

    If your `apiVersion` is `2017-12-01`, your user-assigned managed identities are stored in the `identityIds` array and the `<USERASSIGNEDIDENTITYNAME>` value must be stored in a variable defined in the `variables` section of your template.

    ```json
    {
        "apiVersion": "2017-12-01",
        "type": "Microsoft.Compute/virtualMachines",
        "name": "[variables('vmName')]",
        "location": "[resourceGroup().location]",
        "identity": {
            "type": "userAssigned",
            "identityIds": [
                "[resourceID('Microsoft.ManagedIdentity/userAssignedIdentities/',variables('<USERASSIGNEDIDENTITYNAME>'))]"
            ]
        }
    }
    ```
2. When you're done, the following sections should be added to the `resource` section of your template and it should resemble the following:

    **Microsoft.Compute/virtualMachines API version 2018-06-01**

    ```json
      "resources": [
         {
             //other resource provider properties...
             "apiVersion": "2018-06-01",
             "type": "Microsoft.Compute/virtualMachines",
             "name": "[variables('vmName')]",
             "location": "[resourceGroup().location]",
             "identity": {
                 "type": "userAssigned",
                 "userAssignedIdentities": {
                    "[resourceID('Microsoft.ManagedIdentity/userAssignedIdentities/',variables('<USERASSIGNEDIDENTITYNAME>'))]": {}
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
             "type": "Microsoft.Compute/virtualMachines",
             "name": "[variables('vmName')]",
             "location": "[resourceGroup().location]",
             "identity": {
                 "type": "userAssigned",
                 "identityIds": [
                    "[resourceID('Microsoft.ManagedIdentity/userAssignedIdentities/',variables('<USERASSIGNEDIDENTITYNAME>'))]"
                 ]
             }
         }
    ]
    ```

### Remove a user-assigned managed identity from an Azure VM

To remove a user-assigned identity from a VM, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) role assignment. No other Microsoft Entra directory role assignments are required.

1. Whether you sign in to Azure locally or via the Azure portal, use an account that is associated with the Azure subscription that contains the VM.
2. Load the template into an editor and locate the `Microsoft.Compute/virtualMachines` resource of interest within the `resources` section. If you have a VM that only has user-assigned managed identity, you can disable it by changing the identity type to `None`.

    The following example shows you how to remove all user-assigned managed identities from a VM with no system-assigned managed identities:

    ```json
     {
       "apiVersion": "2018-06-01",
       "type": "Microsoft.Compute/virtualMachines",
       "name": "[parameters('vmName')]",
       "location": "[resourceGroup().location]",
       "identity": {
           "type": "None"
           },
     }
    ```

    **Microsoft.Compute/virtualMachines API version 2018-06-01**

    To remove a single user-assigned managed identity from a VM, remove it from the `userAssignedIdentities` dictionary.

    If you have a system-assigned managed identity, keep it in the `type` value under the `identity` value.

    **Microsoft.Compute/virtualMachines API version 2017-12-01**

    To remove a single user-assigned managed identity from a VM, remove it from the `identityIds` array.

    If you have a system-assigned managed identity, keep it in the `type` value under the `identity` value.

::: zone-end

::: zone pivot="qs-configure-rest-vm"

In this article, using CURL to make calls to the Azure Resource Manager REST endpoint, you learn how to perform the following managed identities for Azure resources operations on an Azure VM:

- Enable and disable the system-assigned managed identity on an Azure VM
- Add and remove a user-assigned managed identity on an Azure VM

If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before continuing.

## Prerequisites

- If you're unfamiliar with managed identities for Azure resources, see [What are managed identities for Azure resources?](overview). To learn about system-assigned and user-assigned managed identity types, see [Managed identity types](overview).

- Use the Bash environment in [Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see [Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).

    [![](../../reusable-content/azure-cli/media/hdi-launch-cloud-shell.png)](https://shell.azure.com)
- If you prefer to run CLI reference commands locally, [install](/en-us/cli/azure/install-azure-cli) the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see [How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).

    - If you're using a local installation, sign in to the Azure CLI by using the [az login](/en-us/cli/azure/reference-index#az-login) command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see [Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).
    - When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see [Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).
    - Run [az version](/en-us/cli/azure/reference-index?#az-version) to find the version and dependent libraries that are installed. To upgrade to the latest version, run [az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).

## System-assigned managed identity

In this section, you learn how to enable and disable system-assigned managed identity on an Azure VM using CURL to make calls to the Azure Resource Manager REST endpoint.

### Enable system-assigned managed identity during creation of an Azure VM

To create an Azure VM with the system-assigned managed identity enabled, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) role assignment. No other Microsoft Entra directory role assignments are required.

1. Create a [resource group](/en-us/azure/azure-resource-manager/management/overview#terminology) for containment and deployment of your VM and its related resources, using [az group create](/en-us/cli/azure/group/#az-group-create). You can skip this step if you already have resource group you would like to use instead:

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```
2. Create a [network interface](/en-us/cli/azure/network/nic#az-network-nic-create) for your VM:

    ```azurecli
     az network nic create -g myResourceGroup --vnet-name myVnet --subnet mySubnet -n myNic
    ```
3. Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your VM with a system-assigned managed identity.

    ```azurecli
    az account get-access-token
    ```
4. Using Azure Cloud Shell, create a VM using CURL to call the Azure Resource Manager REST endpoint. The following example creates a VM named *myVM* with a system-assigned managed identity, as identified in the request body by the value `"identity":{"type":"SystemAssigned"}`. Replace `<ACCESS TOKEN>` with the value you received in the previous step when you requested a Bearer access token and the `<SUBSCRIPTION ID>` value as appropriate for your environment.

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2018-06-01' -X PUT -d '{"location":"westus","name":"myVM","identity":{"type":"SystemAssigned"},"properties":{"hardwareProfile":{"vmSize":"Standard_D2_v2"},"storageProfile":{"imageReference":{"sku":"2016-Datacenter","publisher":"MicrosoftWindowsServer","version":"latest","offer":"WindowsServer"},"osDisk":{"caching":"ReadWrite","managedDisk":{"storageAccountType":"StandardSSD_LRS"},"name":"myVM3osdisk","createOption":"FromImage"},"dataDisks":[{"diskSizeGB":1023,"createOption":"Empty","lun":0},{"diskSizeGB":1023,"createOption":"Empty","lun":1}]},"osProfile":{"adminUsername":"azureuser","computerName":"myVM","adminPassword":"<SECURE PASSWORD STRING>"},"networkProfile":{"networkInterfaces":[{"id":"/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic","properties":{"primary":true}}]}}}' -H "Content-Type: application/json" -H "Authorization: Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PUT https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2018-06-01 HTTP/1.1
    ```

    **Request headers**

    | Request header | Description |
    | --- | --- |
    | *Content-Type* | Required. Set to `application/json`. |
    | *Authorization* | Required. Set to a valid `Bearer` access token. |

    **Request body**

    ```JSON
      {
        "location":"westus",
        "name":"myVM",
        "identity":{
           "type":"SystemAssigned"
        },
        "properties":{
           "hardwareProfile":{
              "vmSize":"Standard_D2_v2"
           },
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
                 "name":"myVM3osdisk",
                 "createOption":"FromImage"
              },
              "dataDisks":[
                 {
                    "diskSizeGB":1023,
                    "createOption":"Empty",
                    "lun":0
                 },
                 {
                    "diskSizeGB":1023,
                    "createOption":"Empty",
                    "lun":1
                 }
              ]
           },
           "osProfile":{
              "adminUsername":"azureuser",
              "computerName":"myVM",
              "adminPassword":"myPassword12"
           },
           "networkProfile":{
              "networkInterfaces":[
                 {
                    "id":"/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic",
                    "properties":{
                       "primary":true
                    }
                 }
              ]
           }
        }
     }  
    ```

### Enable system-assigned identity on an existing Azure VM

To enable system-assigned managed identity on a VM that was originally provisioned without it, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) role assignment. No other Microsoft Entra directory role assignments are required.

1. Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your VM with a system-assigned managed identity.

    ```azurecli
    az account get-access-token
    ```
2. Use the following CURL command to call the Azure Resource Manager REST endpoint to enable system-assigned managed identity on your VM as identified in the request body by the value `{"identity":{"type":"SystemAssigned"}` for a VM named *myVM*. Replace `<ACCESS TOKEN>` with the value you received in the previous step when you requested a Bearer access token and the `<SUBSCRIPTION ID>` value as appropriate for your environment.

    Important

    To ensure you don't delete any existing user-assigned managed identities that are assigned to the VM, you need to list the user-assigned managed identities by using this CURL command: `curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Compute/virtualMachines/<VM NAME>?api-version=2018-06-01' -H "Authorization: Bearer <ACCESS TOKEN>"`. If you have any user-assigned managed identities assigned to the VM as identified in the `identity` value in the response, skip to step 3 that shows you how to retain user-assigned managed identities while enabling system-assigned managed identity on your VM.

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"SystemAssigned"}}' -H "Content-Type: application/json" -H "Authorization:Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2018-06-01 HTTP/1.1
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
3. To enable system-assigned managed identity on a VM with existing user-assigned managed identities, you need to add `SystemAssigned` to the `type` value.

    For example, if your VM has the user-assigned managed identities `ID1` and `ID2` assigned to it, and you would like to add system-assigned managed identity to the VM, use the following CURL call. Replace `<ACCESS TOKEN>` and `<SUBSCRIPTION ID>` with values appropriate to your environment.

    API version `2018-06-01` stores user-assigned managed identities in the `userAssignedIdentities` value in a dictionary format as opposed to the `identityIds` value in an array format used in API version `2017-12-01`.

    **API VERSION 2018-06-01**

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"SystemAssigned, UserAssigned", "userAssignedIdentities":{"/subscriptions/<<SUBSCRIPTION ID>>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1":{},"/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID2":{}}}}' -H "Content-Type: application/json" -H "Authorization:Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2018-06-01 HTTP/1.1
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
              "/subscriptions/<<SUBSCRIPTION ID>>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1":{  
    
              },
              "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID2":{  
    
              }
           }
        }
     }
    ```

    **API VERSION 2017-12-01**

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2017-12-01' -X PATCH -d '{"identity":{"type":"SystemAssigned, UserAssigned", "identityIds":["/subscriptions/<<SUBSCRIPTION ID>>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1","/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID2"]}}' -H "Content-Type: application/json" -H "Authorization:Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2017-12-01 HTTP/1.1
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
              "/subscriptions/<<SUBSCRIPTION ID>>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1",
              "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID2"
           ]
        }
     }
    ```

### Disable system-assigned managed identity from an Azure VM

To disable system-assigned managed identity on a VM, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) role assignment. No other Microsoft Entra directory role assignments are required.

1. Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your VM with a system-assigned managed identity.

    ```azurecli
    az account get-access-token
    ```
2. Update the VM using CURL to call the Azure Resource Manager REST endpoint to disable system-assigned managed identity. The following example disables system-assigned managed identity as identified in the request body by the value `{"identity":{"type":"None"}}` from a VM named *myVM*. Replace `<ACCESS TOKEN>` with the value you received in the previous step when you requested a Bearer access token and the `<SUBSCRIPTION ID>` value as appropriate for your environment.

    Important

    To ensure you don't delete any existing user-assigned managed identities that are assigned to the VM, you need to list the user-assigned managed identities by using this CURL command: `curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Compute/virtualMachines/<VM NAME>?api-version=2018-06-01' -H "Authorization: Bearer <ACCESS TOKEN>"`. If you have any user-assigned managed identities assigned to the VM as identified in the `identity` value in the response, skip to step 3 that shows you how to retain user-assigned managed identities while disabling system-assigned managed identity on your VM.

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"None"}}' -H "Content-Type: application/json" -H "Authorization:Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2018-06-01 HTTP/1.1
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

    To remove system-assigned managed identity from a virtual machine that has user-assigned managed identities, remove `SystemAssigned` from the `{"identity":{"type:" "}}` value while keeping the `UserAssigned` value and the `userAssignedIdentities` dictionary values if you are using **API version 2018-06-01**. If you are using **API version 2017-12-01** or earlier, keep the `identityIds` array.

## User-assigned managed identity

In this section, you learn how to add and remove user-assigned managed identity on an Azure VM using CURL to make calls to the Azure Resource Manager REST endpoint.

### Assign a user-assigned managed identity during the creation of an Azure VM

To assign a user-assigned identity to a VM, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) and [Managed Identity Operator](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-operator) role assignments. No other Microsoft Entra directory role assignments are required.

1. Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your VM with a system-assigned managed identity.

    ```azurecli
    az account get-access-token
    ```
2. Create a [network interface](/en-us/cli/azure/network/nic#az-network-nic-create) for your VM:

    ```azurecli
     az network nic create -g myResourceGroup --vnet-name myVnet --subnet mySubnet -n myNic
    ```
3. Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your VM with a system-assigned managed identity.

    ```azurecli
    az account get-access-token
    ```
4. Create a user-assigned managed identity using the instructions found here: [Create a user-assigned managed identity](how-manage-user-assigned-managed-identities?pivots=identity-mi-methods-rest#create-a-user-assigned-managed-identity).
5. Create a VM using CURL to call the Azure Resource Manager REST endpoint. The following example creates a VM named *myVM* in the resource group *myResourceGroup* with a user-assigned managed identity `ID1`, as identified in the request body by the value `"identity":{"type":"UserAssigned"}`. Replace `<ACCESS TOKEN>` with the value you received in the previous step when you requested a Bearer access token and the `<SUBSCRIPTION ID>` value as appropriate for your environment.

    **API VERSION 2018-06-01**

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2018-06-01' -X PUT -d '{"location":"westus","name":"myVM","identity":{"type":"UserAssigned","identityIds":["/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1"]},"properties":{"hardwareProfile":{"vmSize":"Standard_D2_v2"},"storageProfile":{"imageReference":{"sku":"2016-Datacenter","publisher":"MicrosoftWindowsServer","version":"latest","offer":"WindowsServer"},"osDisk":{"caching":"ReadWrite","managedDisk":{"storageAccountType":"StandardSSD_LRS"},"name":"myVM3osdisk","createOption":"FromImage"},"dataDisks":[{"diskSizeGB":1023,"createOption":"Empty","lun":0},{"diskSizeGB":1023,"createOption":"Empty","lun":1}]},"osProfile":{"adminUsername":"azureuser","computerName":"myVM","adminPassword":"myPassword12"},"networkProfile":{"networkInterfaces":[{"id":"/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic","properties":{"primary":true}}]}}}' -H "Content-Type: application/json" -H "Authorization: Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PUT https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2018-06-01 HTTP/1.1
    ```

    **Request headers**

    | Request header | Description |
    | --- | --- |
    | *Content-Type* | Required. Set to `application/json`. |
    | *Authorization* | Required. Set to a valid `Bearer` access token. |

    **Request body**

    ```JSON
     {  
        "location":"westus",
        "name":"myVM",
        "identity":{  
           "type":"UserAssigned",
           "identityIds":[  
              "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1"
           ]
        },
        "properties":{  
           "hardwareProfile":{  
              "vmSize":"Standard_D2_v2"
           },
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
                 "name":"myVM3osdisk",
                 "createOption":"FromImage"
              },
              "dataDisks":[  
                 {  
                    "diskSizeGB":1023,
                    "createOption":"Empty",
                    "lun":0
                 },
                 {  
                    "diskSizeGB":1023,
                    "createOption":"Empty",
                    "lun":1
                 }
              ]
           },
           "osProfile":{  
              "adminUsername":"azureuser",
              "computerName":"myVM",
              "adminPassword":"myPassword12"
           },
           "networkProfile":{  
              "networkInterfaces":[  
                 {  
                    "id":"/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic",
                    "properties":{  
                       "primary":true
                    }
                 }
              ]
           }
        }
     }
    
    ```

    **API VERSION 2017-12-01**

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2017-12-01' -X PUT -d '{"location":"westus","name":"myVM","identity":{"type":"UserAssigned","identityIds":["/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1"]},"properties":{"hardwareProfile":{"vmSize":"Standard_D2_v2"},"storageProfile":{"imageReference":{"sku":"2016-Datacenter","publisher":"MicrosoftWindowsServer","version":"latest","offer":"WindowsServer"},"osDisk":{"caching":"ReadWrite","managedDisk":{"storageAccountType":"StandardSSD_LRS"},"name":"myVM3osdisk","createOption":"FromImage"},"dataDisks":[{"diskSizeGB":1023,"createOption":"Empty","lun":0},{"diskSizeGB":1023,"createOption":"Empty","lun":1}]},"osProfile":{"adminUsername":"azureuser","computerName":"myVM","adminPassword":"myPassword12"},"networkProfile":{"networkInterfaces":[{"id":"/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic","properties":{"primary":true}}]}}}' -H "Content-Type: application/json" -H "Authorization: Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PUT https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2017-12-01 HTTP/1.1
    ```

    **Request headers**

    | Request header | Description |
    | --- | --- |
    | *Content-Type* | Required. Set to `application/json`. |
    | *Authorization* | Required. Set to a valid `Bearer` access token. |

    **Request body**

    ```JSON
     {
        "location":"westus",
        "name":"myVM",
        "identity":{
           "type":"UserAssigned",
           "identityIds":[
              "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1"
           ]
        },
        "properties":{
           "hardwareProfile":{
              "vmSize":"Standard_D2_v2"
           },
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
                 "name":"myVM3osdisk",
                 "createOption":"FromImage"
              },
              "dataDisks":[
                 {
                    "diskSizeGB":1023,
                    "createOption":"Empty",
                    "lun":0
                 },
                 {
                    "diskSizeGB":1023,
                    "createOption":"Empty",
                    "lun":1
                 }
              ]
           },
           "osProfile":{
              "adminUsername":"azureuser",
              "computerName":"myVM",
              "adminPassword":"myPassword12"
           },
           "networkProfile":{
              "networkInterfaces":[
                 {
                    "id":"/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic",
                    "properties":{
                       "primary":true
                    }
                 }
              ]
           }
        }
     }
    ```

### Assign a user-assigned managed identity to an existing Azure VM

To assign a user-assigned identity to a VM, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) and [Managed Identity Operator](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-operator) role assignments. No other Microsoft Entra directory role assignments are required.

1. Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your VM with a system-assigned managed identity.

    ```azurecli
    az account get-access-token
    ```
2. Create a user-assigned managed identity using the instructions found here, [Create a user-assigned managed identity](how-manage-user-assigned-managed-identities?pivots=identity-mi-methods-rest#create-a-user-assigned-managed-identity).
3. To ensure you don't delete existing user or system-assigned managed identities that are assigned to the VM, you need to list the identity types assigned to the VM by using the following CURL command. If you have managed identities assigned to the virtual machine scale set, they are listed under in the `identity` value.

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Compute/virtualMachines/<VM NAME>?api-version=2018-06-01' -H "Authorization: Bearer <ACCESS TOKEN>" 
    ```

    ```HTTP
    GET https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Compute/virtualMachines/<VM NAME>?api-version=2018-06-01 HTTP/1.1
    ```

    **Request headers**

    | Request header | Description |
    | --- | --- |
    | *Authorization* | Required. Set to a valid `Bearer` access token. |

    If you have any user or system-assigned managed identities assigned to the VM as identified in the `identity` value in the response, skip to step 5 that shows you how to retain the system-assigned managed identity while adding a user-assigned managed identity on your VM.
4. If you don't have any user-assigned managed identities assigned to your VM, use the following CURL command to call the Azure Resource Manager REST endpoint to assign the first user-assigned managed identity to the VM.

    The following example assigns a user-assigned managed identity, `ID1` to a VM named *myVM* in the resource group *myResourceGroup*. Replace `<ACCESS TOKEN>` with the value you received in the previous step when you requested a Bearer access token and the `<SUBSCRIPTION ID>` value as appropriate for your environment.

    **API VERSION 2018-06-01**

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"UserAssigned", "userAssignedIdentities":{"/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1":{}}}}' -H "Content-Type: application/json" -H "Authorization:Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2018-06-01 HTTP/1.1
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
           "type":"UserAssigned",
           "userAssignedIdentities":{
              "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1":{
    
              }
           }
        }
     }
    ```

    **API VERSION 2017-12-01**

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2017-12-01' -X PATCH -d '{"identity":{"type":"userAssigned", "identityIds":["/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1"]}}' -H "Content-Type: application/json" -H "Authorization:Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2017-12-01 HTTP/1.1
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
5. If you have an existing user-assigned or system-assigned managed identity assigned to your VM:

    **API VERSION 2018-06-01**

    Add the user-assigned managed identity to the `userAssignedIdentities` dictionary value.

    For example, if you have system-assigned managed identity and the user-assigned managed identity `ID1` currently assigned to your VM and would like to add the user-assigned managed identity `ID2` to it:

    ```bash
    curl  'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"SystemAssigned, UserAssigned", "userAssignedIdentities":{"/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1":{},"/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID2":{}}}}' -H "Content-Type: application/json" -H "Authorization:Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2018-06-01 HTTP/1.1
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

    For example, if you have system-assigned managed identity and the user-assigned managed identity `ID1` currently assigned to your VM and would like to add the user-assigned managed identity `ID2` to it:

    ```bash
    curl  'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2017-12-01' -X PATCH -d '{"identity":{"type":"SystemAssigned,UserAssigned", "identityIds":["/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1","/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID2"]}}' -H "Content-Type: application/json" -H "Authorization:Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2017-12-01 HTTP/1.1
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

### Remove a user-assigned managed identity from an Azure VM

To remove a user-assigned identity to a VM, your account needs the [Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) role assignment.

1. Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your VM with a system-assigned managed identity.

    ```azurecli
    az account get-access-token
    ```
2. To ensure you don't delete any existing user-assigned managed identities that you would like to keep assigned to the VM or remove the system-assigned managed identity, you need to list the managed identities by using the following CURL command:

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Compute/virtualMachines/<VM NAME>?api-version=2018-06-01' -H "Authorization: Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    GET https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Compute/virtualMachines/<VM NAME>?api-version=2018-06-01 HTTP/1.1
    ```

    **Request headers**

    | Request header | Description |
    | --- | --- |
    | *Content-Type* | Required. Set to `application/json`. |
    | *Authorization* | Required. Set to a valid `Bearer` access token. |

    If you have managed identities assigned to the VM, they are listed in the response in the `identity` value.

    For example, if you have user-assigned managed identities `ID1` and `ID2` assigned to your VM, and you only want to keep `ID1` assigned and retain the system-assigned identity:

    **API VERSION 2018-06-01**

    Add `null` to the user-assigned managed identity you would like to remove:

    ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"SystemAssigned, UserAssigned", "userAssignedIdentities":{"/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID2":null}}}' -H "Content-Type: application/json" -H "Authorization:Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2018-06-01 HTTP/1.1
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
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2017-12-01' -X PATCH -d '{"identity":{"type":"SystemAssigned, UserAssigned", "identityIds":["/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1"]}}' -H "Content-Type: application/json" -H "Authorization:Bearer <ACCESS TOKEN>"
    ```

    ```HTTP
    PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2017-12-01 HTTP/1.1
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
              "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1"
           ]
        }
     }
    ```

If your VM has both system-assigned and user-assigned managed identities, you can remove all the user-assigned managed identities by switching to use only system-assigned managed identity using the following command:

```bash
curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"SystemAssigned"}}' -H "Content-Type: application/json" -H "Authorization:Bearer <ACCESS TOKEN>"
```

```HTTP
PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2018-06-01 HTTP/1.1
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

If your VM has only user-assigned managed identities and you would like to remove them all, use the following command:

```bash
curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"None"}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
```

```HTTP
PATCH https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM?api-version=2018-06-01 HTTP/1.1
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

::: zone pivot="qs-configure-sdk-windows-vm"

In this article, you learn how to enable and remove managed identities for Azure resources for an Azure VM, using an Azure SDK.

## Prerequisites

- If you're not familiar with the managed identities for Azure resources feature, see this [overview](overview). If you don't have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you continue.

## Azure SDKs with managed identities for Azure resources support

Azure supports multiple programming platforms through a series of [Azure SDKs](https://azure.microsoft.com/downloads). Several of them have been updated to support managed identities for Azure resources, and provide corresponding samples to demonstrate usage. This list is updated as other support is added:

| SDK | Sample |
| --- | --- |
| .NET | [Manage resource from a VM enabled with managed identities for Azure resources enabled](https://github.com/Azure-Samples/aad-dotnet-manage-resources-from-vm-with-msi) |
| Java | [Manage storage from a VM enabled with managed identities for Azure resources](https://github.com/Azure-Samples/compute-java-manage-resources-from-vm-with-msi-in-aad-group) |
| Node.js | [Create a VM with system-assigned managed identity enabled](https://github.com/Azure-Samples/compute-node-msi-vm) |
| Python | [Create a VM with system-assigned managed identity enabled](https://github.com/Azure-Samples/compute-python-msi-vm) |
| Ruby | [Create Azure VM with a system-assigned identity enabled](https://github.com/Azure-Samples/compute-ruby-msi-vm/) |

::: zone-end
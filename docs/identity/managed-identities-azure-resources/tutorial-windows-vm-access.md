---
layout: Conceptual
title: 'Tutorial: Use a managed identity on a virtual machine (VM) to access Azure Resource Manager - Managed identities for Azure resources | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/tutorial-windows-vm-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: A tutorial that walks you through the process of using a system-assigned managed identity on a virtual machine (VM) to access Azure Resource Manager.
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.date: 2024-05-28T00:00:00.0000000Z
ms.custom: devx-track-arm-template, linux-related-content
zone_pivot_groups: identity-windows-vm-access
locale: en-us
document_id: d509aca7-fa4d-48ef-ddaf-319822730753
document_version_independent_id: d509aca7-fa4d-48ef-ddaf-319822730753
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/tutorial-windows-vm-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/tutorial-windows-vm-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/tutorial-windows-vm-access.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/4e834929-0ce1-4c1d-9c81-fcb14721edfb
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/2ed91286-6cf7-4b83-810d-75d0ee3b09dd
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/75670257-a3f0-4627-9981-8046f99219e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/6735bd7e-4f7b-457d-b58c-29e6f0198677
platformId: 087d5b00-472a-13fe-70ed-38233545b1ba
---

# Tutorial: Use a managed identity on a virtual machine (VM) to access Azure Resource Manager - Managed identities for Azure resources | Microsoft Learn

This quickstart shows you how to use a system-assigned managed identity as a virtual machine (VM)'s identity to access the Azure Resource Manager API. Managed identities for Azure resources are automatically managed by Azure and enable you to authenticate to services that support Microsoft Entra authentication without needing to insert credentials into your code.

You'll learn how to:

- Grant your virtual machine (VM) access to a resource group in Azure Resource Manager
- Get an access token using a virtual machine (VM) identity and use it to call Azure Resource Manager

::: zone pivot="windows-vm-access-wvm"

## Use a Windows VM system-assigned managed identity to access resource manager

This tutorial explains how to create a system-assigned identity, assign it to a Windows Virtual Machine (VM), and then use that identity to access the [Azure Resource Manager](/en-us/azure/azure-resource-manager/management/overview) API. Managed Service Identities are automatically managed by Azure. They enable authentication to services that support Microsoft Entra authentication, without needing to embed credentials into your code.

You'll learn how to:

- Grant your VM access to Azure Resource Manager.
- Get an access token by using the VM's system-assigned managed identity to access Resource Manager.

1. Sign in to the [Azure portal](https://portal.azure.com) with your administrator account.
2. Navigate to the **Resource Groups** tab.
3. Select the **Resource Group** that you want to grant the VM's managed identity access.
4. In the left panel, select **Access control (IAM)**.
5. Select **Add**, then select **Add role assignment**.
6. In the **Role** tab, select **Reader**. This role allows view all resources, but doesn't allow you to make any changes.
7. In the **Members** tab, for the **Assign access to** option, select **Managed identity**, then select **+ Select members**.
8. Ensure the proper subscription is listed in the **Subscription** dropdown. For **Resource Group**, select **All resource groups**.
9. For the **Manage identity** dropdown, select **Virtual Machine**.
10. For **Select**, choose your VM in the dropdown, then select **Save**.

    ![Screenshot that shows adding the reader role to the managed identity.](media/msi-tutorial-linux-vm-access-arm/msi-permission-linux.png)

## Get an access token

Use the VM's system-assigned managed identity and call the Resource Manager to get an access token.

To complete these steps, you need an SSH client. If you're using Windows, you can use the SSH client in the [Windows Subsystem for Linux](/en-us/windows/wsl/about). If you need assistance configuring your SSH client's keys, see [How to Use SSH keys with Windows on Azure](/en-us/azure/virtual-machines/linux/ssh-from-windows), or [How to create and use an SSH public and private key pair for Linux VMs in Azure](/en-us/azure/virtual-machines/linux/mac-create-ssh-keys).

1. In the portal, navigate to your Linux VM and in the **Overview**, select **Connect**.
2. **Connect** to the VM with the SSH client of your choice.
3. In the terminal window, using `curl`, make a request to the local managed identities for Azure resources endpoint to get an access token for Azure Resource Manager. The `curl` request for the access token is below.

```bash
curl 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com/' -H Metadata:true
```

Note

The value of the `resource` parameter must be an exact match for what is expected by Microsoft Entra ID. In the case of the Resource Manager's resource ID, you must include the trailing slash on the URI.

The response includes the access token you need to access Azure Resource Manager.

Response:

```json
{
  "access_token":"eyJ0eXAiOi...",
  "refresh_token":"",
  "expires_in":"3599",
  "expires_on":"1504130527",
  "not_before":"1504126627",
  "resource":"https://management.azure.com",
  "token_type":"Bearer"
}
```

Use this access token to access Azure Resource Manager; for example, to read the details of the resource group to which you previously granted this VM access. Replace the values of `<SUBSCRIPTION-ID>`, `<RESOURCE-GROUP>`, and `<ACCESS-TOKEN>` with the ones you created earlier.

Note

The URL is case-sensitive, so ensure if you are using the exact case as you used earlier when you named the resource group, and the uppercase “G” in “resourceGroup”.

```bash
curl https://management.azure.com/subscriptions/<SUBSCRIPTION-ID>/resourceGroups/<RESOURCE-GROUP>?api-version=2016-09-01 -H "Authorization: Bearer <ACCESS-TOKEN>" 
```

The response back with the specific resource group information: 

```json
{
"id":"/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/DevTest",
"name":"DevTest",
"location":"westus",
"properties":
{
  "provisioningState":"Succeeded"
  }
} 
```

::: zone-end

::: zone pivot="windows-vm-access-lvm"

## Use a Linux VM system-assigned managed identity to access a resource group in resource manager

This tutorial explains how to create a system-assigned identity, assign it to a Linux Virtual Machine (VM), and then use that identity to access the [Azure Resource Manager](/en-us/azure/azure-resource-manager/management/overview) API. Managed Service Identities are automatically managed by Azure. They enable authentication to services that support Microsoft Entra authentication, without needing to embed credentials into your code.

You learn how to:

- Grant your VM access to Azure resource manager.
- Get an access token by using the VM's system-assigned managed identity to access resource manager.

1. Sign in to the [Azure portal](https://portal.azure.com) with your administrator account.
2. Navigate to the **Resource Groups** tab.
3. Select the **Resource Group** that you want to grant the VM's managed identity access.
4. In the left panel, select **Access control (IAM)**.
5. Select **Add**, then select **Add role assignment**.
6. In the **Role** tab, select **Reader**. This role allows view all resources, but doesn't allow you to make any changes.
7. In the **Members** tab, in the **Assign access to** option, select **Managed identity**, then select **+ Select members**.
8. Ensure the proper subscription is listed in the **Subscription** dropdown. For **Resource Group**, select **All resource groups**.
9. In the **Manage identity** dropdown, select **Virtual Machine**.
10. In the **Select** option, choose your VM in the dropdown, then select **Save**.

    ![Screenshot that shows adding the reader role to the managed identity.](media/msi-tutorial-linux-vm-access-arm/msi-permission-linux.png)

## Get an access token

Use the VM's system-assigned managed identity and call the resource manager to get an access token.

To complete these steps, you need an SSH client. If you're using Windows, you can use the SSH client in the [Windows Subsystem for Linux](/en-us/windows/wsl/about). If you need assistance configuring your SSH client's keys, see [How to Use SSH keys with Windows on Azure](/en-us/azure/virtual-machines/linux/ssh-from-windows), or [How to create and use an SSH public and private key pair for Linux VMs in Azure](/en-us/azure/virtual-machines/linux/mac-create-ssh-keys).

1. In the Azure portal, navigate to your Linux VM.
2. In the **Overview**, select **Connect**.
3. **Connect** to the VM with the SSH client of your choice.
4. In the terminal window, using `curl`, make a request to the local managed identities for Azure resources endpoint to get an access token for Azure resource manager. The `curl` request for the access token is below.

```bash
curl 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com/' -H Metadata:true
```

Note

The value of the `resource` parameter must be an exact match for what is expected by Microsoft Entra ID. In the case of the resource manager resource ID, you must include the trailing slash on the URI.

The response includes the access token you need to access Azure resource manager.

Response:

```json
{
  "access_token":"eyJ0eXAiOi...",
  "refresh_token":"",
  "expires_in":"3599",
  "expires_on":"1504130527",
  "not_before":"1504126627",
  "resource":"https://management.azure.com",
  "token_type":"Bearer"
}
```

Use this access token to access Azure resource manager. For example, to read the details of the resource group to which you previously granted this VM access. Replace the values of `<SUBSCRIPTION-ID>`, `<RESOURCE-GROUP>`, and `<ACCESS-TOKEN>` with the ones you created earlier.

Note

The URL is case-sensitive, so ensure if you are using the exact case as you used earlier when you named the resource group, and the uppercase “G” in `resourceGroup`.

```bash
curl https://management.azure.com/subscriptions/<SUBSCRIPTION-ID>/resourceGroups/<RESOURCE-GROUP>?api-version=2016-09-01 -H "Authorization: Bearer <ACCESS-TOKEN>" 
```

The response back with the specific resource group information: 

```json
{
"id":"/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/DevTest",
"name":"DevTest",
"location":"westus",
"properties":
{
  "provisioningState":"Succeeded"
  }
} 
```

::: zone-end
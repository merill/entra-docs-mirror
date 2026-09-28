---
layout: Conceptual
title: Use managed identities on an Azure VM with Azure SDKs - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/how-to-use-vm-sdk
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Code samples for using Azure SDKs with an Azure VM that has managed identities for Azure resources.
ms.topic: how-to
ms.tgt_pltfrm: na
ms.date: 2023-05-23T00:00:00.0000000Z
locale: en-us
document_id: 51f0d828-e2e9-bd6c-7ebe-de699a39907d
document_version_independent_id: 55839ef8-6be6-54a6-9805-9f048dd9c4ab
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/how-to-use-vm-sdk.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/how-to-use-vm-sdk
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/how-to-use-vm-sdk.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/fd7d5d12-dbbc-4585-98a0-c6a0a5324f97
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/298ced0f-48c4-410b-86eb-c2214b75cbdd
platformId: 3ae7ad8a-1235-6bd7-0c2b-6f5299ccafa6
---

# Use managed identities on an Azure VM with Azure SDKs - Managed identities for Azure resources | Microsoft Learn

This article provides a list of SDK samples, which demonstrate use of their respective Azure SDK's support for managed identities for Azure resources.

## Prerequisites

- If you're not familiar with the managed identities for Azure resources feature, see this [overview](overview). If you don't have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you continue.

Important

- All sample code/script in this article assumes the client is running on a VM with managed identities for Azure resources enabled. Use the VM "Connect" feature in the Azure portal, to remotely connect to your VM. For details on enabling managed identities for Azure resources on a VM, see [Configure managed identities for Azure resources on a VM using the Azure portal](qs-configure-portal-windows-vm), or one of the variant articles (using PowerShell, CLI, a template, or an Azure SDK).

## SDK code samples

| SDK | Code sample |
| --- | --- |
| .NET | [Deploy an Azure Resource Manager template from a Windows VM using managed identities for Azure resources](https://github.com/Azure-Samples/windowsvm-msi-arm-dotnet) |
| .NET Core | [Call Azure services from a Linux VM using managed identities for Azure resources](https://github.com/Azure-Samples/linuxvm-msi-keyvault-arm-dotnet/) |
| Go | [Azure identity client module for Go](https://pkg.go.dev/github.com/Azure/azure-sdk-for-go/sdk/azidentity#ManagedIdentityCredential) |
| Node.js | [Manage resources using managed identities for Azure resources](https://github.com/Azure-Samples/resources-node-manage-resources-with-msi) |
| Python | [Use managed identities for Azure resources to authenticate simply from inside a VM](https://github.com/Azure/azure-sdk-for-python/tree/azure-identity_1.15.0/sdk/identity/azure-identity/) |
| Ruby | [Manage resources from a VM with managed identities for Azure resources enabled](https://github.com/Azure-Samples/resources-ruby-manage-resources-with-msi/) |
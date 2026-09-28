---
layout: Conceptual
title: Known issues with managed identities - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/known-issues
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Known issues with managed identities for Azure resources.
ms.assetid: 2097381a-a7ec-4e3b-b4ff-5d2fb17403b6
ms.topic: troubleshooting-known-issue
ms.date: 2022-01-11T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: 07551795-7de9-95d5-486c-579b8332e054
document_version_independent_id: 925ae422-7975-4ecb-eded-4c36a29a95a3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/known-issues.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
interactive_type: azurecli
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/known-issues
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/known-issues.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 0207afda-c816-f5cf-b711-3b9eec9b4213
---

# Known issues with managed identities - Managed identities for Azure resources | Microsoft Learn

This article discusses a couple of issues around managed identities and how to address them. Common questions about managed identities are documented in our [frequently asked questions](managed-identities-faq) article.

## VM fails to start after being moved

If you move a VM in a running state from a resource group or subscription, it continues to run during the move. However, after the move, if the VM is stopped and restarted, it fails to start. This issue happens because the VM doesn't update the managed identity reference and it continues to use an outdated URI.

**Workaround**

Trigger an update on the VM so it can get correct values for the managed identities for Azure resources. You can do a VM property change to update the reference to the managed identities for Azure resources identity. For example, you can set a new tag value on the VM with the following command:

```azurecli
az vm update -n <VM Name> -g <Resource Group> --set tags.fixVM=1
```

This command sets a new tag "fixVM" with a value of 1 on the VM.

By setting this property, the VM updates with the correct managed identities for Azure resources URI, and then you should be able to start the VM.

Once the VM is started, the tag can be removed by using following command:

```azurecli
az vm update -n <VM Name> -g <Resource Group> --remove tags.fixVM
```

## Transferring a subscription between Microsoft Entra directories

Managed identities don't get updated when a subscription is moved/transferred to another directory. As a result, any existent system-assigned or user-assigned managed identities will be broken.

Workaround for managed identities in a subscription that has been moved to another directory:

- For system assigned managed identities: disable and re-enable.
- For user assigned managed identities: delete, re-create, and attach them again to the necessary resources (for example, virtual machines)

For more information, see [Transfer an Azure subscription to a different Microsoft Entra directory](/en-us/azure/role-based-access-control/transfer-subscription).

## Error during managed identity assignment operations

In rare cases, you may see error messages indicating errors related to assignment of managed identities with Azure resources. Some of the example error messages are as follows:

- Azure resource ‘azure-resource-id' does not have access to identity 'managed-identity-id'.
- No managed service identities are associated with resource ‘azure-resource-id'

**Workaround** In these rare cases the best next steps are

1. For identities no longer needed to be assigned to the resource, remove them from the resource.
2. For User Assigned Managed Identity, reassign the identity to the Azure resource.
3. For System Assigned Managed Identity, disable the identity and enable it again.

Note

To assign/unassign Managed identities please follow below links

- [Documentation for VM](qs-configure-portal-windows-vm)
- [Documentation for VMSS](qs-configure-portal-windows-vmss)
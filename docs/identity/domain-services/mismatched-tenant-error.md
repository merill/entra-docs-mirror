---
layout: Conceptual
title: Fix mismatched directory errors in Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/mismatched-tenant-error
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn what a mismatched directory error means and how to resolve it in Microsoft Entra Domain Services
ms.assetid: 40eb75b7-827e-4d30-af6c-ca3c2af915c7
ms.topic: troubleshooting
ms.date: 2025-02-05T00:00:00.0000000Z
locale: en-us
document_id: 2be1b13d-640b-6260-70d3-cab4a1d1eef8
document_version_independent_id: 5f9a2f74-0c34-e809-c63a-f38d3052c4d0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/mismatched-tenant-error.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/mismatched-tenant-error
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/mismatched-tenant-error.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/20ed8455-bc18-4537-87a4-83784e7b2a39
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/9a7f703b-30bb-4d62-9eb4-97213f571849
platformId: aa2f808c-706a-8b7b-2c05-944a77b544e0
---

# Fix mismatched directory errors in Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

If a Microsoft Entra Domain Services managed domain shows a mismatched tenant error, you can't administer the managed domain until resolved. This error occurs if the underlying Azure virtual network is moved to a different Microsoft Entra directory.

This article explains why the error occurs and how to resolve it.

## What causes this error?

A mismatched directory error happens when a Domain Services managed domain and virtual network belong to two different Microsoft Entra tenants. For example, you may have a managed domain called *aaddscontoso.com* that runs in Contoso's Microsoft Entra tenant. However, the Azure virtual network for managed domain is part of the Fabrikam Microsoft Entra tenant.

Azure role-based access control (Azure RBAC) is used to limit access to resources. When you enable Domain Services in a Microsoft Entra tenant, credential hashes are synchronized to the managed domain. This operation requires you to be a tenant admin for the Microsoft Entra directory, and access to the credentials must be controlled.

To deploy resources to an Azure virtual network and control traffic, you must have administrative privileges on the virtual network in which you deploy the managed domain.

For Azure RBAC to work consistently and secure access to all the resources Domain Services uses, the managed domain and the virtual network must belong to the same Microsoft Entra tenant.

The following rules apply for deployments:

- A Microsoft Entra directory may have multiple Azure subscriptions.
- An Azure subscription may have multiple resources such as virtual networks.
- A single managed domain is enabled for a Microsoft Entra directory.
- A managed domain can be enabled on a virtual network belonging to any of the Azure subscriptions within the same Microsoft Entra tenant.

### Valid configuration

In the following example deployment scenario, the Contoso managed domain is enabled in the Contoso Microsoft Entra tenant. The managed domain is deployed in a virtual network that belongs to an Azure subscription owned by the Contoso Microsoft Entra tenant.

Both the managed domain and the virtual network belong to the same Microsoft Entra tenant. This example configuration is valid and fully supported.

![Valid Domain Services tenant configuration with the managed domain and virtual network part of the same Microsoft Entra tenant](media/getting-started/valid-tenant-config.png)

### Mismatched tenant configuration

In this example deployment scenario, the Contoso managed domain is enabled in the Contoso Microsoft Entra tenant. However, the managed domain is deployed in a virtual network that belongs to an Azure subscription owned by the Fabrikam Microsoft Entra tenant.

The managed domain and the virtual network belong to two different Microsoft Entra tenants. This example configuration is a mismatched tenant and isn't supported. The virtual network must be moved to the same Microsoft Entra tenant as the managed domain.

![Mismatched tenant configuration](media/getting-started/mismatched-tenant-config.png)

## Resolve mismatched tenant error

The following two options resolve the mismatched directory error:

- First, [delete the managed domain](delete-aadds) from your existing Microsoft Entra directory. Then, [create a replacement managed domain](tutorial-create-instance) in the same Microsoft Entra directory as the virtual network you wish to use. When ready, join all machines previously joined to the deleted domain to the recreated managed domain.
- [Move the Azure subscription](/en-us/azure/cost-management-billing/manage/billing-subscription-transfer) containing the virtual network to the same Microsoft Entra directory as the managed domain.
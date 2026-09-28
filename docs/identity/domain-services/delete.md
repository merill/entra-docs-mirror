---
layout: Conceptual
title: Delete Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/delete
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to disable, or delete, a Microsoft Entra Domain Services managed domain
ms.assetid: 89e407e1-e1e0-49d1-8b89-de11484eee46
ms.topic: how-to
ms.date: 2025-01-21T00:00:00.0000000Z
locale: en-us
document_id: 606df97c-361d-97d3-1195-a55243a3bd61
document_version_independent_id: 606df97c-361d-97d3-1195-a55243a3bd61
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/delete.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/delete
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/delete.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: dcd51012-2ed8-78f1-2fa3-ea5dbb94c907
---

# Delete Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

If you no longer need a Microsoft Entra Domain Services managed domain, you can delete it. There's no way to turn off or temporarily disable a Domain Services managed domain. Deleting the managed domain doesn't delete or have any other impact on the Microsoft Entra tenant.

This article shows you how to use the Microsoft Entra admin center to delete a managed domain.

Warning

**Deletion is permanent and can't be reversed.** When you delete a managed domain, the following steps occur:

- Domain controllers for the managed domain are deprovisioned and removed from the virtual network.
- Data on the managed domain is deleted permanently. This data includes custom OUs, GPOs, custom DNS records, service principals, GMSAs, and so on. that you created.
- Machines joined to the managed domain lose their trust relationship with the domain and need to be unjoined from the domain.
- You can't sign in to these machines using corporate AD credentials. Instead, you must use the local administrator credentials for the machine.

## Delete the managed domain

To delete a managed domain, complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](../role-based-access-control/permissions-reference#global-administrator).
2. Search for and select **Microsoft Entra Domain Services**.
3. Select the name of your managed domain, such as *aaddscontoso.com*.
4. On the **Overview** page, select **Delete**. To confirm the deletion, type the domain name of the managed domain again, then select **Delete**.

It can take 15-20 minutes or more to delete the managed domain.
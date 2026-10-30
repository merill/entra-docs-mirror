---
layout: Conceptual
title: Customer data storage for Australian and New Zealand customers - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/data-storage-australia-newzealand
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Learn about where Microsoft Entra ID stores customer-related data for its Australian and New Zealand customers.
ms.topic: concept-article
ms.date: 2025-03-05T00:00:00.0000000Z
ms.custom: it-pro, references_regions
ms.collection: M365-identity-device-management
locale: en-us
document_id: b2ce9a65-aa69-c6e0-89c2-d733af7227a5
document_version_independent_id: 414790e4-7a01-c081-5678-5fb92681af6c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/data-storage-australia-newzealand.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/data-storage-australia-newzealand
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/data-storage-australia-newzealand.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: c0aef493-dbbd-51da-3407-58a926e289df
---

# Customer data storage for Australian and New Zealand customers - Microsoft Entra | Microsoft Learn

## Overview

Microsoft Entra ID stores identity data in a location chosen based on the address provided by your organization when subscribing to a Microsoft service like Microsoft 365 or Azure. Microsoft Online Services include Microsoft 365 and Azure.

For information about where Microsoft Entra ID and other Microsoft services' data is located, see the [Where your data is located](https://www.microsoft.com/trust-center/privacy/data-location) section of the Microsoft Trust Center.

From February 26, 2020, Microsoft began storing Microsoft Entra ID's Customer Data for new tenants with an Australian or New Zealand billing address within the Australian datacenters.

Additionally, certain Microsoft Entra features don't yet support storage of Customer Data in Australia. Go to the [Microsoft global datacenters map](https://datacenters.microsoft.com/globe/explore) for information specific to your region. For example, Microsoft Entra multifactor authentication stores Customer Data in the US and processes it globally. For more information, see [Data residency and customer data for Microsoft Entra multifactor authentication](../identity/authentication/concept-mfa-data-residency).

Note

Microsoft products, services, and third-party applications that integrate with Microsoft Entra ID have access to Customer Data. Evaluate each product, service, and application you use to determine how Customer Data is processed by that specific product, service, and application, and whether they meet your company's data storage requirements. For more information about Microsoft services' data residency, see the [Where your data is located](https://www.microsoft.com/trust-center/privacy/data-location) section of the Microsoft Trust Center.

## Azure role-based access control (Azure RBAC)

Role definitions, role assignments, and deny assignments are stored globally to ensure that you have access to your resources regardless of the region where you created the resource. For more information, see [What is Azure role-based access control (RBAC)?](/en-us/azure/role-based-access-control/overview#where-is-azure-rbac-data-stored).
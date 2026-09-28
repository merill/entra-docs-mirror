---
layout: Conceptual
title: Customer data storage for Japan customers - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/data-storage-japan
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Learn about where Microsoft Entra ID stores customer-related data for its Japan customers.
ms.topic: concept-article
ms.date: 2024-01-03T00:00:00.0000000Z
ms.custom: it-pro, references_regions
ms.collection: M365-identity-device-management
locale: en-us
document_id: 24dab469-6224-4abb-8074-8b6575fde456
document_version_independent_id: be79fbb3-807c-fd05-c585-3b8ef4eaf0ba
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/data-storage-japan.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/data-storage-japan
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/data-storage-japan.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ae65506d-b7bc-7686-06a6-e01dbd214934
---

# Customer data storage for Japan customers - Microsoft Entra | Microsoft Learn

Microsoft Entra ID stores its Customer Data in a geographical location based on the country/region you provided when you signed up for a Microsoft Online service. Microsoft Online services include Microsoft 365 and Azure.

For information about where Microsoft Entra ID and other Microsoft services' data is located, see the [Where your data is located](https://www.microsoft.com/trust-center/privacy/data-location) section of the Microsoft Trust Center.

Additionally, certain Microsoft Entra features do not yet support storage of Customer Data in Japan. For example, Microsoft Entra multifactor authentication stores Customer Data in the US and processes it globally. For more information, see [Data residency and customer data for Microsoft Entra multifactor authentication](../identity/authentication/concept-mfa-data-residency).

Note

Microsoft products, services, and third-party applications that integrate with Microsoft Entra ID have access to Customer Data. Evaluate each product, service, and application you use to determine how Customer Data is processed by that specific product, service, and application, and whether they meet your company's data storage requirements. For more information about Microsoft services' data residency, see the [Where your data is located](https://www.microsoft.com/trust-center/privacy/data-location) section of the Microsoft Trust Center.

## Azure role-based access control (Azure RBAC)

Role definitions, role assignments, and deny assignments are stored globally to ensure that you have access to your resources regardless of the region you created the resource. For more information, see [What is Azure role-based access control (RBAC) (Azure RBAC)?](/en-us/azure/role-based-access-control/overview#where-is-azure-rbac-data-stored).
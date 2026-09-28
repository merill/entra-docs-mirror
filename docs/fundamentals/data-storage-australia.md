---
layout: Conceptual
title: Identity data storage for Australian and New Zealand customers - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/data-storage-australia
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Learn about where Microsoft Entra ID stores identity-related data for its Australian and New Zealand customers.
ms.topic: concept-article
ms.date: 2025-03-05T00:00:00.0000000Z
ms.custom: it-pro
ms.collection: M365-identity-device-management
locale: en-us
document_id: 6ecb35d0-a06e-e948-b1d0-284cef9d42f8
document_version_independent_id: 2ef5c0aa-52e4-be25-9cb2-eb6a8c9f7c20
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/data-storage-australia.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/data-storage-australia
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/data-storage-australia.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 45a552cc-20b9-4ff2-5fc9-3c57aa1ada83
---

# Identity data storage for Australian and New Zealand customers - Microsoft Entra | Microsoft Learn

## Overview

Microsoft Entra ID stores identity data in a location chosen based on the address provided by your organization when subscribing to a Microsoft service like Microsoft 365 or Azure. For information on where your Identity Customer Data is stored, review the Microsoft Trust Center section titled [Where is your data located?](https://www.microsoft.com/trustcenter/privacy/where-your-data-is-located).

Note

Services and applications that integrate with Microsoft Entra ID have access to Identity Customer Data. Evaluate each service and application you use. Determine how that specific service and application process identity data, and whether they meet your company's data storage requirements.

For customers who provided an address in Australia or New Zealand, Microsoft Entra ID keeps identity data for these services within Australian datacenters:

- Microsoft Entra Directory Management
- Authentication

All other Microsoft Entra services store customer data in global datacenters.

## Microsoft Entra multifactor authentication

Multifactor authentication stores Identity Customer Data in global datacenters. To learn more about the user information collected and stored by cloud-based Microsoft Entra multifactor authentication and Azure multifactor authentication Server, see [Microsoft Entra multifactor authentication user data collection](../identity/authentication/concept-mfa-data-residency).
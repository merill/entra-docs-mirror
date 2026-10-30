---
layout: Conceptual
title: Microsoft Entra Private Access and Microsoft Entra Internet Access data storage and privacy - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/reference-data-storage-and-privacy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Global Secure Access includes Microsoft Entra Private Access and Microsoft Entra Internet Access. This article outlines data storage and privacy information.
ms.topic: reference
ms.date: 2026-03-13T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: cdf29704-689e-75d7-0767-a046cf468488
document_version_independent_id: cdf29704-689e-75d7-0767-a046cf468488
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/reference-data-storage-and-privacy.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/reference-data-storage-and-privacy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/reference-data-storage-and-privacy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
platformId: 94bb0e04-156d-1f43-49f9-72b248430b71
---

# Microsoft Entra Private Access and Microsoft Entra Internet Access data storage and privacy - Global Secure Access | Microsoft Learn

## Overview

Frequently asked questions regarding privacy and data handling for Microsoft 365 enriched logs.

Global Secure Access prioritizes the protection of your data and understand the importance of transparency, especially when it comes to data processing and privacy. This article outlines the stringent standards that give you a comprehensive understanding of how your data is handled and the measures put in place to ensure its security.

## What data does Global Secure Access process?

**Microsoft 365 Audit Logs Subset** - By integrating Global Secure Access with Microsoft 365 workloads, a subset of your Microsoft 365 audit logs are copied and sent to the Global Secure Access service for processing.

## Data retention and storage

**Azure Event Hubs disk storage** - Enriched logs are stored on the Azure Event Hubs disk.

**Retention Period** - The data is retained for a duration of 24 hours. Once the data is in the customer repository, it remains there, and Global Secure Access retains its copy for a 24-hour period.

## Data isolation and access

**Access Authentication** - Robust access authentication mechanisms are implemented to ensure only authorized individuals access the data.

## Data processing locations

**Geographical Processing** - All data processing strictly occurs within the US or Europe, based on the following criteria:

- **Europe** - Data from the European customers are processed in the Global Secure Access Europe datacenters.
- **All Other Locations** - Data from any other customers are processed in the Global Secure Access U.S. datacenters.
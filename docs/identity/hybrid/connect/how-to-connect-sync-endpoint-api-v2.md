---
layout: Conceptual
title: Microsoft Entra Connect Sync V2 endpoint - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-sync-endpoint-api-v2
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This document covers updates to the Microsoft Entra Connect Sync v2 endpoints API.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 2073cab7-4918-084c-271a-9a1e05b24447
document_version_independent_id: a919b133-5590-5190-7cc5-5ff86adf2d01
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-sync-endpoint-api-v2.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-sync-endpoint-api-v2
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-sync-endpoint-api-v2.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 31ab3e54-15f3-d74b-0031-58d2cf35e239
---

# Microsoft Entra Connect Sync V2 endpoint - Microsoft Entra ID | Microsoft Learn

Microsoft has deployed a new endpoint (API) for Microsoft Entra Connect that improves the performance of the synchronization service operations to Microsoft Entra ID. By using the new V2 endpoint, you experience noticeable performance gains on export and import to Microsoft Entra ID. This new endpoint supports:

- Syncing groups with up to 250k members.
- Performance gains on export and import to Microsoft Entra ID.

Note

Currently, the new endpoint does not have a configured group size limit for Microsoft 365 groups that are written back. This may have an effect on your Active Directory and sync cycle latencies. It is recommended to increase your group sizes incrementally.

Note

The Microsoft Entra Connect Sync V2 endpoint API is Generally Available but currently can only be used in these Azure environments:

- Azure Commercial
- Microsoft Azure operated by 21Vianet cloud
- Azure US Government cloud It won't be made available in the Azure German cloud

## Prerequisites

In order to use the new V2 endpoint, you need to use Microsoft Entra Connect V2.0. When you deploy Microsoft Entra Connect V2.0, the V2 endpoint is automatically enabled. There's a known issue where upgrading to the latest V1.6 build resets the group membership limit to 50k. When a server is upgraded to Azure AD Connect V1.6, the customer should reapply the rule changes they initially applied to increase the group membership limit to 250k. This should be done before enabling sync for the server.

## Frequently asked questions

**When will the new end point become the default for upgrades and new installations?** The V2 endpoint is the default setting for Microsoft Entra Connect V2.0, and we advise customers to upgrade to Microsoft Entra Connect V2.0 to use the benefits of this endpoint. There's an issue for customers running the V2 endpoint with an older version. When they try to upgrade to a newer V1.6 release, the 50-K limitation on group membership is reinstated. When a server is upgraded to Azure AD Connect V1.6, the customer should reapply the rule changes they initially applied to increase the group membership limit to 250k. This should be done before enabling sync for the server.
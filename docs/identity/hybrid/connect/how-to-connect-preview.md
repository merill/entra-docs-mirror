---
layout: Conceptual
title: 'Microsoft Entra Connect: Features in preview - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-preview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This topic describes in more detail features which are in preview in Microsoft Entra Connect.
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: de45bc8b-a564-80ec-01cb-b5a269738348
document_version_independent_id: cc47a31a-2dc1-f8ca-e4fe-b8c7a53076e0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-preview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-preview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-preview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: e8f6088b-cc17-a1ca-ac37-714044ff4a38
---

# Microsoft Entra Connect: Features in preview - Microsoft Entra ID | Microsoft Learn

This topic describes how to use features currently in preview.

## Microsoft Entra Connect Sync V2 endpoint API

We've deployed a new endpoint (API) for Microsoft Entra Connect that improves the synchronization service operations performance for Microsoft Entra ID. By utilizing the new V2 endpoint, you'll experience noticeable performance gains on export and import to Microsoft Entra ID. This new endpoint also supports syncing groups with up to 250k members. Using this endpoint also allows you to write back Microsoft 365 unified groups, with no maximum membership limit, to your on-premises Active Directory, when group writeback is enabled. For more information, see [Microsoft Entra Connect Sync V2 endpoint API](how-to-connect-sync-endpoint-api-v2).

## User writeback

Important

The user writeback preview feature was removed in the August 2015 update to Microsoft Entra Connect. If you have enabled it, then you should disable this feature.
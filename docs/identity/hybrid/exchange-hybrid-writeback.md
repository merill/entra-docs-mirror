---
layout: Conceptual
title: Exchange hybrid writeback with sync - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/exchange-hybrid-writeback
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes the Exchange hybrid writeback feature with sync clients.
ms.topic: concept-article
ms.tgt_pltfrm: na
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid
ms.custom: sfi-image-nochange
locale: en-us
document_id: e23e8fee-870c-b4e6-9a84-9273905d2791
document_version_independent_id: 3afdbb0b-f49d-5fb5-0003-01aa2c0fc1e3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/exchange-hybrid-writeback.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/exchange-hybrid-writeback
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/exchange-hybrid-writeback.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: f7577eac-b970-85a5-017e-4e2cd2ae4501
---

# Exchange hybrid writeback with sync - Microsoft Entra ID | Microsoft Learn

A hybrid deployment offers organizations the ability to extend the feature-rich experience and administrative control they have with their existing on-premises Microsoft Exchange organization to the cloud. A hybrid deployment provides the seamless look and feel of a single Exchange organization between an on-premises Exchange organization and Exchange Online.

To accomplish this scenario and allow your on-premises users to take full advantage of Exchange online, attributes from the cloud, must be written back to your on-premises users. Both cloud sync or connect sync can write back the attributes.

[![Conceptual image of exchange hybrid scenario.](cloud-sync/media/exchange-hybrid/exchange-hybrid.png)](cloud-sync/media/exchange-hybrid/exchange-hybrid.png#lightbox)

## Cloud sync

You can enable this scenario using cloud sync by ensuring you're using the latest provisioning agent and following the documentation. For more information, see [Exchange hybrid writeback with cloud sync](cloud-sync/exchange-hybrid)

## Connect sync

You can enable the connect sync scenario through the installer. By selecting custom install, you can choose Exchange hybrid writeback. For more information, see [custom install for connect sync](connect/how-to-connect-install-custom)
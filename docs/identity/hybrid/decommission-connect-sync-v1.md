---
layout: Conceptual
title: Decommissioning Azure AD Connect V1 - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/decommission-connect-sync-v1
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes Azure AD Connect V1 decommissioning and how to migrate to V2.
documentationcenter: ''
editor: ''
ms.topic: concept-article
ms.tgt_pltfrm: na
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid
ms.custom: docutune-disable
locale: en-us
document_id: 09eb3bfb-5bcc-3fb1-b36b-6222fe1f4e51
document_version_independent_id: 9772c16b-8364-3ba2-a8b5-2f31a2abef5d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/decommission-connect-sync-v1.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/decommission-connect-sync-v1
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/decommission-connect-sync-v1.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: a776c89a-2020-1117-9253-62d81623481d
---

# Decommissioning Azure AD Connect V1 - Microsoft Entra ID | Microsoft Learn

The one-year advanced notice of Azure AD Connect V1's retirement was announced in August 2021. As of August 31, 2022, all V1 versions went out of support and were subject to stop working unexpectedly at any point.

On **October 1, 2023**, Microsoft Entra cloud services stopped accepting connections from Azure AD Connect V1 servers, and identities no longer synchronize.

If you're still using Azure AD Connect V1, you must take action immediately.

## Migrate to cloud sync

Before moving to Microsoft Entra Connect Sync, you should see if cloud sync is right for you instead. Cloud sync uses a light-weight provisioning agent and is fully configurable through the portal. To choose the best sync tool for your situation, use the [supported sync scenarios comparison.](common-scenarios)

Based on your environment and needs, you may qualify for moving to cloud sync. For a comparison of cloud sync and connect sync, see [Comparison between cloud sync and connect sync](cloud-sync/connect-to-cloud-sync-decision-guide#comparison-between-microsoft-entra-connect-and-cloud-sync). To learn more, read [What is cloud sync?](cloud-sync/what-is-cloud-sync) and [What is the provisioning agent?](cloud-sync/what-is-provisioning-agent)

## Migrating to Microsoft Entra Connect V2

If you aren't yet eligible to move to cloud sync, use this table for more information on migrating to V2.

| Title | Description |
| --- | --- |
| [Information on deprecation](connect/deprecated-azure-ad-connect) | Information on Azure AD Connect V1 deprecation |
| [What is Microsoft Entra Connect V2?](connect/whatis-azure-ad-connect-v2) | Information on the latest version of Microsoft Entra Connect |
| [Upgrading from a previous version](connect/how-to-upgrade-previous-version) | Information on moving from one version of Microsoft Entra Connect to another |

## Frequently asked questions
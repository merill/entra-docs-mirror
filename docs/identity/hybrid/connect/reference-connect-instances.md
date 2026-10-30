---
layout: Conceptual
title: 'Microsoft Entra Connect: Sync service instances - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/reference-connect-instances
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This page documents special considerations for Microsoft Entra instances.
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.tgt_pltfrm: na
ms.topic: reference
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 66587245-45e6-8890-e22b-19de75b6a8ef
document_version_independent_id: 717cb4d2-fca1-0eb5-bcb2-d2b32b7186d4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/reference-connect-instances.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/reference-connect-instances
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/reference-connect-instances.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 95585afb-ef26-3cef-a717-4a83b2cea750
---

# Microsoft Entra Connect: Sync service instances - Microsoft Entra ID | Microsoft Learn

Microsoft Entra Connect is most commonly used with the world-wide instance of Microsoft Entra ID and Microsoft 365. But there are also other instances and these have different requirements for URLs and other special considerations.

## Microsoft Cloud Germany

The [Microsoft Cloud Germany](https://www.microsoft.com/de-de/microsoft-cloud) is a sovereign cloud operated by a German data trustee.

| URLs to open in proxy server |
| --- |
| \*.microsoftonline.de |
| \*.windows.net |
| +Certificate Revocation Lists |

When you sign in to your Microsoft Entra tenant, you must use an account in the onmicrosoft.de domain.

Features currently not present in the Microsoft Cloud Germany:

- **Password writeback** is available for preview with Microsoft Entra Connect version 1.1.570.0 and after.
- Other Microsoft Entra ID P1 or P2 services are not available.

## Microsoft Azure Government

The [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.

This cloud has been supported by earlier releases of DirSync. From build 1.1.180 of Microsoft Entra Connect, the next generation of the cloud is supported. This generation is using US-only based endpoints and has a different list of URLs to open in your proxy server.

| URLs to open in proxy server |
| --- |
| \*.microsoftonline.com |
| \*.microsoftonline.us |
| \*.windows.net (Required for automatic Azure Government tenant detection) |
| \*.gov.us.microsoftonline.com |
| +Certificate Revocation Lists |

Note

As of Microsoft Entra Connect version 1.1.647.0, setting the AzureInstance value in the registry is no longer required provided that \*.windows.net is open on your proxy server(s). However, for customers that do not allow Internet connectivity from their Microsoft Entra Connect server(s), the following manual configuration can be used.

### Manual Configuration

The following manual configuration steps are used to ensure Microsoft Entra Connect uses Azure Government synchronization endpoints.

1. Start the Microsoft Entra Connect installation.
2. When you see the first page where you are supposed to accept the EULA, do not continue but leave the installation wizard running.
3. Start regedit and change the registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` to the value `4`.
4. Go back to the Microsoft Entra Connect installation wizard, accept the EULA, and continue. During installation, make sure to use the **custom configuration** installation path (and not Express installation), then continue the installation as usual.
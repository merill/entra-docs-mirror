---
layout: Conceptual
title: EDR and antivirus coexistence with Global Secure Access client - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-edr-antivirus-coexistence
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn about endpoint detection and response and antivirus solution coexistence with Global Secure Access client.
ms.reviewer: jricketts
ms.topic: concept-article
ms.date: 2025-03-28T00:00:00.0000000Z
locale: en-us
document_id: d39d9419-50ef-861a-be14-3feac9f35c9e
document_version_independent_id: d39d9419-50ef-861a-be14-3feac9f35c9e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-edr-antivirus-coexistence.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-edr-antivirus-coexistence
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-edr-antivirus-coexistence.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: ca11ce24-d962-e74e-80cb-d33a9c731fa2
---

# EDR and antivirus coexistence with Global Secure Access client - Global Secure Access | Microsoft Learn

Running antivirus solutions such as Microsoft Defender for Endpoint side by side with the Global Secure Access client can affect system performance. If your system experiences [high CPU usage or performance issues](/en-us/defender-endpoint/troubleshoot-performance-issues), exclude Global Secure Access client processes from your antivirus solution.

## Configuration overview

In your antivirus solution, configure exclusions and bypasses for all Global Secure Access client processes:

- `C:\Program Files\Global Secure Access Client\GlobalSecureAccessClientManagerService.exe`
- `C:\Program Files\Global Secure Access Client\GlobalSecureAccessEngineService.exe`
- `C:\Program Files\Global Secure Access Client\GlobalSecureAccessETLController.exe`
- `C:\Program Files\Global Secure Access Client\GlobalSecureAccessTunnelingService.exe`
- `C:\Program Files\Global Secure Access Client\TrayApp\GlobalSecureAccessClient.exe`
- `C:\Program Files\Global Secure Access Client\PolicyService\GlobalSecureAccessPolicyRetrieverService.exe`
- `C:\Program Files\Global Secure Access Client\LogsCollector\LogsCollector.exe`
- `C:\Program Files\Global Secure Access Client\AuthenticationRunner\GlobalSecureAccessAuthenticationRunner.exe`
- `C:\Program Files\Global Secure Access Client\AdvancedDiagnostics\GlobalSecureAccessClientAdvancedDiagnostics.exe`

To exclude these processes from Microsoft Defender for Endpoint, see [Configure custom exclusions for Microsoft Defender Antivirus](/en-us/defender-endpoint/configure-exclusions-microsoft-defender-antivirus).
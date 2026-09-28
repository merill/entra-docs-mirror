---
layout: Conceptual
title: Microsoft Entra Private Access Sensor release notes - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/reference-private-access-sensor-release-history
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: This article tracks the released versions of the Microsoft Entra Private Access Sensor and the changes in each version.
ms.topic: reference
ms.date: 2026-06-17T00:00:00.0000000Z
ms.subservice: entra-private-access
ms.reviewer: shkhalid
ai-usage: ai-assisted
locale: en-us
document_id: d5519bab-684f-591e-4350-893946adba4c
document_version_independent_id: d5519bab-684f-591e-4350-893946adba4c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/reference-private-access-sensor-release-history.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/reference-private-access-sensor-release-history
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/reference-private-access-sensor-release-history.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: a7a49f3b-d92b-41de-0e99-17cb47c6098a
---

# Microsoft Entra Private Access Sensor release notes - Global Secure Access | Microsoft Learn

This article lists the released versions of the Microsoft Entra Private Access Sensor and the changes in each version.

## Download the latest version

You can download the current version of the Private Access Sensor from the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Connectors and sensors** &gt; **Private access sensors**.
3. Select **Download private access sensor**.

## Version 2.2.42

Released for download on June 16, 2026.

### Security enhancements

- Hardens file and Event Tracing for Windows (ETW) channels against tampering by using channel permissions.
- Adds fail-close enforcement for policy failures.

### Kerberos observability

- Adds ticket hash computation for AS-REP, TGS-REQ, and TGS-REP.
- Adds differentiated ETW event IDs for all sensor events.

### Configurable ETW trace file size cap

- Caps ETL, trace, and log files at a configurable maximum size.
- Persists the configured maximum size across upgrades.
- Helps prevent disk exhaustion.

### Diagnostics and telemetry

- Improves telemetry reporting to the cloud.

### Access enforcement

- Adds privileged user access enforcement. This capability restricts cloud-based user access to privileged local users by UPN or SID and is in preview.

### Bug fixes

- Includes bug fixes and minor improvements.
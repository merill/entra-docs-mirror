---
layout: Conceptual
title: Global Secure Access Threat intelligence threat types - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/reference-threat-intelligence-threat-types
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Global Secure Access Threat intelligence threat types
ms.topic: reference
ms.date: 2026-03-13T00:00:00.0000000Z
ms.subservice: entra-internet-access
ai-usage: ai-assisted
locale: en-us
document_id: 336d3273-65ef-ec25-a498-95cce15403d2
document_version_independent_id: 336d3273-65ef-ec25-a498-95cce15403d2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/reference-threat-intelligence-threat-types.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/reference-threat-intelligence-threat-types
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/reference-threat-intelligence-threat-types.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 2a0e833c-fafb-42ea-8d78-ad939fc8b25c
---

# Global Secure Access Threat intelligence threat types - Global Secure Access | Microsoft Learn

## Overview

When you set up threat intelligence rules blocking access to high severity threat sites, Microsoft assigns each transaction a threat type. This article provides a list of categories along with explanations.

Note

You can check a destination's threat type using the Threat Type column in Global Secure Access [Traffic Logs](how-to-view-traffic-logs). If you would like to report a false positive, in addition to adding a new rule, you can make a request via email using [this template](mailto:GSAThreatIntel@microsoft.com?subject=%5BCustomer%20Dispute%5D%20%3CDestination%3E%20is%20a%20false%20positive&amp;body=Dispute%20Type%3A%20Threat%20intelligence%20false%20positive%0AURL%20OR%20FQDN%20OR%20IP%20%3A%20%3C%3E%0AThreat%20Type%20%3A%20%3C%3E%0AJustification%3A%20%3C%3E).

## Threat types

| Threat Type | Description |
| --- | --- |
| Botnet | Indicator is detailing a botnet node/member. |
| BruteForce | Indicator is detailing a Brute Force attack. It can be either victim or attacker. |
| C2 | Indicator is detailing a C2 (Command & Control) node of a botnet. |
| CryptoMining | Traffic involving this network address / URL is an indication of Crypto Mining / Resource abuse. |
| Darknet | Indicator is that of a Darknet node/network. |
| DDoS | Indicators relating to an active or upcoming DDoS (distributed denial of service) campaign. |
| MaliciousUrl | URL that is serving malware. |
| Malware | Indicator describing a malicious file or files. |
| Phishing | Indicators relating to a phishing campaign. |
| Proxy | Indicator is that of a proxy service. |
| PUA | PUA (Potentially Unwanted Application). |
| WatchList or Suspicious | This is the generic bucket into which indicators are placed when it cannot be determined exactly what the threat is or will require manual interpretation. |
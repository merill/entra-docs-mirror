---
layout: Conceptual
title: Learn how to solve an issue where Global Secure Access fails with a Distributed File System - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/troubleshoot-distributed-file-system
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: A troubleshooting article that includes a workaround for a case where a Distributed File System (DFS) doesn't operate correctly with Global Secure Access.
ms.topic: troubleshooting
ms.date: 2026-03-13T00:00:00.0000000Z
ms.subservice: entra-private-access
ms.reviewer: nbeesetti
ai-usage: ai-assisted
locale: en-us
document_id: f10747fa-81be-c686-4923-10b4a9290c5c
document_version_independent_id: f10747fa-81be-c686-4923-10b4a9290c5c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/troubleshoot-distributed-file-system.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/troubleshoot-distributed-file-system
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/troubleshoot-distributed-file-system.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 9b090d97-3d19-7502-e2b6-99b3c3b01991
---

# Learn how to solve an issue where Global Secure Access fails with a Distributed File System - Global Secure Access | Microsoft Learn

## Overview

This document presents a case where a Distributed File System (DFS) doesn't operate correctly with Global Secure Access and offers a temporary workaround.

The scenario involves accessing a file-share location. For instance, consider a DFS path: `\\foo.internal\share\bar`. The `bar` folder is set up as shown in the table:

| Referral Status | Site | Path |
| --- | --- | --- |
| Enabled | Location1 | \foo-loc1.contoso.com\bar |
| Enabled | Location2 | \foo-loc2.contoso.com\bar |
| Enabled | Location3 | \foo-loc3.contoso.com\bar |

Furthermore, site-locations are configured as:

- Location1: `10.0.0.1 – 10.0.0.10`
- Location2: `10.0.0.11 – 10.0.0.20`
- Location3: `10.0.0.21 – 10.0.0.30`

If a user tries to access the common DFS path and appears to be coming from the IP address `10.0.0.3`, then the user should get directed to the path: `\\foo-loc1.contoso.com\bar`. The IPs are usually the addresses of VPN locations, and don't correspond to the clients original IP.

![Diagram showing the connection between VPN and DFS.](media/troubleshoot-distributed-file-system/dfs-1.png)

## Issue

IP-based network Access Control Lists (ACL) don't work with Global Secure Access as there’s no VPN in the middle. However, the employee computer should still be referred to the appropriate fileshare.

## Workaround

The proposed workaround for the above-mentioned scenario is as follows.

As a workaround, move this employee-to-fileshare mapping to the employee computer (as a Domain Name System (DNS) search suffix), so the traffic would be:

![Diagram showing the connector.](media/troubleshoot-distributed-file-system/dfs-2.png)

The workaround is to make changes in the network-architecture in the environment:

1. Add more `C-NAME DNS`records (aliases) on domain controllers:
    - `shares.foo-loc1.contoso.com`**-&gt;**`foo-loc1.contoso.com`
    - `shares.foo-loc2.contoso.com`**-&gt;**`foo-loc2.contoso.com`
    - `shares.foo-loc3.contoso.com`**-&gt;**`foo-loc3.contoso.com`
2. Push DNS search suffixes to the employees’ computer such that:
    - Employees at *Location1* get suffix: `foo-loc1.contoso.com`
    - Employees at *Location2* get suffix: `foo-loc2.contoso.com`
    - Employees at *Location3* get suffix: `foo-loc3.contoso.com`
3. Now a dedicated Global Secure Access application can be created for each of the following Fully Qualified Domain Names (FQDNs) (or their IPs):
    - `foo-loc1.contoso.com`
    - `foo-loc2.contoso.com`
    - `foo-loc3.contoso.com`
4. Each of these applications maps to the connector (via connector group specified in the app) in the corresponding location.

After these changes, the employees accessing the common path: `\\shares\bar` from *Location1* are directed to the website: `\\foo-loc1.contoso.com\bar`, and likewise for other locations.
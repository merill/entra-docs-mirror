---
layout: Conceptual
title: Global Secure Access remote network configurations - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/reference-remote-network-configurations
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Valid Global Secure Access configurations for custom remote network device links settings, including IKE, ASN, IPSec, and DH group.
ms.topic: reference
ms.date: 2026-03-13T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: fef6b07e-3af2-312a-20a1-11d3d4e02e9c
document_version_independent_id: 202872e3-3ec2-7227-b2b1-0e9071773b19
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/reference-remote-network-configurations.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/reference-remote-network-configurations
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/reference-remote-network-configurations.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 909efe27-827e-58bc-c532-5453616afdcf
---

# Global Secure Access remote network configurations - Global Secure Access | Microsoft Learn

## Overview

Device links are the physical routers that connect your remote networks, such as branch locations, to Global Secure Access. There's a specific set of combinations you must use if you choose the **Custom** option when adding device links. If you choose the **Default** option, you must enter a specific combination of properties on the customer premises equipment (CPE).

## Custom and default details

The available regions, device types, autonomous system number (ASN), and border gateway protocol (BGP) addresses are used in both the default and custom configurations.

### Available device options

- barracudaNetworks
- checkPoint
- ciscoMeraki
- citrix
- fortinet
- hpeAruba
- netFoundry
- nuage
- openSystems
- paloAltoNetworks
- riverbedTechnology
- silverPeak
- vmWareSdWan
- versa

### Valid regions where remote networks can be created

| Europe Middle East Africa (EMEA) | Asia Pacific (APAC) | Latin America (LATAM) | North America (NA) |
| --- | --- | --- | --- |
| franceCentral | australiaEast | brazilSouth | canadaCentral |
| franceSouth | australiaSouthEast |  | canadaEast |
| germanyWestCentral | centralIndia |  | centralUS |
| israelCentral | japanEast |  | eastUS |
| italyNorth | japanWest |  | northCentralUS |
| northEurope | koreaCentral |  | southCentralUS |
| polandCentral | koreaSouth |  | westCentralUS |
| southAfricaNorth | southEastAsia |  | westUS |
| southAfricaWest | southIndia |  | westUS2 |
| swedenCentral |  |  | westUS3 |
| switzerlandNorth |  |  |  |
| uaeNorth |  |  |  |
| ukSouth |  |  |  |
| westEurope |  |  |  |

### Valid ASN

You can use any 2-byte values (between 1 to 65534) *except* for the following reserved ASNs:

- Azure reserved ASNs: 12076, 65517, 65518, 65519, 65520, 8076, 8075
- IANA reserved ASNs: 23456, &gt;= 64496 && &lt;= 64511, &gt;= 65535 && &lt;= 65551, 4294967295
- 65476

### Valid BGP addresses

You can use any BGP address *except* for the following addresses:

- 0.0.0.0/32
- 127.0.0.0/8
- 224.0.0.0/4
- 255.255.255.255/32

## Default IPSec/IKE configurations

When you select **Default** as your IPsec/IKE policy when configuring remote network device links in the Microsoft Entra admin center, we expect the following combinations in the tunnel handshake. Each value in the combination is entered on your CPE.

Important

You must specify both a Phase 1 *and* Phase 2 combination on your CPE.

### IKE Phase 1 combinations

| Properties | Combination 1 | Combination 2 | Combination 3 | Combination 4 | Combination 5 | Combination 6 | Combination 7 | Combination 8 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| IKE encryption | GCMAES256 | GCMAES128 | AES256 | AES128 | GCMAES256 | GCMAES128 | AES256 | AES128 |
| IKE integrity | SHA384 | SHA256 | SHA384 | SHA256 | SHA384 | SHA256 | SHA384 | SHA256 |
| DH group | DHGroup24 | DHGroup24 | DHGroup24 | DHGroup24 | DHGroup14 | DHGroup14 | DHGroup14 | DHGroup14 |

### IKE Phase 2 combinations

| Properties | Combination 1 | Combination 2 | Combination 3 |
| --- | --- | --- | --- |
| IPSec encryption | GCMAES256 | GCMAES192 | GCMAES128 |
| IPSec integrity | GCMAES256 | GCMAES192 | GCMAES128 |
| PFS Group | None | None | None |

## Custom IPSec/IKE combinations

When you select **Custom** as IPSec/IKE configuration when configuring remote network device links in the Microsoft Entra admin center, you must use one of the following combinations.

### IKE Phase 1 combinations

There no limitations for the IKE phase 1 combinations. Any mix and match of encryption, integrity, and DH group is valid.

### IKE Phase 2 combinations

The IPSec encryption and integrity configurations are provided in the following table:

| IPSec encryption | IPSec integrity |
| --- | --- |
| GCMAES128 | GCMAES128 |
| GCMAES192 | GCMAES192 |
| GCMAES256 | GCMAES256 |
| None | SHA256 |

- PFS group - No limitation.
- SA lifetime - must be &gt;300 seconds.

### Valid enums

The following values can be used for the IKE, IPSec, DH group, and PFS group properties.

#### IKE encryption

| Value | Enum |
| --- | --- |
| AES128 | 0 |
| AES192 | 1 |
| AES256 | 2 |
| GCMAES128 | 3 |
| GCMAES256 | 4 |

#### IKE integrity

| Value | Enum |
| --- | --- |
| SHA256 | 0 |
| SHA384 | 1 |
| GCMAES256 | 2 |
| GCMAES256 | 3 |

#### DH group

| Value | Enum |
| --- | --- |
| DHGroup14 | 0 |
| DHGroup2048 | 1 |
| ECP256 | 2 |
| ECP384 | 3 |
| DHGroup24 | 4 |

#### IPSec encryption

| Value | Enum |
| --- | --- |
| GCMAES128 | 0 |
| GCMAES192 | 1 |
| GCMAES256 | 2 |
| None | 3 |

#### IPSec integrity

| Value | Enum |
| --- | --- |
| GCMAES128 | 0 |
| GCMAES192 | 1 |
| GCMAES256 | 2 |
| SHA256 | 3 |

#### PFS group

| Value | Enum |
| --- | --- |
| PFS1 | 0 |
| None | 1 |
| PFS2 | 2 |
| PFS2048 | 3 |
| ECP256 | 4 |
| ECP384 | 5 |
| PFSMM | 6 |
| PFS24 | 7 |
| PFS14 | 8 |
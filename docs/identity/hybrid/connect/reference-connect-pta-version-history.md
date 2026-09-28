---
layout: Conceptual
title: 'Microsoft Entra pass-through authentication: Version release history - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/reference-connect-pta-version-history
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This article lists all releases of the Microsoft Entra pass-through authentication agent
ms.assetid: ef2797d7-d440-4a9a-a648-db32ad137494
ms.topic: reference
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 85a92a8f-d620-4ec7-1f10-2e1a94b7d8cf
document_version_independent_id: 8fa49faa-9b50-97f0-f687-27d59539e555
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/reference-connect-pta-version-history.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/reference-connect-pta-version-history
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/reference-connect-pta-version-history.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: a0e1aa66-2d47-ef4e-41b8-b18d450efbdc
---

# Microsoft Entra pass-through authentication: Version release history - Microsoft Entra ID | Microsoft Learn

The agents installed on-premises that enable Pass-through Authentication are updated regularly to provide new capabilities. This article lists the versions and features that are added when new functionality is introduced. Pass-through authentication agents are updated automatically when a new version is released.

Here are related topics:

- [User sign-in with Microsoft Entra pass-through authentication](how-to-connect-pta)
- [Microsoft Entra pass-through authentication agent installation](how-to-connect-pta-quick-start)

## 1.5.2482.0

### Release Status:

07/07/2021: Released for download

### New features and improvements

- Upgraded the packages/libraries to newer versions signed using SHA-256RSA.

## 1.5.1742.0

### Release Status:

04/09/2020: Released for download

### New features and improvements

- Added support for targeting cloud environments upon installation. The bundle can be pinned to a given cloud environment.

## 1.5.1007.0

### Release status

1/22/2019: Released for download

### New features and improvements

- Added support for Service Bus reliable channels to add another layer of connection resiliency for outbound connections
- Enforce TLS 1.2 during agent registration

## 1.5.643.0

### Release status

4/10/2018: Released for download

### New features and improvements

- Web socket connection support
- Set TLS 1.2 as the default protocol for the agent

## 1.5.405.0

### Release status

1/31/2018: Released for download

### Fixed issues

- Fixed a bug that caused some memory leaks in the agent.
- Updated the Azure Service Bus version, which includes a bug fix for connector timeout issues.

### New features and improvements

- Added support for websocket based connections between the agent and Microsoft Entra services to improve connection resiliency

## 1.5.402.0

### Release status

11/25/2017: Released for download

### Fixed issues

- Fixed bugs related to the DNS cache for default proxy scenarios

## 1.5.389.0

### Release status

10/17/2017: Released for download

### New features and improvements

- Added DNS cache functionality for outbound connections to add resiliency from DNS failures

## 1.5.261.0

### Release status

08/31/2017: Released for download

### New features and improvements

- GA version of the Microsoft Entra pass-through authentication agent
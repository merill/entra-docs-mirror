---
layout: Conceptual
title: Resilience in identity and access management with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/resilience-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Learn how to build resilience into identity and access management. Resilience helps endure disruption to system components and recover with minimal effort.
ms.topic: overview
ms.date: 2022-08-26T00:00:00.0000000Z
ms.custom:
- it-pro
- kr2b-contr-experiment
ms.subservice: architecture
locale: en-us
document_id: cdb6510d-fff5-f2a6-b6c4-ee66d9999214
document_version_independent_id: 05fd9012-17a9-7e20-f1c0-a25bc078d888
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/resilience-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/resilience-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/resilience-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 534add0e-94d9-c012-c034-2c6ca6545b85
---

# Resilience in identity and access management with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

Identity and access management (IAM) is a framework of processes, policies, and technologies. IAM facilitates the management of identities and what they access. It includes the many components supporting the authentication and authorization of user and other accounts in your system.

IAM resilience is the ability to endure disruption to system components and recover with minimal impact to your business, users, customers, and operations. Reducing dependencies, complexity, and single-points-of-failure, while ensuring comprehensive error handling, increases your resilience.

Disruption can come from any component of your IAM systems. To build a resilient IAM system, assume disruptions will occur and plan for them.

When planning the resilience of your IAM solution, consider the following elements:

- Your applications that rely on your IAM system
- The public infrastructures your authentication calls use, including telecom companies, Internet service providers, and public key providers
- Your cloud and on-premises identity providers
- Other services that rely on your IAM, and the APIs that connect them
- Any other on-premises components in your system

Whatever the source, recognizing and planning for the contingencies is important. However, adding other identity systems, and their resultant dependencies and complexity, may reduce your resilience rather than increase it.

To build more resilience in your systems, review the following articles:

- [Build resilience in your IAM infrastructure](resilience-in-infrastructure)
- [Build IAM resilience in your applications](resilience-app-development-overview)
- [Build resilience in your Customer Identity and Access Management (CIAM) systems](resilience-b2c)

## Related resources

- [Microsoft Entra deployment plans](deployment-plans) — deployment guidance including hybrid scenarios, authentication, and governance
- [Build resilience in your hybrid architecture](resilience-in-hybrid) — architecture diagrams for PHS, PTA, and Federation topologies
- [Identity and access management architecture in Azure](/en-us/azure/architecture/identity/identity-start-here) — reference architectures and design guidance
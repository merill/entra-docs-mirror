---
layout: Conceptual
title: Achieve NIST authenticator assurance levels with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/nist-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Use Microsoft Entra ID to meet NIST authenticator assurance levels.
ms.service: entra
ms.subservice: standards
ms.topic: how-to
author: janicericketts
ms.author: jricketts
ms.reviewer: gasinh
ms.date: 2022-11-23T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 4805345b-87c5-f6dd-0ab9-7568513794a6
document_version_independent_id: 1c1e0fea-0146-8d9e-d1ea-1e091e0b5b3a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/nist-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/nist-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/nist-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 7b670541-fcf1-ef07-2ad5-84b36fb95fe9
---

# Achieve NIST authenticator assurance levels with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

If you provide services for federal agencies, there can be challenges meeting multiple standards. As a cloud service provider (CSP) or federal agency, you ensure compliance with all relevant standards. Azure and Microsoft Entra ID make configuring requirements easier with our certifications. Azure is certified for more than 90 compliance offerings. For more details, see [Trust your cloud](https://azure.microsoft.com/overview/trusted-cloud/).

This article set has guidance on attaining the authenticator assurance levels (AALs) in NIST SP 800-63B by using Microsoft Entra ID and other Microsoft solutions. See Next steps below.

## Why meet NIST standards?

The National Institute of Standards and Technology (NIST) develops the technical requirements for US federal agencies that implement identity solutions. Organizations working with federal agencies also must meet these requirements. For more information about the NIST identity requirements, see [Special Publication 800-63 Revision 3](https://pages.nist.gov/800-63-3/sp800-63-3.html) (NIST SP 800-63-3).

NIST SP 800-63 is referenced by:

- The Electronic Prescription of Controlled Substances [EPCS](https://deadiversion.usdoj.gov/ecomm/e_rx/) program
- [Financial Industry Regulatory Authority (FINRA) requirements](https://www.finra.org/rules-guidance)
- Healthcare, defense, and other industry associations often use the NIST SP 800-63-3 as a baseline for identity and access management requirements

NIST guidelines are referenced in other standards, most notably the Federal Risk and Authorization Management Program (FedRAMP) for CSPs. Azure is certified for FedRAMP High Impact.

The NIST digital identity guidelines cover proofing and authentication of users, such as employees, partners, suppliers, customers, or citizens.

NIST SP 800-63-3 digital identity guidelines encompass three areas:

- [SP 800-63A](https://pages.nist.gov/800-63-3/sp800-63a.html) - enrollment and identity proofing
- [SP 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html) - authentication and lifecycle management
- [SP 800-63C](https://pages.nist.gov/800-63-3/sp800-63c.html) - federation and assertions

Each area has assurance levels. Use the following links to help attain the authenticator assurance levels (AALs) in NIST SP 800-63B by using Microsoft Entra ID and other Microsoft solutions.
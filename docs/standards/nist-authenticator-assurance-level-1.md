---
layout: Conceptual
title: Achieve NIST AAL1 with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/nist-authenticator-assurance-level-1
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Guidance on achieving NIST authenticator assurance level 1 (AAL1) with Microsoft Entra ID.
ms.service: entra
ms.subservice: standards
ms.topic: how-to
author: janicericketts
ms.author: jricketts
ms.reviewer: martinco, gasinh
ms.date: 2022-12-08T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: c6238f33-50fe-ea10-ca62-1bc070b3fea4
document_version_independent_id: 56a9868b-6c21-c347-7cd1-efb68c81c0b6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/nist-authenticator-assurance-level-1.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/nist-authenticator-assurance-level-1
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/nist-authenticator-assurance-level-1.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
platformId: c08a1373-675a-58d0-e1da-d17b7243b364
---

# Achieve NIST AAL1 with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

The National Institute of Standards and Technology (NIST) develops technical requirements for US federal agencies implementing identity solutions. Organizations must meet these requirements when working with federal agencies.

Before you begin authenticator assurance level 1 (AAL1), you can review the following resources:

- [NIST overview](nist-overview): Understand AAL levels
- [Authentication basics](nist-authentication-basics): Terminology and authentication types
- [NIST authenticator types](nist-authenticator-types): Authenticator types
- [NIST AALs](nist-about-authenticator-assurance-levels): AAL components, Microsoft Entra authentication methods, and Trusted Platform Modules (TPMs).

## Permitted authenticator types

To achieve AAL1, you can use any NIST single-factor or multifactor [permitted authenticator](nist-authenticator-types).

| Microsoft Entra authentication method | NIST authenticator type |
| --- | --- |
| Password  QR Code (PIN) | Memorized Secret |
| Phone (SMS): Not recommended | Single-factor out-of-band |
| Microsoft Authenticator app (Phone Sign-In) | Multi-factor out-of-band |
| Single-factor software certificate | Single-factor crypto software |
| Multi-factor software certificate  Windows Hello for Business with software TPM | Multi-factor crypto software |
| Multi-factor hardware protected certificate  FIDO 2 security key  Platform SSO for macOS (Secure Enclave)  Windows Hello for Business with hardware TPM  Passkey in Microsoft Authenticator | Multi-factor crypto hardware |

Tip

We recommend you select at a minimum phishing resistant AAL2 authenticators. Select AAL3 authenticators as necessary for business reasons, industry standards, or compliance requirements.

## FIPS 140 validation

### Verifier requirements

Microsoft Entra ID uses the Windows FIPS 140 Level 1 cryptographic module for its authentication cryptographic operations. It's therefore a FIPS 140-compliant verifier required by government agencies.

## Man-in-the-middle resistance

Communications between the claimant and Microsoft Entra ID are over an authenticated, protected channel, to resist man-in-the-middle (MitM) attacks. This configuration satisfies the MitM-resistance requirements for AAL1, AAL2, and AAL3.
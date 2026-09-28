---
layout: Conceptual
title: Microsoft Entra Verified ID-supported standards - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/verifiable-credentials-standards
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: This article outlines current and upcoming standards
ms.topic: how-to
ms.date: 2024-12-16T00:00:00.0000000Z
locale: en-us
document_id: d4ba8cb0-44b3-9b9d-7874-e400c5bedc2a
document_version_independent_id: c1178663-ae66-d813-dd54-bcf17e87595a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/verifiable-credentials-standards.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/verifiable-credentials-standards
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/verifiable-credentials-standards.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
platformId: e0bdef57-4124-549e-f560-4b9ba9426217
---

# Microsoft Entra Verified ID-supported standards - Microsoft Entra Verified ID | Microsoft Learn

## Overview

Microsoft is actively collaborating with members of the Decentralized Identity Foundation (DIF), the W3C Credentials Community Group, and the wider identity community. Microsoft works with these groups to identify and develop critical standards and implements the open standards in its services.

In this article, you find the currently supported open standards for Microsoft Entra Verified ID.

## Standards bodies

- [OpenID Foundation (OIDF)](https://openid.net/foundation/)
- [Decentralized Identity Foundation (DIF)](https://identity.foundation/)
- [World Wide Web Consortium (W3C)](https://www.w3.org/)
- [Internet Engineering Task Force (IETF)](https://www.ietf.org/)

## Supported standards

Microsoft Entra Verified ID supports the following open standards:

| **Technology stack component** | **Open standard** | **Standard body** |
| --- | --- | --- |
| Data model | [Verifiable Credentials Data Model v1.1](https://www.w3.org/TR/vc-data-model) | W3C VC WG |
| Credential format | [JSON Web Token VC (JWT-VC)](https://www.w3.org/TR/vc-data-model/#json-web-token) - encoded as JSON and signed as a JWS ([RFC7515](https://datatracker.ietf.org/doc/html/rfc7515)) | W3C VC WG /IETF |
| Entity identifier (issuer, verifier) | [did:web](https://github.com/w3c-ccg/did-method-web) | W3C CCG |
| User authentication | [Self-Issued OpenID Provider v2](https://openid.net/specs/openid-connect-self-issued-v2-1_0.html) | OIDF |
| Presentation | [OpenID for Verifiable Credentials](https://openid.net/sg/openid4vc/) | OIDF |
| Issuance | [OpenID for Verifiable Credentials Issuance](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0-11.html) | OIDF |
| Query language | [Presentation Exchange v2.0.0](https://identity.foundation/presentation-exchange/spec/v2.0.0/) | DIF |
| Trust in DID (decentralized identifier) owner | [Well Known DID Configuration](https://identity.foundation/.well-known/resources/did-configuration) | DIF |
| Revocation | [Verifiable Credential Status List](https://www.w3.org/TR/2023/WD-vc-status-list-20230427/) | W3C CCG |

## Supported algorithms

Microsoft Entra Verified ID supports the following key types for the JSON Web Signature (JWS) signature verification:

| **Key type** | **JWT algorithm** |
| --- | --- |
| secp256k1 | ES256K |
| Ed25519 | EdDSA |
| EC | P-256 |

Starting February 2024, Verified ID supports the NIST-compliant P-256 curve.

For quick setup customers, newly issued credentials use the P-256 curve as the default, and any previously issued credentials continue to work until they expire. Existing authorities automatically migrate to using P-256 for any future issuances.

For advanced setup customers, Verified ID signs credentials with the P-256 curve by default for any new authorities. For existing authorities, there are no changes to already issued or newly issued credentials.

## Interoperability

Microsoft is collaborating with organization members of Decentralized Identity Foundation (DIF), the W3C Credentials Community Group, and the wider identity community. These collaboration efforts aim to build a Verifiable Credentials Interoperability profile to support standards-based issuance, revocation, presentation, and wallet portability.

Today, a working JWT verifiable credentials presentation profile supports the interoperable presentation of verifiable credentials between wallets and verifiers/resource providers. For more information, see the DIF Claims and Credentials working group at https://aka.ms/vcinterop and https://aka.ms/vcinteroppresentation.
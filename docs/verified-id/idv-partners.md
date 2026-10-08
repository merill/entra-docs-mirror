---
layout: Conceptual
title: Microsoft Entra Verified ID - IDV partner gallery - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/idv-partners
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: Explore Microsoft Entra Verified ID identity verification partners and integrations for remote onboarding, secure access, and account recovery.
ms.topic: overview
ms.date: 2026-10-08T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1026
locale: en-us
document_id: 115bf371-2c37-c26a-3c73-10722745b971
document_version_independent_id: 115bf371-2c37-c26a-3c73-10722745b971
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/idv-partners.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/idv-partners
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/idv-partners.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
platformId: 752a209d-1362-dbe4-921e-75f0919ab39e
---

# Microsoft Entra Verified ID - IDV partner gallery - Microsoft Entra Verified ID | Microsoft Learn

## Overview

The Identity Verification (IDV) partner network extends Microsoft Entra Verified ID capabilities to help you build seamless end-user experiences. With Verified ID, you can integrate with IDV partners to enable remote onboarding, secure access to resources, and account recovery. These scenarios use Government ID checks through identity verification and proofing services.

## IDV integrations

Verified ID supports two types of IDV integrations:

- **Store-based integration**: Simple click-to-configure offers that you can purchase, subscribe to, and transact through Security Store. This integration works with Microsoft Entra ID Account Recovery and Microsoft Entra ID Governance Access Packages in-product experiences. This pattern doesn't require any custom billing contracts. Customers can select the partner offers from the respective Microsoft Entra in-product feature page for Government ID checks with IDV partners.
- **Verified ID API-based integration**: Microsoft Entra Verified ID offers REST APIs that customers and partners can use for identity verification and proofing services integration from IDV partners. This pattern requires the customer to set up billing contracts directly with the IDV partner and to use REST APIs for integration. The integration guidance page covers the step-by-step process and flows for issuer and verifier integrations.

## Partners

The following table showcases the list of Verified ID IDV partners. If you're an IDV partner seeking to get listed in this gallery, submit your solution details using the [self-submission form](https://aka.ms/VIDCertifiedPartnerForm).

### Security Store integration partners

| Partner | Partner offers | VerifiedIdentity Manifest uri | Description |
| --- | --- | --- | --- |
| 1Kosmos | [1Kosmos offer](https://aka.ms/1kosmos) | [VerifiedIdentity](https://verifiedid.did.msidentity.com/v1.0/tenants/8108e610-606c-4dc3-ae95-d3ad8be3b24c/verifiableCredentials/contracts/1197e066-a9a2-2dc5-f245-4c31d1f4b456/manifest) | 1Kosmos and Microsoft Entra Verified ID unite to deliver trusted, privacy-preserving identity verification that empowers secure, passwordless access across ecosystems. |
| AU10TIX | [AU10TIX offer](https://securitystore.microsoft.com/solutions/au10tix1662380672540.au10tixverifiedid) | [VerifiedIdentity](https://verifiedid.did.msidentity.com/v1.0/tenants/7e3c5dae-db64-4f71-8eed-e9608f62da12/verifiableCredentials/contracts/370f04a8-c259-5ef7-b61a-a4302ddb2a78/manifest) | AU10TIX improves verifiability while protecting privacy for businesses, employees, contractors, vendors, and customers. |
| CLEAR | [CLEAR offer](https://aka.ms/clear1) | [VerifiedIdentity](https://verifiedid.did.msidentity.com/v1.0/tenants/ff8690d2-858e-4cc1-927e-a9d79dfe86df/verifiableCredentials/contracts/cbbfeb49-aae3-faab-7f8d-13ac0c2d23a4/manifest) | CLEAR collaborates with Microsoft to create more secure digital experiences through verification credentials. |
| IDEMIA | [IDEMIA offer](https://securitystore.microsoft.com/solutions/idemia.idverification-global-payasugo) | [VerifiedIdentity](https://verifiedid.did.msidentity.com/v1.0/tenants/927eef35-435d-482f-be37-477c1a5164d4/verifiableCredentials/contracts/e5d08171-4b52-63ae-a586-d8490f7d1d3d/manifest) | IDEMIA Integration with Microsoft Entra Verified ID enables "Verify once, use everywhere" functionality. |
| TrueCredential (LexisNexis) | [TrueCredential offer](https://securitystore.microsoft.com/solutions/whoiamai1647469237981.truecredential) | [VerifiedIdentity](https://verifiedid.did.msidentity.com/v1.0/tenants/1dd3b364-3147-4083-96ac-e66b1e1f7b5f/verifiableCredentials/contracts/ac0bf718-61fe-2d72-f7ef-3131699bc9ed/manifest) | TrueCredential is a secure identity verification solution powered by LexisNexis Risk Solutions, leveraging Microsoft Entra Verified ID to deliver trusted, decentralized credentials. |

### Verified ID API-based integration partners

| Partner | Partner offers | Description |
| --- | --- | --- |
| authID | [authID documentation](https://developer.authid.ai/docs/proof-and-entra-verified-id) | authID integrates with Microsoft Entra Verified ID to deliver privacy-preserving biometrics and high identity assurance to verify the real user at every interaction, enabling secure onboarding and fraud-resistant access across the enterprise. |
| 1Kosmos | [1Kosmos deployment guide](https://docs.1kosmos.com/productdocs/docs/verifiable-credentials/1Kosmos-entra-verified-id/) | 1Kosmos and Microsoft Entra Verified ID unite to deliver trusted, privacy-preserving identity verification that empowers secure, passwordless access across ecosystems. |
| AU10TIX | [AU10TIX documentation](https://info.au10tix.com/hubfs/PDFs/AU10TIX-Verified-ID-Deployment-Guide.pdf) | AU10TIX improves verifiability while protecting privacy for businesses, employees, contractors, vendors, and customers. |
| CLEAR | [CLEAR documentation](https://ir.clearme.com/news-events/press-releases/detail/25/clear-collaborates-with-microsoft-to-create-more-secure) | CLEAR collaborates with Microsoft to create more secure digital experiences through verification credentials. |
| Entrust (formerly Onfido) | [Entrust documentation](https://www.entrust.com/blog/2025/11/verify-every-user-and-empower-your-workforce-with-entrust-and-microsoft-entra-verified-id) | Entrust integrates high-assurance, phishing-resistant identity verification with Microsoft Entra Verified ID to unlock trusted user-owned credentials, enabling advanced security and a seamless, frictionless user experience. |
| HYPR | [HYPR documentation](https://www.hypr.com/integrations/microsoft-verified-id) | HYPR combines multifactor identity verification with decentralized credential verification through Microsoft Entra Verified ID. This integration helps enterprises securely issue and verify trusted workforce identities with minimal friction. |
| ID Dataweb | [ID Dataweb deployment guide](https://docs.iddataweb.com/docs/microsoft) | ID Dataweb offers secure and low friction identity verification processes to ensure the validity of your Microsoft Entra Verified ID credential. Easy to integrate, easy for your users, secure for your enterprise. |
| IDEMIA | [IDEMIA documentation](https://na.idemia.com/identity/verifiable-credentials/) | IDEMIA Integration with Microsoft Entra Verified ID enables "Verify once, use everywhere" functionality. |
| Jumio | [Jumio deployment guide](https://www.jumio.com/microsoft-verifiable-credentials/) | Jumio is helping to support a new form of digital identity by Microsoft based on verifiable credentials and decentralized identifiers standards to let consumers verify once and use everywhere. |
| LexisNexis | [LexisNexis documentation](https://solutions.risk.lexisnexis.com/did-microsoft) | LexisNexis risk solutions Verifiable credentials enable faster onboarding for employees, students, citizens, or others to access services. |
| Persona | [Persona deployment guide](https://help.withpersona.com/articles/2sjBNj9gDT6ea7kShXVb5q/) | Persona integrates with Microsoft Entra Verified ID to unlock identity verification processes, enabling trusted user-owned credentials and frictionless onboarding. |
| Transmit Security | [Transmit Security deployment guide](https://developer.transmitsecurity.com/guides/verify/integrate_idv_with_endtraid/) | Mosaic by Transmit Security integrates with Microsoft Entra Verified ID to deliver seamless, secure, and accurate identity verification through verifiable credentials. |
| Vu | [Vu documentation](https://www.vusecurity.com/en) | Vu verifiable credentials with just a selfie and your ID. |
| ZealID | [ZealID deployment guide](https://developer.zealid.com/docs/zealid-vc) | ZealID Verified Credential Wallet powered by Microsoft Entra Verified ID completes the full cycle of identification and signing for various workflows. |
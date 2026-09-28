---
layout: Hub
title: Microsoft Entra Verified ID documentation - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/
summary: >
  Explore guidance for IT admins, developers, partners, and end users who set up, build with, integrate, or use Microsoft Entra Verified ID.
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: CelesteDG
ms.author: celested
ms.service: entra-verified-id
manager: dougeby
description: Learn how to set up Microsoft Entra Verified ID, build issuer and verifier solutions, integrate partner services, and use verifiable credentials.
ms.topic: hub-page
ms.date: 2026-08-28T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1023
locale: en-us
document_id: e66790e0-40f1-eb1b-bcc6-f22e2fa1a8bd
document_version_independent_id: 3964765b-5a8b-0e49-1e8f-a2830cffada2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/index.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: hub
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/index
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/index.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
platformId: b4a67a59-f998-012e-aec8-5d59fd1a2794
---

# Microsoft Entra Verified ID documentation

Explore guidance for IT admins, developers, partners, and end users who set up, build with, integrate, or use Microsoft Entra Verified ID. 

![](/en-us/media/hubs/shared/icon-overview.svg?branch=main)

Overview
[Introduction to Microsoft Entra Verified ID](decentralized-identifier-overview)

![](/en-us/media/hubs/shared/icon-tutorial.svg?branch=main)

Tutorial
[Issue a credential for directory-based claims](how-to-use-quickstart-verifiedemployee)

![](/en-us/media/hubs/shared/icon-architecture.svg?branch=main)

Architecture
[Microsoft Entra Verified ID architecture](introduction-to-verifiable-credentials-architecture)

![](/en-us/media/hubs/shared/icon-overview.svg?branch=main)

Overview
[Microsoft Entra Verified ID pricing](https://azure.microsoft.com/en-us/pricing/details/microsoft-entra-verified-id/?msockid=3c2f5dfa1b84682d126a4af31ae069c2)

![](/en-us/media/hubs/shared/icon-tutorial.svg?branch=main)

Tutorial
[Use Face Check](using-facecheck)

![](/en-us/media/hubs/shared/icon-whats-new.svg?branch=main)

What's new
[What's new](whats-new)

## Configure and build

Find setup and development guidance that matches what you want to do.

### IT admin

- [Set up Microsoft Entra Verified ID](verifiable-credentials-configure-tenant-quick)
- [Configure advanced setup](verifiable-credentials-configure-tenant)
- [Register your decentralized ID](how-to-register-didwebsite)
- [Verify domain ownership](how-to-dnsbind)
- [Rotate signing keys](how-to-rotate-keys)

### Developer

- [Get started with the Request API](get-started-request-api)
- [Issue credentials from an application](verifiable-credentials-configure-issuer)
- [Verify credentials from an application](verifiable-credentials-configure-verifier)
- [Get started with the Admin API](admin-api)

## Integrate and use

Find partner integration and credential usage guidance.

### Partner

- [Use the Verified ID Network API](vc-network-api)
- [Explore identity verification partners](idv-partners)
- [Explore services partners](services-partners)
- [Use the Verified ID Network](how-use-vcnetwork)

### End user

- [Use Verified ID with Microsoft Authenticator](using-authenticator)
- [Review frequently asked questions](verifiable-credentials-faq)

## Browse scenario categories

Explore common scenarios for employee lifecycles, external identities, application development, security, and partner integrations.

[Employee lifecycle](remote-onboarding-new-employees-id-verification)
Use Verified ID for remote onboarding and identity verification for employee support and account recovery.

[Consumer and external user](../id-governance/entitlement-management-verified-id-settings)
Secure onboarding, identity verification, and account recovery for consumers and external users.

[Developer platform](issuer-openid)
Understand communication between an identity provider and an issuer service.

[Security and compliance](signing-key-upgrade)
Upgrade signing keys to support FIPS-compliant signing.

[Partner ecosystem](integration-guidance)
Integrate Verified APIs into your applications and services.

## Plan and manage your solution

[Plan credential issuance](plan-issuance-solution)
Design an issuance solution for the credentials your organization provides.

[Review supported standards](verifiable-credentials-standards)
Learn about the standards that Microsoft Entra Verified ID supports.

[Customize credentials](credential-design)
Define the claims and visual presentation of a Verified ID credential.

[Review API reference](issuance-request-api)
Find specifications for issuance, presentation, administration, and the Verified ID Network.
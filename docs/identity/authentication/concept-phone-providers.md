---
layout: Conceptual
title: Choose a telephony provider for SMS and voice authentication - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-phone-providers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about Choose Your Own Telephony Provider for SMS and voice authentication in Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2026-09-23T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: 096319fc-09be-11d8-706d-0490641448f7
document_version_independent_id: 096319fc-09be-11d8-706d-0490641448f7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-phone-providers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-phone-providers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-phone-providers.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: c61bf76c-2a59-e1f2-d915-1a9535dcfaeb
---

# Choose a telephony provider for SMS and voice authentication - Microsoft Entra ID | Microsoft Learn

Microsoft Entra ID will support Choose Your Own Telephony Provider, which lets organizations continue using SMS or voice authentication with a supported telephony provider. You select a telephony provider through the Microsoft Security Store and manage the provider relationship for your organization.

Microsoft recommends phishing-resistant authentication methods, such as [passkeys](concept-authentication-passkeys-fido2), instead of SMS or voice. Use a telephony provider only for user populations that have a business, regulatory, or technical requirement for telephony-based authentication.

Important

Choose Your Own Telephony Provider isn't available to configure yet. Information about the providers participating in the private preview is available now. The configuration experience becomes available beginning October 30, 2026.

## Available telephony providers

Soprano and Telesign are the initial telephony providers available during the private preview. More providers will become available by general availability.

Review pricing and other commercial details for the available provider offers:

- Soprano: [Per-user offer](https://securitystore.microsoft.com/solutions/sopranodesignlimited1620113206416.soprano_entraid_per_user) or [per-transaction offer](https://securitystore.microsoft.com/solutions/sopranodesignlimited1620113206416.soprano_entraid_per_transaction) in Microsoft Security Store.
- Telesign: [Telesign Verify for Microsoft Entra](https://securitystore.microsoft.com/solutions/telesigncorporation1779799505747.telesign-verify-cyot-azure) in Microsoft Security Store.

## How Choose Your Own Telephony Provider works

Your selected telephony provider delivers the SMS messages or voice calls that users need to complete authentication. Microsoft Entra ID continues to enforce your authentication method policies and coordinates the authentication experience.

Your organization is responsible for selecting a telephony provider, reviewing its regional coverage and terms, completing the provider agreement, configuring the provider for Microsoft Entra ID, and monitoring the service.

For the full transition schedule, see [Passkeys by default and retirement of Microsoft-provided SMS and voice authentication](concept-sms-voice-retirement).

## Plan your Choose Your Own Telephony Provider deployment

Before you select a provider:

- Identify the users who have a documented requirement for SMS or voice authentication.
- Confirm that a phishing-resistant method doesn't meet the requirement.
- Compare supported telephony providers based on geographic coverage, supported delivery channels, pricing, support, security, and compliance capabilities.
- Review procurement, privacy, and regulatory requirements with the appropriate teams in your organization.
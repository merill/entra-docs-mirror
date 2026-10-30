---
layout: Conceptual
title: Choose your own telephony provider for SMS and voice authentication - Microsoft Entra ID | Microsoft Learn
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
description: Learn how CYOT works, available telecom providers, and how to plan setup, fraud protection, resiliency, and costs.
ms.topic: concept-article
ms.date: 2026-10-30T00:00:00.0000000Z
ai-usage: ai-assisted
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
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: c61bf76c-2a59-e1f2-d915-1a9535dcfaeb
---

# Choose your own telephony provider for SMS and voice authentication - Microsoft Entra ID | Microsoft Learn

Choose Your Own Telephony Provider (CYOT) lets your organization use a supported telecom provider to deliver SMS and voice authentication for Microsoft Entra ID.

With CYOT, Microsoft Entra continues to manage the authentication experience, including one-time passcode (OTP) generation and validation, while SMS messages and voice calls are delivered through the telecom provider that your organization selects and configures.

CYOT gives your organization more control over telecom provider selection, geographic coverage, pricing, and telecom delivery.

Important

Microsoft recommends phishing-resistant authentication methods, such as [passkeys](concept-authentication-passkeys-fido2), instead of SMS or voice. Use a telephony provider only for user populations that have a business, regulatory, or technical requirement for telephony-based authentication.

## How CYOT works

When SMS or voice authentication is required:

1. Microsoft Entra initiates the authentication request.
2. Microsoft Entra sends the request to the CYOT integration deployed in your Azure subscription.
3. The integration sends the request to your configured telecom provider.
4. Your telecom provider delivers the SMS message or voice call to the user.
5. Microsoft Entra completes the authentication flow.

The Azure Function deployed in your subscription connects Microsoft Entra with your telecom provider.

[![Simplified CYOT architecture diagram showing Microsoft Entra connected to a telecom provider through an Azure Function in your Azure subscription.](media/concept-phone-providers/telephony-provider-integration-diagram.jpeg)](media/concept-phone-providers/telephony-provider-integration-diagram.jpeg#lightbox)

## Available telephony providers

Select a supported telecom provider based on your organization's coverage, pricing, and other requirements.

Review pricing and other commercial details for the available provider offers:

- Soprano: [Per-user offer](https://securitystore.microsoft.com/solutions/sopranodesignlimited1620113206416.soprano_entraid_per_user) or [per-transaction offer](https://securitystore.microsoft.com/solutions/sopranodesignlimited1620113206416.soprano_entraid_per_transaction) in [Microsoft Security Store](https://securitystore.microsoft.com/).
- Telesign: [Telesign Verify for Microsoft Entra](https://securitystore.microsoft.com/solutions/telesigncorporation1779799505747.telesign-verify-cyot-azure) in [Microsoft Security Store](https://securitystore.microsoft.com/).
- Infobip.

Note

Provider availability, coverage, pricing, and commercial terms can vary. Review the provider's [Microsoft Security Store](https://securitystore.microsoft.com/) listing for the latest information before purchasing.

## Understand your responsibilities

With CYOT, your organization owns the Azure resources deployed in your subscription and your telecom provider account, so you keep full control over how they run. The guided deployment sets up the integration for you, and your team manages the Azure Function and provider account from there.

| Owner | Responsibilities |
| --- | --- |
| Microsoft | Microsoft Entra authentication and the handoff to your endpoint. |
| Customer | Deploying and operating the integration, managing the telecom provider account, and configuring fraud controls. |
| Telephony provider | SMS and voice delivery, and offering fraud controls. |

## Get started with CYOT

At a high level, setting up CYOT involves:

1. **Subscribe to a telecom provider.** Review the available provider offers in [Microsoft Security Store](https://securitystore.microsoft.com/) and purchase the offer that meets your organization's requirements.
2. **Set up the provider integration.** Deploy the integration in your Azure subscription and connect it to your provider.
3. **Create an SMS or voice profile.** Route SMS or voice authentication through your provider.
4. **Evaluate.** Validate the integration while Microsoft continues to deliver messages, so users aren't affected.
5. **Roll out.** Move traffic to your provider gradually, validating at each stage.

For detailed instructions, see [Set up SMS and voice with your own telecom provider by using APIs](how-to-set-up-sms-voice-api).

## Plan your deployment

Before moving production authentication traffic to CYOT, consider fraud protection, resiliency, and costs based on your organization's requirements.

### Prevent telephony fraud

Work with your telecom provider to configure the fraud protection, destination, usage, and spending controls appropriate for your organization's traffic and risk requirements.

See [Prevent telephony fraud when using your own telecom provider](choose-your-own-telephony-fraud-costs).

### Plan for resiliency

Plan the availability and recovery of the Azure resources and telecom provider used by your CYOT integration.

Organizations with additional availability requirements can implement cross-region resiliency and, where appropriate, configure provider redundancy.

See [Plan for resiliency when using your own telecom provider](choose-your-own-telephony-reliability).

### Understand costs

CYOT can involve two separate categories of costs:

- Telecom provider costs for SMS and voice delivery through your selected provider.
- Azure costs for the Azure Function and supporting resources deployed in your subscription.

Review both before moving production authentication traffic to CYOT.

See [Estimate telecom-provider and Azure hosting costs](phone-providers-faq#how-much-does-choose-your-own-telephony-provider-cost).

## Troubleshoot CYOT

To diagnose SMS or voice issues, identify whether the issue is in Microsoft Entra authentication and configuration, your CYOT integration, or telecom provider delivery.

See [Troubleshoot SMS and voice with your own telecom provider](choose-your-own-telephony-troubleshoot#monitor-and-troubleshoot-your-own-telephony-provider) for diagnostic guidance and information about where to get support.
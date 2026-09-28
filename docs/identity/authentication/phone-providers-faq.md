---
layout: FAQ
title: Frequently asked questions about telephony providers in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/phone-providers-faq
summary: >
  <p>The following are frequently asked questions about Choose Your Own Telephony Provider in Microsoft Entra ID. For questions not answered here, ask the community on the <a href="/answers/topics/azure-active-directory.html">Microsoft Q&amp;A question page for Microsoft Entra ID</a>.</p>

  <p>This FAQ covers:</p>

  <ul>

  <li><a href="#provider-selection-and-availability">Provider selection and availability</a></li>

  <li><a href="#costs-and-billing">Costs and billing</a></li>

  <li><a href="#migration-and-evaluation">Migration and evaluation</a></li>

  <li><a href="#support-and-troubleshooting">Support and troubleshooting</a></li>

  </ul>
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Find answers to common questions about selecting, configuring, evaluating, and supporting Choose Your Own Telephony Provider for Microsoft Entra ID.
ms.topic: faq
ms.date: 2026-09-20T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 5459ec2c-0730-9fc0-1d9d-072e6c52cde2
document_version_independent_id: 5459ec2c-0730-9fc0-1d9d-072e6c52cde2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/phone-providers-faq.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/phone-providers-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/phone-providers-faq.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 581d556e-0098-71c3-84f3-2946c92b6c4e
---

# Frequently asked questions about telephony providers in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The following are frequently asked questions about Choose Your Own Telephony Provider in Microsoft Entra ID. For questions not answered here, ask the community on the [Microsoft Q&A question page for Microsoft Entra ID](/en-us/answers/topics/azure-active-directory.html).

This FAQ covers:

- Provider selection and availability
- Costs and billing
- Migration and evaluation
- Support and troubleshooting

## Provider selection and availability

### When will Choose Your Own Telephony Provider be available?

Information about the telephony providers participating in the private preview is now available. The configuration experience will become available starting October 30, 2026.

Until the configuration experience is available, review the supported provider options and begin planning your migration from Microsoft-managed SMS and voice authentication.

### Which telephony providers are available during the private preview?

Soprano and Telesign are the initial telephony providers available during the private preview. More providers will become available by general availability.

Pricing and other commercial details for these providers are available in Microsoft Security Store.

### Can I use my existing SMS provider?

Yes, you can use your existing provider if it's one of the supported telephony providers. If your current provider isn't supported, you will need to select a supported provider to continue using SMS or voice authentication after Microsoft-managed telephony is retired.

### Can I use Choose Your Own Telephony Provider to keep SMS sign-in as a primary authentication method?

No. The feature doesn't support SMS sign-in as a primary authentication method. The retirement of SMS sign-in as a primary authentication method applies even when you use Choose Your Own Telephony Provider. If your organization currently uses SMS sign-in for primary authentication, migrate users to supported alternatives based on their scenarios. Alternatives include passkeys, QR code authentication, FIDO2 security keys, and other authentication methods supported by Microsoft Entra ID.

### Does this work with Microsoft Entra ID, Microsoft Entra External ID, and Azure AD B2C?

Choose Your Own Telephony Provider is currently available only for Microsoft Entra ID. Microsoft Entra External ID and Azure AD B2C aren't included.

### Can I configure multiple telephony providers?

Starting October 30, 2026, you can configure one telephony provider per channel: one provider for SMS and one provider for voice.

## Costs and billing

### How much does Choose Your Own Telephony Provider cost?

The primary cost is what your selected telephony provider charges for SMS and voice messages, based on the provider's pricing and your usage. The feature uses a routing function deployed in your Azure subscription to securely connect Microsoft Entra ID with your selected telephony provider. Standard Azure consumption charges apply to the routing function, but these costs are expected to be minimal for most customers compared to telephony provider charges.

Review pricing and other commercial details for the available provider offers:

- Soprano: [Per-user offer](https://securitystore.microsoft.com/solutions/sopranodesignlimited1620113206416.soprano_entraid_per_user) or [per-transaction offer](https://securitystore.microsoft.com/solutions/sopranodesignlimited1620113206416.soprano_entraid_per_transaction) in Microsoft Security Store.
- Telesign: [Telesign Verify for Microsoft Entra](https://securitystore.microsoft.com/solutions/telesigncorporation1779799505747.telesign-verify-cyot-azure) in Microsoft Security Store.

## Migration and evaluation

### How do I migrate?

Choose Your Own Telephony Provider will be available starting October 30, 2026. When it becomes available, you will configure the feature from the Microsoft Entra admin center.

Migration typically involves the following steps:

1. Select a supported telephony provider and establish an account with that provider.
2. Deploy a routing function in your Azure subscription. The routing function securely sends authentication requests from Microsoft Entra ID to your provider.
3. Select the users or groups that will use the provider for SMS, voice, or both.
4. Evaluate the integration before it affects users.
5. Gradually enable the provider for production authentication traffic.

Detailed configuration and deployment instructions will be available when the feature is released. Complete your migration before the February 1, 2027 retirement of Microsoft-managed telephony to allow sufficient time for testing and a phased production rollout.

### Can I evaluate before switching my users to a new provider?

Yes. Evaluation mode lets you validate that authentication requests are successfully routed to your telephony provider without changing the authentication experience for your users.

Your users continue to receive authentication messages through the currently active delivery method while you review the evaluation results. After you confirm that the integration is working as expected, you can enable the provider for production traffic and gradually expand the rollout.

## Support and troubleshooting

### What is the support model?

Microsoft provides support for the Microsoft Entra ID platform, including the telephony provider configuration experience, authentication workflows, and the routing between Microsoft Entra ID and your telephony provider.

Your organization is responsible for managing its selected telephony provider relationship, including provider account configuration, service availability, message delivery, and issues related to SMS or voice delivery. For provider or message delivery issues, contact your provider's support team.

Microsoft provides diagnostics and troubleshooting guidance to help determine whether an issue is related to the Microsoft Entra ID platform or the telephony provider integration.
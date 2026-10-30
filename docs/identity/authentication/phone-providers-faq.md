---
layout: FAQ
title: Frequently asked questions about Choose Your Own Telephony Provider - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/phone-providers-faq
summary: >
  <p><a id="frequently-asked-questions-about-choose-your-own-telephony-provider"></a></p>

  <p>These are common questions about Choose Your Own Telephony Provider (CYOT) in Microsoft Entra ID. For an overview, see <a href="concept-phone-providers">Choose your own telephony provider for SMS and voice authentication</a>.</p>

  <p>This FAQ covers:</p>

  <ul>

  <li><a href="#provider-selection-and-availability">Provider selection and availability</a>.</li>

  <li><a href="#supported-scenarios">Supported scenarios</a>.</li>

  <li><a href="#costs-and-billing">Costs and billing</a>.</li>

  <li><a href="#evaluation-and-migration">Evaluation and migration</a>.</li>

  <li><a href="#reliability-and-recovery">Reliability and recovery</a>.</li>

  <li><a href="#support">Support</a>.</li>

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
description: Find answers about CYOT provider selection, supported scenarios, costs, evaluation, migration, reliability, recovery, and support in Microsoft Entra ID.
ms.topic: faq
ms.date: 2026-10-30T00:00:00.0000000Z
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
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 581d556e-0098-71c3-84f3-2946c92b6c4e
---

# Frequently asked questions about Choose Your Own Telephony Provider - Microsoft Entra ID | Microsoft Learn

These are common questions about Choose Your Own Telephony Provider (CYOT) in Microsoft Entra ID. For an overview, see [Choose your own telephony provider for SMS and voice authentication](concept-phone-providers).

This FAQ covers:

- Provider selection and availability.
- Supported scenarios.
- Costs and billing.
- Evaluation and migration.
- Reliability and recovery.
- Support.

## Provider selection and availability

### When is CYOT available?

CYOT is generally available starting October 30, 2026, for Microsoft Entra ID workforce tenants in global Azure.

### Which telecom providers can I use?

You can choose Soprano, Telesign, or Infobip. For coverage, pricing, and terms, see [Available telecom providers](concept-phone-providers#available-telephony-providers) and each provider's [Microsoft Security Store](https://securitystore.microsoft.com/) listing.

### Can I use my existing account with a provider?

Check with your provider. Your provider might also need its own registration, such as sender registration.

### Can I use a provider that isn't on the list?

CYOT supports the providers listed in [Available telecom providers](concept-phone-providers#available-telephony-providers). Check that list for providers as they're added.

### Can I use different providers for SMS and voice?

Yes. You can use one provider for SMS and another for voice.

## Supported scenarios

### Which Microsoft Entra products support CYOT?

CYOT is available for Microsoft Entra ID workforce tenants. It isn't currently available for Microsoft Entra External ID or Azure AD B2C.

### Can I use CYOT for SMS sign-in as a primary method?

No. CYOT supports SMS and voice as verification methods, not as primary sign-in. Move users who sign in with SMS to another supported method.

Important

Microsoft recommends phishing-resistant methods such as [passkeys](concept-authentication-passkeys-fido2). Use SMS or voice only for users with a business, regulatory, or technical need for it.

## Costs and billing

### How much does CYOT cost?

Plan for two costs:

- **Provider costs:** SMS and voice charges set by your provider's offer on [Microsoft Security Store](https://securitystore.microsoft.com/).
- **Azure costs:** the resources that host the integration in your subscription.

For estimates, see [Estimate telecom provider and Azure hosting costs](https://github.com/Azure-Samples/ExternalPhoneProvider-AzureFunction-Sample/blob/main/docs/COST-CALCULATOR.md).

### Does Microsoft charge me for SMS and voice sent through my provider?

Your provider sets SMS and voice charges under the offer you purchase in [Microsoft Security Store](https://securitystore.microsoft.com/). Azure hosting costs are billed to your Azure subscription.

## Evaluation and migration

### How do I move to my own telecom provider?

1. Subscribe to a provider offer in [Microsoft Security Store](https://securitystore.microsoft.com/).
2. Set up the integration in your Azure subscription.
3. Create an SMS and voice profile.
4. Evaluate the integration.
5. Roll out traffic to your provider.

For details, see [Set up SMS and voice with your own telecom provider by using APIs](how-to-set-up-sms-voice-api).

### Can I test CYOT before I move traffic?

Yes. **Evaluation** mode sends requests to your integration while Microsoft continues to deliver codes to users. Use `migrationPercentage` to set the evaluation sampling percentage when configuring the policy through APIs. To confirm delivery through your provider, switch to **Production** at a low traffic percentage.

### Can I move traffic gradually?

Yes. Increase the **Traffic routed through provider percentage** in stages, and check results before each increase.

### How long do policy changes take to apply?

Changes to the authentication methods policy can take up to about an hour to apply.

### I lost the setup output when Cloud Shell closed. What do I do?

Copy the deployment summary as soon as the script finishes. Cloud Shell sessions are temporary and can close when you switch tabs. If you lost it, find the deployed resources in the Azure portal.

## Reliability and recovery

### What should I do if SMS or voice codes aren't arriving?

If you're partway through a rollout, pause it. Then use [Monitor and troubleshoot SMS and voice with your own telecom provider](choose-your-own-telephony-troubleshoot#monitor-and-troubleshoot-your-own-telephony-provider) to find where the request stopped and who to contact.

### How do I plan for high availability?

You can deploy the integration across multiple Azure regions, review your provider's redundancy, and add a secondary provider. The multi-region and secondary-provider designs are sample-only guidance. Test failover before you rely on it. See [Plan for resiliency and high availability](choose-your-own-telephony-reliability).

## Support

### Who manages each part of CYOT?

| Owner | Responsibility |
| --- | --- |
| Microsoft | Microsoft Entra authentication and the handoff to your endpoint |
| Your organization | Deploying and running the integration, managing the provider account, and renewing integration credentials and certificates |
| Telecom provider | SMS and voice delivery, and fraud controls |

### Who do I contact for help?

| Issue | Contact |
| --- | --- |
| Microsoft Entra authentication, code validation, or the handoff to your endpoint | [Microsoft Support](/en-us/entra/fundamentals/how-to-get-support) |
| Your Azure Function or Azure resources | Your Azure team |
| Delivery, sender registration, destinations, fraud controls, or charges | Your telecom provider. Contact details are in its [Security Store](https://securitystore.microsoft.com/) listing. |
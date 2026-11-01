---
layout: Conceptual
title: Protect against telephony fraud with your own telecom provider - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/choose-your-own-telephony-fraud-costs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Configure provider fraud protections, destination and spending controls, secure your CYOT integration, monitor unusual activity, and respond to suspected fraud.
ms.topic: how-to
ms.date: 2026-10-30T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 72350b1a-8c4d-15d7-1e2b-943f50732ebf
document_version_independent_id: 72350b1a-8c4d-15d7-1e2b-943f50732ebf
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/choose-your-own-telephony-fraud-costs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/choose-your-own-telephony-fraud-costs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/choose-your-own-telephony-fraud-costs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 0e0e312f-34ec-5ec6-8352-086bba9d4cd9
---

# Protect against telephony fraud with your own telecom provider - Microsoft Entra ID | Microsoft Learn

With Choose Your Own Telephony Provider (CYOT), SMS and voice traffic runs through your own telecom provider account. You control the fraud protections, allowed destinations, and spending limits that match your organization's traffic and risk profile.

Important

Set up your provider's fraud and spending controls before you move production traffic to CYOT.

## Shared responsibility

| Owner | Responsibility |
| --- | --- |
| Microsoft | Protects code generation and validation in Microsoft Entra ID, and the handoff to your endpoint. |
| Your organization | Manages the provider account, secures the integration, and configures fraud controls. |
| Telecom provider | Delivers SMS and voice, and offers fraud, destination, and spending controls. |

## Configure fraud protections with your provider

Work with your provider to turn on the controls available for your account:

- **Fraud protection:** Turn on the provider's detection for suspicious SMS and voice traffic.
- **Destination restrictions:** Allow only the countries and regions where your users are.
- **Channel restrictions:** Turn on only the channels you use.
- **Spending controls:** Set usage limits and budget alerts.
- **Notifications:** Turn on alerts for unusual activity.

Note

Controls and defaults vary by provider. Ask your provider which protections are on by default and which you need to configure.

## Keep your integration secure

The setup script configures authentication and request validation for your Azure Function. Keep these settings in place, including when you customize the Function.

Your organization is responsible for renewing and rotating the integration's application credentials and certificates.

## Monitor for unusual activity

Review SMS and voice volume in your provider's usage reports. A sudden increase in volume, or traffic to destinations you don't expect, can signal fraud.

## Respond to suspected fraud

1. Contact your telecom provider to review the affected traffic.
2. Restrict the affected destinations, channels, or usage with your provider's controls.
3. Investigate the requests using the Microsoft Entra audit logs, the Function App logs, and your provider's records.
4. Update your protections before you restore traffic.

## Get support

| Issue | Contact |
| --- | --- |
| Fraud, provider account restrictions, delivery, or charges | Your telecom provider. Find contact details in the provider's [Microsoft Security Store](https://securitystore.microsoft.com/) listing. |
| Microsoft Entra authentication, code validation, or the handoff to your endpoint | Microsoft Support. See [Find help and get support for Microsoft Entra](/en-us/entra/fundamentals/how-to-get-support). |
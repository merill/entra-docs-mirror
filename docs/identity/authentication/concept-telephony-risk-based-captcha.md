---
layout: Conceptual
title: Risk-based anti-bot verification (CAPTCHA) for telephony-based sign-in - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-telephony-risk-based-captcha
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about risk-based anti-bot verification before Microsoft Entra ID sends SMS messages or places voice calls for telephony-based sign-in.
ms.topic: concept-article
ms.date: 2026-10-14T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: d60bdc72-2bdf-fca1-bf67-df0035eced33
document_version_independent_id: d60bdc72-2bdf-fca1-bf67-df0035eced33
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-telephony-risk-based-captcha.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-telephony-risk-based-captcha
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-telephony-risk-based-captcha.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 5184a590-33fa-9206-62c3-7f3f3b1b67b6
---

# Risk-based anti-bot verification (CAPTCHA) for telephony-based sign-in - Microsoft Entra ID | Microsoft Learn

Microsoft Entra ID uses safeguards to help reduce automated abuse of telephony-based sign-in. In some cases, users might be asked to complete a risk-based anti-bot verification step, such as a CAPTCHA, before Microsoft sends an SMS message or places a voice call for sign-in. This safeguard helps protect against telephony fraud, such as International Revenue Share Fraud (IRSF).

For more information about telephony fraud and how Microsoft helps limit the impact of fraudulent activity, see [Understanding telephony fraud risk](concept-mfa-telephony-fraud).

## What anti-bot verification is

The provider for this CAPTCHA experience is Arkose Labs. The challenge opens in a dialog during the authentication flow. The interaction helps confirm that the request is being made by a person before Microsoft sends an SMS message or places a voice call.

The experience is risk-based and uses client behavior signals, so not every user or authentication attempt is affected. Microsoft doesn't publish the risk criteria or implementation details that determine when anti-bot verification is shown.

## What users experience

When anti-bot verification is required, the user must complete the verification step before Microsoft sends the SMS message or places the voice call. If the user can't complete the verification step, they should try again or use another available authentication method. If the CAPTCHA dialog doesn't load, your organization might need to allow the Arkose Labs domains. For more information, see Network requirements.

Help desk teams should communicate that:

- SMS and voice authentication aren't removed by this safeguard.
- A user might need to complete an anti-bot verification step before receiving an SMS message or voice call.
- If the verification step doesn't load, the issue might be related to network or firewall restrictions. For more information, see Network requirements.
- Users should use another available non-telephony authentication method when possible. Non-telephony methods are more secure, aren't subject to this safeguard, and might provide a better user experience.

## Network requirements

Anti-bot verification can depend on resources that are loaded during the authentication flow. If an organization uses restrictive firewalls, proxies, or web filtering, users might be blocked from completing verification if the required endpoints aren't allowed.

To allow the Arkose Labs verification challenge to load and complete during authentication, configure the firewall, proxy, or secure web gateway to permit outbound HTTPS traffic on TCP port 443 from users' devices to:

- `*.arkoselabs.com`
- `arkoselabs.com`

Use your product's wildcard-domain or fully qualified domain name (FQDN) allowlist syntax so the rule covers all subdomains. Some products don't match the base domain with a wildcard entry, so add both domains.

Also make sure that:

- DNS filtering and web-content/category filtering policies don't block these domains, and that your allow rule takes priority over category-based blocks.
- These domains are excluded from TLS/SSL inspection (HTTPS decryption), which can stop the challenge from loading or validating.

## Prepare users and help desks

To prepare for risk-based anti-bot verification:

- Tell users that some SMS and voice authentication attempts might require anti-bot verification before Microsoft sends an SMS message or places a voice call.
- Make sure help desk teams know that the verification step is expected when risk-based safeguards apply.
- Review network requirements when the verification experience doesn't load.
- Encourage users to register and use phishing-resistant authentication methods where possible, such as passkeys.
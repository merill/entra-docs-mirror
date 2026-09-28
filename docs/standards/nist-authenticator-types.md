---
layout: Conceptual
title: NIST authenticator types and aligned Microsoft Entra methods - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/nist-authenticator-types
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Explanations of how Microsoft Entra authentication methods align with NIST authenticator types.
ms.service: entra
ms.subservice: standards
ms.topic: how-to
author: janicericketts
ms.author: jricketts
ms.reviewer: martinco, gasinh
ms.date: 2022-11-23T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 53c5b09b-b9bd-5403-b167-437e08720a12
document_version_independent_id: 2f40eb99-9912-2fb2-6778-abcaa00ace7a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/nist-authenticator-types.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/nist-authenticator-types
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/nist-authenticator-types.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
platformId: ffc42407-7cd3-5859-5188-d47c89bada5b
---

# NIST authenticator types and aligned Microsoft Entra methods - Microsoft Entra | Microsoft Learn

The authentication process begins when a claimant asserts its control of one of more authenticators associated with a subscriber. The subscriber is a person or another entity. Use the following table to learn about National Institute of Standards and Technology (NIST) authenticator types and associated Microsoft Entra authentication methods.

| NIST authenticator type | Microsoft Entra authentication method |
| --- | --- |
| Memorized secret  (something you know) | Password  QR Code (PIN) |
| Look-up secret  (something you have) | None |
| Single-factor out-of-band (something you have) | Microsoft Authenticator app (Push Notification)  Microsoft Authenticator Lite (Push Notification)  Phone (SMS): Not recommended |
| Multi-factor Out-of-band  (something you have + something you know/are) | Microsoft Authenticator app (Phone Sign-In) |
| Single-factor one-time password (OTP)  (something you have) | Microsoft Authenticator app (OTP)  Microsoft Authenticator Lite (OTP)  Single-factor hardware/software OTP^1^ |
| Multi-factor OTP  (something you have + something you know/are) | Treated as single-factor OTP |
| Single-factor crypto software  (something you have) | Single-factor software certificate  Microsoft Entra joined ^2^ with software TPM  Microsoft Entra hybrid joined ^2^ with software TPM  Compliant mobile device^2^ |
| Single-factor crypto hardware  (something you have) | Single-factor hardware protected certificate  Microsoft Entra joined ^2^ with hardware TPM  Microsoft Entra hybrid joined ^2^ with hardware TPM |
| Multi-factor crypto software  (something you have + something you know/are) | Multi-factor software certificate  Windows Hello for Business with software TPM |
| Multi-factor crypto hardware  (something you have + something you know/are) | Multi-factor hardware protected certificate  FIDO 2 security key  Platform SSO for macOS (Secure Enclave)  Windows Hello for Business with hardware TPM  Passkey in Microsoft Authenticator |

^1^ 30-second or 60-second OATH-TOTP SHA-1 token

^2^ For more information on device join states, see [Microsoft Entra device identity](../identity/devices/)

## Public Switch Telephone Network (PSTN) SMS/Voice are not recommended

NIST does not recommend SMS or voice. The risks of device swap, SIM changes, number porting, and other behaviors can cause issues. If these actions are malicious, they can result in an insecure experience. Although SMS/Voice are not recommended, they are better than using only a password, because they require more effort for hackers.
---
layout: Conceptual
title: Microsoft Entra authentication overview - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/overview-authentication
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Authentication is the process of verifying identity before granting access. Learn about the authentication methods available in Microsoft Entra ID.
ms.reviewer: tilarso
ms.topic: concept-article
ms.custom: msecd-doc-authoring-108
ms.date: 2026-04-30T00:00:00.0000000Z
locale: en-us
document_id: 31d311ce-04db-267c-2519-b770e546eac0
document_version_independent_id: c9b9b2c0-32f4-7838-be72-0c26ce483d1c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/overview-authentication.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/overview-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/overview-authentication.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ce2f12f8-506e-b3f5-a708-974ae573b8d2
---

# Microsoft Entra authentication overview - Microsoft Entra ID | Microsoft Learn

Authentication is a security process that verifies a user's identity before granting access to apps, services, devices, or networks.

## Authentication methods supported by Microsoft Entra ID

The following table outlines when an authentication method can be used for primary authentication (first factor), secondary authentication with Microsoft Entra multifactor authentication (MFA), self-service password reset (SSPR), or account recovery.

| Method | Primary authentication | Secondary authentication | SSPR / Account recovery |
| --- | --- | --- | --- |
| [Authenticator Lite](how-to-mfa-authenticator-lite) | No | MFA | No |
| [Certificate-based authentication](concept-certificate-based-authentication) | Yes | MFA | No |
| [Email OTP](concept-sspr-howitworks#authentication-methods) | No | SSPR and sign-in^2^ | SSPR |
| [External MFA](how-to-authentication-external-method-manage) | No | MFA | No |
| [Hardware OATH tokens (preview)](concept-authentication-oath-tokens#hardware-oath-tokens-preview) | No | MFA | SSPR |
| [Microsoft Authenticator passwordless](concept-authentication-authenticator-app#passwordless-sign-in-via-notifications) | Yes | No | No |
| [Microsoft Authenticator push notifications](concept-authentication-authenticator-app#mfa-via-notifications-through-mobile-app) | No | MFA | SSPR |
| [Passkey (FIDO2)](concept-authentication-passkeys-fido2) | Yes | MFA | No |
| [Passkey in Microsoft Authenticator](concept-authentication-authenticator-app) | Yes | MFA | No |
| Password | Yes | No | No |
| [Platform Credential for macOS](concept-authentication-platform-credential-for-macos) | Yes | MFA | No |
| [QR code](concept-authentication-qr-code) | Yes | No | No |
| [SMS sign-in](howto-authentication-sms-signin) | Yes | MFA | SSPR |
| [Software OATH tokens](concept-authentication-oath-tokens#software-oath-tokens) | No | MFA | SSPR |
| [Synced passkey](concept-authentication-passkeys-fido2) | Yes | MFA | No |
| [Temporary Access Pass (TAP)](howto-authentication-temporary-access-pass) | Yes | MFA | No |
| [Verified ID](concept-authentication-verified-id)^3^ | No | No | Account recovery |
| [Voice call](concept-authentication-phone-options) | No | MFA | SSPR |
| [Windows Hello for Business](/en-us/windows/security/identity-protection/hello-for-business/hello-overview) | Yes | MFA^1^ | No |

^1^Windows Hello for Business can serve as a step-up MFA credential if a user is enabled for passkey (FIDO2) and has a passkey registered.

^2^Email OTP is available for tenant members for [self-service password reset (SSPR)](concept-sspr-howitworks#authentication-methods). You can also configure it for [sign-in by guest users](/en-us/entra/external-id/one-time-passcode).

^3^Verified ID is an identity verification capability, not a traditional authentication method. It provides proof of identity for account recovery but can't be used for sign-in, MFA, or SSPR.

## Phishing-resistant authentication methods

While traditional MFA with SMS, email OTP, or authenticator apps significantly improves security over password-only systems, these options introduce friction — requiring additional steps for users, like entering codes, approving push notifications, or using authenticator apps. Moreover, these MFA options are prone to remote phishing attacks. In a remote phishing attack, attackers use social engineering and AI-driven tools to steal identity credentials — like passwords or one-time codes — without physical access to a user's device.

Microsoft recommends using phishing-resistant authentication methods such as Windows Hello for Business, passkeys (FIDO2) and FIDO2 security keys, or certificate-based authentication (CBA) because they provide the most secure sign-in experience.

The following phishing-resistant authentication methods are available in Microsoft Entra ID:

- Windows Hello for Business
- Platform Credential for macOS
- Synced passkeys (FIDO2)
- FIDO2 security keys
- Passkeys in Microsoft Authenticator
- Certificate-based authentication (CBA)

## Verified ID identity verification

Verified ID is an identity verification capability in Microsoft Entra ID — not a traditional authentication method. It can't be used to satisfy authentication requirements like sign-in, MFA, or SSPR. Instead, Verified ID provides cryptographic proof of a user's verified identity for scenarios where trust must be re-established, such as account recovery when all authentication methods are lost.

Identity verification profiles control which users can participate in Verified ID flows, which provider performs verification, and how identity claims are validated. Admins configure profiles through the Account Recovery setup wizard in the Microsoft Entra admin center, and the Verified ID policy page provides visibility into profile assignments and global exclusions.

For more information, see [Verified ID identity verification overview](concept-authentication-verified-id).

## High-assurance account recovery

Account recovery is the process of helping users who have lost all their credentials and can no longer access their account. Traditionally, a user calls the help desk, answers questions to verify their identity, and the help desk resets their credentials. Microsoft Entra ID now supports government-issued ID verification with biometric matching for high-assurance account recovery — removing the need for helpdesk intervention and eliminating social engineering risks.

Organizations can choose from leading identity verification providers (IDV) through the [Microsoft Security Store](https://securitystore.microsoft.com/). These partners offer coverage across 192 countries/regions and remote verification for most government-issued ID documents, including driver's licenses and passports. Microsoft Entra Verified ID Face Check, powered by Azure AI services, verifies proof of presence by matching a user's real-time selfie to the photo from their identity document. Only the match result is shared — no sensitive identity data — which preserves user privacy while providing strong identity assurance.
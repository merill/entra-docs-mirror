---
layout: Conceptual
title: Passkeys (FIDO2) authentication method in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-passkeys-fido2
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about using passkey (FIDO2) authentication in Microsoft Entra ID to help improve and secure sign-in events
ms.topic: concept-article
ms.date: 2026-02-02T00:00:00.0000000Z
ms.reviewer: kimhana
ms.custom: sfi-image-nochange
locale: en-us
document_id: 1c2894e5-9f2c-2581-3f9f-02808d6a6241
document_version_independent_id: 1c2894e5-9f2c-2581-3f9f-02808d6a6241
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-authentication-passkeys-fido2.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-authentication-passkeys-fido2
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-authentication-passkeys-fido2.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: fede46fb-d104-ec55-24a7-8beddec8e0f8
---

# Passkeys (FIDO2) authentication method in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Remote phishing attacks are on the rise. These attacks aim to steal or relay identity proofs—such as passwords, SMS codes, or email one-time passcodes—without physical access to the user’s device. Attackers often use social engineering, credential harvesting, or downgrade techniques to bypass stronger protections like passkeys or security keys. With AI-driven attack toolkits, these threats are becoming more sophisticated and scalable.

Passkeys help prevent remote phishing by replacing phishable methods like passwords, SMS, and email codes. Built on **FIDO (Fast Identity Online) standards**, passkeys use origin-bound public key cryptography, ensuring credentials can't be replayed or shared with malicious actors.

Built on interoperable **FIDO (Fast Identity Online) standards** developed by industry security experts. They use origin-bound public-key cryptography and require local user interaction. Taken together, these characteristics make passkeys almost impossible to phish.

A private key is stored on your device and public key is stored with the app or the website that you sign into. Both unique keys are needed to sign in. This key pair combination is unique, so your passkey only works on the website or the app you created it for.

Every sign-in attempt requires that you're present to unlock the passkey on the device that you use for sign in. Someone can’t trick you to sign in on another device that they control.

In addition to stronger security, passkeys (FIDO2) offer a frictionless sign-in experience by eliminating passwords, reducing prompts, and enabling fast, secure authentication across devices. You can use them to sign in to Microsoft Entra ID or Microsoft Entra hybrid joined Windows 11 devices and get single-sign on to cloud and on-premises resources.

## What are passkeys?

Passkeys are phishing-resistant credentials that provide **strong authentication** and can serve as a **multifactor authentication (MFA)** method when combined with device biometrics or PIN. They also provide verifier impersonation resistance, which ensures an authenticator only releases secrets to the Relying Party (RP) the passkey was registered with and not an attacker pretending to be that RP. Passkeys (FIDO2) follow FIDO2 standards, using WebAuthn for browsers and CTAP for authenticator communication.

The following process is used when a user signs in to Microsoft Entra ID with a passkey (FIDO2):

1. The user initiates sign-in to Microsoft Entra ID.
2. The user selects a passkey:
    - Same device (stored on the device)
    - Cross-device (via QR code) or a FIDO2 security key
3. Microsoft Entra ID sends a challenge (nonce) to the authenticator.
4. The authenticator locates the key pair using the hashed RP ID and credential ID.
5. The user performs a biometric or PIN gesture to unlock the private key.
6. The authenticator signs the challenge with the private key and returns the signature.
7. Microsoft Entra ID verifies the signature using the public key and issues a token.

## Types of passkeys

- **Device-bound passkeys**: The private key is created and stored on a single physical device and never leaves it. Examples:
    - Microsoft Authenticator
    - FIDO2 Security keys
- **Synced passkeys**: The private key is created by the hardware security module (HSM) and encrypted on the local device. This encrypted key is then synced and stored in the cloud passkey provider. Other devices authenticated with the passkey provider may then use the passkey. This may differ depending on the provider. Synced passkeys do not support attestation. Examples:
    - [Apple iCloud Keychain](https://support.apple.com/en-us/102195)
    - [Google Password Manager](https://security.googleblog.com/2022/10/SecurityofPasskeysintheGooglePasswordManager.html)

Synced passkeys offer a seamless and convenient user experience where users can use a device’s native unlock mechanism like face, fingerprint or PIN to authenticate. Based on the learnings from hundreds of millions of consumer users of Microsoft accounts that have registered and are using synced passkeys, we have learned:

- **99% of users successfully register synced passkeys**
- Synced passkeys are **14x faster compared to password and a traditional MFA combination: 3 seconds instead of 69 seconds**
- Users are **3x more successful signing-in with synced passkey than legacy authentication methods (95% vs 30%)**
- Synced passkeys in Microsoft Entra ID bring MFA simplicity at scale for all enterprise users. They're a convenient and low-cost alternative to traditional MFA options like SMS and authenticator apps.

For more information about how to deploy passkeys in your organization, see [How to enable synced passkeys](how-to-authentication-passkeys-fido2).

**Attestation** verifies the authenticity of the passkey provider or device during registration. When enforced:

- It provides cryptographically verifiable device identity through FIDO Metadata Service (MDS). When attestation is enforced, relying parties can validate the authenticator model and apply policy decisions for certified devices.
- Unattested passkeys, including synced passkeys and unattested device-bound passkeys, don't provide device provenance.

In Microsoft Entra ID:

- Attestation can be enforced at the **passkey profile** level.
- If attestation is enabled, only device-bound passkeys are allowed; synced passkeys are excluded.

## Choose the right passkey option

FIDO2 security keys are recommended for highly regulated industries or users with elevated privileges. They provide strong security, but can increase costs for equipment, training, and helpdesk support—especially when users lose their physical keys and need account recovery. Passkeys in the Microsoft Authenticator app are another option for these user groups.

For most users—those outside highly regulated environments or without access to sensitive systems—**synced passkeys** offer a convenient, low-cost alternative to traditional MFA. Apple and Google have implemented advanced protections for passkeys stored in their clouds.

Regardless of type—device-bound or synced—passkeys represent a significant security upgrade over phishable MFA methods.

For more details, see [Get started with phishing-resistant MFA deployment in Microsoft Entra ID](how-to-plan-prerequisites-phishing-resistant-passwordless-authentication).
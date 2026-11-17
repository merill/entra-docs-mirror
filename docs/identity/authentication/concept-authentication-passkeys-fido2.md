---
layout: Conceptual
title: Passkeys (FIDO2) authentication method in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-passkeys-fido2
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: tilarso
ms.author: tilarso
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about using passkey (FIDO2) authentication in Microsoft Entra ID to help improve and secure sign-in events
ms.topic: concept-article
ms.date: 2026-11-10T00:00:00.0000000Z
ms.reviewer: kimhana
ms.custom: sfi-image-nochange, msecd-doc-authoring-108
ai-usage: ai-assisted
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
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
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

## Credential provenance (preview)

Credential provenance records how a passkey was established, including its relationship to identity verification at registration. It's separate from the user's current account verification status and from passkey device or provider attestation.

Note

During preview, credential provenance and credential assurance classification are available only for passkeys. Status and provenance reporting don't provide credential-provenance policy enforcement.

An account can have passkeys with different provenance. Review the passkey involved in an operation rather than treating every credential on the account as equivalent.

On the user's **Authentication methods** page, select a passkey to open its details. The details show **Credential assurance**, registration history, and **Credential provenance** for that credential. A visible assurance label doesn't prove a successful verification ceremony.

The following illustrative example shows **Employee ID** under **Verified with** and **Temporary Access Pass** under **Derived from**. These edited example values aren't evidence of a live verification or registration event.

[![Illustrative screenshot of John Doe's passkey details showing High assurance, Employee ID under Verified with, and Temporary Access Pass under Derived from.](media/concept-authentication-passkeys-fido2/passkey-credential-provenance.png)](media/concept-authentication-passkeys-fido2/passkey-credential-provenance.png#lightbox)

The user's separate **Identity verification** page shows account-level verification status and history. It isn't part of the authentication method details.

Administrators can overwrite credential provenance. An administrative overwrite is separate from the user completing identity verification and doesn't prove a successful verification ceremony. For administrative operations and entitlements, see [Manage identity verification for a user](concept-authentication-methods-manage#manage-identity-verification-for-a-user) and [Identity verification licensing](../../fundamentals/licensing#identity-verification).

Usability is separate from assurance. Method details retain assurance information for an unusable method so that an administrator can investigate it. A displayed assurance label doesn't establish that the passkey can currently sign in or that an access policy will grant access.

If provenance information is missing, don't infer that identity verification succeeded or failed. Check whether the credential and registration path are supported. Missing information isn't the same as a recorded change to a credential's trust context.

For account-level records, see [Identity verification status and history](concept-authentication-methods-manage#identity-verification-status-and-history). For reporting entitlements, see [Identity verification licensing](../../fundamentals/licensing#identity-verification). For investigation guidance, see [Identity verification reporting](howto-authentication-methods-activity#identity-verification-reporting).

### Credential assurance classification (preview)

Credential assurance describes how a passkey is tied to identity verification. Review the classification of the individual passkey rather than treating every credential on a verified account as equivalent.

| Classification | Meaning for passkeys during preview |
| --- | --- |
| **High** | A new passkey is registered through an identity-verified registration journey. Its provenance records identity verification and an intact chain of trust. |
| **Medium** | An existing passkey is used in conjunction with identity verification, rather than a new passkey being registered in the identity-verified journey. |
| **Low** | No identity-verification provenance is recorded for the passkey, or its recorded chain of trust is broken. |

Using an existing passkey with identity verification results in **Medium** assurance. It isn't the same as registering a new **High** assurance passkey through an identity-verified journey.

During preview, this classification and credential provenance apply only to passkeys. An absent classification for another authentication method doesn't establish **Low** assurance. Account-level [identity verification status and history](concept-authentication-methods-manage#identity-verification-status-and-history) are separate from the classification of a particular passkey.

Assurance classification is also separate from device or provider attestation, method usability, and the outcome of a Conditional Access policy. A **High** label doesn't by itself grant access.

### Credential assurance lifecycle

A passkey's assurance can change when its supporting identity verification changes. Expiration or invalidation lowers **High** or **Medium** assurance to **Low**. Successful reverification restores the affected passkey's previous assurance level. These changes apply only to passkeys whose provenance relies on that verification, not every passkey on the account.

Use the following table to distinguish identity verification from credential registration and later changes to trust:

| Event or journey | Effect on passkey assurance |
| --- | --- |
| Identity verification with an existing passkey. | The existing passkey used with identity verification has **Medium** assurance. This isn't a new identity-verified passkey registration. |
| New passkey registration through an identity-verified registration journey. | The new passkey has **High** assurance when its provenance records identity verification and an intact chain of trust. |
| Identity-verified onboarding with new passkey registration. | The new passkey has **High** assurance when registered through the supported identity-verified journey. Completing identity verification alone doesn't establish that passkey registration finished. |
| Identity-verified recovery with replacement passkey registration. | The replacement passkey has **High** assurance when registered through the supported identity-verified journey. Verification history on the account and provenance on the replacement passkey are separate records. |
| Supporting identity verification expires. | Affected **High** and **Medium** assurance passkeys become **Low**. A historical successful verification event doesn't establish that the supporting verification is still valid. |
| Supporting identity verification is invalidated. | Affected **High** and **Medium** assurance passkeys become **Low**. Review the current verification state as well as the passkey's provenance and classification. |
| The user completes reverification. | A previously **High** assurance passkey returns to **High** without new passkey registration. A previously **Medium** assurance passkey returns to **Medium**, not **High**. |

Review individual passkeys after each change. Don't assume that verifying an account gives every existing passkey **High** assurance, or that a change in assurance means a passkey is unusable. For the account-level evidence, see [Identity verification status and history](concept-authentication-methods-manage#identity-verification-status-and-history).
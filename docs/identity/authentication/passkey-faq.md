---
layout: FAQ
title: Passkey FAQs - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/passkey-faq
summary: >
  <p>This article addresses frequently asked questions about passkeys. Keep checking back for updated content.</p>
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Frequently asked questions and answers related to passkeys.
ms.topic: faq
ms.date: 2026-03-26T00:00:00.0000000Z
ms.reviewer: sipower
locale: en-us
document_id: 3e07177a-41e9-afbd-e363-57f8ad57bea3
document_version_independent_id: 3e07177a-41e9-afbd-e363-57f8ad57bea3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/passkey-faq.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/passkey-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/passkey-faq.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 97096079-c4f3-3884-2be1-d1adea256de0
---

# Passkey FAQs - Microsoft Entra ID | Microsoft Learn

This article addresses frequently asked questions about passkeys. Keep checking back for updated content.

## Passkeys in Microsoft Entra FAQ

### When do users get prompted to register a passkey during sign in?

Users might see a passkey registration prompt if:

- A passkey registration campaign (nudge) is enabled, or
- An admin explicitly requires passkey registration through policy, for example by enforcing phishing-resistant MFA with a Conditional Access authentication strength.

### How can admins monitor or audit passkey usage?

Admins can use audit logs, sign in logs, and user notifications to track passkey creation and usage. There is currently no automatic expiration for passkeys, so monitoring and lifecycle hygiene are recommended.

### Are passkeys in Microsoft Entra quantum proof?

Passkeys aren't fully quantum safe today, but Microsoft has a published [roadmap](https://www.microsoft.com/en-us/security/blog/2025/08/20/quantum-safe-security-progress-towards-next-generation-cryptography/) to make Microsoft Entra authentication, including passkeys, quantum safe through post-quantum cryptography, with full transition targeted by 2033.

## Synced passkey FAQs

### What are the benefits of synced passkeys?

Synced passkeys stored in native and third-party passkey providers that already exist on users' devices solve many of the hard issuance and management problems associated with a separate authentication device. The fact that the passkey can sync between the user's client devices and the cloud massively reduces the recoverability and reissuance costs associated with device-bound passkeys. We expect this combination of benefits will make synced passkeys the best option for most users and organizations.

### How can I do a staged rollout of synced passkeys?

You can use passkey profiles to scope the rollout of synced passkeys to select user groups. Microsoft recommends device-bound passkeys for admins and highly privileged users, and synced passkeys for all users with non-admin permissions in your organization.

### As an admin, can I revoke the use of a passkey?

Yes. Admins can use the per-user authentication methods UX or API to delete the passkey from a user's Microsoft Entra ID account.

### What protections are in place to protect user accounts and devices when using synced passkeys?

To register a passkey with a passkey provider, most require two-factor authentication to be set up first. Most passkey providers also require a device lock to be configured before a passkey can be stored on the device. This experience is common across Google password manager and iCloud Keychain but may vary with other passkey providers.

### Can administrators control which devices a synced passkey is available on, or prevent passkeys from being shared?

Today, administrators can't see or control exactly which devices hold a copy of a synced passkey, nor can they query where a synced passkey has been synchronized. This reflects a broader, industry-wide limitation around visibility into credentials that are synchronized across a user’s personal devices. The industry, together with the FIDO Alliance, is actively working on improvements in this area to provide stronger signals and controls for relying parties. Because of this, it’s important to select the appropriate passkey model based on security and compliance requirements: If strict device boundary control is a hard requirement, device-bound passkeys are the recommended option. These credentials are tied to a specific device and don't synchronize elsewhere. For other user populations, synced passkeys are recommended. Synced passkeys provide strong phishing resistance, while many traditional methods offer no device visibility and are susceptible to phishing attacks.

## Authenticator passkey FAQs

### How does Microsoft Authenticator store passkeys on a device?

Authenticator passkeys are backed by hardware.

On iOS, Authenticator stores the private key in the [Secure Enclave](https://support.apple.com/guide/security/secure-enclave-sec59b0b31ff/web).

On Android, Authenticator uses the [Android Keystore system API](https://developer.android.com/privacy-and-security/keystore) to securely store device-bound passkeys. The Android Keystore system supports binding key material to the secure hardware of an Android device, in this order of preference:

- [Secure Element (SE)](https://developer.android.com/privacy-and-security/keystore#StrongBoxKeyMint)
- [Trusted Execution Environment (TEE)](https://source.android.com/docs/security/features/trusty)

On Android, Authenticator only stores a passkey (private key) if the Android device has one of these two secure hardware options. If neither hardware option exists, Authenticator passkey registration fails, even if attestation is disabled.

### Can I restore or sync Authenticator passkeys to a new device?

Authenticator passkeys are only device-bound and can't be synced. For more information, see [Device-bound passkeys in Microsoft Authenticator](/en-us/entra/identity/authentication/concept-authentication-authenticator-app#device-bound-passkey).

### Do I need to enable Bluetooth to perform cross-device authentication?

To use cross-device authentication with passkeys in Authenticator, you must enable Bluetooth and have internet access on both devices.

### Why do cross-device sign-in and registration fail with "Device couldn't connect"?

Make sure both devices have internet access and Bluetooth enabled. For cross-device registration and authentication, users can't use cross-device registration or authentication if you enable attestation.

| Platform | URL |
| --- | --- |
| Android | `cable.ua5v.com` |
| iOS | `cable.auth.com``app-site-association.cdn-apple.com``app-site-association.networking.apple` |

If your organization restricts Bluetooth usage, you can [permit Bluetooth pairing exclusively with passkey-enabled FIDO2 authenticators](/en-us/windows/security/identity-protection/passkeys/?tabs=windows%2Cintune#passkeys-in-bluetooth-restricted-environments) to allow cross-device sign-in and registration of passkeys.

### Can I have multiple passkeys in Authenticator?

You can have only one passkey for each account in Authenticator. At this time, Authenticator only supports passkeys for Microsoft Entra ID.

### Can I use the Authenticator app camera to scan the WebAuthn QR code for registration and authentication?

You can use the Authenticator camera to register and authenticate with passkeys. This option is useful if your organization doesn't push the system camera app to Android Work Profile.

### Can I use passkeys in Authenticator without an internet connection?

You can't use passkeys without an internet connection. For same-device scenarios, the mobile device that contains the passkey needs internet access. For cross-device scenarios, both the device with the passkey and the secondary device where you want to sign in need internet access.

### I tried to register a passkey in the Microsoft Authenticator app but received an error of “Passkey could not be added” or “unknown error”, what should I do?

If you encounter this error, submit feedback from the app by going to the main menu and selecting Send Feedback → Having Trouble. Once submitted, provide the feedback ID so the authentication app logs can be reviewed.

### I'm on an Android 14 device, and I followed all the steps. Why can't I register passkeys in the Authenticator app?

The Authenticator app uses [Android APIs](https://developer.android.com/identity/sign-in/credential-provider) on Android 14 or higher to use passkeys. Manufacturers choose whether or not to implement these APIs for each device they make. If your device doesn't support these APIs, the Authenticator app might not work for your device on Android 14. For the best experience, we recommend that you upgrade to Android 15.

### I stored my passkey in the Microsoft Authenticator app in my Android personal profile and I can't use it in my work profile?

This behavior isn't specific to the Microsoft Authenticator app. Android Work Profile intentionally creates two isolated environments (personal and work), and applications that participate in corporate identity and device security must run inside the work profile container. Because of this isolation model, apps (including Microsoft Authenticator) can't be shared across profiles, and a separate instance is required for the work profile. This is a platform-level security design, not an application choice or limitation.

### Why do I get prompted for PIN instead of biometric sign-in on my Android device?

If biometric sign-in fails on an Android device, the Authenticator app prompts you to enter your PIN instead. The next time you sign in with the passkey, Authenticator continues to request the PIN rather than biometric sign-in. Authenticator periodically retries biometric sign-in. If biometric sign-in succeeds, it's used for subsequent sign-ins.

### What happens to my passkey after I change my PIN or biometric sign-in on my Android device?

Your passkey is invalidated if you change your PIN, or if you change your biometric sign in from thumbprint to face, or vice-versa. If your passkey is invalidated, you need to sign-in by using a different method, and then create a new passkey.

### Can I sign in with a passkey in Authenticator in China?

Passkeys aren't available for Microsoft Azure operated by 21Vianet. On iOS, you can sign in with a passkey in Authenticator to other global organizations, such as while traveling. For more information, see [Download Microsoft Authenticator in China](https://support.microsoft.com/account-billing/download-microsoft-authenticator-in-china-ebbef05c-a429-4236-8570-1bb1900fec35).
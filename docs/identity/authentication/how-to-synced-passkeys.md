---
layout: Conceptual
title: Enable synced passkeys in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-synced-passkeys
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about synced passkeys in Microsoft Entra ID, including how to configure, register, and sign in with synced passkeys.
ms.topic: how-to
ms.date: 2026-07-05T00:00:00.0000000Z
ms.reviewer: kimhana
ms.collection: M365-identity-device-management
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 7836b07f-0963-1f7f-0c07-7032dd7c5b29
document_version_independent_id: 7836b07f-0963-1f7f-0c07-7032dd7c5b29
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-synced-passkeys.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-synced-passkeys
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-synced-passkeys.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3644bfb4-e6df-5d82-ad4f-211fb01ccaa9
---

# Enable synced passkeys in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article provides an overview of synced passkeys in Microsoft Entra ID, including how they work and how to get started. Synced passkeys allow the private key to be created, encrypted, and synced to a cloud passkey provider so it can be used across multiple devices.

## Overview

Synced passkeys are passkeys where the private key is created by the hardware security module (HSM) and encrypted on the local device. The encrypted key is then synced and stored in the cloud passkey provider. Other devices authenticated with the same passkey provider can then use the passkey. Examples of passkey providers include [Apple iCloud Keychain](https://support.apple.com/en-us/102195) and [Google Password Manager](https://security.googleblog.com/2022/10/SecurityofPasskeysintheGooglePasswordManager.html).

Synced passkeys solve many of the issuance and management challenges associated with device-bound passkeys:

- **Recovery**: Because synced passkeys are backed up to the cloud, users don't lose access if they lose a single device.
- **Ease of use**: Users don't need to register a separate passkey on each device. The passkey syncs automatically.
- **Reduced cost**: Organizations don't need to issue and manage separate physical authenticators.

Based on learnings from hundreds of millions of consumer users of Microsoft accounts:

- **99% of users successfully register synced passkeys.**
- Synced passkeys are **14x faster compared to a password and traditional MFA combination: 3 seconds instead of 69 seconds.**
- Users are **3x more successful signing in with a synced passkey than with legacy authentication methods (95% vs 30%).**

Synced passkeys don't support attestation. For most users outside highly regulated environments or without access to sensitive systems, synced passkeys offer a convenient, low-cost alternative to traditional MFA. For admins and highly privileged users, consider device-bound passkeys such as [FIDO2 security keys](how-to-register-passkey-with-security-key) or [passkeys in Microsoft Authenticator](how-to-enable-authenticator-passkey).

For a comparison of passkey types, see [Passkeys (FIDO2) authentication method in Microsoft Entra ID](concept-authentication-passkeys-fido2).

## Prerequisites for synced passkey

- An account with at least [Authentication Policy Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#authentication-policy-administrator) permissions to configure authentication methods.
- You need to [enable passkey sign-in](how-to-authentication-passkeys-fido2#enable-passkey-profiles) in the **Passkey (FIDO2)** policy in **Authentication methods** in the Microsoft Entra admin center.
- The following table outlines the minimum device requirements for using synced passkeys. The columns represent the device platform where the user signs in.

    | Passkey provider | Windows | macOS | iOS | Android |
    | --- | --- | --- | --- | --- |
    | Apple Passwords (also called iCloud Keychain) | N/A | Natively built in.macOS 13+ | Natively built in.iOS 16+ | N/A |
    | Google Password Manager | Built into Chrome | Built into Chrome | Built into Chrome.iOS 17+ | Natively built in (excluding Samsung devices).Android 9+ |
    | Other passkey providers (such as 1Password, Bitwarden) | Check for a browser extension | Check for a browser extension | Check for an app.iOS 17+ | Check for an app.Android 14+ |

## Configure a profile for synced passkeys

1. Sign in to the Microsoft Entra admin center as at least an [Authentication Policy Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#authentication-policy-administrator).
2. Browse to **Entra ID** &gt; **Authentication methods**.
3. On the **Authentication methods | Policies** page, select **Passkey (FIDO2)** &gt; **Configure**.
4. Make sure **Allow self-service setup** is selected.
5. Select **+ Add profile**.
6. Provide a name and for **Passkey types**, select **Synced** and **Save**.

    [![Screenshot that shows how to add a synced passkey profile.](media/how-to-authentication-passkey-profiles/synced-passkey-profile.png)](media/how-to-authentication-passkey-profiles/synced-passkey-profile.png#lightbox)

    Note

    If you disable synced passkeys for a given passkey profile, targeted users can't sign in with a synced passkey even if they already registered one.

## Enable and target groups for a profile for synced passkeys

1. Sign in to the Microsoft Entra admin center as at least an [Authentication Policy Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#authentication-policy-administrator).
2. Browse to **Entra ID** &gt; **Authentication methods**.
3. On the **Authentication methods | Policies** page, select **Passkey (FIDO2)** &gt; **Enable and target**.
4. On the **Enable and Target** tab, make sure **Enable** is **On**.
5. Select **Add target**, and choose **All users** or **Select targets** to choose specific groups.

    [![Screenshot that shows how to add a target for a passkey profile.](media/how-to-authentication-passkey-profiles/add-target.png)](media/how-to-authentication-passkey-profiles/add-target.png#lightbox)
6. Select the profile for synced passkeys, and select **Save**.

    [![Screenshot that shows how to enable a synced passkey profile.](media/how-to-authentication-passkey-profiles/enable-target-synced.png)](media/how-to-authentication-passkey-profiles/enable-target-synced.png#lightbox)

    Note

    A target group (for example, Engineering) can be scoped for multiple passkey profiles. When a user is scoped for multiple passkey profiles, registration and authentication with a passkey are allowed if the passkey fully satisfies the requirements of at least one of the scoped passkey profiles. There's no particular order to the check. If a user is a member of an excluded group in the **Passkey (FIDO2)** policy, they're blocked from passkey (FIDO2) registration or sign-in entirely. The block takes precedence over membership in any included groups.
7. Select **Save** to enable synced passkeys for the selected users.

## Register a synced passkey

After an admin enables synced passkeys, users can register a passkey on their device. The passkey syncs to other devices through the user's passkey provider (such as iCloud Keychain, Google Password Manager, or a third-party provider).

For registration steps, see [Register a synced passkey (FIDO2)](how-to-register-passkey).

## Sign in with a synced passkey

After registration, users can sign in to Microsoft Entra ID by using the synced passkey on any device where the passkey is available.

For sign-in steps, see [Sign in with a synced passkey (FIDO2)](how-to-sign-in-passkey).
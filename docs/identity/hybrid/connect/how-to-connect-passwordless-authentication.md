---
layout: Conceptual
title: Sign in to Microsoft Entra Connect Sync by using passwordless authentication - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-passwordless-authentication
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Learn how to sign in to Microsoft Entra Connect Sync by using passwordless authentication methods such as FIDO2 security keys and passkeys.
ms.subservice: hybrid-connect
ms.topic: how-to
ms.custom: msecd-doc-authoring-1013
ms.date: 2026-06-15T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 6c1c300d-b1a0-def0-e6b6-49218b075c1d
document_version_independent_id: 6c1c300d-b1a0-def0-e6b6-49218b075c1d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-passwordless-authentication.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-passwordless-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-passwordless-authentication.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7b7249e1-19b8-e761-6b59-aa06901081e6
---

# Sign in to Microsoft Entra Connect Sync by using passwordless authentication - Microsoft Entra ID | Microsoft Learn

Passwordless authentication for Microsoft Entra Connect Sync lets administrators sign in with secure, modern credentials (such as FIDO2 security keys, passkeys, or Windows Hello) instead of typing a password.

This article shows you how to enable passwordless authentication methods in Microsoft Entra ID, register a credential, turn on passwordless sign-in for Microsoft Entra Connect Sync, and verify that you can sign in without a password. You can choose from the following passwordless methods:

- **FIDO2 security keys**: Insert a USB or NFC key (for example, a YubiKey), enter a PIN, and tap the key.
- **Passkeys**: Use a platform-stored credential (for example, an iCloud Keychain or Android passkey) through the system browser or a device prompt.

## Prerequisites

- A Microsoft Entra account with the **Hybrid Administrator** or **Global Administrator** role.
- A FIDO2 security key, such as a YubiKey.
- Windows Server 2022 or later.

## Enable passwordless authentication methods in Microsoft Entra ID

Before you can register a passwordless credential, enable the passkey or FIDO2 authentication method for your account in Microsoft Entra ID.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Authentication methods** &gt; **Policies**.
3. Select **Passkey (FIDO2)**.
4. Set the method to **Enabled**, and target **All users** or a specific group that contains your administrator account.

    [![Screenshot of the Authentication methods Policies page in the Microsoft Entra admin center with Passkey (FIDO2) enabled for all users.](media/how-to-connect-passwordless-authentication/authentication-methods-policies.png)](media/how-to-connect-passwordless-authentication/authentication-methods-policies.png#lightbox)

## Register a passwordless credential

After the authentication method is enabled, register the credential that you want to use to sign in. You can register a passkey, a security key, or both.

### Register a passkey

Register a passkey that's stored on your device or password manager:

1. Go to [Security info](https://mysignins.microsoft.com/security-info) and sign in with your administrator account.
2. Select **Add sign-in method**.
3. Select **Passkey**.
4. Follow the prompts to create the passkey with your device, such as Windows Hello, Face ID, Touch ID, or a synced password manager.

After registration finishes, the new passkey appears under your registered sign-in methods.

### Register a security key

Register your FIDO2 security key, such as a YubiKey:

1. Go to [Security info](https://mysignins.microsoft.com/security-info) and sign in with your administrator account.
2. Select **Add sign-in method**.
3. Select **Security key**.
4. Select **USB device**.
5. Insert your YubiKey, and then touch it when it blinks.
6. Set a PIN if you're prompted, and then touch the key again to finish registration.

## Turn on passwordless authentication for Microsoft Entra Connect Sync

To make passwordless sign-in available in the installation wizard, install Microsoft Entra Connect Sync and set a registry key.

1. Install Microsoft Entra Connect Sync. For installation steps, see [Get started with Microsoft Entra Connect Sync by using express settings](how-to-connect-install-express).
2. On the server, open PowerShell and run the following command to enable passwordless authentication:

    ```powershell
    # Enable passwordless authentication
    New-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Azure AD Connect" -Name "EnablePasswordlessAuth" -Value 1 -PropertyType DWORD -Force
    ```

## Sign in to Microsoft Entra Connect Sync without a password

After passwordless authentication is enabled, use your passkey or security key to sign in when you run the installer.

1. Run the Microsoft Entra Connect Sync installer. When you're prompted to sign in to Microsoft Entra ID, select **Sign-in options**.

    [![Screenshot of the Microsoft sign-in window with Sign-in options available below the sign-in dialog.](media/how-to-connect-passwordless-authentication/sign-in-options.png)](media/how-to-connect-passwordless-authentication/sign-in-options.png#lightbox)
2. Select **Face, fingerprint, PIN or security key**, and then complete the prompt with the passkey or security key that you registered.

    [![Screenshot of the Sign-in options screen with Face, fingerprint, PIN or security key selected.](media/how-to-connect-passwordless-authentication/face-fingerprint-pin-security-key.png)](media/how-to-connect-passwordless-authentication/face-fingerprint-pin-security-key.png#lightbox)

When sign-in succeeds, you're signed in to Microsoft Entra Connect Sync without entering a password. The same steps apply whether you sign in with a passkey or a security key.

## Disable passwordless authentication

To turn off passwordless authentication and return to signing in with a username and password, set the registry value to `0`.

1. On the server, open PowerShell and run the following command to disable passwordless authentication:

    ```powershell
    # Disable passwordless authentication
    Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Azure AD Connect" -Name "EnablePasswordlessAuth" -Value 0
    ```
2. Run the Microsoft Entra Connect Sync installer again. The passwordless sign-in option is no longer available, and you can sign in with your username and password.
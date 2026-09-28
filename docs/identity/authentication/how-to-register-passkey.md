---
layout: Conceptual
title: Register a synced passkey (FIDO2) - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-register-passkey
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how to register a synced passkey (FIDO2) as an authentication method on Windows, iOS, or Android by using a browser for phishing-resistant sign-in.
ms.topic: how-to
ms.date: 2026-07-05T00:00:00.0000000Z
ms.reviewer: kimhana, calui, tilarso
ms.collection: M365-identity-device-management
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 5b8f13ce-ddec-084f-7de6-d57a4a97af6a
document_version_independent_id: 5b8f13ce-ddec-084f-7de6-d57a4a97af6a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-register-passkey.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-register-passkey
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-register-passkey.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: b9e7a5a7-0c13-a7ea-bb9f-07a58a771900
---

# Register a synced passkey (FIDO2) - Microsoft Entra ID | Microsoft Learn

This article shows how users can register a synced passkey (FIDO2) by using the **Passkey** flow. A synced passkey is stored in a passkey provider (such as iCloud Keychain or Google Password Manager) and syncs across the user's devices. For an overview of synced passkeys, see [Synced passkeys in Microsoft Entra ID](how-to-synced-passkeys).

Note

Looking to provide passkeys (FIDO2) on behalf of users? Use our [APIs](https://aka.ms/passkeyprovision).

## Prerequisites

You need to configure a password manager on your mobile device to save a synced passkey.

- On your iOS device, you need to set **Set Up Codes In** to **Passwords** to manage synced passkeys. Open **Settings** &gt; **General** &gt; **AutoFill & Passwords**. For **Set Up Codes In**, select **Passwords**.
- On your Android device, open **Settings** &gt; **Security and privacy** &gt; **More security settings** &gt; **Passwords, passkeys, and autofill**, and then select a provider.

## Register a passkey

To register a passkey on your device, follow these steps:

1. Open a web browser and sign in to [Security info](https://mysignins.microsoft.com/security-info).
2. Sign in with multifactor authentication (MFA).
3. Tap **+ Add sign-in method**.

    [![Screenshot of the Security info page on iOS showing the Add sign-in method option.](media/how-to-register-passkey/add-sign-in-method-ios.png)](media/how-to-register-passkey/add-sign-in-method-ios.png#lightbox)
4. Tap **Passkey**.

    [![Screenshot of the Add a sign-in method page on iOS showing the Passkey option.](media/how-to-register-passkey/choose-passkey-ios.png)](media/how-to-register-passkey/choose-passkey-ios.png#lightbox)
5. Tap **Next**.

    [![Screenshot of the Sign in faster with your face, fingerprint, or PIN page on iOS showing the Next option.](media/how-to-register-passkey/sign-in-faster-ios.png)](media/how-to-register-passkey/sign-in-faster-ios.png#lightbox)
6. On iOS, tap **Next**.

    [![Screenshot of the Setting up your passkey page on iOS showing the Next option.](media/how-to-register-passkey/setting-up-passkey-ios.png)](media/how-to-register-passkey/setting-up-passkey-ios.png#lightbox)

    On Android, tap **Continue**.

    Note

    The steps to enable passkey providers on Android might vary based on the make and model of your device. Search for Passkey on your device settings, or consult your device manufacturer for guidance. If your device runs Android 14 and you can't enable Authenticator as a passkey provider, we recommend that you upgrade to Android 15.

    [![Screenshot of the Create a passkey page on Android showing the account name and Continue option.](media/how-to-register-passkey/android-complete.png)](media/how-to-register-passkey/android-complete.png#lightbox)
7. Name your passkey and tap **Next**.

    [![Screenshot of the Let's name your passkey page showing the passkey name field and Next option.](media/how-to-register-passkey/name-passkey.png)](media/how-to-register-passkey/name-passkey.png#lightbox)
8. After the passkey is created, tap **Done**.

    [![Screenshot of the Passkey created page showing the Done option.](media/how-to-register-passkey/passkey-created-ios.png)](media/how-to-register-passkey/passkey-created-ios.png#lightbox)
9. You can see your passkey in [Security info](https://mysignins.microsoft.com/security-info).

    [![Screenshot of the Security info page showing the registered passkey.](media/how-to-register-passkey/passkey-added-ios.png)](media/how-to-register-passkey/passkey-added-ios.png#lightbox)
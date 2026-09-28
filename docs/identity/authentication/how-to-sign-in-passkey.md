---
layout: Conceptual
title: Sign in with a synced passkey (FIDO2) - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-sign-in-passkey
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how to sign in to Microsoft Entra ID with a synced passkey (FIDO2) for your work or school account by using a browser on Windows, iOS, or Android.
ms.topic: how-to
ms.date: 2026-07-05T00:00:00.0000000Z
ms.reviewer: kimhana
ms.collection: M365-identity-device-management
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: f0702fc3-5f08-0655-d3eb-4104f8e6676f
document_version_independent_id: f0702fc3-5f08-0655-d3eb-4104f8e6676f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-sign-in-passkey.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-sign-in-passkey
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-sign-in-passkey.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: acc5bb6d-59bf-4dcf-d96e-42e0ea3650c0
---

# Sign in with a synced passkey (FIDO2) - Microsoft Entra ID | Microsoft Learn

This article describes how to sign in to your work or school account with a synced passkey.

Your passkey can be synced to the same device where you want to sign in, or it can be synced to another device.

- Use a passkey from the same device
- Use a passkey from another device

## Use a passkey from the same device

1. Select **Sign in** for a Microsoft application or website such as the [Azure portal](https://ms.portal.azure.com/).
2. If you most recently used a passkey to sign in, you're automatically prompted to sign in with a passkey. Choose your account.

    [![Screenshot that shows the Pick an account dialog with a work or school account.](media/how-to-sign-in-passkey/choose-synced-passkey-account.png)](media/how-to-sign-in-passkey/choose-synced-passkey-account.png#lightbox)

    Otherwise, you can enter your username and select **Next** to sign in.

    [![Screenshot that shows the Sign in dialog with a username entered and the Next button.](media/how-to-sign-in-passkey/sign-in-options-name.png)](media/how-to-sign-in-passkey/sign-in-options-name.png#lightbox)
3. Complete multifactor authentication (MFA).
4. You're signed in with your work or school account.

## Use a passkey from another device

1. Select **Sign in** for a Microsoft application or website such as the [Azure portal](https://ms.portal.azure.com/).
2. In Microsoft Edge, right-click where you enter your name, select **Use passkey from another device** &gt; **Use a phone, tablet or security key**.

    [![Screenshots that show the Use passkey from another device option in Microsoft Edge and the Use a phone, tablet or security key option in the Sign in using a saved passkey dialog.](media/how-to-sign-in-passkey/use-passkey-from-another-device-edge.png)](media/how-to-sign-in-passkey/use-passkey-from-another-device-edge.png#lightbox)

    In Google Chrome, select where you enter your name, then select **Use passkey from another device**.

    [![Screenshot that shows the Use passkey from another device option in the Chrome account list.](media/how-to-sign-in-passkey/use-passkey-on-another-device-chrome.png)](media/how-to-sign-in-passkey/use-passkey-on-another-device-chrome.png#lightbox)

    You can also click **Sign in**, select **Sign-in options** &gt; **Face, fingerprint, PIN or security key**.

    ![Screenshots that show the Sign-in options button and the Face, fingerprint, PIN or security key option.](media/how-to-sign-in-passkey/sign-in-options-combined.png)
3. Select **iPhone, iPad, or Android device**. The other sign-in options that are shown vary depending on your account and device.

    [![Screenshot that shows the iPhone, iPad, or Android device option in the Choose a passkey dialog.](media/how-to-sign-in-passkey/sign-in-options-device.png)](media/how-to-sign-in-passkey/sign-in-options-device.png#lightbox)
4. The device where you want to sign in shows a QR code. Scan the QR code with the other device that has your passkey.

    [![Screenshot that shows the Sign in with a passkey dialog with a QR code to scan.](media/how-to-sign-in-passkey/scan-code-no-name.png)](media/how-to-sign-in-passkey/scan-code-no-name.png#lightbox)
5. On iOS, select **Sign in with passkey**. On Android, select **Use passkey to sign in**.
6. Bluetooth and an internet connection are required for this step and must be enabled on both devices. The device where you want to sign in shows this screen:

    [![Screenshot that shows the Sign in with a passkey dialog with a Device connected message.](media/how-to-sign-in-passkey/device-connected.png)](media/how-to-sign-in-passkey/device-connected.png#lightbox)
7. Complete multifactor authentication (MFA).
8. You're signed in with the synced passkey for your work or school account.

## Known issues

Review the following known issues to avoid problems with synced passkey sign-in.

### Bluetooth must be enabled on both devices for cross-device authentication

If you're signing in by using a different mobile device, Bluetooth must be enabled on the device you're trying to sign in on and the mobile device with the passkey.

Some organizations restrict Bluetooth usage, which includes the use of passkeys. In such cases, organizations can allow passkeys by permitting Bluetooth pairing exclusively with passkey-enabled FIDO2 authenticators. For more information, see [Passkeys in Bluetooth-restricted environments](/en-us/windows/security/identity-protection/passkeys/?tabs=intune#passkeys-in-bluetooth-restricted-environments).

### Orphaned passkey

An orphaned passkey occurs when a passkey remains on a user's device but is no longer registered with Microsoft Entra ID. This typically happens if the passkey was deleted from a user's Security info or removed due to policy changes, but the local credential wasn't cleaned up.

If you're blocked from sign-in by an orphaned passkey:

1. Remove the orphaned passkey from the device or passkey provider.
2. Re-register a new passkey after cleanup.
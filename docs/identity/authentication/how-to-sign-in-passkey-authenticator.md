---
layout: Conceptual
title: Sign in with passkeys in Authenticator for Android and iOS devices - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-sign-in-passkey-authenticator
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how to sign in with passkeys in Microsoft Authenticator for Android and iOS. Use same-device, cross-device, or native app authentication.
ms.topic: how-to
ms.date: 2026-07-05T00:00:00.0000000Z
ms.reviewer: mjsantani, calui
ms.collection: M365-identity-device-management
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: e251214c-f2d6-3167-ec55-1959714ea1c6
document_version_independent_id: e251214c-f2d6-3167-ec55-1959714ea1c6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-sign-in-passkey-authenticator.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-sign-in-passkey-authenticator
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-sign-in-passkey-authenticator.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/2624a017-7337-44fa-9494-a407bb0e59fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/a438284e-c3c3-4c36-ab0b-aa7c244b912c
platformId: 86580968-024d-f307-e768-5eefa16d205e
---

# Sign in with passkeys in Authenticator for Android and iOS devices - Microsoft Entra ID | Microsoft Learn

This article explains the sign-in experience when you use passkeys in Authenticator with Microsoft Entra ID. For more information about the availability of Microsoft Entra ID passkey (FIDO2) authentication across native applications, web browsers, and operating systems, see [Support for FIDO2 authentication with Microsoft Entra ID](concept-fido2-compatibility).

# [iOS](#tab/iOS)
To sign in with a passkey in Authenticator, your iOS device needs to run iOS 17 or later.

### Same-device authentication in a browser (iOS)

Follow these steps to sign in to Microsoft Entra ID with a passkey in Authenticator on your iOS device.

1. On your iOS device, open your browser and go to the resource you're trying to access, such as [Office](https://www.office.com).
2. Enter your username to sign in. If you most recently used a passkey to sign in, you're prompted to sign in with a passkey. Otherwise, select **Other ways to sign in**, and then select **Face, fingerprint, PIN or security key**.

    Alternatively, select **Sign-in options** to sign in without entering a username. If you selected **Sign-in options**, then select **Face, fingerprint, PIN or security key**. Otherwise, skip to the next step.

    Note

    If you try to sign in without a username and multiple passkeys are saved to your device, you're prompted to choose which passkey to use for sign-in.
3. To select your passkey, follow the steps in the iOS operating system dialog. Verify yourself by using Face ID or Touch ID, or by entering your device PIN.

You're now signed in to Microsoft Entra ID.

### Cross-device authentication (iOS)

Follow these steps to sign in to Microsoft Entra ID on another device with a passkey in Authenticator on your iOS device.

This sign-in option requires Bluetooth and an internet connection for both devices. If your organization restricts Bluetooth usage, an administrator can allow cross-device sign-in for passkeys by permitting Bluetooth pairing exclusively with passkey-enabled FIDO2 authenticators. For more information about how to configure Bluetooth usage only for passkeys, see [Passkeys in Bluetooth-restricted environments](/en-us/windows/security/identity-protection/passkeys/?tabs=windows%2Cintune#passkeys-in-bluetooth-restricted-environments).

1. On the other device where you want to sign in to Microsoft Entra ID, go to the resource you're trying to access, such as [Office](https://www.office.com).
2. Enter your username to sign in. If you last used a passkey to authenticate, you're prompted to authenticate with a passkey. Otherwise, select **Other ways to sign in**, and then select **Face, fingerprint, PIN or security key**.

    Alternatively, select **Sign-in options** to sign in without entering a username. If you selected **Sign-in options**, then select **Face, fingerprint, PIN or security key**. Otherwise, skip to the next step.

    Note

    If you try to sign in without a username and multiple passkeys are saved to your device, you're prompted to choose which passkey to use for sign-in.
3. To begin cross-device authentication, follow the steps in the operating system or browser prompt. On Windows 11 23H2 or later, select **iPhone, iPad, or Android device**.
4. When a QR code appears on the screen, open the camera app and scan the QR code.

    The camera inside the iOS Authenticator app doesn't support scanning a WebAuthn QR code. You need to use the system camera app.
5. Select **Sign in with passkey** when the option appears.

    Bluetooth and an internet connection are required for this step and must both be enabled on your mobile and remote device.
6. To select your passkey, follow the steps in the iOS operating system dialog. Verify yourself by using Face ID or Touch ID, or by entering your device PIN.

You're now signed in to Microsoft Entra ID on your other device.

### Same-device authentication in native Microsoft applications (iOS)

You can use Authenticator on your iOS device to seamlessly sign in with a passkey to other Microsoft apps, such as OneDrive, SharePoint, and Outlook.

# [Android](#tab/Android)
To sign in with a passkey in Authenticator, your Android device needs to run Android 14 or later.

### Same-device authentication in a browser (Android)

Follow these steps to sign in to Microsoft Entra ID with a passkey in Authenticator on your Android device.

Note

Support for same-device authentication in Microsoft Edge on Android is coming soon.

1. On your Android device, open your browser and go to the resource you want to access, such as [Office](https://www.office.com).
2. Enter your username to sign in. If you most recently used a passkey to sign in, you're prompted to sign in with a passkey. Otherwise, select **Other ways to sign in**, and then select **Face, fingerprint, PIN or security key**.

    Alternatively, select **Sign-in options** to sign in without entering a username. If you selected **Sign-in options**, then select **Face, fingerprint, PIN or security key**. Otherwise, skip to the next step.

    Note

    If you try to sign in without a username and multiple passkeys are saved to your device, you're prompted to choose which passkey to use for sign-in.
3. To select your passkey, follow the steps in the Android operating system dialog. Verify yourself by scanning your face or fingerprint, or by entering your device PIN or unlock gesture.

You're now signed in to Microsoft Entra ID.

### Cross-device authentication (Android)

Follow these steps to sign in to Microsoft Entra ID on another device with a passkey in Authenticator on your Android device.

This sign-in option requires Bluetooth and an internet connection for both devices. If your organization restricts Bluetooth usage, an administrator can allow cross-device sign-in for passkeys by permitting Bluetooth pairing exclusively with passkey-enabled FIDO2 authenticators. For more information about how to configure Bluetooth usage only for passkeys, see [Passkeys in Bluetooth-restricted environments](/en-us/windows/security/identity-protection/passkeys/?tabs=windows%2Cintune#passkeys-in-bluetooth-restricted-environments).

1. On the other device where you want to sign in to Microsoft Entra ID, go to the resource you're trying to access, such as [Office](https://www.office.com).
2. Enter your username to sign in. If you last used a passkey to authenticate, you're prompted to authenticate with a passkey. Otherwise, select **Other ways to sign in**, and then select **Face, fingerprint, PIN or security key**.

    Alternatively, select **Sign-in options** to sign in without having to enter a username. If you selected **Sign-in options**, then select **Face, fingerprint, PIN or security key**. Otherwise, skip to the next step.
3. To begin cross-device authentication, follow the steps in the operating system or browser prompt. On Windows 11 23H2 or later, select **iPhone, iPad, or Android device**.
4. When a QR code appears on the screen, open the camera app and scan the QR code. You can also use the camera in Authenticator. Go to the passkey account tile and tap it. Under **Passkey details**, you can see a button in the lower-right corner to scan the QR code.

    Note

    Bluetooth and an internet connection are required for this step and both must be enabled on your mobile and remote device.
5. To select your passkey, follow the steps in the Android operating system dialog. Verify yourself by scanning your face or fingerprint, or enter your device PIN or unlock gesture.

On your other device, you're now signed in to Microsoft Entra ID.

### Same-device authentication in native Microsoft applications (Android)

You can use Authenticator on your Android device to seamlessly sign in with a passkey to other Microsoft apps, such as OneDrive, SharePoint, and Outlook.

---
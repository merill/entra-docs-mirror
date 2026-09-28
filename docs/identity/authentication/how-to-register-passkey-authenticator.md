---
layout: Conceptual
title: Register passkeys in Authenticator on Android and iOS devices - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-register-passkey-authenticator
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how to register passkeys in Microsoft Authenticator on Android and iOS. Sign in to the app, use Security info, or register cross-device.
ms.topic: how-to
ms.date: 2026-07-05T00:00:00.0000000Z
ms.reviewer: hanki77, tilarso
ms.collection: M365-identity-device-management
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: bf0a2fcb-d5f4-6916-eb36-e84776a8b6c4
document_version_independent_id: bf0a2fcb-d5f4-6916-eb36-e84776a8b6c4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-register-passkey-authenticator.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-register-passkey-authenticator
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-register-passkey-authenticator.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 835c2960-7147-782f-4570-cf55c5790968
---

# Register passkeys in Authenticator on Android and iOS devices - Microsoft Entra ID | Microsoft Learn

This article shows how to register a passkey in Microsoft Authenticator on your iOS or Android device.

# [iOS](#tab/iOS)
You can register by signing in to the Authenticator app directly, by using [Security info](https://aka.ms/mysecurityinfo), or from your mobile device browser or through cross-device registration by using another device, such as a laptop. Your mobile device needs to run iOS version 17 or later.

- Use Authenticator (iOS)
- Use Security info (iOS)
- Use WebAuthn flow (iOS)

### Use Authenticator (iOS)

You can sign in to Authenticator to create a passkey in the app and get seamless single sign-on across Microsoft native apps. **This flow is the recommended way to set up a passkey in Authenticator.** If you're signed in or already have an account in Authenticator, you still need to complete these steps to add a passkey in Authenticator.

1. Download Authenticator from the App Store, and go through the privacy screens.
2. Add your account in Authenticator on your iOS device:

If you installed Authenticator for the first time on your device, on the **Secure Your Digital Life** screen, tap **Add work or school account**.

[![Screenshot that shows the first screen to appear for Authenticator for iOS devices.](media/howto-register-passwordless-passkey-direct-ios/ios-first-run.png)](media/howto-register-passwordless-passkey-direct-ios/ios-first-run.png#lightbox)

If you installed Authenticator on your device but you didn't add an account, tap **Add account** or the **+** button, and select **Work or school account**. Then tap **Sign in**.

[![Screenshot that shows how to register by using Authenticator for iOS devices.](media/howto-register-passwordless-passkey-direct-ios/add-account-ios.png)](media/howto-register-passwordless-passkey-direct-ios/add-account-ios.png#lightbox)

If you already added an account in Authenticator, tap your account, and then tap **Create a passkey**.

[![Screenshot that shows how to create a passkey in Authenticator for iOS devices.](media/howto-register-passwordless-passkey-direct-ios/ios-create-passkey.png)](media/howto-register-passwordless-passkey-direct-ios/ios-create-passkey.png#lightbox)
3. Complete multifactor authentication (MFA).
4. If necessary, tap **Settings** and set up a screen lock.

    ![Screenshot that shows how to set up a screen lock for a passkey in Authenticator for Android devices.](media/howto-register-passwordless-passkey-direct-android/android-lock-screen-required.png)
5. Tap **Settings** to enable Authenticator as a passkey provider.

    ![Screenshot that shows opening Settings to follow the onscreen instructions by using Authenticator for iOS devices.](media/howto-register-passwordless-passkey-direct-ios/passkey-provider-ios.png)
6. On your iOS 18 device, go to **Settings** &gt; **General** &gt; **Autofill & Passwords**. On your iOS 17 device, go to **Settings** &gt; **Passwords** &gt; **Password Options**.

    On both operating systems, make sure that **AutoFill Passwords and Passkeys** is turned on. Under **Autofill From**, make sure that **Authenticator** is selected.

    ![Screenshot that shows the turn-on passkey support option in Authenticator for iOS devices.](media/howto-authenticate-passwordless-passkey-ios/password-options-three.png)
7. After you return to Authenticator, tap **Done** to confirm that you added Authenticator as a passkey provider. Then you can see **Passkey** added as a sign-in method for your account. Tap **Done** again to finish.

    ![Screenshot that shows an account added to Authenticator for Android devices.](media/howto-register-passwordless-passkey-direct-android/android-account-added.png)

    Authenticator sets up passkey, passwordless, and MFA for sign-in according to your work or school account policies. Tap your account to see information, including your new passkey.

### Use Security info (iOS)

1. On the same iOS device as the Authenticator or by using another device, such as a laptop, open a web browser and sign in with MFA to [Security info](https://mysignins.microsoft.com/security-info).
2. On **Security info**, tap **+ Add sign-in method** and select **Passkey in Microsoft Authenticator**.

    ![Screenshot that shows how to select passkey in Authenticator as a sign-in method.](media/howto-authenticate-passwordless-passkey-ios/select-passkey-in-authenticator.png)
3. If you're asked to sign in with MFA, select **Next**.
4. If necessary, download Authenticator to your iOS device. You can select [Microsoft Authenticator](https://www.microsoft.com/security/mobile-authenticator-app) and scan a QR code to install Authenticator from the iOS App Store. After you download Authenticator, tap **Next**.

    ![Screenshot that gives users an option to download Authenticator.](media/howto-authenticate-passwordless-passkey-ios/download-authenticator-laptop.png)
5. You're prompted to open the Authenticator app and create your passkey there. Open Authenticator and go through the privacy screens as needed.

    ![Screenshot that shows the wizard used to complete the passkey setup in Authenticator.](media/howto-authenticate-passwordless-passkey-ios/complete-setup-in-authenticator.png)
6. Add your account in Authenticator on your iOS device.

If you installed Authenticator for the first time on your device, on the **Secure Your Digital Life** screen, tap **Add work or school account**.

[![Screenshot that shows the first screen to appear for Authenticator for iOS devices.](media/howto-register-passwordless-passkey-direct-ios/ios-first-run.png)](media/howto-register-passwordless-passkey-direct-ios/ios-first-run.png#lightbox)

If you installed Authenticator on your device before but didn't add an account, tap **Add account** or the **+** button, and select **Work or school account**. Then tap **Sign in**.

[![Screenshot that shows how to register by using Authenticator for iOS devices.](media/howto-register-passwordless-passkey-direct-ios/add-account-ios.png)](media/howto-register-passwordless-passkey-direct-ios/add-account-ios.png#lightbox)

If you already added an account in Authenticator, tap your account, and then tap **Create a passkey**.

[![Screenshot that shows how to create a passkey in Authenticator for iOS devices.](media/howto-register-passwordless-passkey-direct-ios/ios-create-passkey.png)](media/howto-register-passwordless-passkey-direct-ios/ios-create-passkey.png#lightbox)
7. Complete multifactor authentication (MFA).
8. If necessary, tap **Settings** and set up a screen lock.

    ![Screenshot that shows how to set up a screen lock for a passkey in Authenticator for Android devices.](media/howto-register-passwordless-passkey-direct-android/android-lock-screen-required.png)
9. Tap **Settings** to enable Authenticator as a passkey provider.
10. On your iOS 18 device, go to **Settings** &gt; **General** &gt; **Autofill & Passwords**. On your iOS 17 device, go to **Settings** &gt; **Passwords** &gt; **Password Options**.

    On both operating systems, make sure that **AutoFill Passwords and Passkeys** is turned on. Under **Autofill From**, make sure that **Authenticator** is selected.

    ![Screenshot that shows the turn-on passkey support option in Authenticator for iOS devices.](media/howto-authenticate-passwordless-passkey-ios/password-options-three.png)
11. After you return to Authenticator, tap **Done** to confirm that you added Authenticator as a passkey provider. Then you can see **Passkey** added as a sign-in method for your account. Tap **Done** again to finish.

    ![Screenshot that shows an account added to Authenticator for Android devices.](media/howto-register-passwordless-passkey-direct-android/android-account-added.png)

    Authenticator sets up passkey, passwordless, and MFA for sign-in according to your work or school account policies.
12. Return to your browser after you finish the passkey setup in Authenticator, and select **Next**.

    ![Screenshot that shows returning to the wizard to finish the passkey setup in Authenticator.](media/howto-authenticate-passwordless-passkey-ios/after-setup-in-authenticator.png)
13. The wizard verifies that the passkey was created in Authenticator.

    ![Screenshot that shows the wizard that verifies the passkey in Authenticator.](media/howto-authenticate-passwordless-passkey-ios/verifying-passkey.png)
14. After the passkey is created, select **Done**.

    ![Screenshot that confirms that the passkey was created.](media/howto-authenticate-passwordless-passkey-ios/passkey-created.png)
15. On **Security info**, you can see the new passkey that was added.

    ![Screenshot that shows a new passkey sign-in method on Security info on your other device.](media/howto-authenticate-passwordless-passkey-ios/passkey-ios-security-info-laptop.png)

### Use WebAuthn flow (iOS)

If you can't sign in to Authenticator to register a passkey, you can register directly from **Security info** with WebAuthn.

Note

You can't register a passkey in Authenticator this way if attestation is enabled by your administrator.

If you sign in to **Security info** on a different device, make sure both devices have internet access and Bluetooth enabled.

If your organization restricts Bluetooth usage, you can [permit Bluetooth pairing exclusively with passkey-enabled FIDO2 authenticators](/en-us/windows/security/identity-protection/passkeys/?tabs=windows%2Cintune#passkeys-in-bluetooth-restricted-environments) to allow cross-device passkey sign-in and registration.

Your organization needs to allow connectivity to endpoints in the following table to enable cross-device registration and authentication. Devices must be allowed to reach these URLs without interception. They need to be excluded from network proxies, interception, and other enterprise systems.

| Platform | URL |
| --- | --- |
| Android | `cable.ua5v.com` |
| iOS | `cable.auth.com``app-site-association.cdn-apple.com``app-site-association.networking.apple` |

1. On **Security info**, when you add a passkey in Authenticator, tap **Having trouble**.

    ![Screenshot that shows how to register another way if you have trouble.](media/howto-register-passwordless-passkey-direct-android/having-trouble-complete.png)
2. Now, tap **create your passkey a different way**.

    ![Screenshot that shows how to register a passkey another way.](media/howto-register-passwordless-passkey-direct-android/having-trouble.png)
3. Select **iPhone or iPad**, and go through the rest of the flow to register a passkey on the device.

    ![Screenshot that shows how to choose another way on iOS if you have trouble.](media/howto-register-passwordless-passkey-direct-android/choose-ios-device.png)

If a user wants to revert to the original instructions and register a passkey in Authenticator through sign-in:

1. On **Security info**, when you add a passkey in Authenticator, tap **Having trouble**.
2. Now, tap **create your passkey a different way** by signing in to Authenticator.
3. Go through the rest of the flow to register a passkey on your device.

Note

If you register your passkey with the Chrome browser on macOS, allow `login.microsoft.com` to access your security key or device when prompted.

### Delete your passkey in Authenticator for iOS

To remove the passkey from Authenticator, tap the account name, and then tap **Settings** &gt; **Delete passkey**. You also need to delete your passkey from [Security info](https://mysignins.microsoft.com/security-info).

### Troubleshoot passkey registration on iOS

In some cases when you try to register a passkey, it gets stored locally in the Authenticator app but isn't registered on the authentication server. For example, the passkey provider might not be permitted or the connection might time out. If you try to register a passkey and see an error that the passkey already exists, delete the passkey that was created locally in Authenticator and retry registration.

# [Android](#tab/Android)
You can register by signing in to the Authenticator app directly, by using [Security info](https://aka.ms/mysecurityinfo), or from your mobile device browser or through cross-device registration by using another device, such as a laptop. Your mobile device needs to run Android version 14 or later.

- Use Authenticator (Android)
- Use Security info (Android)
- Use WebAuthn flow (Android)

### Use Authenticator (Android)

You can sign in to Authenticator to create a passkey in the app and get seamless single sign-on across Microsoft native apps. **This flow is the recommended way to set up a passkey in Authenticator.** If you're signed in or already have an account in Authenticator, you still need to complete these steps to add a passkey in Authenticator.

1. Download Authenticator from Google Play, open it, and go through the privacy screens.
2. Add your account in Authenticator on your Android device:

If you installed Authenticator for the first time on your device, on the **Secure Your Digital Life** screen, tap **Add work or school account**.

[![Screenshot that shows the first screen to appear for Authenticator for Android devices.](media/howto-register-passwordless-passkey-direct-android/android-first-run.png)](media/howto-register-passwordless-passkey-direct-android/android-first-run.png#lightbox)

If you installed Authenticator on your device before but didn't add an account, tap **Add account** or the **+** button, and select **Work or school account**. Then tap **Sign in**.

[![Screenshot that shows how to register by using Authenticator for Android devices.](media/howto-register-passwordless-passkey-direct-android/add-account-android.png)](media/howto-register-passwordless-passkey-direct-android/add-account-android.png#lightbox)

If you already added an account in Authenticator, tap your account, and then tap **Create a passkey**.

[![Screenshot that shows how to create a passkey in Authenticator for Android devices.](media/howto-register-passwordless-passkey-direct-android/android-create-passkey.png)](media/howto-register-passwordless-passkey-direct-android/android-create-passkey.png#lightbox)
3. Complete multifactor authentication (MFA).
4. If necessary, tap **Settings** and set up a screen lock.

    ![Screenshot that shows how to set up a screen lock for a passkey in Authenticator for Android devices.](media/howto-register-passwordless-passkey-direct-android/android-lock-screen-required.png)
5. Tap **Settings** to enable Authenticator as a passkey provider.

    Note

    The steps to enable passkey providers on Android might vary based on the make and model of your device. Search for **Passkey** on your device settings, or consult your device manufacturer for guidance. If your device runs Android 14 and you can't enable Authenticator as a passkey provider, we recommend that you upgrade to Android 15.

    ![Screenshot that shows opening Settings and following the onscreen instructions by using Authenticator for Android devices.](media/howto-register-passwordless-passkey-direct-android/android-allow-authenticator.png)

    1. Open **Passwords & accounts**.

        ![Screenshot that shows selecting passwords and password options by using Authenticator for Android devices.](media/howto-register-passwordless-passkey-direct-android/password-options-android.png)
    2. In the **Additional providers** section, make sure that **Authenticator** is selected.

        ![Screenshot that shows enabling Authenticator as a provider by using Authenticator for Android devices.](media/howto-register-passwordless-passkey-direct-android/enable-authenticator-android.png)
6. After you return to Authenticator, tap **Done** to confirm that you added Authenticator as a passkey provider. Then you can see **Passkey** added as a sign-in method for your account. Tap **Done** again to finish.

    ![Screenshot that shows an account added to Authenticator for Android devices.](media/howto-register-passwordless-passkey-direct-android/android-account-added.png)

    Authenticator sets up passkey, passwordless, and MFA for sign-in according to your work or school account policies. Tap your account to see information, including your new passkey.

### Use Security info (Android)

1. On the same Android device as Authenticator or by using another device, such as a laptop, open a web browser and sign in with MFA to [Security info](https://mysignins.microsoft.com/security-info).
2. On **Security info**, tap **+ Add sign-in method** and select **Passkey in Microsoft Authenticator**.

    ![Screenshot that shows how to select a passkey in Authenticator as a sign-in method.](media/howto-authenticate-passwordless-passkey-ios/select-passkey-in-authenticator.png)
3. If prompted, tap **Next** and sign in with MFA.
4. If necessary, download Authenticator to your Android device. You can select [Microsoft Authenticator](https://www.microsoft.com/security/mobile-authenticator-app) and scan a QR code to install Authenticator from Google Play. After you download Authenticator to your Android device, select **Next**.

    ![Screenshot that gives users an option to download Authenticator.](media/howto-authenticate-passwordless-passkey-ios/download-authenticator-laptop.png)
5. You're prompted to open the Authenticator app and create your passkey there.

    ![Screenshot that shows the wizard to complete the passkey setup in Authenticator.](media/howto-authenticate-passwordless-passkey-ios/complete-setup-in-authenticator.png)
6. Open Authenticator and go through the privacy screens, as needed.

    - If you installed Authenticator for the first time on your device, on the **Secure Your Digital Life** screen, tap **Add work or school account**.

        ![Screenshot that shows the first screen to appear for Authenticator for Android devices.](media/howto-register-passwordless-passkey-direct-android/android-first-run.png)
    - If you installed Authenticator on your device before but didn't add an account, tap **Add account** or the **+** button, and select **Work or school account**. Then tap **Sign in**.

        ![Screenshot that shows how to register by using Authenticator for Android devices.](media/howto-register-passwordless-passkey-direct-android/add-account-android.png)
    - If you already added an account in Authenticator, tap your account, and then tap **Create a passkey**.

        ![Screenshot that shows how to create a passkey in Authenticator for Android devices.](media/howto-register-passwordless-passkey-direct-android/android-create-passkey.png)
7. Complete multifactor authentication (MFA).
8. If necessary, tap **Settings** and set up a screen lock.

    ![Screenshot that shows how to set up a lock screen for a passkey in Authenticator for Android devices.](media/howto-register-passwordless-passkey-direct-android/android-lock-screen-required.png)
9. Tap **Settings** to enable Authenticator as a passkey provider.

    Note

    The steps to enable passkey providers on Android might vary based on the make and model of your device. Search for **Passkey** on your device settings, or consult your device manufacturer for guidance. If your device runs Android 14 and you can't enable Authenticator as a passkey provider, we recommend that you upgrade to Android 15.

    ![Screenshot that shows opening Settings and following the onscreen instructions by using Authenticator for Android devices.](media/howto-register-passwordless-passkey-direct-android/android-allow-authenticator.png)

    1. Open **Passwords & accounts**.

        ![Screenshot that shows selecting passwords and password options by using Authenticator for Android devices.](media/howto-register-passwordless-passkey-direct-android/password-options-android.png)
    2. In the **Additional providers** section, make sure that **Authenticator** is selected.

        ![Screenshot that shows enabling Authenticator as a provider by using Authenticator for Android devices.](media/howto-register-passwordless-passkey-direct-android/enable-authenticator-android.png)
10. After you return to Authenticator, tap **Done** to confirm that you added Authenticator as a passkey provider. Then you can see **Passkey** added as a sign-in method for your account. Tap **Done** again to finish.

    ![Screenshot that shows an account added to Authenticator for Android devices.](media/howto-register-passwordless-passkey-direct-android/android-account-added.png)

    Authenticator sets up passkey, passwordless, and MFA for sign-in according to your work or school account policies.
11. After you finish the passkey setup in Authenticator, return to your browser where **Security info** is open. Select **Next**. ![Screenshot that shows the wizard to complete the passkey setup in Authenticator on Android.](media/howto-authenticate-passwordless-passkey-ios/complete-setup-authenticator.png)
12. The wizard verifies that the passkey was created in Authenticator.
13. After the passkey is created, select **Done**.

    ![Screenshot that confirms the passkey was created on Android.](media/howto-authenticate-passwordless-passkey-ios/passkey-created.png)
14. On **Security info**, you can see that the new passkey was added.

    ![Screenshot that shows a new passkey on Android sign-in method in Security info on your other device.](media/howto-authenticate-passwordless-passkey-android/passkey-android-security-info-laptop.png)

### Use WebAuthn flow (Android)

If you can't sign in to Authenticator to register a passkey, you can register directly from **Security info** with WebAuthn.

Note

You can't register a passkey in Authenticator this way if attestation is enabled by your administrator.

If you sign in to **Security info** on a different device, you need Bluetooth and an internet connection. Connectivity to the following two endpoints must be allowed in your organization:

- `cable.ua5v.com`
- `cable.auth.com`

If your organization restricts Bluetooth usage, you can permit Bluetooth pairing exclusively with passkey-enabled FIDO2 authenticators to allow cross-device registration of passkeys. For more information, see [Passkeys in Bluetooth-restricted environments](/en-us/windows/security/identity-protection/passkeys/?tabs=windows%2Cintune#passkeys-in-bluetooth-restricted-environments).

1. On **Security info**, when you add a passkey in Authenticator, tap **Having trouble**.

    ![Screenshot that shows how to register another way if you have trouble.](media/howto-register-passwordless-passkey-direct-android/having-trouble-complete.png)
2. Now, tap **create your passkey a different way**.

    ![Screenshot that shows how to register a passkey another way.](media/howto-register-passwordless-passkey-direct-android/having-trouble.png)
3. Select **Android** and go through the rest of the flow to register a passkey on your device.

    ![Screenshot that shows how to choose another way on Android if you have trouble.](media/howto-register-passwordless-passkey-direct-android/choose-android-device.png)

If a user wants to revert to the original instructions and register a passkey in Authenticator through sign-in:

1. On **Security info**, when you add a passkey in Authenticator, tap **Having trouble**.
2. Now, tap **create your passkey a different way** by signing in to Authenticator.
3. Go through the rest of the flow to register a passkey on your device.

Note

If you register your passkey with the Chrome browser on macOS, allow `login.microsoft.com` to access your security key or device when prompted.

## Delete your passkey in Authenticator for Android

To remove the passkey from Authenticator, tap the account name, tap **Settings**, and then tap **Delete passkey**.

In most cases, the passkey is also deleted from [Security info](https://mysignins.microsoft.com/security-info). If not, go to **Security info** and select **Delete** to remove it.

## Troubleshoot passkey registration on Android

In some cases when you try to register a passkey, it gets stored locally in the Authenticator app but isn't registered on the authentication server. For example, the passkey provider might not be permitted, or the connection might time out. If you try to register a passkey and see an error that the passkey already exists, delete the passkey that was created locally in Authenticator and retry registration.

---
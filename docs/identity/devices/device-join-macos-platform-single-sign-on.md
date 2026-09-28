---
layout: Conceptual
title: Join a Mac device with Microsoft Entra ID during the out of box experience with macOS PSSO - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/device-join-macos-platform-single-sign-on
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: pmwongera
description: How users can set up a Microsoft Entra with a new Mac device with macOS Platform Single Sign-on
ms.topic: tutorial
ms.date: 2024-12-19T00:00:00.0000000Z
ms.reviewer: brianmel
ms.custom: sfi-image-nochange
locale: en-us
document_id: 121c9be2-6be9-b696-b3da-be1f0f1dcf1e
document_version_independent_id: 121c9be2-6be9-b696-b3da-be1f0f1dcf1e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/device-join-macos-platform-single-sign-on.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/device-join-macos-platform-single-sign-on
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/device-join-macos-platform-single-sign-on.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
platformId: 2b73206a-5e42-903b-cb9c-b5e6c4992fd1
---

# Join a Mac device with Microsoft Entra ID during the out of box experience with macOS PSSO - Microsoft Entra ID | Microsoft Learn

Mac users can join their new device to Microsoft Entra ID during the first-run out-of-box experience (OOBE). The macOS Platform single sign-on (PSSO) is a capability on macOS that is enabled using the [Microsoft Enterprise Single Sign-on Extension](../../identity-platform/apple-sso-plugin). PSSO allows users to sign in to a Mac device using a hardware-bound key, smart card or their Microsoft Entra ID password. This tutorial shows you how to set up a Mac device during the OOBE to use PSSO using Automated Device Enrollment.

## Prerequisites

- A recommended minimum version of macOS 14 Sonoma. While macOS 13 Ventura is supported, we strongly recommend using macOS 14 Sonoma for the best experience.
- A device with [Automated Device Enrollment (ADE)](https://support.apple.com/HT204142) enrolled. Check with your administrator if you're unsure if your device is enrolled with this requirement.
- [Microsoft Intune Company Portal](/en-us/mem/intune/apps/apps-company-portal-macos) version 5.2404.0 or later.
- A Mac device enrolled in mobile device management (MDM) with Microsoft Intune.
- A configured single sign-on (SSO) extension MDM payload with [PSSO settings in Intune](/en-us/mem/intune/configuration/platform-sso-macos) by an administrator
- [Microsoft Authenticator](https://support.microsoft.com/account-billing/how-to-use-the-microsoft-authenticator-app-9783c865-0308-42fb-a519-8cf666fe0acc) (recommended): The user must be registered for some form of Microsoft Entra ID multifactor authentication (MFA) on their mobile device to complete device registration.
- For smart card setup, [certificate based authentication](/en-us/entra/identity/authentication/how-to-certificate-based-authentication) configured and enabled. A smart card loaded with a certificate for authentication with Microsoft Entra and the smart card paired with local account.
- Users must have sufficient permissions to [register and join devices to Microsoft Entra ID](troubleshoot-macos-platform-single-sign-on-extension?tabs=macOS14#insufficient-permissions).
- If you have network proxy filtering or TLS inspection enabled in your environment, be sure to review the suggested settings documented in the [Platform Single Sign-On troubleshooting guide](troubleshoot-macos-platform-single-sign-on-extension?tabs=macOS14#tls-inspection-urls-to-be-excluded-for-platform-sso)

## Set up your macOS device

1. Upon seeing the "Hello" screen when opening your Mac for the first time, follow the steps to select your country or region, and configure network settings as required.
2. You're prompted to download a **Remote Management** profile, which allows the configuration setup in Microsoft Intune to be applied to your device. Select **Continue**, and enter your Microsoft Entra ID credentials when prompted to approve the management profile download.

    ![Screenshot of remote management window.](media/device-join-macos-platform-single-sign-on-out-of-box/psso-remote-management.png)
3. Enter the code sent to your **Authenticator app** (recommended) or use another MFA method.
4. To create a user account, fill in your full name, account name, and create a local account password. Select **Continue** and your home screen appears.

    ![Screenshot of the window used to create a computer account, where the user enters their name, account name and local password.](media/device-join-macos-platform-single-sign-on-out-of-box/psso-local-account.png)

## Registration with Automated Device Enrollment

There are three authentication methods for PSSO registration:

- **Secure Enclave**: User logs on to their device which has a secure enclave backed cryptographic key used for SSO across apps that use Microsoft Entra ID for authentication. It can also be referred to as Platform Credential for macOS.
- **Smart card**: User logs into the machine using an external smart card or smart card compatible hard token.
- **Password**: User logs on to their local device with a local account, updated to use their Microsoft Entra ID password. This method also supports federated identity credentials.

Check that your system administrator has the Mac enrolled using secure enclave or smart card. These new passwordless features are supported only by PSSO. Check which authentication method has been set up by your administrator before continuing.

# [Secure Enclave](#tab/secure-enclave)
1. Navigate to the **Registration Required** popup at the top right of the screen. Hover over the popup and select **Register**. For macOS 14 Sonoma users, you see a prompt to register your device with Microsoft Entra. This prompt doesn't appear for macOS 13 Ventura.

    ![Screenshot of a Microsoft Entra registration prompt that appears on macOS 14 after the registration required notification is selected.](media/device-join-macos-platform-single-sign-on-out-of-box/macos-14-microsoft-entra-registration-required.png)
2. A prompt appears to enter your local account password. Enter your password and select **Ok**.
3. Once your account is unlocked, select the account to sign in to, enter your sign-in credentials and select **Next**.
4. MFA is required as part of this sign in flow. Open your **Authenticator app** (recommended) or use your other MFA methods you have registered, and enter the number displayed on the screen to finish registration.
5. When the MFA flow completes and the loading screen disappears, your device should be registered with PSSO. You can now use PSSO to access Microsoft app resources.

### Enable Platform Credential for macOS for use as a passkey

Setting up your device using secure enclave method enables you to use the resulting credential saved to the Mac as a passkey in the browser. To enable it;

1. Open the **Settings** app, and navigate to **Passwords** &gt; **Password options**.
2. Under **Password Options**, find **Use passwords and passkeys from** and enable **Company Portal** through the toggle switch.

    ![Screenshot of the Password Options window indicating that the use of passwords and passkeys from Company Portal has been enabled by a switch.](media/device-join-macos-platform-single-sign-on-out-of-box/password-options-enable-passkeys.png)

# [Smart Card](#tab/smart-card)
### Pair the smart card with your local account

Before you can register your device with a smart card, you need to pair the smart card with your local account using `sudo`. Open the **Terminal** app and run the following `sudo` commands to find the public key hash of the smart card certificate and pair it with your local account, then check it was successful.

```console
sc_auth identities
sudo sc_auth pair -h <HASH> -u <USERNAME>
sc_auth list
```

### Register your device with the smart card

1. Navigate to the **Registration Required** popup at the top right of the screen. Hover over the popup and select **Register**. If your smart card is paired with your local account, you see a prompt to enter the smart card pin

    ![Screenshot of the Platform SSO registration prompting the user to enter their smart card pin.](media/device-join-macos-platform-single-sign-on-out-of-box/smartcard-paired-registration-prompt.png)
2. Check if your administrator has configured MFA for the device registration flow. If so, open your **Authenticator** app on your mobile device and complete the MFA flow.

    ![Screenshot of the registration window prompting sign in with Microsoft.](media/device-join-macos-platform-single-sign-on-out-of-box/psso-register-device-prompt.png)
3. If the certificate isn't already paired with the local account, the user sees a prompt to use the smart card. Select **Smart card**.
4. You're prompted to enter the pin for your smart card. Enter your pin and select **Enter pin for the smart card**. When the correct pin is entered, PSSO registration with smart card authentication is complete.
5. You can now use PSSO to access Microsoft app resources, and unlock the device with the smart card pin. You'll need to use the local password to sign in after a reboot to unlock the keychain access.

# [Password](#tab/password)
1. Navigate to the **Registration Required** popup at the top right of the screen. Hover over the popup and select **Register**.

    ![Screenshot of a desktop screen with a registration required popup in the top right of the screen.](media/device-join-macos-platform-single-sign-on-out-of-box/psso-registration-required-popup.png)
2. A prompt appears to enter your local account password. Enter your password and select **Ok**.
3. Once your account is unlocked, select the account to sign in to, enter your sign-in credentials and select **Next**.
4. MFA is required as part of this sign in flow. Open your **Authenticator app** (recommended) or use your other MFA methods you have registered, and enter the number displayed on the screen to finish registration.
5. If your local password differs to your Microsoft Entra ID password, an **Authentication Required** popup appears on the top right of the screen. Hover over the banner and select **Sign-in**.
6. When a **Microsoft Entra** window appears, enter your Microsoft Entra ID password and select **Sign In**.

    ![Screenshot of a Microsoft Entra sign in window.](media/device-join-macos-platform-single-sign-on-out-of-box/psso-entra-account-password-prompt.png)
7. After unlocking the Mac, you can now use PSSO to access Microsoft app resources. From this point on, your old password doesn't work because PSSO is enabled for your device.

---

## Check your device registration status

Once you've completed the steps above, it's a good idea to check your device registration status.

1. To check that registration has completed successfully, navigate to **Settings** and select **Users & Groups**.
2. Select **Edit** next to **Network Account Server** and check that **Platform SSO** is listed as **Registered**.
3. To verify the method used for authentication, navigate to your username in the **Users & Groups** window and select the **Information** icon. Check the method listed, which should be **Secure enclave**, **Smart Card**, or **Password**.

    Note

    You can also use the **Terminal** app to check the registration status. Run the following command to check the status of your device registration. You should see in the bottom of the output that SSO tokens are retrieved. For macOS 13 Ventura users, this command is required to check the registration status.

    ```console
    app-sso platform -s
    ```
---
layout: Conceptual
title: Join a Mac device with Microsoft Entra ID using Company Portal - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/device-join-microsoft-entra-company-portal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: pmwongera
description: How users can set up a new macOS with macOS Platform single sign-on extension, using Company Portal.
ms.topic: tutorial
ms.date: 2024-12-19T00:00:00.0000000Z
ms.reviewer: jploegert
ms.custom: sfi-image-nochange
locale: en-us
document_id: 5ba6fc16-5b28-107c-af10-f411af4f2bc8
document_version_independent_id: 5ba6fc16-5b28-107c-af10-f411af4f2bc8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/device-join-microsoft-entra-company-portal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/device-join-microsoft-entra-company-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/device-join-microsoft-entra-company-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
platformId: 1855f731-c2f4-26ec-77b8-6563fdd6f43c
---

# Join a Mac device with Microsoft Entra ID using Company Portal - Microsoft Entra ID | Microsoft Learn

In this tutorial, you learn how to register a Mac device with macOS Platform Single Sign-on (PSSO) using Company Portal and the Intune MDM enrollment with Microsoft Entra Join. There are three methods in which you can register a Mac device with PSSO, secure enclave, smart card, or password. We recommend using secure enclave or smart card for the best passwordless experience, however it's important to note that this method will be preset by your company administrator using Microsoft Intune.

## Prerequisites

- A recommended minimum version of macOS 14 Sonoma. While macOS 13 Ventura is supported, we strongly recommend using macOS 14 Sonoma for the best experience.
- Microsoft Intune [Company Portal app](/en-us/mem/intune/apps/apps-company-portal-macos) version 5.2404.0 or later
- A Mac device enrolled in mobile device management (MDM) with [Microsoft Intune](/en-us/mem/intune/user-help/enroll-your-device-in-intune-macos-cp).
- A configured SSO extension MDM payload with PSSO settings in Intune by an administrator
- [Microsoft Authenticator](https://support.microsoft.com/account-billing/how-to-use-the-microsoft-authenticator-app-9783c865-0308-42fb-a519-8cf666fe0acc) (recommended), the user must be registered for some form of Microsoft Entra ID multifactor authentication (MFA) to complete device registration.
- For smart card setup, [certificate based authentication](/en-us/entra/identity/authentication/how-to-certificate-based-authentication) configured and enabled. A smart card loaded with a certificate for authentication with Microsoft Entra and the smart card paired with local account.
- Users must have sufficient permissions to [register and join devices to Microsoft Entra ID](troubleshoot-macos-platform-single-sign-on-extension?tabs=macOS14#insufficient-permissions).
- If you have network proxy filtering or TLS inspection enabled in your environment, be sure to review the suggested settings documented in the [Platform Single Sign-On troubleshooting guide](troubleshoot-macos-platform-single-sign-on-extension?tabs=macOS14#tls-inspection-urls-to-be-excluded-for-platform-sso)

## Intune MDM and Microsoft Entra Join using Company Portal

To register a Mac device with PSSO, you must first enroll your device in Microsoft Intune using the Company Portal app. Once enrolled, you can use secure enclave, smart card, or password to register your device with PSSO.

1. Open the **Company Portal** app and select **Sign in**.
2. Enter your Microsoft Entra ID credentials and select **Next**.
3. You're prompted to **Set up {Company} access**. The placeholder "Company" is different depending on your setup. Select **Begin**, then on the next screen, select **Continue**.

    ![Screenshot of the Company portal access setup window.](media/device-registration-macos-platform-single-sign-on/pssoe-company-portal-set-up-access.png)
4. You're presented with steps to install the management profile. The management profile should have been set up by an administrator using Microsoft Intune. Select **Download profile**.

    ![Screenshot of a Company Portal window requesting the user to download the management profile.](media/device-registration-macos-platform-single-sign-on/pssoe-company-portal-install-management-profile.png)
5. Open **Settings** &gt; **Privacy & Security** &gt; **Profiles** if it doesn't automatically appear. Select **Management Profile**.

    ![Screenshot of the Settings app Profiles showing a downloaded management profile.](media/device-registration-macos-platform-single-sign-on/pssoe-settings-profiles-management-profile.png)
6. Select **Install** to get access to company resources.

    ![Screenshot the prompt to install the management profile in settings.](media/device-registration-macos-platform-single-sign-on/pssoe-settings-profiles-install-management-profile.png)
7. Enter your local device password in the **Profiles** window that appears and select **Enroll**.

    ![Screenshot of the profiles window requesting a password to enroll you into an MDM service.](media/device-registration-macos-platform-single-sign-on/pssoe-profiles-enroll.png)
8. You see a notification in **Company Portal** that the installation is complete. Select **Done**.

## Platform SSO registration

Now that the device is in compliance with Company Portal, you need to register your device with PSSO. A **Registration Required** popup appears at the top right of the screen following successful completion of Intune MDM and Microsoft Entra Join using Company Portal. Use the tabs to register your device with PSSO using secure enclave, smart card, or password.

Tip

If the **Registration Required** popup doesn't appear or disappears before you can interact with it:

- **Wait approximately 10 minutes** — the popup automatically reappears after a failed or missed registration attempt.
- **Sign out and sign back in** to your Mac — this retriggers the registration notification.
- **Repair the registration** (macOS 14+) — go to **Settings** &gt; **Users & Groups** &gt; **Network Account Server** &gt; **Edit** &gt; **Repair** to restart the registration flow.
- If you closed the SSO authentication prompt during registration, signing out and back in restores the notification.

For more troubleshooting steps, see [Platform SSO known issues and troubleshooting](troubleshoot-macos-platform-single-sign-on-extension).

# [Secure Enclave](#tab/secure-enclave)
1. Navigate to the **Registration Required** popup at the top right of the screen. Hover over the popup and select **Register**. For macOS 14 Sonoma users, you see a prompt to register your device with Microsoft Entra. This prompt doesn't appear for macOS 13 Ventura.

    ![Screenshot of a Microsoft Entra registration prompt that appears on macOS 14 after the registration required notification is selected.](media/device-join-macos-platform-single-sign-on-out-of-box/macos-14-microsoft-entra-registration-required.png)
2. Once your account is unlocked with Touch ID or password, select the account to sign in to, enter your sign-in credentials and select **Next**.
3. MFA is required as part of this sign in flow. Open your **Authenticator app** (recommended) or use your other MFA methods you have registered, and enter the number displayed on the screen to finish registration.
4. When the MFA flow completes and the loading screen disappears, your device should be registered with PSSO. You can now use PSSO to access Microsoft app resources.

### Enable Platform Credential for macOS for use as a passkey

Setting up your device using secure enclave method enables you to use the resulting credential saved to the Mac as a passkey in the browser. To enable it;

1. Open the **Settings** app, and navigate to **General** &gt; **Autofill & Passwords**.
2. Under **Autofill & Passwords**, find **Autofill from** and enable **Company Portal** through the toggle switch.

    ![Screenshot of the Password Options window indicating that the use of passwords and passkeys from Company Portal has been enabled by a switch.](media/device-join-macos-platform-single-sign-on-out-of-box/password-options-enable-passkeys.png)

# [Smart Card](#tab/smart-card)
### Pair the smart card with your local account

Before you can register your device with a smart card, you need to pair the smart card with your local account. Open the **Terminal** app and run the following commands to find the public key hash of the smart card certificate and pair it with your local account, then check it was successful. This needs to be run using `sudo`.

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
5. You can now use PSSO to access Microsoft app resources, and unlock the device with the smart card pin. You'll need to use the local password to log in after a reboot to unlock the keychain access.

# [Password](#tab/password)
1. Navigate to the **Registration Required** popup at the top right of the screen. Hover over the popup and select **Register**.

    - For macOS 13 Ventura users, you see a prompt to register your device with Microsoft Entra ID. Enter your sign-in credentials and select **Next**.

    ![Screenshot of a desktop screen with a registration required popup in the top right of the screen.](media/device-join-macos-platform-single-sign-on-out-of-box/psso-registration-required-popup.png)
2. You're prompted to register your device with Microsoft Entra ID. Enter your sign-in credentials and select **Next**.

    1. Check if your administrator has configured MFA for the device registration flow. If so, open your **Authenticator** app on your mobile device and complete the MFA flow.

    ![Screenshot of the registration window prompting sign in with Microsoft.](media/device-join-macos-platform-single-sign-on-out-of-box/psso-register-device-prompt.png)
3. When a **Single Sign-On** window appears, enter your local account password and select **OK**. If you're on macOS 14, you're prompted to unlock your local account beforehand.

    ![Screenshot of a single sign-on window prompting the user to enter their local account password.](media/device-join-macos-platform-single-sign-on-out-of-box/psso-enter-local-password.png)
4. If your local password differs to your Microsoft Entra ID password, an **Authentication Required** popup appears on the top right of the screen. Hover over the banner and select **Sign-in**.
5. When a **Microsoft Entra** window appears, enter your Microsoft Entra ID password and select **Sign In**.

    ![Screenshot of a Microsoft Entra sign in window.](media/device-join-macos-platform-single-sign-on-out-of-box/psso-entra-account-password-prompt.png)
6. After unlocking the Mac, you can now use PSSO to access Microsoft app resources. From this point on, your old password doesn't work because PSSO is enabled for your device.

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

## Update your Mac device to enable PSSO

For macOS users whose device is already enrolled in Company Portal, your administrator can enable PSSO by updating your device's SSO extension profile. Once the PSSO profile is deployed and installed on your device, you're prompted to register your device with PSSO via the **Registration Required** notification at the top right of the screen. This removes the old SSO registration from your device in place of the new PSSO registration.

Although it's recommended to do it immediately, you can choose to select this and start your device registration at a time convenient to you.
---
layout: Conceptual
title: Join a Mac device with Microsoft Entra ID and configure it for shared device scenarios - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/device-join-macos-platform-single-sign-on-multi-user-device
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: leventbesik
description: How users can set up a Microsoft Entra Joined Mac that supports multiple users for shared device scenarios with macOS Platform Single Sign-on
ms.topic: tutorial
ms.date: 2026-02-23T00:00:00.0000000Z
ms.reviewer: jploegert
ms.custom: sfi-image-nochange
locale: en-us
document_id: 9289465b-86f4-fb0f-31cb-f2e73ff14b99
document_version_independent_id: 9289465b-86f4-fb0f-31cb-f2e73ff14b99
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/device-join-macos-platform-single-sign-on-multi-user-device.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/device-join-macos-platform-single-sign-on-multi-user-device
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/device-join-macos-platform-single-sign-on-multi-user-device.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: a5f758bc-2683-98a4-7936-06e6b98331a2
---

# Join a Mac device with Microsoft Entra ID and configure it for shared device scenarios - Microsoft Entra ID | Microsoft Learn

In this tutorial, you will learn how to configure a Microsoft Entra Joined Mac via Mobile Device Management (MDM) to support multiple users. There are three methods in which you can register a Mac device with Platform SSO (PSSO), secure enclave, smart card, or password. We recommend using secure enclave or smart card for the best passwordless experience, however shared or multi-user Macs may benefit from using the password method instead. Common scenarios for shared Macs with passwords would be computer labs in schools or universities. In these scenarios, students use multiple devices, multiple students use the same device, and they only have passwords and no MFA or passwordless credentials.

## Prerequisites

- A required minimum version of macOS 14 Sonoma or later. While macOS 13 Ventura is supported for Platform SSO overall, only Sonoma supports the necessary tools for the Platform SSO shared Mac scenario described in this guide.
- Microsoft Intune [Company Portal app](/en-us/mem/intune/apps/apps-company-portal-macos) version 5.2404.0 or later.
- A configured Platform SSO MDM payload in your MDM by an administrator.

## MDM configuration

There are three main steps for configuring Platform SSO on a shared device:

1. **Deploy Company Portal.** For more information, see [Add the Company Portal for macOS app](/en-us/mem/intune/apps/apps-company-portal-macos).
2. **Deploy Platform SSO Configuration.** Create and deploy a settings catalog profile with the required Platform SSO Configuration.
3. **Deploy macOS Login Screen Configuration.** The macOS Login screen configuration can be changed to allow new users to log in.

### Shared Device Limitations

Please note the following regarding shared macOS devices:

- macOS devices that are intended to be shared between users should ensure they are enrolled as user-less ([enrollment w/o user affinity for ADE](/en-us/intune/intune-service/enrollment/device-enrollment-program-enroll-macos), [direct enrollment for non-ADE](/en-us/intune/intune-service/enrollment/device-enrollment-direct-enroll-macos)).
- Conditional access policies are not supported on macOS devices that are shared with multiple users.

### Platform SSO profile configuration

Your Platform SSO MDM profile should apply the following configurations to support multi-user devices:

| Configuration Parameter | Value(s) | Note |
| --- | --- | --- |
| Screen Locked Behavior | Do Not Handle | Required |
| Registration Token | {{DEVICEREGISTRATION}} | Recommended for the best registration user experience |
| Authentication Method | Password, smartcard, secure enclave | During new user creation at the login screen, user will need to specify a user name and password regardless of the auth method chosen. |
| Enable Authorization | Enabled | Required |
| Enable Create User At Login | Enabled | Required |
| New User Authorization Mode | Standard | Recommended |
| Token To User Mapping --&gt; Account Name | preferred\_username | Required |
| Token To User Mapping --&gt; Full Name | name | Required |
| Use Shared Device Keys | Enabled | Required |
| User Authorization Mode | Standard | Recommended |
| Team Identifier | UBF8T346G9 | Required |
| Extension Identifier | com.microsoft.CompanyPortalMac.ssoextension | Required |
| Type | Redirect | Required |
| URLs | `https://login.microsoftonline.com`, https://login.microsoft.com, `https://sts.windows.net`, https://login.partner.microsoftonline.cn, https://login.chinacloudapi.cn, https://login.microsoftonline.us, https://login-us.microsoftonline.com | Required |

If you use Intune as your MDM of choice, then the configuration profile settings will appear like this:

![Screenshot of a Platform SSO MDM profile in Intune.](media/device-registration-macos-platform-single-sign-on/intune-psso-shared-device-profile.png)

### macOS login screen configuration

To allow new users to log on and be created from the macOS login screen, there are two configurations that can be used:

- **Show Other Users Managed**. With this configuration, the macOS login screen shows a list of profiles that have been created and an "other user" button that can be used to log in with a username and password. Users can select their existing profile to log in or log in with their Microsoft Entra ID user principal name (UPN).
- **Show full name**. With this configuration, the macOS login screen displays and username and password field with no list of users. Users can log in with their Microsoft Entra ID UPN.

These configurations can be found in Intune Settings Catalog under **Login** &gt; **Login Window Behavior**.

## Enrolling and registering devices

To register a Mac device with Platform SSO, devices must be enrolled into MDM. For shared devices, the user who sets up the device would typically be an administrator or technician - this user will have local administrative rights unless there is alternative local admin account created.

Note

If you are enrolling using Automated Device Enrollment you may choose to encourage the user setting up the device to create the local account as:

- **Account name:** Microsoft Entra ID username (eg. user@domain.com).
- **Full Name:** First and Last Name. This is because the local account that is created during setup assistant will be associated with the Microsoft Entra ID account during registration.

There are three high-level steps to set up Platform SSO on a shared device:

1. IT admin or delegated person enrolls device with Intune.
2. IT admin or delegated person registers the device with Microsoft Entra ID using their credentials.
3. Now the device is ready for new users to log in from the Microsoft Entra ID login screen.

Organizations can enroll shared devices into Intune using different methods depending on the device ownership.

| Enrollment method | Device Ownership | Requirements |
| --- | --- | --- |
| [Automated Device Enrollment with no user affinity](/en-us/mem/intune/enrollment/device-enrollment-program-enroll-ios) | Company or school owned | ✔️Registration in Apple Business Manager✔️ Automated Device Enrollment configured in Intune |
| [Company Portal](/en-us/mem/intune/user-help/enroll-your-device-in-intune-macos-cp) | Personal | None |

### Platform SSO registration

Once the device is MDM enrolled and has Company Portal installed, you need to register your device with Platform SSO. A **Registration Required** popup appears at the top right of the screen. Use the popup to register your device with Platform SSO using your Microsoft Entra ID credentials:

1. Navigate to the **Registration Required** popup at the top right of the screen. Hover over the popup and select **Register**.

    [![Screenshot of a desktop screen with a registration required popup in the top right of the screen.](media/device-join-macos-platform-single-sign-on-out-of-box/psso-registration-required-popup.png)](media/device-join-macos-platform-single-sign-on-out-of-box/psso-registration-required-popup.png#lightbox)
2. You're prompted to register your device with Microsoft Entra ID. Enter your sign-in credentials and select **Next**.

    1. Your administrator may have configured MFA for the device registration flow. If so, open your **Authenticator** app on your mobile device and complete the MFA flow.

    ![Screenshot of the registration window prompting sign in with Microsoft.](media/device-join-macos-platform-single-sign-on-out-of-box/psso-register-device-prompt.png)
3. When a **Single Sign-On** window appears, enter your local account password and select **OK**. 

    ![Screenshot of a single sign-on window prompting the user to enter their local account password.](media/device-join-macos-platform-single-sign-on-out-of-box/psso-enter-local-password.png)
4. If your local password differs to your Microsoft Entra ID password, an **Authentication Required** popup appears on the top right of the screen. Hover over the banner and select **Sign-in**.
5. When a **Microsoft Entra** window appears, enter your Microsoft Entra ID password and select **Sign In**.

    ![Screenshot of a Microsoft Entra sign in window.](media/device-join-macos-platform-single-sign-on-out-of-box/psso-entra-account-password-prompt.png)
6. After unlocking the Mac, you can now use Platform SSO to access Microsoft app resources. From this point on, your old password doesn't work because Platform SSO is enabled for your device.

## Check your device registration status

After completing the steps above, it's recommended to check your device registration status.

1. To check that registration has completed successfully, navigate to **Settings** and select **Users & Groups**.
2. Select **Edit** next to **Network Account Server** and check that **Platform SSO** is listed as **Registered**.
3. To verify the method used for authentication, navigate to your username in the **Users & Groups** window and select the **Information** icon. Check the method listed, which should be **Secure enclave**, **Smart Card**, or **Password**.

    Note

    You can also use the **Terminal** app to check the registration status. Run the following command to check the status of your device registration. You should see in the bottom of the output that SSO tokens are retrieved. For macOS 13 Ventura users, this command is required to check the registration status.

    ```console
    app-sso platform -s
    ```

## Test the Enable Create User At Login Functionality

Next you should validate that the device is ready for other users in the tenant to log into it.

1. Log out of the Mac with the account that you used to do the initial setup.
2. At the login screen, choose the **Other...** option to sign in with a new user account

![Screenshot of the macOS login screen.](media/device-registration-macos-platform-single-sign-on/psso-new-user-login.png)

1. Enter a user's Microsoft Entra ID User Principal Name and password.

![Screenshot of the macOS login box where a user has entered their credentials.](media/device-registration-macos-platform-single-sign-on/psso-new-user-login-upn.png)

1. If the User Principal Name and password were correct then the user will be logged in. The user is directed to go through several Setup Assistant dialog screens by default and then they land on the macOS desktop.

## Troubleshooting

If the user cannot sign in successfully, then use the following resources to troubleshoot:

1. Refer to the [macOS Platform single sign-on known issues and troubleshooting](troubleshoot-macos-platform-single-sign-on-extension) guide
2. Validate that the user can successfully sign in to Microsoft Entra ID using their User Principal Name and password in a browser on another device. You can test by having the user go to a web app, such as https://myapps.microsoft.com
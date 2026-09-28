---
layout: Conceptual
title: Microsoft Entra certificate-based authentication on Android devices - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-certificate-based-authentication-mobile-android
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about Microsoft Entra certificate-based authentication on Android devices
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: vimrang
ms.custom: has-adal-ref
locale: en-us
document_id: 19084361-84be-7144-6907-747f357a6e03
document_version_independent_id: 8c7d04b1-f15e-fe31-c98b-bb4d3d4f5683
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-certificate-based-authentication-mobile-android.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-certificate-based-authentication-mobile-android
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-certificate-based-authentication-mobile-android.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: 9549be3c-1ac8-32eb-8534-0df37d6268d1
---

# Microsoft Entra certificate-based authentication on Android devices - Microsoft Entra ID | Microsoft Learn

Microsoft Entra Certificate-based authentication is supported with certificates provisioned on the device and with external security keys like YubiKeys.

## Prerequisites

- Android version must be Android 5.0 (Lollipop) or later.
- Microsoft first-party apps with latest MSAL libraries or Microsoft Authenticator can do CBA.
- Third party applications using latest MSAL libraries or integrated with Microsoft Authenticator can do CBA.

## CBA with on-device certificates

Customers can use their choice of Mobile Device Management (MDM) to provision the certificates on the device. End users must first register their devices with MDM and get the certificate provisioned on the device. Once the certificate is provisioned on the device, users can authenticate using CBA.

Steps to test YubiKey on Microsoft apps on Android:

1. Open Outlook.
2. Select **Add account** and enter your user principal name (UPN).
3. Click **Continue**.
4. Select **Use Certificate or smart card**.
5. Select **Certificate on the device** in the dialog\*\*.\*\*
6. The certificate picker appears.
7. Select the certificate associated with the user’s account. Click **Continue**.
8. User is allowed to access the Outlook resource if the authentication is successful.

## CBA with certificates on hardware security key

Certificates can be provisioned in external devices like hardware security keys along with a PIN to protect private key access. Microsoft Entra ID supports CBA with YubiKey.

### Advantages of certificates on hardware security key

Security keys with certificates:

- Have the roaming nature of a security key, which allows users to use the same certificate on different devices.
- Are hardware-secured with a PIN, which makes them phishing-resistant.
- Provide multifactor authentication with a PIN as second factor to access the private key of the certificate.
- Satisfy the industry requirement to have MFA on separate device.
- Help in future proofing where multiple credentials can be stored including Fast Identity Online 2 (FIDO2) keys.

### Microsoft Entra CBA on Android mobile with YubiKey

Android needs a middleware application to be able to support smartcard or security keys with certificates. To support YubiKeys with Microsoft Entra CBA, YubiKey Android SDK has been integrated into the Microsoft broker code which can be leveraged through the latest Microsoft Authentication Library (MSAL).

Because Microsoft Entra CBA with YubiKey on Android mobile is enabled by using the latest MSAL, YubiKey Authenticator app isn't required for Android support.

Steps to test YubiKey on Microsoft apps on Android:

1. Install Microsoft Authenticator.
2. If your YubiKey has USB-C, open Outlook and plug in your YubiKey.
3. Select **Add account** and enter your user principal name (UPN).
4. Click **Continue**, and when asked for permission to access your YubiKey, click **OK**.
5. Select **Use Certificate or smart card**.
6. If you're using an NFC-enabled Yubikey, hold the Yubikey to the back of the device.
7. A custom certificate picker appears.
8. Select the certificate associated with the user’s account, and click **Continue**.
9. Enter the PIN to access YubiKey and select **Unlock**.
10. If you're using a Yubikey with NFC, hold the Yubikey to the back of the phone again to validate the PIN.
11. After authentication succeeds, you can access Outlook.

Note

For a smooth CBA flow, plug in YubiKey as soon as the application is opened and accept the consent dialog from YubiKey before selecting the link **Use Certificate or smart card**. If you want to experience only a single connection, consider having users plug in the YubiKey by using USB instead of NFC, which only needs to be done once at the beginning of login.

## Support for Exchange ActiveSync clients

Certain Exchange ActiveSync applications on Android 5.0 (Lollipop) or later are supported. To determine if your email application supports Microsoft Entra CBA, contact your application developer.

## Supported Microsoft Entra use cases

### Microsoft mobile application support

| Applications | Support |
| --- | --- |
| Azure Information Protection app | ✅ |
| Company Portal | ✅ |
| Microsoft Teams | ✅ |
| Office (mobile) | ✅ |
| OneNote | ✅ |
| OneDrive | ✅ |
| Outlook | ✅ |
| Power BI | ✅ |
| Skype for Business | ✅ |
| Word / Excel / PowerPoint | ✅ |
| Yammer | ✅ |
| Edge browser with profile login | ✅ |
| Managed Home Screen | ✅ |

Note

When using Microsoft Entra certificate-based authentication on Android devices in kiosk mode (common in Shared Device Mode), customers should allow list com.android.systemui as a required package to ensure they are presented with the appropriate UI to complete their authentication.

### Browsers

| Operating system | Chrome certificate on-device | Chrome smart card/security key | Safari certificate on-device | Safari smart card/security key | Edge certificate on-device | Edge smart card/security key |
| --- | --- | --- | --- | --- | --- | --- |
| Android | ✅ | ❌ | N/A | N/A | ✅ | ❌ |

Note

Although Edge as a browser isn't supported, Edge as a profile (for account login) is an MSAL app that supports CBA on Android.

### Operating systems

| Operating system | Certificate on-device/Derived PIV | Smart cards/Security keys |
| --- | --- | --- |
| Android | ✅ | Supported vendors only |

### Security key providers

| Provider | Android |
| --- | --- |
| YubiKey | ✅ |

### Troubleshoot certificates on hardware security key

#### What will happen if the user has certificates both on the Android device and YubiKey?

- If the user has certificates both on the android device and YubiKey, then if the YubiKey is plugged in before user clicks **Use Certificate or smart card**, the user will be shown the certificates in the YubiKey.
- If the YubiKey isn't plugged in before user clicks **Use Certificate or smart card**, the user will be asked to select between certificates on device or physical smart card. If the user chooses **Certificate on device**, the user will be shown the certificates on the device. If the user chooses **Certificates on physical smart card**, plug in or hold the YubiKey to the back, and the user will be shown the certificates in the YubiKey.

#### My YubiKey is locked after incorrectly typing PIN three times. How do I fix it?

- Users should see a dialog informing you that too many PIN attempts have been made. This dialog also pops up during subsequent attempts to select **Use Certificate or smart card**.
- Users should contact the admin to reset a YubiKey PIN.

#### I have installed Microsoft authenticator but still don't see an option to do Certificate based authentication with YubiKey.

Before installing Microsoft Authenticator, uninstall Company Portal and install it after Microsoft Authenticator installation.

#### Does Microsoft Entra CBA support YubiKey via NFC?

Microsoft Entra CBA supports using YubiKey with USB and NFC.

#### Once CBA fails, clicking on the CBA option again in the ‘Other ways to sign in’ link on the error page fails.

This issue happens because of certificate caching. As a workaround, clicking cancel and restarting the login flow will let the user choose a new certificate and successfully login.

#### Microsoft Entra CBA with YubiKey is failing. What information would help debug the issue?

1. Open Microsoft Authenticator app, click the three dots icon in the top right corner and select **Send Feedback**.
2. Click **Having Trouble?**.
3. For **Select an option**, select **Add or sign into an account**.
4. Describe any details you want to add.
5. Click the send arrow in the top right corner. Note the code provided in the dialog that appears.
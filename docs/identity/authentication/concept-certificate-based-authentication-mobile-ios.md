---
layout: Conceptual
title: Microsoft Entra certificate-based authentication on Apple devices - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-certificate-based-authentication-mobile-ios
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about Microsoft Entra certificate-based authentication on Apple devices that run macOS or iOS
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: vimrang
ms.custom: has-adal-ref
locale: en-us
document_id: ca4f3ee8-480a-1022-32b0-008d2bf1d1a5
document_version_independent_id: e7ae68ea-6dc9-fdbf-3c0b-978235e73c86
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-certificate-based-authentication-mobile-ios.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-certificate-based-authentication-mobile-ios
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-certificate-based-authentication-mobile-ios.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: b2356a0f-2198-7a07-5fb1-ccac4adbedad
---

# Microsoft Entra certificate-based authentication on Apple devices - Microsoft Entra ID | Microsoft Learn

This topic covers Microsoft Entra certificate-based authentication (CBA) support for macOS and iOS devices.

## Microsoft Entra certificate-based authentication on macOS devices

Devices that run macOS can use CBA to authenticate against Microsoft Entra ID by using their X.509 client certificate. Microsoft Entra CBA is supported with certificates on-device and external hardware protected security keys. On macOS, Microsoft Entra CBA is supported on all browsers and on Microsoft first-party applications.

### Browsers supported on macOS

| Edge | Chrome | Safari | Firefox |
| --- | --- | --- | --- |
| ✅ | ✅ | ✅ | ✅ |

### macOS device sign-in with Microsoft Entra CBA

Microsoft Entra CBA today isn't supported for device-based sign-in to macOS machines. The certificate used to sign in to the device can be the same certificate used to authenticate to Microsoft Entra ID from a browser or desktop application, but the device sign-in itself isn't supported against Microsoft Entra ID yet. 

## Microsoft Entra certificate-based authentication on iOS devices

Devices that run iOS can use certificate-based authentication (CBA) to authenticate to Microsoft Entra ID using a client certificate on their device when connecting to:

- Office mobile applications such as Microsoft Outlook and Microsoft Word
- Exchange ActiveSync (EAS) clients

Microsoft Entra CBA is supported for certificates on-device on native browsers and on Microsoft first-party applications on iOS devices.

### Prerequisites

- iOS version must be iOS 9 or later.
- Microsoft Authenticator or Company portal is required for first party applications.

### Support for on-device certificates and external storage

On-device certificates are provisioned on the device. Customers can use Mobile Device Management (MDM) to provision the certificates on the device. Since iOS doesn't support hardware protected keys out of the box, customers can use external storage devices for certificates.

### Supported platforms

- Only native browsers are supported
- Applications using latest MSAL libraries or Microsoft Authenticator can do CBA
- Edge with profile, when users add account and logged in a profile support CBA
- Microsoft first party apps with latest MSAL libraries or Microsoft Authenticator can do CBA

### Browsers

| Edge | Chrome | Safari | Firefox |
| --- | --- | --- | --- |
| ❌ | ❌ | ✅ | ❌ |

### Microsoft mobile applications support

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

### Support for Exchange ActiveSync clients

On iOS 9 or later, the native iOS mail client is supported.

To determine if your email application supports Microsoft Entra CBA, contact your application developer.

## Support for certificates on hardware security key

Certificates can be provisioned in external devices like hardware security keys along with a PIN to protect private key access. Microsoft's mobile certificate-based solution coupled with the hardware security keys is a simple, convenient, FIPS (Federal Information Processing Standards) certified phishing-resistant MFA method.

As for iOS 16/iPadOS 16.1, Apple devices provide native driver support for USB-C or Lightning connected CCID-compliant smart cards. This means Apple devices on iOS 16/iPadOS 16.1 see a USB-C or Lightning connected CCID-compliant device as a smart card without the use of additional drivers or third-party apps. Microsoft Entra CBA works on these USB-A, USB-C, or Lightning connected CCID-compliant smart cards.

### Advantages of certificates on hardware security key

Security keys with certificates:

- Can be used on any device, and don't need a certificate to be provisioned on every device the user has
- Are hardware-secured with a PIN, which makes them phishing-resistant
- Provide multifactor authentication with a PIN as second factor to access the private key of the certificate
- Satisfy the industry requirement to have MFA on separate device
- Help in future proofing where multiple credentials can be stored including Fast Identity Online 2 (FIDO2) keys

### Microsoft Entra CBA on iOS mobile with YubiKey

Even though the native Smartcard/CCID driver is available on iOS/iPadOS for Lightning connected CCID-compliant smart cards, the YubiKey 5Ci Lightning connector isn't seen as a connected smart card on these devices without the use of PIV (Personal Identity Verification) middleware like the Yubico Authenticator.

### One-time registration prerequisite

- Have a PIV-enabled YubiKey with a smartcard certificate provisioned on it
- Download the [Yubico Authenticator for iOS app](https://apps.apple.com/app/yubico-authenticator/id1476679808) on your iPhone with v14.2 or later
- Open the app, insert the YubiKey or tap over near field communication (NFC) and follow steps to upload the certificate to iOS keychain

### Steps to test YubiKey on Microsoft apps on iOS mobile

1. Install the latest Microsoft Authenticator app.
2. Open Outlook and plug in your YubiKey.
3. Select **Add account** and enter your user principal name (UPN).
4. Select **Continue** and the iOS certificate picker appears.
5. Select the public certificate copied from YubiKey that is associated with the user’s account.
6. Select **YubiKey required** to open the YubiKey authenticator app.
7. Enter the PIN to access YubiKey and select the back button at the top left corner.

The user should be successfully logged in and redirected to the Outlook homepage.

### Troubleshoot certificates on hardware security key

#### What happens if the user has certificates both on the iOS device and YubiKey?

The iOS certificate picker shows all the certificates on both iOS device and the ones copied from YubiKey into iOS device. Depending on the certificate user picks, they may be taken to YubiKey authenticator to enter a PIN, or directly authenticated.

#### My YubiKey is locked after incorrectly typing PIN 3 times. How do I fix it?

- Users should see a dialog informing you that too many PIN attempts have been made. This dialog also pops up during subsequent attempts to select **Use Certificate or smart card**.
- [YubiKey Manager](https://www.yubico.com/support/download/yubikey-manager/) can reset a YubiKey’s PIN.

#### After CBA fails, the CBA option in the ‘Other ways to sign in’ link also fails. Is there a workaround?

This issue happens because of certificate caching. We're working on an update to clear the cache. As a workaround, select **Cancel**, retry sign-in, and choose a new certificate.

#### Microsoft Entra CBA with YubiKey is failing. What information would help debug the issue?

1. Open Microsoft Authenticator app, select the three dots icon in the top right corner and select **Send Feedback**.
2. Select **Having Trouble?**.
3. For **Select an option**, select **Add or sign into an account**.
4. Describe any details you want to add.
5. Select the send arrow in the top right corner. Note the code provided in the dialog that appears.

#### How can I enforce phishing-resistant MFA using a hardware security key on browser-based applications on mobile?

Certificate-based authentication and Conditional Access authentication strength capability makes it powerful for customers to enforce authentication needs. Edge as a profile (add an account) works with a hardware security key like YubiKey and a Conditional Access policy with authentication strength capability can enforce phishing-resistant authentication with CBA.

CBA support for YubiKey is available in the latest Microsoft Authentication Library (MSAL) libraries, and any third-party application that integrates the latest MSAL. All Microsoft first-party applications can use CBA and Conditional Access authentication strength.

### Supported operating systems

| Operating system | Certificate on-device/Derived PIV | Smart cards/Security keys |
| --- | --- | --- |
| iOS | ✅ | Supported vendors only |

### Supported browsers

| Operating system | Chrome certificate on-device | Chrome smart card/security key | Safari certificate on-device | Safari smart card/security key | Edge certificate on-device | Edge smart card/security key |
| --- | --- | --- | --- | --- | --- | --- |
| iOS | ❌ | ❌ | ✅ | ✅ | ❌ | ❌ |

### Security key providers

| Provider | iOS |
| --- | --- |
| YubiKey | ✅ |
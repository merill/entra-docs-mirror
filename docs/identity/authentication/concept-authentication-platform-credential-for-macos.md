---
layout: Conceptual
title: Platform Credential for macOS authentication method in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-platform-credential-for-macos
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about using Platform Credential for macOS authentication in Microsoft Entra ID to help improve and secure sign-in events
ms.topic: concept-article
ms.date: 2025-10-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 2e7e470d-ead7-35f5-a5c1-09a2678f8203
document_version_independent_id: 2e7e470d-ead7-35f5-a5c1-09a2678f8203
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-authentication-platform-credential-for-macos.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-authentication-platform-credential-for-macos
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-authentication-platform-credential-for-macos.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: dd1fcf4b-7f71-e01d-445e-caf0280c1faf
---

# Platform Credential for macOS authentication method in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Platform Credential for macOS is a new capability on macOS that is enabled using the Microsoft Enterprise single sign-on Extension (SSOe). It provisions a secure enclave backed hardware-bound cryptographic key that is used for SSO across apps that use Microsoft Entra ID for authentication. The user’s local account password is not affected and is required to log on to the Mac.

![Screenshot showing an example of a pop up window prompting user to register their macOS account with their identity provider using Platform single sign-on.](media/concept-authentication-passwordless/macos-platform-sso.png)

Platform Credential for macOS allows users to go passwordless by configuring Touch ID to unlock the device, and uses phish-resistant credentials, based on Windows Hello for Business technology. This saves customer organizations money by removing the need for security keys and advances Zero Trust objectives using integration with the Secure Enclave.

Platform Credential for macOS can also be used as a phishing-resistant credential for use in WebAuthn challenges, including browser re-authentication scenarios. If you use Key Restriction Policies in your FIDO policy, you need to add the AAGUID for the macOS Platform Credential to your list of allowed AAGUIDs: `7FD635B3-2EF9-4542-8D9D-164F2C771EFC`.

![Diagram that outlines the steps involved for user sign-in with macOS Platform SSO.](media/concept-authentication-passwordless/macos-platform-single-sign-on-flow.png)

1. A user unlocks macOS using fingerprint or password gesture, which unlocks the key bag to provide access to UserSecureEnclaveKey.
2. The macOS requests a nonce (a random arbitrary number that can be used just once) from Microsoft Entra ID.
3. Microsoft Entra ID returns a nonce that's valid for 5 minutes.
4. The operating system (OS) sends a login request to Microsoft Entra ID with an embedded assertion signed with the UserSecureEnclaveKey that resides in the Secure Enclave.
5. Microsoft Entra ID validates the signed assertion using the user's securely registered public key of UserSecureEnclave key. Microsoft Entra ID validates the signature and nonce. Once the assertion is validated, Microsoft Entra ID creates a [primary refresh token (PRT)](../devices/concept-primary-refresh-token) encrypted with the public key of the UserDeviceEncryptionKey that is exchanged during registration and sends the response back to the OS.
6. The OS decrypts and validates the response, retrieves the SSO tokens, stores and shares it with the SSO extension for providing SSO. The user is able to access macOS, cloud and on-premises applications by using SSO.

Refer to [macOS Platform SSO](../devices/macos-psso) for more information on how to configure and deploy Platform Credential for macOS.

## Platform single sign-on for macOS with SmartCard

Platform single sign-on (PSSO) for macOS allows users to go passwordless using the SmartCard authentication method. The user signs in to the device by using an external smart card, or smart card-compatible hardware-based token (such as Yubikey). Once the device is unlocked, the smart card is used with Microsoft Entra ID to grant SSO across apps that use Microsoft Entra ID for authentication by using [certificate-based authentication (CBA)](concept-certificate-based-authentication). CBA needs to be configured and enabled for users for this feature to work. For more information about how to configure CBA, see [How to configure Microsoft Entra certificate-based authentication](how-to-certificate-based-authentication).

To enable it, an administrator needs to configure PSSO by using Microsoft Intune or another supported Mobile Device Management (MDM) solution.

![Diagram that outlines the steps involved for user sign-in with macOS Platform SSO.](media/concept-authentication-passwordless/macos-platform-single-sign-on-flow.png)

1. A user unlocks macOS using smart card pin, which unlocks the smart card and the key bag to provide access to device registration keys present in Secure Enclave.
2. The macOS requests a nonce (a random arbitrary number that can be used only once) from Microsoft Entra ID.
3. Microsoft Entra ID returns a nonce that's valid for 5 minutes.
4. The operating system (OS) sends a login request to Microsoft Entra ID with an embedded assertion signed with the user's Microsoft Entra certificate from the smart card.
5. Microsoft Entra ID validates the signed assertion, signature and nonce. Once the assertion is validated, Microsoft Entra ID creates a [primary refresh token (PRT)](../devices/concept-primary-refresh-token) encrypted with the public key of the UserDeviceEncryptionKey that is exchanged during registration and sends the response back to the OS.
6. The OS decrypts and validates the response, retrieves the SSO tokens, stores and shares it with the SSO extension for providing SSO. The user is able to access macOS, cloud and on-premises applications by using SSO.
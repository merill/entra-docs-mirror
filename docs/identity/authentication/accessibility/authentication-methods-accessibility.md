---
layout: Conceptual
title: Enhance accessibility with multifactor authentication in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/accessibility/authentication-methods-accessibility
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Explains authentication Methods Accessibility
ms.topic: concept-article
ms.date: 2025-03-04T00:00:00.0000000Z
locale: en-us
document_id: 3bb67b91-2e00-9de0-9421-64849cb9b508
document_version_independent_id: 3bb67b91-2e00-9de0-9421-64849cb9b508
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/accessibility/authentication-methods-accessibility.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/accessibility/authentication-methods-accessibility
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/accessibility/authentication-methods-accessibility.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 9a8091a0-9af9-4fb3-abf3-88f5e789946e
---

# Enhance accessibility with multifactor authentication in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

As cybersecurity threats evolve, multifactor authentication (MFA) has become a cornerstone of secure digital identity. Microsoft Entra ID offers a range of MFA methods designed for robust security and diverse user needs, including those with accessibility constraints. Here's a closer look at how these MFA options enhance accessibility and inclusivity.

## Microsoft Authenticator

The Microsoft Authenticator app provides either notifications for quick approval or generates time-based codes for more traditional MFA entry. This app is compatible with various assistive technologies, including screen readers, making it accessible for users with visual impairments. It also offers flexibility for individuals who prefer not to rely solely on SMS or voice calls.

[Download Microsoft Authenticator](https://www.microsoft.com/security/mobile-authenticator-app?msockid=04750fac1789618938f71b4a16ee6056).

## Text and voice calls

Text and voice call options cater to those who may not use a smartphone app. This can be beneficial for individuals with certain accessibility needs:

- **Text:** Allows users to receive a verification code via text message, which can be useful for those with hearing impairments or those who prefer text-based communication.
- **Voice calls:** Voice calls are a great option for users with visual impairments, as they provide audio cues rather than visual or tactile ones.

For more information, see [Phone authentication methods](/en-us/entra/identity/authentication/concept-authentication-phone-options).

## FIDO2 security keys

FIDO2 security keys are physical devices that offer a highly accessible and secure MFA option. These hardware keys support biometric authentication (such as fingerprint scans) or PINs, making them ideal for users who may find traditional passwords or other authentication methods challenging. FIDO2 keys are beneficial for users with physical disabilities who may have difficulty typing complex passwords.

For more information, see [How to register passkey (FIDO2)](/en-us/entra/identity/authentication/how-to-register-passkey-with-security-key).

## Windows Hello for Business

Windows Hello for Business leverages biometric authentication (facial recognition or fingerprint) and PINs, offering a quick, secure, and accessible MFA option. This method eliminates the need for password input, which can be challenging for users with physical or cognitive disabilities. Biometric authentication allows for seamless access while maintaining strong security.

For more information, see [Windows Hello for Business](/en-us/windows/security/identity-protection/hello-for-business/policy-settings?tabs=feature).

## Email verification

While not as secure as other MFA methods, email verification can be useful in certain accessibility scenarios, providing a fallback option. For users who experience difficulty with text, voice, or app-based authentication, email can offer a familiar and easily accessible alternative.

References:

- [Available verification methods](/en-us/entra/identity/authentication/concept-mfa-howitworks)
- [How to enable MFA](/en-us/entra/identity/authentication/tutorial-enable-azure-mfa)

## Conclusion

Microsoft Entra ID's range of MFA options enables individuals with diverse needs to access secure authentication without compromising on usability. To ensure that security measures remain accessible and inclusive for all users, Microsoft Entra ID offers various options like the Authenticator app, SMS and voice calls, FIDO2 keys, Windows Hello, and email verification.

Selecting the right MFA method depends on individual needs and constraints. Microsoft’s commitment to flexible and inclusive authentication helps everyone stay secure, regardless of their physical or technological limitations. For those with specific accessibility requirements, it’s worth exploring each MFA option to find the one that aligns best with personal preferences and usability needs.
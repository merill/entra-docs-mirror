---
layout: Conceptual
title: Achieve NIST AAL2 with the Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/nist-authenticator-assurance-level-2
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Guidance on achieving NIST authenticator assurance level 2 (AAL2) with Microsoft Entra ID.
ms.service: entra
ms.subservice: standards
ms.topic: how-to
author: janicericketts
ms.author: jricketts
ms.reviewer: martinco, gasinh
ms.date: 2024-09-27T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 230430f9-e55a-1848-d5c0-c0a8f1c41787
document_version_independent_id: f25077cb-ebd8-8e5e-c584-cc0fe5958c47
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/nist-authenticator-assurance-level-2.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/nist-authenticator-assurance-level-2
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/nist-authenticator-assurance-level-2.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 518f3723-4aa3-a04c-47e1-cd090ba0426f
---

# Achieve NIST AAL2 with the Microsoft Entra ID - Microsoft Entra | Microsoft Learn

The National Institute of Standards and Technology (NIST) develops technical requirements for US federal agencies implementing identity solutions. Organizations working with federal agencies must meet these requirements.

Before starting authenticator assurance level 2 (AAL2), you can see the following resources:

- [NIST overview](nist-overview): Understand AAL levels
- [Authentication basics](nist-authentication-basics): Terminology and authentication types
- [NIST authenticator types](nist-authenticator-types): Authenticator types
- [NIST AALs](nist-about-authenticator-assurance-levels): AAL components and Microsoft Entra authentication methods

## Permitted AAL2 authenticator types

The following table has authenticator types permitted for AAL2:

| Microsoft Entra authentication method | Phishing Resistant | NIST authenticator type |
| --- | --- | --- |
| **Recommended methods** |  |  |
| Multi-factor software certificate  Windows Hello for Business with software Trusted Platform Module (TPM) | Yes | Multi-factor crypto software |
| Multi-factor hardware protected certificate  FIDO 2 security key  Platform SSO for macOS (Secure Enclave)  Windows Hello for Business with hardware TPM  Passkey in Microsoft Authenticator | Yes | Multi-factor crypto hardware |
| **Additional methods** |  |  |
| Microsoft Authenticator app (Phone Sign-in) | No | Multi-factor out-of-band |
| Password **OR** QR Code (PIN) **AND**- Microsoft Authenticator app (Push Notification) - **OR**- Microsoft Authenticator Lite (Push Notification) - **OR**- Phone (SMS) | No | Memorized secret **AND** Single-factor out-of-band |
| Password **OR** QR Code (PIN) **AND**- OATH hardware tokens (preview) - **OR**- Microsoft Authenticator app (OTP)- **OR**- Microsoft Authenticator Lite (OTP)- **OR**- OATH software tokens | No | Memorized secret **AND**Single-factor OTP |
| Password **OR** QR Code (PIN) **AND**- Single-factor software certificate - **OR**- Microsoft Entra joined with software TPM - **OR**- Microsoft Entra hybrid joined with software TPM - **OR**- Compliant mobile device | Yes^1^ | Memorized secret **AND** Single-factor crypto software |
| Password **OR** QR Code (PIN) **AND**- Microsoft Entra joined with hardware TPM - **OR**- Microsoft Entra hybrid joined with hardware TPM | Yes^1^ | Memorized secret **AND**Single-factor crypto hardware |

^1^[Protection from external phishing](memo-22-09-multi-factor-authentication#protection-from-external-phishing)

### AAL2 recommendations

For AAL2, use multi-factor cryptographic authenticator. This is phishing resistant, eliminates the greatest attack surface (the password), and offers users a streamlined method to authenticate.

For guidance on selecting a passwordless authentication method, see [Plan a passwordless authentication deployment in Microsoft Entra ID](../identity/authentication/howto-authentication-passwordless-deployment). See also, [Windows Hello for Business deployment guide](/en-us/windows/security/identity-protection/hello-for-business/hello-deployment-guide)

## FIPS 140 validation

Use the following sections to learn about FIPS 140 validation.

### Verifier requirements

Microsoft Entra ID uses the Windows FIPS 140 Level 1 overall validated cryptographic module for authentication cryptographic operations. It's therefore a FIPS 140-compliant verifier required by government agencies.

### Authenticator requirements

Government agency cryptographic authenticators are validated for FIPS 140 Level 1 overall. This requirement isn't for non-governmental agencies. The following Microsoft Entra authenticators meet the requirement when running on [Windows in a FIPS 140-approved mode](/en-us/windows/security/security-foundations/certification/fips-140-validation):

- Password
- Microsoft Entra joined with software or with hardware TPM
- Microsoft Entra hybrid joined with software or with hardware TPM
- Windows Hello for Business with software or with hardware TPM
- Certificate stored in software or hardware (smartcard/security key/TPM)

For Microsoft Authenticator app (iOS/Android) FIPS 140 compliance information, See [FIPS 140 compliant for Microsoft Entra authentication](../identity/authentication/concept-authentication-authenticator-app#fips-140-compliant-for-microsoft-entra-authentication)

For OATH hardware tokens and smartcards we recommend you consult with your provider for current FIPS validation status.

FIDO 2 security key providers are in various stages of FIPS certification. We recommend you review the list of [supported FIDO 2 key vendors](../identity/authentication/concept-authentication-passkeys-fido2). Consult with your provider for current FIPS validation status.

Platform SSO for macOS is FIPS 140 compliant. We recommend referring to the [Apple Platform Certifications](https://support.apple.com/guide/certifications/apc3a7433eb89/web).

## Reauthentication

For AAL2, the NIST requirement is reauthentication every 12 hours, regardless of user activity. Reauthentication is required after a period of inactivity of 30 minutes or longer. Because the session secret is something you have, presenting something you know, or are, is required.

To meet the requirement for reauthentication, regardless of user activity, Microsoft recommends configuring [user sign-in frequency](../identity/conditional-access/howto-conditional-access-session-lifetime) to 12 hours.

With NIST you can use compensating controls to confirm subscriber presence:

- Set session inactivity time out to 30 minutes: Lock the device at the operating system level with Microsoft System Center Configuration Manager, group policy objects (GPOs), or Intune. For the subscriber to unlock it, require local authentication.
- Time out regardless of activity: Run a scheduled task (Configuration Manager, GPO, or Intune) to lock the machine after 12 hours, regardless of activity.

## Man-in-the-middle resistance

Communications between the claimant and Microsoft Entra ID are over an authenticated, protected channel. This configuration provides resistance to man-in-the-middle (MitM) attacks and satisfies the MitM resistance requirements for AAL1, AAL2, and AAL3.

## Replay resistance

Microsoft Entra authentication methods at AAL2 use nonce or challenges. The methods resist replay attacks because the verifier detects replayed authentication transactions. Such transactions won't contain needed nonce or timeliness data.
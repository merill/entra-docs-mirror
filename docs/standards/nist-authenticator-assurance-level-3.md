---
layout: Conceptual
title: Achieve NIST AAL3 by using Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/nist-authenticator-assurance-level-3
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: This article provides guidance on achieving NIST authenticator assurance level 3 (AAL3) by using Microsoft Entra ID.
ms.service: entra
ms.subservice: standards
ms.topic: how-to
author: janicericketts
ms.author: jricketts
ms.reviewer: martinco, gasinh
ms.date: 2022-09-13T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 36a92a90-4b26-8f6f-5c90-77dec7b55c95
document_version_independent_id: 5d2b6ef8-126a-a7cd-3fd5-b91fcb81065b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/nist-authenticator-assurance-level-3.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/nist-authenticator-assurance-level-3
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/nist-authenticator-assurance-level-3.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/798bd9d1-9cc5-4fc7-b0e5-8699d1f6ce2a
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b5dc5f65-34a8-4bfc-9917-97d1e20c88b2
platformId: 825db1c6-6df4-a7ed-2cf8-0fb7ece77df4
---

# Achieve NIST AAL3 by using Microsoft Entra ID - Microsoft Entra | Microsoft Learn

Use the information in this article for National Institute of Standards and Technology (NIST) authenticator assurance level 3 (AAL3).

Before obtaining AAL2, you can review the following resources:

- [NIST overview](nist-overview): Understand AAL levels
- [Authentication basics](nist-authentication-basics): Terminology and authentication types
- [NIST authenticator types](nist-authenticator-types): Authenticator types
- [NIST AALs](nist-about-authenticator-assurance-levels): AAL components and Microsoft Entra authentication methods

## Permitted authenticator types

Use Microsoft authentication methods to meet required NIST authenticator types.

| Microsoft Entra authentication methods | NIST authenticator type |
| --- | --- |
| **Recommended methods** |  |
| Multi-factor hardware protected certificate  FIDO 2 security key  Platform SSO for macOS (Secure Enclave)  Windows Hello for Business with hardware TPM  Passkey in Microsoft Authenticator^1^ | Multi-factor cryptographic hardware |
| **Additional methods** |  |
| Password **OR** QR Code (PIN) **AND**Single-factor hardware protected certificate | Memorized secret **AND**Single-factor cryptographic hardware |

^1^ Passkey in Microsoft Authenticator is overall considered partial AAL3 and can qualify as AAL3 on platforms with FIPS 140 Level 2 Overall (or higher) and FIPS 140 level 3 physical security (or higher). For additional information on FIPS 140 compliance for Microsoft Authenticator (iOS/Android) See [FIPS 140 compliant for Microsoft Entra authentication](../identity/authentication/concept-authentication-authenticator-app#fips-140-compliant-for-microsoft-entra-authentication)

### Recommendations

For AAL3, we recommend using a multi-factor cryptographic hardware authenticator that provides passwordless authentication eliminating the greatest attack surface, the password.

For guidance, see [Plan a passwordless authentication deployment in Microsoft Entra ID](../identity/authentication/howto-authentication-passwordless-deployment). See also [Windows Hello for Business deployment guide](/en-us/windows/security/identity-protection/hello-for-business/hello-deployment-guide).

## FIPS 140 validation

### Verifier requirements

Microsoft Entra ID uses the Windows FIPS 140 Level 1 overall validated cryptographic module for its authentication cryptographic operations, making Microsoft Entra ID a compliant verifier.

### Authenticator requirements

Single-factor and multi-factor cryptographic hardware authenticator requirements.

#### Single-factor cryptographic hardware

Authenticators are required to be:

- FIPS 140 Level 1 Overall, or higher
- FIPS 140 Level 3 Physical Security, or higher

Single-factor hardware protected certificate used with Windows device meet this requirement when:

- You run [Windows in a FIPS-140 approved mode](/en-us/windows/security/security-foundations/certification/fips-140-validation)
- On a machine with a TPM that's FIPS 140 Level 1 Overall, or higher, with FIPS 140 Level 3 Physical Security

    - Find compliant TPMs: search for Trusted Platform Module and TPM on [Cryptographic Module Validation Program](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/validated-modules/Search).

Consult your mobile device vendor to learn about their adherence with FIPS 140.

#### Multi-factor cryptographic hardware

Authenticators are required to be:

- FIPS 140 Level 2 Overall, or higher
- FIPS 140 Level 3 Physical Security, or higher

FIDO 2 security keys, smart cards, and Windows Hello for Business can help you meet these requirements.

- Multiple FIDO2 security key providers meet FIPS requirements. We recommend you review the list of [supported FIDO2 key vendors](../identity/authentication/concept-fido2-hardware-vendor). Consult with your provider for current FIPS validation status.
- Smart cards are a proven technology. Multiple vendor products meet FIPS requirements.

    - Learn more on [Cryptographic Module Validation Program](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/validated-modules/Search)

**Windows Hello for Business**

FIPS 140 requires the cryptographic boundary, including software, firmware, and hardware, to be in scope for evaluation. Windows operating systems can be paired with thousands of these combinations. As such, it is not feasible for Microsoft to have Windows Hello for Business validated at FIPS 140 Security Level 2. Federal customers should conduct risk assessments and evaluate each of the following component certifications as part of their risk acceptance before accepting this service as AAL3:

- **Windows 10 and Windows Server** use the [US Government Approved Protection Profile for General Purpose Operating Systems Version 4.2.1](https://www.niap-ccevs.org/Profile/Info.cfm?PPID=442&amp;id=442) from the National Information Assurance Partnership (NIAP). This organization oversees a national program to evaluate commercial off-the-shelf (COTS) information technology products for conformance with the international Common Criteria.
- **Windows Cryptographic Library**[has FIPS Level 1 Overall in the NIST Cryptographic Module Validation Program](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Certificate/3544) (CMVP), a joint effort between NIST and the Canadian Center for Cyber Security. This organization validates cryptographic modules against FIPS standards.
- Choose a **Trusted Platform Module (TPM)** that's FIPS 140 Level 2 Overall, and FIPS 140 Level 3 Physical Security. Your organization ensures hardware TPM meets the AAL level requirements you want.

To determine the TPMs that meet current standards, go to [NIST Computer Security Resource Center Cryptographic Module Validation Program](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/validated-modules/Search). In the **Module Name** box, enter **Trusted Platform Module** for a list of hardware TPMs that meet standards.

**MacOS Platform SSO**

Apple macOS 13 (and above) are FIPS 140 Level 2 Overall, with most devices also FIPS 140 Level 3 Physical Security. We recommend referring to the [Apple Platform Certifications](https://support.apple.com/guide/certifications/apc3a7433eb89/web).

#### Passkey in Microsoft Authenticator

For additional information on FIPS 140 compliance for Microsoft Authenticator (iOS/Android) See [FIPS 140 compliant for Microsoft Entra authentication](../identity/authentication/concept-authentication-authenticator-app#fips-140-compliant-for-microsoft-entra-authentication)

## Reauthentication

For AAL3, NIST requirements are reauthentication every 12 hours, regardless of user activity. Reauthentication is recommended after a period of inactivity 15 minutes or longer. Presenting both factors is required.

To meet the requirement for reauthentication, regardless of user activity, Microsoft recommends configuring [user sign-in frequency](../identity/conditional-access/howto-conditional-access-session-lifetime) to 12 hours.

NIST allows for compensating controls to confirm subscriber presence:

- Set timeout, regardless of activity, by running a scheduled task using Configuration Manager, GPO, or Intune. Lock the machine after 12 hours, regardless of activity.
- For the recommended inactivity time out, you can set a session inactivity time out of 15 minutes: Lock the device at the OS level by using Microsoft Configuration Manager, Group Policy Object (GPO), or Intune. For the subscriber to unlock it, require local authentication.

## Man-in-the-middle resistance

Communications between the claimant and Microsoft Entra ID are over an authenticated, protected channel for resistance to man-in-the-middle (MitM) attacks. This configuration satisfies the MitM resistance requirements for AAL1, AAL2, and AAL3.

## Verifier impersonation resistance

Microsoft Entra authentication methods that meet AAL3 use cryptographic authenticators that bind the authenticator output to the session being authenticated. The methods use a private key controlled by the claimant. The public key is known to the verifier. This configuration satisfies the verifier-impersonation resistance requirements for AAL3.

## Verifier compromise resistance

All Microsoft Entra authentication methods that meet AAL3:

- Use a cryptographic authenticator that requires the verifier store a public key corresponding to a private key held by the authenticator
- Store the expected authenticator output by using FIPS-140 validated hash algorithms

For more information, see [Microsoft Entra Data Security Considerations](https://aka.ms/AADDataWhitepaper).

## Replay resistance

Microsoft Entra authentication methods that meet AAL3 use nonce or challenges. These methods are resistant to replay attacks because the verifier can detect replayed authentication transactions. Such transactions won't contain the needed nonce or timeliness data.

## Authentication intent

Requiring authentication intent makes it more difficult for directly connected physical authenticators, like multi-factor cryptographic hardware, to be used without the subject's knowledge (for example, by malware on the endpoint). Microsoft Entra methods that meet AAL3 require user entry of pin or biometric, demonstrating authentication intent.
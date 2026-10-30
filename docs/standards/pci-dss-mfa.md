---
layout: Conceptual
title: Microsoft Entra PCI-DSS Multi-Factor Authentication guidance - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/pci-dss-mfa
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Learn the authentication methods supported by Microsoft Entra ID to meet PCI MFA requirements
ms.service: entra
ms.subservice: standards
ms.topic: how-to
author: janicericketts
ms.author: jricketts
ms.reviewer: martinco, jricketts
ms.date: 2023-04-18T00:00:00.0000000Z
ms.custom: it-pro
ms.collection: 
locale: en-us
document_id: 781fad92-8cd6-a727-c329-21494e68574d
document_version_independent_id: f4009201-641f-cdbc-31c2-ed131fa36f76
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/pci-dss-mfa.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/pci-dss-mfa
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/pci-dss-mfa.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
platformId: 41efc37d-034e-262b-69c4-93f11dd8d41c
---

# Microsoft Entra PCI-DSS Multi-Factor Authentication guidance - Microsoft Entra | Microsoft Learn

**Information Supplement: Multi-Factor Authentication v 1.0**

Use the following table of authentication methods supported by Microsoft Entra ID to meet requirements in the PCI Security Standards Council [Information Supplement, Multi-Factor Authentication v 1.0](https://listings.pcisecuritystandards.org/pdfs/Multi-Factor-Authentication-Guidance-v1.pdf).

| Method | To meet requirements | Protection | MFA element |
| --- | --- | --- | --- |
| [Passwordless phone sign in with Microsoft Authenticator](../identity/authentication/howto-authentication-passwordless-phone) | Something you have (device with a key), something you know or are (PIN or biometric)  In iOS, Authenticator Secure Element (SE) stores the key in Keychain. [Apple Platform Security, Keychain data protection](https://support.apple.com/guide/security/keychain-data-protection-secb0694df1a/web) In Android, Authenticator uses Trusted Execution Engine (TEE) by storing the key in Keystore. [Developers, Android Keystore system](https://developer.android.com/training/articles/keystore) When users authenticate using Microsoft Authenticator, Microsoft Entra ID generates a random number the user enters in the app. This action fulfills the out-of-band authentication requirement. | Customers configure device protection policies to mitigate device compromise risk. For instance, Microsoft Intune compliance policies. | Users unlock the key with the gesture, then Microsoft Entra ID validates the authentication method. |
| [Windows Hello for Business Deployment Prerequisite Overview](/en-us/windows/security/identity-protection/hello-for-business/hello-identity-verification) | Something you have (Windows device with a key), and something you know or are (PIN or biometric).  Keys are stored with device Trusted Platform Module (TPM). Customers use devices with hardware TPM 2.0 or later to meet the authentication method independence and out-of-band requirements. [Certified Authenticator Levels](https://fidoalliance.org/certification/authenticator-certification-levels/) | Configure device protection policies to mitigate device compromise risk. For instance, Microsoft Intune compliance policies. | Users unlock the key with the gesture for Windows device sign in. |
| [Enable passwordless security key sign-in, Enable FIDO2 security key method](../identity/authentication/howto-authentication-passwordless-security-key) | Something that you have (FIDO2 security key) and something you know or are (PIN or biometric).  Keys are stored with hardware cryptographic features. Customers use FIDO2 keys, at least Authentication Certification Level 2 (L2) to meet the authentication method independence and out-of-band requirement. | Procure hardware with protection against tampering and compromise. | Users unlock the key with the gesture, then Microsoft Entra ID validates the credential. |
| [Overview of Microsoft Entra certificate-based authentication](../identity/authentication/concept-certificate-based-authentication) | Something you have (smart card) and something you know (PIN).  Physical smart cards or virtual smartcards stored in TPM 2.0 or later, are a Secure Element (SE). This action meets the authentication method independence and out-of-band requirement. | Procure smart cards with protection against tampering and compromise. | Users unlock the certificate private key with the gesture, or PIN, then Microsoft Entra ID validates the credential. |
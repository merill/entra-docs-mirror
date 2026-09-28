---
layout: Conceptual
title: Limitations with Microsoft Entra certificate-based authentication without federation - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-certificate-based-authentication-limitations
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn supported and unsupported scenarios for Microsoft Entra certificate-based authentication
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: vimrang
ms.custom: has-adal-ref
locale: en-us
document_id: e9dcd7a8-230b-ae33-5f15-db2bf32018b5
document_version_independent_id: 8f302cc8-b87d-8503-d5e6-0451bef3d233
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-certificate-based-authentication-limitations.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-certificate-based-authentication-limitations
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-certificate-based-authentication-limitations.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 91d556a4-c00d-6e06-44e3-7f4ffa928289
---

# Limitations with Microsoft Entra certificate-based authentication without federation - Microsoft Entra ID | Microsoft Learn

This article covers supported and unsupported scenarios for Microsoft Entra certificate-based authentication.

## Supported scenarios

The following scenarios are supported:

- User sign-ins to web browser-based applications on all platforms.
- User sign-ins to Office mobile apps, including Outlook, OneDrive, and so on.
- User sign-ins on mobile native browsers.
- Support for granular authentication rules for multifactor authentication by using the certificate issuer **Subject** and **policy OIDs**.
- Configuring certificate-to-user account bindings by using any of the certificate fields:
    - Subject Alternate Name (SAN) PrincipalName and SAN RFC822Name
    - Subject Key Identifier (SKI) and SHA1PublicKey
- Configuring certificate-to-user account bindings by using any of the user object attributes:
    - User Principal Name
    - onPremisesUserPrincipalName
    - CertificateUserIds

## Unsupported scenarios

The following scenarios aren't supported:

- Public Key Infrastructure for creating client certificates. Customers need to configure their own Public Key Infrastructure (PKI) and provision certificates to their users and devices.
- Certificate Authority hints aren't supported, so the list of certificates that appears for users in the UI isn't scoped.
- Only one CRL Distribution Point (CDP) for a trusted CA is supported.
- The CDP can be only HTTP URLs. We don't support Online Certificate Status Protocol (OCSP), or Lightweight Directory Access Protocol (LDAP) URLs.
- Configuring other certificate-to-user account bindings, such as using the **subject + issuer** or **Issuer + Serial Number**, aren’t available in this release.
- Currently, password can't be disabled when CBA is enabled and the option to sign in using a password is displayed.

## Supported operating systems

| Operating system | Certificate on-device/Derived PIV | Smart cards |
| --- | --- | --- |
| Windows | ✅ | ✅ |
| macOS | ✅ | ✅ |
| iOS | ✅ | Supported vendors only |
| Android | ✅ | Supported vendors only |

## Supported browsers

| Operating system | Chrome certificate on-device | Chrome smart card | Safari certificate on-device | Safari smart card | Microsoft Edge certificate on-device | Microsoft Edge smart card |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| macOS | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| iOS | ❌ | ❌ | ✅ | Supported vendors only | ❌ | ❌ |
| Android | ✅ | ❌ | N/A | N/A | ❌ | ❌ |

Note

On iOS and Android mobile, Microsoft Edge browser users can sign into Microsoft Edge to set up a profile by using the Microsoft Authentication Library (MSAL), like the Add account flow. When logged in to Microsoft Edge with a profile, CBA is supported with on-device certificates and smart cards.

## Smart card providers

| Provider | Windows | macOS | iOS | Android |
| --- | --- | --- | --- | --- |
| YubiKey | ✅ | ✅ | ✅ | ✅ |
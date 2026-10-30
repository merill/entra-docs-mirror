---
layout: Conceptual
title: Ciphers for Microsoft Entra Private Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/reference-ciphers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn about the supported cryptographic algorithms, or ciphers, used for Microsoft Entra Private Access.
ms.topic: reference
ms.date: 2026-03-09T00:00:00.0000000Z
ms.reviewer: sumeetmittal
locale: en-us
document_id: d168c238-9edd-4784-fdb8-37c42bc5908e
document_version_independent_id: d168c238-9edd-4784-fdb8-37c42bc5908e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/reference-ciphers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/reference-ciphers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/reference-ciphers.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 964c4b12-30d7-73d5-b355-c9bddf2ed739
---

# Ciphers for Microsoft Entra Private Access - Global Secure Access | Microsoft Learn

Microsoft Entra private network connector supports Transport Layer Security (TLS) 1.2, TLS 1.3, and higher, according to the TLS version the customer chooses to enforce.

## Cipher suites

A cipher suite is a set of cryptographic algorithms used to create a secure connection. TLS 1.2 and TLS 1.3 use the default Windows ciphers.

The following tables list the supported cipher suites for TLS 1.3 and TLS 1.2.

| # TLS 1.3 (suites in server-preferred order) | - | - | - |
| --- | --- | --- | --- |
| TLS\_AES\_256\_GCM\_SHA384 (0x1302) | ECDH secp384r1 (eq. 7680 bits RSA) | FS |  |
| TLS\_AES\_128\_GCM\_SHA256 (0x1301) | ECDH secp256r1 (eq. 3072 bits RSA) | FS |  |

| # TLS 1.2 (suites in server-preferred order) | - | - | - |
| --- | --- | --- | --- |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_GCM\_SHA384 (0xc030) | ECDH secp384r1 (eq. 7680 bits RSA) | FS |  |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_GCM\_SHA256 (0xc02f) | ECDH secp256r1 (eq. 3072 bits RSA) | FS |  |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA384 (0xc028) | ECDH secp384r1 (eq. 7680 bits RSA) | FS | **WEAK** |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0xc027) | ECDH secp256r1 (eq. 3072 bits RSA) | FS | **WEAK** |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA (0xc014) | ECDH secp384r1 (eq. 7680 bits RSA) | FS | **WEAK** |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA (0xc013) | ECDH secp256r1 (eq. 3072 bits RSA) | FS | **WEAK** |
| TLS\_RSA\_WITH\_AES\_256\_GCM\_SHA384 (0x9d) |  |  | **WEAK** |
| TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256 (0x9c) |  |  | **WEAK** |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA256 (0x3d) |  |  | **WEAK** |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0x3c) |  |  | **WEAK** |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA (0x35) |  |  | **WEAK** |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA (0x2f) |  |  | **WEAK** |

## Filter ciphers

To determine which of the default TLS 1.2 and TLS 1.3 ciphers to use and which to filter out, consider factors such as:

- The connector operating system.
- The TLS library.
- The application configuration.

To view the list of ciphers:

1. Use a protocol analyzer such as Wireshark to view specific requests to the connector.
2. Expand the **Client Hello** message.
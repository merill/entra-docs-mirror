---
layout: Conceptual
title: TLS 1.2 enforcement - Microsoft Entra Registration Service - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/reference-device-registration-tls-1-2
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Remove support for TLS 1.0 and 1.1 for the Microsoft Entra Device Registration Service
ms.topic: reference
ms.date: 2025-06-27T00:00:00.0000000Z
ms.reviewer: spunukol
locale: en-us
document_id: b766b07d-1acb-66e8-7c75-53b6091c6a6f
document_version_independent_id: 98f59912-cc2c-1d7f-ffb3-aa7e311d7b8f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/reference-device-registration-tls-1-2.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/reference-device-registration-tls-1-2
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/reference-device-registration-tls-1-2.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 6fbab6df-5ad4-5d76-6c67-051993d71b46
---

# TLS 1.2 enforcement - Microsoft Entra Registration Service - Microsoft Entra ID | Microsoft Learn

The Microsoft Entra Device Registration Service is used to connect devices to the cloud with a device identity. The Microsoft Entra Device Registration Service currently supports using Transport Layer Security (TLS) 1.2 for communications with Azure. To ensure security and best-in-class encryption, Microsoft recommends disabling TLS 1.0 and 1.1. This document will provide information on how to ensure machines used to complete registration and communicate with the Microsoft Entra Device Registration Service use TLS 1.2.

The TLS protocol version 1.2 is a cryptography protocol that is designed to provide secure communications. The TLS protocol aims primarily to provide privacy and data integrity. TLS has gone through many iterations with version 1.2 being defined in [RFC 5246 (external link)](https://tools.ietf.org/html/rfc5246).

Current analysis of connections shows little TLS 1.1 and 1.0 usage, but we are providing this information so that you can update any affected clients or servers as necessary before support for TLS 1.1 and 1.0 ends. If you are using any on-premises infrastructure for hybrid scenarios or Active Directory Federation Services (AD FS), make sure that the infrastructure can support both inbound and outbound connections that use TLS 1.2.

## Update Windows servers

For Windows servers that use the Microsoft Entra Device Registration Service or act as proxies, use the following steps to ensure TLS 1.2 is enabled:

Important

After you have updated the registry, you must restart the Windows server for the changes to take effect.

### Enable TLS 1.2

Ensure the following registry strings are configured as shown:

- HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client
    - "DisabledByDefault"=dword:00000000
    - "Enabled"=dword:00000001
- HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server
    - "DisabledByDefault"=dword:00000000
    - "Enabled"=dword:00000001
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft.NETFramework\v4.0.30319
    - "SchUseStrongCrypto"=dword:00000001

## Update non-Windows proxies

Any machines that act as proxies between devices and the Microsoft Entra Device Registration Service must ensure that TLS 1.2 is enabled. Follow your vendor's guidance to ensure support.

## Update AD FS servers

Any AD FS servers used to communicate with the Microsoft Entra Device Registration Service must ensure that TLS 1.2 is enabled. See [Managing SSL/TLS Protocols and Cipher Suites for AD FS](/en-us/windows-server/identity/ad-fs/operations/manage-ssl-protocols-in-ad-fs) for information on how to enable/verify this configuration.

## Client updates

Since all client-server and browser-server combinations must use TLS 1.2 to connect with the Microsoft Entra Device Registration Service, you may need to update these devices.

The following clients are known to be unable to support TLS 1.2. Update your clients to ensure uninterrupted access.

- Android version 4.3 and earlier
- Firefox version 5.0 and earlier
- Internet Explorer versions 8-10 on Windows 7 and earlier
- Internet Explorer 10 on Windows Phone 8.0
- Safari version 6.0.4 on OS X 10.8.4 and earlier
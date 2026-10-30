---
layout: Conceptual
title: Learn about the Global Secure Access clients for Microsoft Entra Private Access and Microsoft Entra Internet Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/concept-clients
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn about the Global Secure Access clients for Microsoft Entra Private Access and Microsoft Entra Internet Access.
ms.topic: concept-article
ms.date: 2026-03-12T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: af585d0f-bfeb-9671-ce73-6d23468d312b
document_version_independent_id: af585d0f-bfeb-9671-ce73-6d23468d312b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/concept-clients.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/concept-clients
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/concept-clients.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 2e578513-37ad-4062-dbec-2f8a244884c5
---

# Learn about the Global Secure Access clients for Microsoft Entra Private Access and Microsoft Entra Internet Access - Global Secure Access | Microsoft Learn

## Overview

The Global Secure Access client gives organizations control over network traffic at the end-user computing device. With this client, organizations can route specific traffic profiles through Microsoft Entra Internet Access and Microsoft Entra Private Access. Routing traffic in this method allows for more controls like continuous access evaluation (CAE), device compliance, or multifactor authentication to be required for resource access.

The Global Secure Access client uses a lightweight filter (LWF) driver to acquire traffic. In contrast, many other Security Service Edge (SSE) solutions integrate as a virtual private network (VPN) connection. This distinction allows the Global Secure Access client to coexist with these other solutions. The Global Secure Access client acquires traffic based on the traffic forwarding profiles you configure.

## Available clients

You install the client on a device, such as computer or phone, and then use Global Secure Access settings in the Microsoft Entra admin center to secure the device. Clients are currently available for Windows, Android, macOS, and iOS. For more information about installing the Windows client, see [Global Secure Access client for Windows](how-to-install-windows-client). For more information about installing the Android client, see [Global Secure Access client for Android](how-to-install-android-client). For more information about installing the macOS client, see [Global Secure Access client for macOS](how-to-install-macos-client). For more information about installing the iOS client, see [Global Secure Access client for iOS](how-to-install-ios-client).
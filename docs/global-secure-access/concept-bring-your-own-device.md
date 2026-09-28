---
layout: Conceptual
title: Learn about bring your own device (BYOD) with the Global Secure Access clients for Microsoft Entra Private Access and Microsoft Entra Internet Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/concept-bring-your-own-device
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn about bring your own device (BYOD) with the Global Secure Access clients for Microsoft Entra Private Access and Microsoft Entra Internet Access.
ms.topic: concept-article
ms.date: 2026-03-12T00:00:00.0000000Z
ms.reviewer: gauthamca
ai-usage: ai-assisted
locale: en-us
document_id: 7b586cd0-146a-8cce-f853-933f6451a2ed
document_version_independent_id: 7b586cd0-146a-8cce-f853-933f6451a2ed
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/concept-bring-your-own-device.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/concept-bring-your-own-device
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/concept-bring-your-own-device.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 140da440-cc9f-22b6-fd3a-615821ba5cc0
---

# Learn about bring your own device (BYOD) with the Global Secure Access clients for Microsoft Entra Private Access and Microsoft Entra Internet Access - Global Secure Access | Microsoft Learn

## Overview

The Global Secure Access client supports bring your own device (BYOD) scenarios so users can access company resources. As a tenant administrator, enable Global Secure Access traffic profiles for members, including internal guests. The client supports automatic Microsoft Entra device registration.

Important

To block access from BYOD, configure conditional access policy to allow access only from a compliant device.

## Windows

- Supports secure access on Microsoft Entra registered Windows devices.
- Only private application traffic is supported. Enable Private Access traffic profiles for these users.
- If the device isn’t registered or joined, the client registers the device to your tenant during first sign-in.
- If the device isn’t joined and has multiple registrations, the user selects the tenant at sign-in with Microsoft Entra user of the tenant.
- Supports an account picker in the sign-in flow to make it easier to sign in with a different account.
- The account picker appears by default on Microsoft Entra-registered devices.
- To enable the account picker or to switch to another tenant on Microsoft Entra-joined devices, enable the **Sign out** option. For details, see [Hide or unhide menu buttons in the system tray](how-to-install-windows-client#hide-or-unhide-system-tray-menu-buttons).

Important

On Windows devices that are Microsoft Entra joined or hybrid joined, the client connects to the joined tenant by default.

## Android

- BYOD support without device enrollment is available using Microsoft Authenticator or the Microsoft Intune Company Portal through Microsoft Entra device registration.
- On the device:
    1. Install Microsoft Authenticator from the App Store and register the device to the tenant or install the Company Portal app (no device enrollment required).
    2. Install the Microsoft Defender app from Google Play and complete sign-in.
    3. A device-wide VPN profile is created. The Global Secure Access tile is off by default; the user must turn it on to send Private Access traffic.
- Enable private traffic profiles for these users.

## iOS

- BYOD support without device enrollment is available using Microsoft Authenticator through Microsoft Entra device registration.
- On the device:
    1. Install Microsoft Authenticator from the App Store and register the device to the tenant.
    2. Install the Microsoft Defender app from App Store and complete sign-in.
    3. A device-wide VPN profile is created. The Global Secure Access tile is off by default; the user must turn it on to send Private Access traffic.
- Enable private traffic profiles for these users.

## MacOS

MacOS devices must be enrolled through a Mobile Device Management (MDM) solution. BYOD scenarios without device enrollment aren't supported on macOS.

### Platform behavior

| Platform/device state | Connection target | Microsoft Entra tunnel | M365 tunnel | Internet tunnel | Private tunnel | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| Windows Microsoft Entra Joined and Hybrid joined device | Client connects to the tenant to which device joined. | ✅ | ✅ | ✅ | ✅ | Enable the Sign out option in the client to allow users to sign out and switch to an external tenant. Allows user to switch to a resource tenant using external user access(B2B). |
| Windows Microsoft Entra Registered device | User selects a tenant at first sign-in. | ❌ | ❌ | ❌ | ✅ | Can switch to other tenant by selecting **Sign out** option on the client. Allows user to switch to a resource tenant using external user access(B2B). |
| macOS Microsoft Entra Registered device with device enrollment | User selects a tenant at first sign-in; remains connected to that tenant | ✅ | ✅ | ✅ | ✅ | Requires device enrollment through an MDM solution. |
| Android Microsoft Entra Registered with and without device enrollment | User selects a tenant at first sign-in; remains connected to that tenant | ✅ | ✅ | ✅ | ✅ | Applies to enrolled devices with Company Portal. For unmanaged devices, Microsoft Entra registration can be done with Company portal and Authenticator app. |
| iOS Microsoft Entra Registered with and without device enrollment | User selects a tenant at first sign-in; remains connected to that tenant | ✅ | ✅ | ✅ | ✅ | Applies to enrolled devices with Company Portal. For unmanaged devices, Microsoft Entra registration can be done with Authenticator app. |

### Summary

- ✅ Device join takes precedence on Windows.
- ✅ Registered devices choose a tenant at initial sign-in.
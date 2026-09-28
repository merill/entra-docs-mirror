---
layout: Conceptual
title: Manage preferences for Microsoft Single Sign-on for macOS - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/macos-manage-preferences
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: ploegert
ms.author: jploegert
ms.service: entra-id
ms.subservice: devices
manager: asteen
description: This article helps users understand what preferences are within the Microsoft Single Sign-On for macOS app, and what each setting does
ms.topic: ui-reference
ms.date: 2026-06-30T00:00:00.0000000Z
locale: en-us
document_id: fe06a9eb-4d2f-a8b3-6d33-b83e531d5465
document_version_independent_id: fe06a9eb-4d2f-a8b3-6d33-b83e531d5465
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/macos-manage-preferences.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/macos-manage-preferences
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/macos-manage-preferences.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 2fbb8573-aacd-5103-d066-949720ccc322
---

# Manage preferences for Microsoft Single Sign-on for macOS - Microsoft Entra ID | Microsoft Learn

Select your preferences for single sign-on and in-app data collection in Microsoft Single Sign-on for macOS. To access your preferences:

1. Open Microsoft single sign on for macOS the app.
2. Go to the menu bar and select **Advanced**.

## Single sign-on

Single sign-on (SSO) configures your work or school account so that you only have to authenticate once to access all cloud-based work apps and services. Preferences include:

- **Register device**: Register your device to enable SSO and gain access to protected resources. This setting is only available on devices enabled for platform SSO.
- **Deregister**: Remove device registration and disable SSO. To access protected resources again on this device, you must reregister. This setting is only available on devices enabled for platform SSO.
- **Remove account from this device**: Remove your work or school account and any SSO authentication tokens from the device.

To opt out of SSO on your Mac, select the checkbox next to **Don't ask me to sign in with single sign-on for this device**.

## Send usage data to Microsoft

This setting enables Microsoft to collect data about your Intune Company Portal usage. When the checkbox is selected, your in-app performance and usage data are automatically anonymized and shared with Microsoft to help improve the reliability and performance of our products. Your organization doesn't have control over the collection of this data and cannot change your preference.

To turn off data collection in Company Portal, deselect the checkbox next to **Allow Microsoft to collect usage data**.

## Advanced logging

Select the checkbox next to **Turn on advanced logging** to turn on verbose logging, which is used for troubleshooting, for Microsoft Single Sign-on for macOS and MSAL. Microsoft Single Sign-on for macOS logs certificate usage and network responses when advanced logging is turned on. Advanced logging is turned off by default. Keep this setting turned off unless otherwise instructed by your organization's IT administrator.
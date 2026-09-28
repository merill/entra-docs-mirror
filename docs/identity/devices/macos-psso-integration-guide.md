---
layout: Conceptual
title: Integrate macOS Platform Single Sign-On (PSSO) into your MDM solution - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/macos-psso-integration-guide
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Learn how to integrate macOS Platform Single Sign-On (PSSO) into your MDM solution.
ms.topic: how-to
ms.date: 2025-07-23T00:00:00.0000000Z
locale: en-us
document_id: ea4241bc-c357-bfc9-f6d7-c71f4aa3ba1b
document_version_independent_id: ea4241bc-c357-bfc9-f6d7-c71f4aa3ba1b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/macos-psso-integration-guide.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/macos-psso-integration-guide
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/macos-psso-integration-guide.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d6b10980-49fb-4df0-7b1a-28f97359a618
---

# Integrate macOS Platform Single Sign-On (PSSO) into your MDM solution - Microsoft Entra ID | Microsoft Learn

Platform Single Sign-On (PSSO) for macOS devices is a feature that allows users to sign in to macOS devices using their Microsoft Entra credentials. This feature provides a seamless sign-in experience for users and helps organizations manage access to resources on macOS devices.

In this guide, you learn how to integrate macOS Platform Single Sign-On (PSSO) into your MDM solution. This guide is intended for developers of third party MDM solutions who want to support PSSO for macOS devices.

## Prerequisites

Before getting started, we recommend that you familiarize yourself with the following articles:

- Any documentation you were provided by Intune for Partner Managed Device Compliance Integration APIs
- [Microsoft Enterprise Single Sign-On (SSO) plug-in for Apple devices](../../identity-platform/apple-sso-plugin).
- [macOS Platform Single Sign-on overview](macos-psso).

## Minimum required payload properties

The following settings and payload properties are required for use with the [Microsoft Enterprise Single Sign-On (SSO) plug-in for Apple devices](../../identity-platform/apple-sso-plugin). Ensure these settings are configured with the following values and add other settings as required to ensure proper SSO for your apps.

| **Setting** | **Value(s)** |
| --- | --- |
| Extension identifier | com.microsoft.CompanyPortalMac.ssoextension |
| Team identifier | UBF8T346G9 |
| Authentication Method (Deprecated) [Required for OS13 devices] | One of... Password  UserSecureEnclaveKey |
| Authentication method (OS14+ devices) | One of... Password  UserSecureEnclaveKey  Smartcard (macOS 14+) |
| Screen Locked Behavior | Do Not Handle |
| Type | Redirect |
| URLs | Supply the following URLs `https://login.microsoftonline.com`https://login.microsoft.com`https://sts.windows.net`https://login.partner.microsoftonline.cnhttps://login.chinacloudapi.cnhttps://login.microsoftonline.ushttps://login-us.microsoftonline.com |
| Use Shared Device Keys | Enable "Use Shared Device Keys" for the best PSSO experience and to avoid unnecessary re-registration experiences if enabled later. |

## Event notifications

You may need to perform other actions upon completion of various PSSO events depending on the event's status. The following list contains notifications posted by the Entra ID SSO extension for various PSSO events. MDMs can choose to listen to these notifications and perform appropriate actions.

### Events

Consider using these events to record telemetry or monitoring for errors or success cases. Once Device & User registration have completed, you should mark the device compliant via the compliance API service.

| Notification Name | Trigger |
| --- | --- |
| Microsoft.PlatformSSO.DeviceRegistration.Started | Device registration started |
| Microsoft.PlatformSSO.DeviceRegistration.Succeeded | Device registration finished |
| Microsoft.PlatformSSO.DeviceRegistration.Failed | Device registration failed |
| Microsoft.PlatformSSO.UserRegistration.Started | User registration started |
| Microsoft.PlatformSSO.UserRegistration.Succeeded | User registration finished |
| Microsoft.PlatformSSO.UserRegistration.Failed | User registration failed |
| Microsoft.PlatformSSO.Registration.Succeeded | Both device and user registration finished |
| Microsoft.PlatformSSO.Registration.Failed | Either device or user registration failed |
| Microsoft.PlatformSSO.Registration.Removed | Platform SSO registration removed |
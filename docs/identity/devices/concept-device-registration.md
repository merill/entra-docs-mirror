---
layout: Conceptual
title: What are Microsoft Entra registered devices? - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/concept-device-registration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Learn how Microsoft Entra registered devices provide your users with support for bring your own device (BYOD) or mobile device scenarios.
ms.topic: concept-article
ms.date: 2025-06-27T00:00:00.0000000Z
ms.reviewer: sandeo
locale: en-us
document_id: 8b5b4ad9-f729-c381-3a69-8aa0daf0b89f
document_version_independent_id: ef468de3-24e5-52be-1984-b5ab4361b331
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/concept-device-registration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/concept-device-registration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/concept-device-registration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: a4248202-c6d8-e9de-870b-b39e3d36dd8c
---

# What are Microsoft Entra registered devices? - Microsoft Entra ID | Microsoft Learn

The goal of Microsoft Entra registered - also known as Workplace joined - devices is to provide your users with support for bring your own device (BYOD) or mobile device scenarios. In these scenarios, a user can access your organization's resources using a personal device.

| Microsoft Entra registered | Description |
| --- | --- |
| **Definition** | Registered to Microsoft Entra ID without requiring organizational account to sign in to the device |
| **Primary audience** | Applicable to all users with the following criteria: <br>- Bring your own device<br>- Mobile devices |
| **Device ownership** | User or Organization |
| **Operating Systems** | - Windows 10 or newer<br>- macOS 10.15 or newer<br>- iOS 15 or newer<br>- Android<br>- Linux editions:<br>- Ubuntu 22.04/24.04 LTS<br>- Red Hat Enterprise Linux 8/9 LTS |
| **Provisioning** | - Windows 10 or newer – Settings<br>- iOS/Android – Company Portal or Microsoft Authenticator app<br>- macOS – Company Portal<br>- Linux - Intune Agent |
| **Device sign in options** | - End-user local credentials<br>- Password<br>- Windows Hello<br>- PIN<br>- Biometrics or pattern for other devices |
| **Device management** | - Mobile Device Management (example: Microsoft Intune)<br>- Mobile Application Management |
| **Key capabilities** | - Single sign-on (SSO) to cloud resources<br>- Conditional Access when enrolled into Intune<br>- Conditional Access via App protection policy<br>- Enables Phone sign in with Microsoft Authenticator app |

![Microsoft Entra registered devices](media/concept-device-registration/azure-ad-registered-device.png)

Microsoft Entra registered devices are signed in to using a local account like a Microsoft account on a Windows 10 or newer device. These devices have a Microsoft Entra account for access to organizational resources. Access to resources in the organization can be limited based on that Microsoft Entra account and Conditional Access policies applied to the device identity.

Microsoft Entra Registration isn't the same as device enrollment. If Administrators permit users to enroll their devices, organizations can further control these Microsoft Entra registered devices by enrolling them into Mobile Device Management (MDM) tools like Microsoft Intune. MDM provides a means to enforce organization-required configurations like requiring storage to be encrypted, password complexity, and security software kept updated.

Microsoft Entra registration can be accomplished when accessing a work application for the first time or manually using the Windows 10 or Windows 11 Settings menu.

## Scenarios

A user in your organization wants to access your benefits enrollment tool from their home PC. Your organization requires that anyone accesses this tool from an Intune compliant device. The user registers their home PC with Microsoft Entra ID and Enrolls the device in Intune, then the required Intune policies are enforced giving the user access to their resources.

Another user wants to access their organizational email on their personal Android phone that is rooted. Your company requires a compliant device and has an Intune device compliance policy to block any rooted devices. The employee is stopped from accessing organizational resources on this device.

Note

Microsoft Entra registered devices don't support the [Unified Write Filter](/en-us/windows/configuration/unified-write-filter/) feature.
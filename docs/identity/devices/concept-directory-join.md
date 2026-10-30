---
layout: Conceptual
title: What is a Microsoft Entra joined device? - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/concept-directory-join
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Microsoft Entra joined devices can help you to manage devices accessing resources in your environment.
ms.topic: concept-article
ms.date: 2025-06-27T00:00:00.0000000Z
ms.reviewer: sandeo
locale: en-us
document_id: 08003efa-d3f6-6b9a-c855-67e356ba2e4f
document_version_independent_id: 60949414-f20a-951b-832a-7e2f3a1f342b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/concept-directory-join.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/concept-directory-join
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/concept-directory-join.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 86239553-90d2-a938-7e3b-69591760fc28
---

# What is a Microsoft Entra joined device? - Microsoft Entra ID | Microsoft Learn

Any organization can deploy Microsoft Entra joined devices no matter the size or industry. Microsoft Entra join works even in hybrid environments, enabling access to both cloud and on-premises apps and resources.

| Microsoft Entra join | Description |
| --- | --- |
| **Definition** | - Joined only to Microsoft Entra ID requiring organizational account to sign in to the device |
| **Primary audience** | - Suitable for both cloud-only and hybrid organizations.<br>- Applicable to all users in an organization |
| **Device ownership** | - Organization |
| **Operating Systems** | - All Windows 11 and Windows 10 devices except Home editions<br>- [Windows Enterprise multi-session Virtual Machines running in Azure](/en-us/azure/virtual-desktop/windows-multisession-faq#can-windows-enterprise-multi-session-be-microsoft-entra-joined)<br>- [Windows Server 2019 and newer Virtual Machines running in Azure](howto-vm-sign-in-azure-ad-windows) (Server core isn't supported)<br>- Apple devices running macOS 13 or newer<br>- Linux editions:<br>    - Ubuntu 22.04/24.04/26.04 LTS<br>    - Red Hat Enterprise Linux 9/10 LTS |
| **Provisioning** | - Self-service: Windows Out of Box Experience (OOBE) or Settings<br>- Bulk enrollment<br>- Windows Autopilot<br>- (Public preview) Apple Automated Device Enrollment (applies to Apple devices only) |
| **Device management** | - Mobile Device Management (example: Microsoft Intune)<br>- [Configuration Manager standalone or co-management with Microsoft Intune](/en-us/mem/configmgr/comanage/overview) |
| **Key capabilities** | - single sign-on (SSO) to both cloud and on-premises resources<br>- Conditional Access<br>- [Self-service Password Reset and Windows Hello PIN reset on lock screen](../authentication/howto-sspr-windows) |
|  |  |

## **Device sign in options**

The following are the supported sign-in options for Microsoft Entra joined devices. The availability of these options depends on the device's operating system and configuration. For example, Windows Hello for Business requires additional setup and may not be available on all devices.

| Platform | Password | SmartCard | Microsoft Authenticatorphone sign-in | [Windows Hello for Business](/en-us/windows/security/identity-protection/hello-for-business/hello-planning-guide)/[Platform Credentials](macos-psso) | Web Sign-In | FIDO2 |
| --- | --- | --- | --- | --- | --- | --- |
| Windows 10/11 | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| macOS 13+ | ✅ | ✅ |  | ✅ |  |  |
| Ubuntu 22.04/24.04/26.04 LTS | ✅ | ✅ | ✅ |  |  |  |
| RHEL 9/10 | ✅ | ⚠️ Preview | ✅ |  |  |  |

You sign in to Microsoft Entra joined devices using a Microsoft Entra account. Access to resources can be controlled based on your account and [Conditional Access policies](../conditional-access/policy-alt-all-users-compliant-hybrid-or-mfa) applied to the device.

Administrators can secure and further control Microsoft Entra joined devices using Mobile Device Management (MDM) tools like Microsoft Intune or in co-management scenarios using Microsoft Configuration Manager. These tools provide a means to enforce organization-required configurations like:

- Requiring storage to be encrypted
- Password complexity
- Software installation
- Software updates

Administrators can make organization applications available to Microsoft Entra joined devices using Configuration Manager to [Manage apps from the Microsoft Store for Business and Education](/en-us/mem/configmgr/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

Microsoft Entra join can be accomplished using self-service options like the Out of Box Experience (OOBE), bulk enrollment, [Apple Automated Device Enrollment (public preview)](/en-us/mem/intune/enrollment/device-enrollment-program-enroll-macos), or [Windows Autopilot](/en-us/autopilot/enrollment-autopilot).

Microsoft Entra joined devices can still maintain single sign-on access to on-premises resources when they are on the organization's network. Devices that are Microsoft Entra joined can still authenticate to on-premises servers like file, print, and other applications.

## Scenarios

Microsoft Entra join can be used in various scenarios like:

- You want to transition to cloud-based infrastructure using Microsoft Entra ID and MDM like Intune.
- You can't use an on-premises domain join, for example, if you need to get mobile devices such as tablets and phones under control.
- Your users primarily need to access Microsoft 365 or other software as a service (SaaS) apps integrated with Microsoft Entra ID.
- You want to manage a group of users in Microsoft Entra ID instead of in Active Directory. This scenario can apply, for example, to seasonal workers, contractors, or students.
- You want to provide joining capabilities to workers who work from home or are in remote branch offices with limited on-premises infrastructure.

You can configure Microsoft Entra join for all Windows 11 and Windows 10 devices except for Home editions.

The goal of Microsoft Entra joined devices is to simplify:

- Windows and macOS deployments of work-owned devices
- Access to organizational apps and resources from any Windows or macOS device
- Cloud-based management of work-owned devices
- Users to sign in to their devices with their Microsoft Entra ID or synced Active Directory work or school accounts.

![A diagram showing Microsoft Entra joined devices interacting with an on-premises domain.](media/concept-directory-join/azure-ad-joined-device.png)

Microsoft Entra join can be deployed by using any of the following methods:

- [Windows Autopilot](/en-us/autopilot/windows-autopilot)
- [Bulk deployment](/en-us/mem/intune/enrollment/windows-bulk-enroll)
- [Self-service experience](device-join-out-of-box)
- [Apple Automated Device Enrollment (public preview)](/en-us/mem/intune/enrollment/device-enrollment-program-enroll-macos)
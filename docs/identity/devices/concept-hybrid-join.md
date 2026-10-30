---
layout: Conceptual
title: What is a Microsoft Entra hybrid joined device? - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/concept-hybrid-join
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Learn how Microsoft Entra hybrid joined devices connect Active Directory and Microsoft Entra ID, and how Cloud Sync synchronizes their computer objects.
ms.topic: concept-article
ms.date: 2026-10-06T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1023
ai-usage: ai-assisted
ms.reviewer: sandeo
locale: en-us
document_id: 7003ad77-d8b2-ad14-abb6-902a3d8745be
document_version_independent_id: 8cb55c69-27a0-ad42-4f98-ab92db487e53
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/concept-hybrid-join.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/concept-hybrid-join
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/concept-hybrid-join.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 51bff77b-7962-77a7-737e-319f93d4d7b9
---

# What is a Microsoft Entra hybrid joined device? - Microsoft Entra ID | Microsoft Learn

Organizations with existing Active Directory implementations can benefit from some of the functionality provided by Microsoft Entra ID by implementing Microsoft Entra hybrid joined devices. These devices are joined to your on-premises Active Directory and registered with Microsoft Entra ID.

Microsoft Entra hybrid joined devices require network line of sight to your on-premises domain controllers periodically. Without this connection, devices become unusable. If this requirement is a concern, consider [Microsoft Entra joining](concept-directory-join) your devices.

| Microsoft Entra hybrid join | Description |
| --- | --- |
| **Definition** | Joined to on-premises Microsoft Windows Server Active Directory and Microsoft Entra ID requiring organizational account to sign in to the device |
| **Primary audience** | Suitable for hybrid organizations with existing on-premises Microsoft Windows Server Active Directory infrastructure |
|  | Applicable to all users in an organization |
| **Device ownership** | Organization |
| **Operating Systems** | Windows 11 or Windows 10 except Home editions |
|  | Windows Server 2016, 2019, and 2022 |
| **Provisioning** | Windows 11, Windows 10, Windows Server 2016/2019/2022 |
|  | Domain join by IT and autojoin via Microsoft Entra Connect or AD FS config |
|  | Domain join by Windows Autopilot and autojoin via Microsoft Entra Connect or AD FS config |
| **Device sign in options** | Organizational accounts using: |
|  | Password |
|  | [Passwordless](../authentication/concept-authentication-passkeys-fido2) options like [Windows Hello for Business](/en-us/windows/security/identity-protection/hello-for-business/hello-planning-guide) and FIDO2.0 security keys. |
| **Device management** | [Group Policy](/en-us/mem/configmgr/comanage/faq#my-environment-has-too-many-group-policy-objects-and-legacy-authenticated-apps--do-i-have-to-use-hybrid-azure-ad-) |
|  | [Configuration Manager standalone or co-management with Microsoft Intune](/en-us/mem/configmgr/comanage/overview) |
| **Key capabilities** | single sign-on (SSO) to both cloud and on-premises resources |
|  | Conditional Access through Domain join or through Intune if co-managed |
|  | [Self-service Password Reset and Windows Hello PIN reset on lock screen](../authentication/howto-sspr-windows) |

When enabled, Microsoft Entra Cloud Sync can synchronize Active Directory computer objects to Microsoft Entra ID for Microsoft Entra hybrid join. It doesn't configure AD FS or other federation settings. For configuration steps, see [Configure device sync with Microsoft Entra Cloud Sync](../hybrid/cloud-sync/device-sync).

![Diagram showing Active Directory Domain Services sending device information to Microsoft Entra ID for hybrid join.](media/concept-hybrid-join/azure-ad-hybrid-joined-device.png)

## Scenarios

Use Microsoft Entra hybrid joined devices if:

- You want to continue to use [Group Policy](/en-us/mem/configmgr/comanage/faq#my-environment-has-too-many-group-policy-objects-and-legacy-authenticated-apps--do-i-have-to-use-hybrid-azure-ad-) to manage device configuration.
- You want to continue to use existing imaging solutions to deploy and configure devices.
- You have Win32 apps deployed to these devices that rely on Active Directory machine authentication.
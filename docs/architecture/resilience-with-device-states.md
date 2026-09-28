---
layout: Conceptual
title: Build resilience by using device states in Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/resilience-with-device-states
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: A guide for architects and IT administrators to building resilience by using device states
ms.topic: concept-article
ms.date: 2022-11-16T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 1d78992e-bafa-1cfb-d3c2-b16c5428cae9
document_version_independent_id: dc40edcb-d61c-5150-83d3-88862aaab174
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/resilience-with-device-states.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/resilience-with-device-states
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/resilience-with-device-states.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: e07fce79-5a22-48c4-3e24-e047b3214663
---

# Build resilience by using device states in Microsoft Entra ID - Microsoft Entra | Microsoft Learn

By enabling [device states](../identity/devices/overview) with Microsoft Entra ID, administrators can author [Conditional Access policies](../identity/conditional-access/overview) that control access to applications based on device state. Enabling device states satisfies strong authentication requirements for resource access, reduces multifactor authentication requests, and improves resiliency.

The following flow chart presents ways to onboard devices in Microsoft Entra ID that enable device states. You can use more than one in your organization.

![flow chart for choosing device states](media/resilience-with-device-states/admin-resilience-devices.png)

When you use [device states](../identity/devices/overview), in most cases users will experience single sign-on to resources through a [Primary Refresh Token (PRT)](../identity/devices/concept-primary-refresh-token). The PRT contains claims about the user and the device. You can use these claims to get authentication tokens to access applications from the device. The PRT is valid for 14 days and is continuously renewed as long as the user actively uses the device, providing users a resilient experience. For more information about how a PRT can get multifactor authentication claims, see [When does a PRT get an MFA claim](../identity/devices/concept-primary-refresh-token).

## How do device states help?

When a PRT requests access to an application, its device, session, and MFA claims are trusted by Microsoft Entra ID. When administrators create policies that require either a device-based control or a multifactor authentication control, then the policy requirement can be met through its device state without attempting MFA. Users won't see more MFA prompts on the same device. This increases resilience to a disruption of the Microsoft Entra multifactor authentication service or dependencies such as local telecom providers.

## How do I implement device states?

- Enable [Microsoft Entra hybrid joined](../identity/devices/hybrid-join-plan) and [Microsoft Entra join](../identity/devices/device-join-plan) for company-owned Windows devices and require that they be joined, if possible. If not possible, require that they be registered. If there are older versions of Windows in your organization, upgrade those devices to use Windows 10.
- Standardize user browser access to use either [Microsoft Edge](/en-us/deployedge/microsoft-edge-security-identity) or Google Chrome with the [Microsoft Single Sign On extension](https://chrome.google.com/webstore/detail/windows-10-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji) that enable seamless SSO to web applications using the PRT.
- For personal or company-owned iOS and Android devices, deploy the [Microsoft Authenticator App](https://support.microsoft.com/account-billing/how-to-use-the-microsoft-authenticator-app-9783c865-0308-42fb-a519-8cf666fe0acc). In addition to MFA and password-less sign-in capabilities, the Microsoft Authenticator app enables single sign-on across native applications through [brokered authentication](../identity-platform/msal-android-single-sign-on) with fewer authentication prompts for end users.
- For personal or company-owned iOS and Android devices, use [mobile application management](/en-us/mem/intune/apps/app-management) to securely access company resources with fewer authentication requests.
- For macOS devices, use the [Microsoft Enterprise SSO plug-in for Apple devices (preview)](../identity-platform/apple-sso-plugin) to register the device and provide SSO across browser and native Microsoft Entra applications. Then, based on your environment, follow the steps specific to Microsoft Intune or Jamf Pro.
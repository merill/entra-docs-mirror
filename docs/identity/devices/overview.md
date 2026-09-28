---
layout: Conceptual
title: What is device identity in Microsoft Entra ID? - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Device identities and their use cases
ms.topic: overview
ms.date: 2025-06-27T00:00:00.0000000Z
ms.reviewer: sandeo, jogro, jploegert
locale: en-us
document_id: 8877b198-deb1-6ae9-ea0d-3830370b0b4a
document_version_independent_id: f1a4495c-7da8-0c3f-5d97-4f816a2b696c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: bef300f6-85a6-b836-4ce6-1ec13fdd4e2d
---

# What is device identity in Microsoft Entra ID? - Microsoft Entra ID | Microsoft Learn

A [device identity](/en-us/graph/api/resources/device) is an object in Microsoft Entra ID. This device object is similar to users, groups, or applications. A device identity gives administrators information they can use when making access or configuration decisions.

![Devices displayed in Microsoft Entra Devices blade](media/overview/azure-entra-devices-all-devices.png)

There are three ways to get a device identity:

- Microsoft Entra registration
- Microsoft Entra join
- Microsoft Entra hybrid join

Device identities are a prerequisite for scenarios like [device-based Conditional Access policies](../conditional-access/concept-conditional-access-grant) and [Mobile Device Management with the Microsoft Intune family of products](/en-us/mem/endpoint-manager-overview).

## Modern device scenario

The modern device scenario focuses on two of these methods:

- [Microsoft Entra registration](concept-device-registration)
    - Bring your own device (BYOD)
    - Mobile device (cell phone and tablet)
- [Microsoft Entra join](concept-directory-join)
    - Windows 11 and Windows 10 devices owned by your organization
    - [Windows Server 2019 and newer servers in your organization running as VMs in Azure](howto-vm-sign-in-azure-ad-windows)

[Microsoft Entra hybrid join](concept-hybrid-join) is seen as an interim step on the road to Microsoft Entra join. All three scenarios can coexist in a single organization.

## Resource access

Registering and joining devices to Microsoft Entra ID gives users Seamless Sign-on (SSO) to cloud-based resources.

Devices that are Microsoft Entra joined benefit from [SSO to your organization's on-premises resources](device-sso-to-on-premises-resources).

## Provisioning

Getting devices in to Microsoft Entra ID can be done in a self-service manner or a controlled process managed by administrators.
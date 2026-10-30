---
layout: Conceptual
title: 'Tutorial: Get started with Microsoft traffic labs - Global Secure Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/tutorial-microsoft-traffic-introduction
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn about Microsoft traffic labs for Global Secure Access, including source IP restoration, compliant network checks, and universal tenant restrictions.
ms.topic: tutorial
ms.date: 2026-06-22T00:00:00.0000000Z
ms.subservice: entra-internet-access
ms.reviewer: jebley
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 1bb53c82-e2b7-2249-3eb8-ca6e18db302e
document_version_independent_id: 1bb53c82-e2b7-2249-3eb8-ca6e18db302e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/tutorial-microsoft-traffic-introduction.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/tutorial-microsoft-traffic-introduction
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/tutorial-microsoft-traffic-introduction.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
platformId: 72723216-22e3-934e-07c2-c5fa4da58604
---

# Tutorial: Get started with Microsoft traffic labs - Global Secure Access | Microsoft Learn

This learning lab series provides hands-on experience with the Microsoft traffic profile in Global Secure Access. The Microsoft traffic profile is part of Microsoft Entra Internet Access for Microsoft services. It routes supported Microsoft service traffic through Global Secure Access so you can apply identity-aware controls to Microsoft traffic.

In this tutorial, you learn how to:

- Recognize what the Microsoft traffic profile is and how it works.
- Review the key use cases the Microsoft traffic profile supports.
- Navigate the learning progression for the lab series.

## What is the Microsoft traffic profile?

The Microsoft traffic profile routes supported Microsoft service traffic through Microsoft's security service edge (SSE). The profile uses preconfigured fully qualified domain names (FQDNs) and IP ranges that are required for supported Microsoft services.

The Microsoft traffic profile is optimized for Microsoft traffic. Traffic available for acquisition in the Microsoft traffic profile can only be acquired in the Microsoft traffic profile. Even if the Internet Access profile is the one profile enabled, Microsoft traffic isn't acquired by the Internet Access profile.

For more information, see [Microsoft traffic profile overview](concept-microsoft-traffic-profile).

## Key use cases

Use the Microsoft traffic profile when you want to improve access controls and observability for supported Microsoft service traffic.

| Use case | Recommended configuration |
| --- | --- |
| Preserve the original user source IP in Microsoft Entra sign-in logs. | Configure [source IP restoration](tutorial-microsoft-traffic-source-ip-restoration). |
| Require users to connect through your tenant's Global Secure Access service before accessing apps integrated with Microsoft Entra ID. | Configure the [compliant network check](tutorial-microsoft-traffic-compliant-network). |
| Restrict sign-ins to authorized external tenants from managed devices and networks. | Configure [universal tenant restrictions](tutorial-microsoft-traffic-tenant-restrictions). |

## How to run the lab exercises

This series covers the fundamentals of the Microsoft traffic profile. Follow the exercises in order. Some exercises depend on earlier configuration. For example, the compliant network check depends on Global Secure Access signaling for Conditional Access.

## Prerequisites

To complete this tutorial series, you need:

- A Microsoft Entra ID tenant with Microsoft Entra ID P1 or Microsoft Entra ID P2 licenses. Microsoft Entra Internet Access for Microsoft services capabilities are included in Microsoft Entra ID P1 and Microsoft Entra ID P2.
- Either the Global Administrator role or both of the following roles:
    - Global Secure Access Administrator.
    - Security Administrator.
- The Application Administrator role for exercises that assign users or groups to a traffic forwarding profile.
- The Conditional Access Administrator role for exercises that create or manage Conditional Access policies.
- A Windows 11 device that's Microsoft Entra joined or hybrid joined and has internet access.

## Learning progression

Each lab builds on the previous one and follows a logical progression.

| Exercise | What you learn |
| --- | --- |
| [Enable the Microsoft traffic profile](tutorial-microsoft-traffic-enable-profile) | How the Microsoft traffic profile works and how to route Microsoft 365 and Microsoft Entra ID traffic through Global Secure Access. |
| [Enable source IP restoration](tutorial-microsoft-traffic-source-ip-restoration) | How to preserve the original client IP in Microsoft Entra sign-in logs for accurate policy evaluation and investigation. |
| [Enable the compliant network check](tutorial-microsoft-traffic-compliant-network) | How to require traffic to flow through Global Secure Access before granting access to apps integrated with Microsoft Entra ID. |
| [Configure universal tenant restrictions](tutorial-microsoft-traffic-tenant-restrictions) | How to block sign-ins to unauthorized external tenants from managed devices. |
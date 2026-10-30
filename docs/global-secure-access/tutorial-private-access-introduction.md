---
layout: Conceptual
title: 'Tutorial: Get started with Microsoft Entra Private Access labs - Global Secure Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/tutorial-private-access-introduction
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn about Microsoft Entra Private Access labs covering connector setup, traffic forwarding, Quick Access, per-app segmentation, and more.
ms.topic: tutorial
ms.date: 2026-03-11T00:00:00.0000000Z
ms.subservice: entra-private-access
ms.reviewer: jebley
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 6748bc95-df0e-e31d-7d0e-3a5b0e7694b2
document_version_independent_id: 6748bc95-df0e-e31d-7d0e-3a5b0e7694b2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/tutorial-private-access-introduction.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/tutorial-private-access-introduction
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/tutorial-private-access-introduction.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: eb021acc-d836-4e88-a1b2-f9471490378a
---

# Tutorial: Get started with Microsoft Entra Private Access labs - Global Secure Access | Microsoft Learn

This tutorial series offers practical, hands-on experience with Microsoft Entra Private Access, an identity-centric Zero Trust Network Access (ZTNA) solution. Microsoft Entra Private Access delivers granular access to on-premises resources without exposing the broader network, while strengthening access security through modern Microsoft Entra ID controls such as Conditional Access, Continuous Access Evaluation (CAE), Privileged Identity Management (PIM), and more.

In this tutorial, you learn how to:

- Understand what Microsoft Entra Private Access is and how it works
- Review Security Service Edge (SSE) concepts and capabilities
- Navigate the learning progression for the lab series

## How to run the lab exercises

This series is designed to build foundational and advanced skills in Microsoft Entra Private Access. **The exercises assume you've gone in order.** Skipping steps might leave required prerequisites unconfigured. For example, the per-app access segmentation tutorial guides you through creating a specific Enterprise Application for an on-premises resource; however, if the enable Private Access tutorial is skipped, the required traffic forwarding profile might not be enabled, and traffic won't reach the Connector. To ensure successful outcomes, complete the tutorials in the prescribed order.

## Prerequisites

To complete this tutorial series, you need the following:

- Microsoft Entra ID tenant with P1 and either Microsoft Entra Private Access or Microsoft Entra Suite licenses.
- Either Global Admin role or all three of the following roles: Global Secure Access Admin, Security Admin, Application Admin.
- A Windows 11 device (must be Entra joined, hybrid joined, or Entra registered) with internet access.
- A Windows Server 2016 or later to host the Private Network Connector.
- An on-premises resource such as a server for RDP, an internal website, a file share, or similar. The tutorial steps assume it's an SMB file share.

## Learning progression

Each lab builds upon the previous one, following a logical progression:

| Exercise | What you learn |
| --- | --- |
| [Connector setup](tutorial-private-access-connector-setup) | How to set up the Private Network Connector used to broker access to private resources. |
| [Enable Private Access](tutorial-private-access-enable-traffic-forwarding) | How to enable the Private Access traffic forwarding profile and assign users or groups. |
| [VPN replacement with Quick Access](tutorial-private-access-vpn-replacement) | How to publish broad private network access using Quick Access, including subnets, private DNS, and assignments. |
| [Per-app access segmentation](tutorial-private-access-app-segmentation) | How to transition from broad access to least-privilege per-app enterprise applications using discovery insights, and enforce Conditional Access policies on on-premises apps. |
| [Intelligent Local Access](tutorial-private-access-intelligent-local-access) | How to configure Intelligent Local Access (ILA) to optimize in-office/private network routing and validate traffic behavior. |
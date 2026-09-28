---
layout: Conceptual
title: Learn about Microsoft Entra Private Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/concept-private-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn about how Microsoft Entra Private Access secures access to your private corporate resources through the creation of Quick Access and Global Secure Access apps.
ms.topic: concept-article
ms.date: 2026-03-12T00:00:00.0000000Z
ms.subservice: entra-private-access
ms.reviewer: katabish
ai-usage: ai-assisted
locale: en-us
document_id: 60a795e9-b433-a0f1-cadb-3b19dc572ead
document_version_independent_id: bd9801cf-e1c7-af03-6380-576caf2bd8eb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/concept-private-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/concept-private-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/concept-private-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 8eccf58a-67b1-a878-40da-14cd8eddcc72
---

# Learn about Microsoft Entra Private Access - Global Secure Access | Microsoft Learn

## Overview

Microsoft Entra Private Access unlocks the ability to specify the fully qualified domain names (FQDNs) and IP addresses that you consider private or internal, so you can manage how your organization accesses them. With Private Access, you can modernize how your organization's users access private apps and resources. Remote workers don't need to use a VPN to access these resources if they have the Global Secure Access Client installed. The client quietly and seamlessly connects them to the resources they need.

Private Access provides two ways to configure the private resources that you want to tunnel through the service. You can configure Quick Access, which is the primary group of FQDNs and IP addresses that you want to secure. You can also configure a Global Secure Access app for per-app access, which allows you to specify a subset of private resources that you want to secure. The Global Secure Access app provides a granular approach to securing your private resources.

The features of Microsoft Entra Private Access provide a quick and easy way to replace your VPN to allow secure access to your internal resources with an easy, one-time configuration, using the secure capabilities of Conditional Access.

## Quick Access and Global Secure Access apps

When you configure the Quick Access and Global Secure Access apps, you create a new enterprise application. The app serves as a container for the private resources that you want to secure. The application has its own [Microsoft Entra private network connector](how-to-configure-connectors) to broker the connection between the service and the internal resource. You can assign users and groups to the app, and then use Conditional Access policies to control access to the app.

Quick Access and Per-app Access are similar, but there are a few key concepts to understand so you can decide how to configure each one.

### Quick Access app

Quick Access is the primary group of FQDNs and IP addresses that you want to secure. As you're planning your Global Secure Access deployment, review your list of private resources and determine which resources you *always* want to tunnel through the service. This primary group of FQDNs, IP addresses, and IP ranges is what you add to Quick Access.

![Diagram of the Quick Access app process with traffic flowing through the service to the app, and granting access through the private network connector.](media/concept-private-access/quick-access-diagram.png)

### Global Secure Access app

A Global Secure Access app could be configured if any of the following scenarios sound familiar:

- I need to apply a different set of Conditional Access policies to a subset of users.
- I have a few private resources that I want to secure, but they should have a different set of access policies.
- I have a subset of private resources that I only want to secure for a specific time frame.

![Diagram of the Global Secure Access app process with traffic flowing through the service to the app, and granting access through the private network connector.](media/concept-private-access/private-access-diagram.png)

The Global Secure Access app takes a more detailed approach to securing your private resources. You can create multiple per-app access apps to secure different private resources. Paired with Conditional Access policies, you have a powerful yet fine-grained way to secure your private resources.
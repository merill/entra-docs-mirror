---
layout: Conceptual
title: Learn about the Microsoft Traffic Profile - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/concept-microsoft-traffic-profile
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: alexpav
ms.service: global-secure-access
manager: dougeby
description: Learn about the capabilities and traffic handling in the Microsoft traffic profile
ms.topic: concept-article
ms.date: 2024-10-11T00:00:00.0000000Z
locale: en-us
document_id: da0e950b-5e2b-9bc3-5eee-7894d4f34ae6
document_version_independent_id: da0e950b-5e2b-9bc3-5eee-7894d4f34ae6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/concept-microsoft-traffic-profile.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/concept-microsoft-traffic-profile
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/concept-microsoft-traffic-profile.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: a54e44d8-5e11-e116-ce8e-020b202f8600
---

# Learn about the Microsoft Traffic Profile - Global Secure Access | Microsoft Learn

Microsoft traffic profile ensures the best performance characteristics for supported services and simplifies the configuration of rules governing traffic acquisition. Preconfigured fully qualified domain names (FQDNs) and IP ranges that are necessary for Microsoft services to function enable you define traffic acquisition behavior based on the Microsoft services that your organization is using.

## Traffic forwarding in the Microsoft traffic profile

A traffic forwarding rules includes the Destination Type (IP or FQDN), Destination (specific FQDNs or IP ranges), Protocol (TCP or UDP), Ports, Traffic Category, and Action. Microsoft traffic profile derives the traffic forwarding rules from the [Microsoft 365 IP and FQDN list](/en-us/microsoft-365/enterprise/urls-and-ip-address-ranges) and combines related services based on the traffic category. The traffic category details are described in the [Microsoft 365 Network Connectivity Principles](/en-us/microsoft-365/enterprise/microsoft-365-network-connectivity-principles#optimizing-connectivity-to-microsoft-365-services)

You can configure traffic acquisition behavior for each rule according to specific needs of your organization. Configuring the action to Forward will instruct the Global Secure Access client and Remote Networks to acquire traffic. Configuring the rule action to Bypass will instruct the Global Secure Access Client and Remote Networks to skip traffic acquisition for FQDNs and IP ranges in that rule.

Important

When a rule is set to Bypass, the Internet Access traffic profile will not acquire this traffic. Even with the Internet Access profile enabled, the bypassed traffic will skip Global Secure Access acquisition and use that client's network routing path to egress to the Internet. Traffic available for acquisition in the Microsoft traffic profile can be only acquired in the Microsoft traffic profile.

Traffic rules are grouped based on the application type. You can enable or disable traffic acquisition for an entire group. When the group is enabled, you can control the behavior of individual rules separately. When the group is disabled, all traffic covered by the rules in that group is bypassed.

## Default traffic acquisition behavior

When you enable the Microsoft traffic profile, the rule list available to you is populated based on the supported traffic rules at the time of the traffic profile enablement. When we introduce a new rule, it will become visible in your configuration in the Forward mode in the Microsoft traffic profile, and in Bypass mode in the Internet Access profile.
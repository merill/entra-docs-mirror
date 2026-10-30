---
layout: Conceptual
title: Learn about Microsoft Entra Internet Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/concept-internet-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn about how Microsoft Entra Internet Access secures access to the Internet.
ms.topic: concept-article
ms.date: 2026-03-12T00:00:00.0000000Z
ms.subservice: entra-internet-access
ai-usage: ai-assisted
locale: en-us
document_id: 9db86f0a-8133-8bbf-5c06-df93d11b5495
document_version_independent_id: 9db86f0a-8133-8bbf-5c06-df93d11b5495
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/concept-internet-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/concept-internet-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/concept-internet-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 2870833d-6177-f143-8917-eaf8474e6478
---

# Learn about Microsoft Entra Internet Access - Global Secure Access | Microsoft Learn

## Overview

Microsoft Entra Internet Access provides an identity-centric Secure Web Gateway (SWG) solution for Software as a Service (SaaS) applications and other Internet traffic. It protects users, devices, and data from the Internet's wide threat landscape with best-in-class security controls and visibility through Traffic Logs.

## Web content filtering

The key introductory feature for Microsoft Entra Internet Access for all apps is **Web content filtering**. This feature provides granular access control for web categories and Fully Qualified Domain Names (FQDNs). By explicitly blocking known inappropriate, malicious, or unsafe sites, you protect your users and their devices from any Internet connection whether they're remote or within the corporate network.

When traffic reaches Microsoft's Secure Service Edge, Microsoft Entra Internet Access performs security controls in two ways. For unencrypted HTTP traffic, it uses the Uniform Resource Locator (URL). For HTTPS traffic encrypted with Transport Layer Security (TLS), it uses the Server Name Indication (SNI).

Web content filtering is implemented using filtering policies, which are grouped into security profiles, which can be linked to Conditional Access policies. For more information about Conditional Access, see [Microsoft Entra Conditional Access](/en-us/azure/active-directory/conditional-access/).

Note

While web content filtering is a core capability for any Secure Web Gateway, similar capabilities exist in other security products, such as endpoint security products like [Microsoft Defender for Endpoint](/en-us/defender-endpoint/web-content-filtering/) and firewalls like [Azure Firewall](/en-us/azure/firewall/web-categories/). Microsoft Entra Internet Access provides additional security value via identity-aware policy integration with Microsoft Entra ID, policy enforcement on the cloud edge, universal support for all device platforms, and security enhancements through Transport Layer Security (TLS) Inspection, such as higher fidelity web categorization. Internet access also simplifies traditional policy management since policies are all based on the user identity. Learn more in the [FAQ](resource-faq).

## Security profiles

Security profiles are objects you use to group filtering policies and deliver them through user aware Conditional Access policies. For instance, to block all **News** websites except for `msn.com` for user `angie@contoso.com` you create two web filtering policies and add them to a security profile. You then take the security profile and link it to a Conditional Access policy assigned to `angie@contoso.com`.

```
"Security Profile for Angie"       <---- the security profile
    Allow msn.com at priority 100  <---- higher priority filtering policies
    Block News at priority 200     <---- lower priority filtering policy
```

## Policy processing logic

Within a security profile, policies are enforced according to logical ordering of unique priority numbers, with 100 being the highest priority and 65,000 being the lowest priority (similar to traditional firewall logic). As a best practice, add spacing of about 100 between priorities to allow for policy flexibility in the future.

Once you link a security profile to a Conditional Access policy, if multiple Conditional Access policies match, both security profiles are processed in priority ordering of the matching security profiles.

Important

The baseline security profile applies to all traffic even without linking it to a Conditional Access policy. It enforces policy at the lowest priority in the policy stack, applying to all Internet Access traffic routed through the service as a 'catch-all' policy. The baseline security profile executes even if a Conditional Access policy matches another security profile.

## Known limitations

For detailed information about known issues and limitations, see [Known limitations for Global Secure Access](reference-current-known-limitations).
---
layout: Conceptual
title: 'Tutorial: Get Started with Microsoft Entra Internet Access Labs - Global Secure Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/tutorial-internet-access-introduction
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn about Microsoft Entra Internet Access labs covering web filtering, TLS inspection, and threat intelligence.
ms.topic: tutorial
ms.date: 2026-03-07T00:00:00.0000000Z
ms.subservice: entra-internet-access
ms.reviewer: jebley
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: c6fba4d1-ba9e-017a-5341-4d8ce7fc7398
document_version_independent_id: c6fba4d1-ba9e-017a-5341-4d8ce7fc7398
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/tutorial-internet-access-introduction.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/tutorial-internet-access-introduction
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/tutorial-internet-access-introduction.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: bba59e71-ef7c-84a4-dd86-386ff2e2af73
---

# Tutorial: Get Started with Microsoft Entra Internet Access Labs - Global Secure Access | Microsoft Learn

This learning lab series provides hands-on experience with Microsoft Entra Internet Access, a cloud-delivered secure web gateway and AI gateway.

In this tutorial, you learn how to:

- Recognize what Internet Access is and understand how it works.
- Review security service edge (SSE) concepts and capabilities.
- Navigate the learning progression for the lab series.

## What is Microsoft Entra Internet Access?

Internet Access is part of the Microsoft SSE solution. It works by routing internet traffic through the Microsoft globally distributed cloud proxies, where security policies are applied before traffic reaches its destination.

As a secure web gateway, it protects users and devices from internet threats while enabling secure, identity-aware access to web resources. As an AI Gateway, it gives admins visibility into shadow AI apps, protects your organization's data behind your company AI tools, and helps prevent data leakage to unauthorized AI sites.

This approach provides:

- **Identity-aware security**: Policies can be targeted based on user identity, group membership, and device state.
- **Cloud-native protection**: No on-premises infrastructure to maintain.
- **Zero Trust alignment**: Every request is evaluated against your security policies.

## How to run the lab exercises

This series of exercises covers the fundamentals of Internet Access. The exercises assume that you follow them in order. If you skip around, you might miss a step. For example, in the baseline web-filtering tutorial, you create a security profile and assign it to a Microsoft Entra Conditional Access policy. Subsequent labs instruct you to assign the new policy to this existing security profile rather than creating a new security profile and Conditional Access policy each time.

## Prerequisites

To complete this tutorial series, you need the following:

- Microsoft Entra ID tenant with P1 and either Microsoft Entra Internet Access or Microsoft Entra Suite licenses.
- Either Global Admin role or both of the following roles: Global Secure Access Admin, Security Admin.
- A Windows 11 device (must be Entra joined or hybrid joined) with internet access.

## Learning progression

Each lab builds on the previous one and follows a logical progression.

| Exercise | What you learn |
| --- | --- |
| [Enable Internet Access](tutorial-internet-access-enable-traffic-forwarding) | How traffic forwarding works and how to route internet traffic through Global Secure Access. |
| [Configure web content filtering](tutorial-internet-access-web-content-filtering) | How to create policies that apply to all users and understand policy evaluation. |
| [Transport Layer Security (TLS) inspection](tutorial-internet-access-tls-inspection) | Why encrypted traffic inspection is essential for modern security. |
| [URL filtering](tutorial-internet-access-url-filtering) | What the difference is between FQDN and URL filtering, and how TLS inspection enables deeper inspection. |
| [Threat intelligence](tutorial-internet-access-threat-intelligence) | How the Microsoft threat feeds protect against known malicious sites. |
| [Application discovery](tutorial-internet-access-application-discovery) | How to identify shadow IT and manage application risk. |
| [Content policies](tutorial-internet-access-content-policies) | How to prevent data exfiltration through network content filtering and file upload controls. |
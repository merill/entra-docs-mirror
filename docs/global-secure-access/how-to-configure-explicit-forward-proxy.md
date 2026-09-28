---
layout: Conceptual
title: Configure Explicit Forward Proxy - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-explicit-forward-proxy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: alexpav
ms.service: global-secure-access
manager: dougeby
description: Learn how to configure Explicit Forward Proxy.
ms.topic: how-to
ms.date: 2026-04-06T00:00:00.0000000Z
locale: en-us
document_id: 0400d3b7-5315-b274-6555-705aa6b16a5d
document_version_independent_id: 0400d3b7-5315-b274-6555-705aa6b16a5d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-configure-explicit-forward-proxy.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-configure-explicit-forward-proxy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-configure-explicit-forward-proxy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 5110ec36-fa7a-ff86-1367-01b0a02c794f
---

# Configure Explicit Forward Proxy - Global Secure Access | Microsoft Learn

With Explicit Forward Proxy, you can use the secure web and AI gateway capabilities of Microsoft Entra Internet Access without installing the Global Secure Access client. Explicit Forward Proxy works with any browser that supports proxy automatic configuration (PAC).

## Prerequisites

- Ensure that you have the following Microsoft Entra admin roles:
    - The Global Secure Access Administrator role to manage the Global Secure Access features
    - The Conditional Access Administrator role to create and manage Microsoft Entra Conditional Access policies
- Complete the [guide for getting started with Global Secure Access](/en-us/entra/global-secure-access/quickstart-access-admin-center).
- Review the [Explicit Forward Proxy concepts](/en-us/entra/global-secure-access/concept-explicit-forward-proxy) and [Explicit Forward Proxy session management concepts](/en-us/entra/global-secure-access/concept-explicit-forward-proxy-session-management).
- Enable the Internet Access traffic-forwarding profile.
- Configure Transport Layer Security (TLS) inspection.

## Enable Explicit Forward Proxy

You can enable and manage Explicit Forward Proxy by using the Microsoft Entra admin center:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Go to **Global Secure Access** &gt; **Session management**, and then select the **Explicit Forward Proxy** tab.
3. Set the **Internet Access** toggle to **Enabled**. By default, smart session management is enabled when you enable Explicit Forward Proxy.
4. Optionally, enable HTTP header session management. For more information, see [Configure HTTP header session management](how-to-configure-explicit-forward-proxy-headers).

[![Screenshot of the tab in the Microsoft Entra admin center for configuring Explicit Forward Proxy.](media/how-to-configure-explicit-forward-proxy/enable-explicit-forward-proxy.png)](media/how-to-configure-explicit-forward-proxy/enable-explicit-forward-proxy.png#lightbox)

Important

Explicit Forward Proxy session management relies on IP affinity as one of the session management anchors. We recommend that you configure a Conditional Access policy that restricts the use of Explicit Forward Proxy to networks you trust. For more information, see [Explicit Forward Proxy session management](/en-us/entra/global-secure-access/concept-explicit-forward-proxy-session-management) and [Configure a Conditional Access policy for Explicit Forward Proxy](/en-us/entra/global-secure-access/how-to-configure-conditional-access-policy-for-explicit-forward-proxy).
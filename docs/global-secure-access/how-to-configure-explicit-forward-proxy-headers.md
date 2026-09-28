---
layout: Conceptual
title: Configure Explicit Forward Proxy HTTP Header Session Management - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-explicit-forward-proxy-headers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: alexpav
ms.service: global-secure-access
manager: dougeby
description: Learn how to configure HTTP header session management for Explicit Forward Proxy.
ms.topic: concept-article
ms.date: 2026-04-06T00:00:00.0000000Z
locale: en-us
document_id: b0fa0a08-f02a-3003-c641-4818f09ea9a0
document_version_independent_id: b0fa0a08-f02a-3003-c641-4818f09ea9a0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-configure-explicit-forward-proxy-headers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-configure-explicit-forward-proxy-headers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-configure-explicit-forward-proxy-headers.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: d1d62ea7-2fe5-5b9f-df2e-b3863019954c
---

# Configure Explicit Forward Proxy HTTP Header Session Management - Global Secure Access | Microsoft Learn

You can configure Explicit Forward Proxy (preview) to rely on the private IP addresses of devices on your network to associate authenticated users with their devices. To use HTTP header session management with Explicit Forward Proxy, you need to securely communicate the private IP address of the device to the Explicit Forward Proxy feature.

Important

The HTTP header session management feature is currently in preview. This information relates to a prerelease product that might be substantially modified before release. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Prerequisites

- The account that you use to configure HTTP header session management has an active Global Secure Access Administrator role assignment.
- Your organization has an existing proxy service that can perform Transport Layer Security (TLS) inspection and header injection before sending traffic to Explicit Forward Proxy.
- Client devices that use Explicit Forward Proxy with HTTP header session management trust the TLS certificate's root certificate authority.

## Configuration steps

1. Go to the Microsoft Entra admin center. Under **Global Secure Access** &gt; **Session management** &gt; **Explicit Forward Proxy**, select the **HTTP Header Session Management** checkbox.
2. Configure your outbound proxy service to intercept traffic to `*.internet.efp.globalsecureaccess.microsoft.com`.
3. Configure your outbound proxy service to inject the `x-ms-gsa-efp-forwarded-for` header with the value of the private IP address detected on the incoming connection.
4. Configure the Microsoft Entra Conditional Access policy to allow authentication to Explicit Forward Proxy only from the known networks that your organization trusts.

Important

Don't skip the step for configuring the Conditional Access policy. HTTP headers can be easily manipulated, so it's essential that `x-ms-gsa-efp-forwarded-for` is sent only from networks that you trust.
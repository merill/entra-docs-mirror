---
layout: Conceptual
title: How to Customize Global Secure Access Block Page - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-customize-block-page
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Use custom block pages to display organization-specific messaging internet access policies block users from accessing websites.
ms.topic: how-to
ms.date: 2025-09-24T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: bb5643b4-134f-32a1-30fe-4865db073e76
document_version_independent_id: bb5643b4-134f-32a1-30fe-4865db073e76
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-customize-block-page.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-customize-block-page
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-customize-block-page.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
platformId: 9bb24781-76f9-877d-6de8-8e848512610d
---

# How to Customize Global Secure Access Block Page - Global Secure Access | Microsoft Learn

## Overview

The custom block page empowers you to customize the default body of the page from, "It's been restricted by your organization." you configure and preview tailored messaging to coincide with your organization's style guide when internet access policies block a user's request to access an internet resource. Use custom block pages to display organization-specific messaging internet access policies block users from accessing websites.

## Prerequisites

- Configure [Transport Layer Security (TLS) inspection](how-to-transport-layer-security).
- Configure [web content filtering](how-to-configure-web-content-filtering) and/or [threat intelligence filtering](how-to-configure-threat-intelligence).
- Ensure you have the [Global Secure Access Administrator role](/en-us/azure/active-directory/roles/permissions-reference) or equivalent role in Microsoft Entra ID assigned.

## Configure a custom block page

1. Navigate to **Global Secure Access** &gt; **Settings** &gt; **Session management** &gt; **Custom Block Page**
2. Switch **Custom body message** to **On**.
3. Configure the Customized body message you would prefer. For example, `Your admin at Contoso has blocked your access.`
4. (Optional) Paste one or multiple clickable links via limited markdown language (for example, `[click here](https://bing.com)`).
5. Preview the customized message with the **Preview** button.
6. Select **Save** to save the custom block page.

![Screenshot showing the preview experience in the admin portal](media/how-to-customize-block-page/custom-block-preview.png)

Note

A known transient issue could result in the configuration failing. The current mitigation is to reconfigure the custom block page and try again.

## Verify the block page

1. From a device with the Global Secure Access client installed and the Internet Access traffic forwarding profile enabled, attempt to navigate to a site that your policy blocks.
2. Observe the block experience and confirm the custom messaging displays.

![Screenshot showing end user experience of the custom block page](media/how-to-customize-block-page/custom-block.png)

## Notes and limitations

- The Custom body message is limited to 1024 Unicode (utf-8) characters.
- Changes to a custom block page might take a few minutes to propagate to active sessions.
- Custom block pages appear for TLS inspected traffic only.
- A known transient issue could result in the configuration failing. The current mitigation is to reconfigure the custom block page and try again.
- Ensure any contact information you publish complies with your organization's privacy policies.
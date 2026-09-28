---
layout: Conceptual
title: Check web content filtering categories (preview) - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-check-web-content-filtering-categories
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Use the web category checker to find which web content category a URL belongs to via Microsoft Graph.
ms.topic: how-to
ms.date: 2025-08-28T00:00:00.0000000Z
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: bba9f041-3151-4fff-1ea5-74d7c23dd7fc
document_version_independent_id: bba9f041-3151-4fff-1ea5-74d7c23dd7fc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-check-web-content-filtering-categories.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-check-web-content-filtering-categories
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-check-web-content-filtering-categories.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 8058e803-1005-b038-4e0b-48338d446c28
---

# Check web content filtering categories (preview) - Global Secure Access | Microsoft Learn

## Overview

The article shows how to use the web category checker tool to determine which content category a given Uniform Resource Locator (URL) belongs to. The tool is currently available only via Microsoft Graph API.

## How to use the Web category checker

1. Sign in to Graph Explorer at https://aka.ms/ge as a Global Secure Access Administrator.
2. Set the HTTP method to **GET** and the API version to **beta**.
3. Use the following request format, replacing example.com with the host/path you want to check (for example, `msn.com/en-us/sports`):

```http
GET https://graph.microsoft.com/beta/networkaccess/connectivity/microsoft.graph.networkaccess.getWebCategoriesByUrl(url='@url')?@url=example.com
```

Example:

```http
GET https://graph.microsoft.com/beta/networkaccess/connectivity/microsoft.graph.networkaccess.getWebCategoriesByUrl(url='@url')?@url=msn.com/en-us/sports
```

Note

- If the URL contains characters that need encoding (for example, spaces or query strings), URL-encode the `@url` value.
- The feature is API-only at the moment; there's no UI in the Microsoft Entra admin center for this feature.

## Responses

- 200 OK — The API returns JSON containing category information for the supplied URL. Example (illustrative):

```json
{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#microsoft.graph.networkaccess.webCategory",
    "name": "Sports",
    "displayName": "Sports",
    "group": "GeneralSurfing"
}
```
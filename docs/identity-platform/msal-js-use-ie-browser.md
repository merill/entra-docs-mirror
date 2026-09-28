---
layout: Conceptual
title: Issues on Internet Explorer (MSAL.js) - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/msal-js-use-ie-browser
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Use the Microsoft Authentication Library for JavaScript (MSAL.js) with Internet Explorer browser.
manager: pmwongera
ms.custom: 
ms.date: 2021-12-01T00:00:00.0000000Z
ms.reviewer: 
ms.topic: concept-article
locale: en-us
document_id: f5596300-5a08-0552-2e93-2b367e297afb
document_version_independent_id: 2cb71252-3f09-409e-bba2-768d75dfbbdd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/msal-js-use-ie-browser.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/msal-js-use-ie-browser
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/msal-js-use-ie-browser.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fe39cd45-39de-4047-953d-db268d7c71d9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ca56ff04-5597-4109-9f5d-17812bae2fac
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: d051c5d3-282b-7fea-4c13-18cb8a81cf7c
---

# Issues on Internet Explorer (MSAL.js) - Microsoft identity platform | Microsoft Learn

For better compatibility with Internet Explorer, we generate the Microsoft Authentication Library for JavaScript (MSAL.js) for [JavaScript ES5](https://262.ecma-international.org/5.1/), but there are other things to consider as you develop your application.

## Run an app in Internet Explorer

Internet Explorer lacks native support for JavaScript Promises, required by MSAL.js.

To support JavaScript Promises in an Internet Explorer app, reference a Promise polyfill before you reference MSAL.js.

```html
<script
  src="https://cdnjs.cloudflare.com/ajax/libs/bluebird/3.3.4/bluebird.min.js"
  class="pre"
></script>
```

## Debugging an application running in Internet Explorer

### Running in production

Deploying your application to production (for instance in Azure Web apps) normally works fine, provided the end user has accepted popups. We tested it with Internet Explorer 11.

### Running locally

To debug your application locally, temporarily disable Internet Explorer's *Protected Mode* during your debugging session.

1. In Internet Explorer, select **Tools** &gt; **Internet Options** &gt; **Security** tab &gt; **Internet** zone.
2. Clear the **Enable Protected Mode (requires restarting Internet Explorer)** checkbox.
3. Select **OK** to restart Internet Explorer.

When you're done debugging, follow the previous steps and select (instead of clear) the **Enable Protected Mode (requires restarting Internet Explorer)** checkbox.
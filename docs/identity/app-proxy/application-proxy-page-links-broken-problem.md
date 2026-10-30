---
layout: Conceptual
title: Broken links in an application - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-page-links-broken-problem
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Troubleshoot problems with broken links in application proxy apps that are integrated with Microsoft Entra ID.
ms.topic: troubleshooting
ms.date: 2026-03-11T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
locale: en-us
document_id: a2c8c26b-72f0-e053-ec89-9ec72735fda4
document_version_independent_id: a8075126-ebe1-8ad6-8b3b-e56142f8e560
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-page-links-broken-problem.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-page-links-broken-problem
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-page-links-broken-problem.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 8fe4d722-3eee-9baf-d519-a1ebba4ecfc2
---

# Broken links in an application - Microsoft Entra ID | Microsoft Learn

## Overview

This article describes why broken links might occur in your Microsoft Entra application proxy application and resolution options.

After you publish an application proxy app, by default, the only links that work in the app are links to destinations that are located in the published root URL.

If a link in the app doesn't work, the likely cause is that the link goes to a destination that is outside the published root URL.

*What causes broken links in my app?* When an app user selects a link in an application, application proxy tries to resolve the URL as either an internal URL within the same application or as an externally available URL. If the link points to an internal URL that isn't in the same application, the link doesn't fit in either of these buckets. The result is a "not found" error.

## Resolve broken links

You have three options to resolve this issue. The choices are listed in increasing complexity.

1. Make sure that the internal URL is a root that contains all the relevant links for the application. The root lets all links resolve as content published within the same application.

    If you change the internal URL but don’t want to change the landing page for users, change the home page URL to the previously published internal URL. Go to **Microsoft Entra ID** &gt; **App Registrations** and select the **Branding** for the application. In the branding section, set **Home Page URL** to the original published landing page URL.

    Important

    To make this change, a user must have permissions to modify application objects in Microsoft Entra ID. The user must be assigned the [Application Administrator](../role-based-access-control/delegate-app-roles#assign-built-in-application-administrator-roles) role.
2. If your applications use fully qualified domain names (FQDNs), use [custom domains](how-to-configure-custom-domain) to publish your applications. When you use the custom domains feature, you can use the same URL both internally and externally.

    This option ensures that the links in your application are externally accessible through application proxy because the application links to internal URLs are also recognized externally. All links still need to belong to a published application. However, with this option, the links don't need to belong to the same application and can belong to multiple applications.
3. If neither of these options are feasible, there are multiple options to set up inline link translation. These options include using the Intune Managed Browser, the My Apps extension, or the link translation setting on your application.

    For more information about each of these options and how to enable them, see [Redirect hardcoded links for apps published with Microsoft Entra application proxy](application-proxy-configure-hard-coded-link-translation).
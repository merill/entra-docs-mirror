---
layout: Conceptual
title: Debug application proxy issues - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-debug-apps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Learn about debugging issues that occur when configuring Microsoft Entra application proxy.
ms.topic: troubleshooting
ms.date: 2026-03-11T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
locale: en-us
document_id: cacd6ebc-222b-b917-90ca-2f3e81f860f2
document_version_independent_id: 86e20cda-247f-3fe4-a020-8234776dbb94
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-debug-apps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-debug-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-debug-apps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: a5f50502-9859-80e0-2bfc-287dddd2a98b
---

# Debug application proxy issues - Microsoft Entra ID | Microsoft Learn

## Overview

This article explains how to troubleshoot issues with Microsoft Entra application proxy. Use the flowchart to fix remote access issues for an on-premises web application.

## Before you begin

First, check the connector. Learn how in [Troubleshoot private network connectors](../../global-secure-access/troubleshoot-connectors).

## Flowchart for application issues

This flowchart helps you debug and fix common issues with the Microsoft Entra application proxy.

The table after the flowchart contains details about each step.

![Diagram of a flowchart that helps debug an application for Microsoft Entra application proxy issues.](media/application-proxy-debug-apps/application-proxy-apps-debugging-flowchart.png)

| Step | Goal | Action |
| --- | --- | --- |
| 1 | Sign in and check for user-related errors | Open a browser and sign into the app with your username and password. Check for errors like [This corporate app can't be accessed](application-proxy-sign-in-bad-gateway-timeout-error). |
| 2 | Verify user permissions and test app access | Make sure your user account has permissions for the app from inside the corporate network. Then test signing into the app by following the steps in [Test the application](application-proxy-add-on-premises-application#test-the-application). If sign-in issues continue, check [Troubleshoot sign-in errors](../monitoring-health/concept-provisioning-logs?context=azure/active-directory/manage-apps/context/manage-apps-context). |
| 3 | Confirm correct application proxy configuration | Open a browser and use the app. If an error appears immediately, check if the application proxy is set up correctly. For details about specific error messages, see [Troubleshoot application proxy problems and error messages](application-proxy-troubleshoot). |
| 4 | Ensure custom domain setup is correct or troubleshoot errors | If the page doesn't display, check if your custom domain is set up correctly. Review the information in [Work with custom domains](how-to-configure-custom-domain).If the page doesn't load and an error message appears, troubleshoot the error using the information in [Troubleshoot application proxy problems and error messages](application-proxy-troubleshoot).If it takes longer than 20 seconds before an error message appears, there might be a connectivity issue. Follow the steps in [Troubleshoot private network connectors](../../global-secure-access/troubleshoot-connectors). |
| 5 | Debug connectivity issues between the proxy and the connector | If issues persist, try connector debugging. Complete the steps described in [Troubleshoot private network connectors](../../global-secure-access/troubleshoot-connectors). |
| 6 | Publish all resources and resolve publishing issues | Ensure the publishing path includes all the necessary images, scripts, and style sheets for your application. For details, see [Add an on-premises app to Microsoft Entra ID](application-proxy-add-on-premises-application).Use the browser's developer tools (F12 tools in Internet Explorer or Microsoft Edge) for troubleshooting publishing issues. See [Application page doesn't display correctly](application-proxy-troubleshoot).Review options to fix broken links in [Links on the page don't work](application-proxy-page-links-broken-problem). |
| 7 | Minimize network latency | If the page loads slowly, explore ways to reduce network latency in [Considerations for reducing latency](application-proxy-network-topology#considerations-for-reducing-latency). |
| 8 | Access more troubleshooting resources | If issues persist, review more articles about [troubleshooting application proxy](application-proxy-troubleshoot). |
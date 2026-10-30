---
layout: Conceptual
title: Claims-aware apps - Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-configure-for-claims-aware-applications
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: How to publish on-premises ASP.NET applications that accept Active Directory Federation Services claims for secure remote access by your users.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
locale: en-us
document_id: fe17a31b-dd15-4f70-08a8-ab422ddc1af7
document_version_independent_id: 3100355f-ea67-5c36-0744-b1e65f9ecad2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-configure-for-claims-aware-applications.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-configure-for-claims-aware-applications
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-configure-for-claims-aware-applications.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 39274a57-2fab-f91a-6e4e-508a89851d18
---

# Claims-aware apps - Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn

## Overview

[Claims-aware apps](/en-us/previous-versions/windows/desktop/legacy/bb736227%28v=vs.85%29) perform a redirection to the Security Token Service (STS). The STS requests credentials from the user in exchange for a token and then redirects the user to the application. There are a few ways to enable application proxy to work with these redirects. Use this article to configure your deployment for claims-aware apps.

## Prerequisites

The STS that the claims-aware app redirects to must be available outside of your on-premises network. Expose it through a proxy or by allowing outside connections.

## Publish your application

1. Publish your application according to the instructions in [Publish applications with application proxy](application-proxy-add-on-premises-application).
2. Navigate to the application page in the portal and select **Single sign-on**.
3. If you chose **Microsoft Entra ID** as your **Preauthentication Method**, select **Microsoft Entra single sign-on disabled** as your **Internal Authentication Method**. If you chose **Passthrough** as your **Preauthentication Method**, you don't need to change anything.

## Configure Active Directory Federation Services

You can configure Active Directory Federation Services for claims-aware apps in one of two ways. The first is by using custom domains. The second is with WS-Federation.

### Option 1: Custom domains

If all the internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](how-to-configure-custom-domain) for your applications. Use the custom domains to create external URLs that are the same as the internal URLs. When your external URLs match your internal URLs, then the STS redirections work whether your users are on-premises or remote.

### Option 2: WS-Federation

1. Open Active Directory Federation Services management.
2. Go to **Relying Party Trusts**, right-click on the app you're publishing with application proxy, and choose **Properties**.

    ![Relying Party Trusts right-click on app name.](media/application-proxy-configure-for-claims-aware-applications/appproxyrelyingpartytrust.png)
3. On the **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.
4. Under **Trusted URL**, enter the URL you entered in the application proxy under **External URL** and select **OK**.

    ![Add an Endpoint - set Trusted URL value.](media/application-proxy-configure-for-claims-aware-applications/appproxyendpointtrustedurl.png)
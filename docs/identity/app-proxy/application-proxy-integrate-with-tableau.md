---
layout: Conceptual
title: Microsoft Entra application proxy and Tableau - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-integrate-with-tableau
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Publish Tableau Server through Microsoft Entra application proxy to provide secure remote access with preauthentication and Conditional Access.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
locale: en-us
document_id: 4e6e756a-2bf6-e971-17d3-082de55f81c2
document_version_independent_id: d49a6065-f7cf-7205-eb2c-0292c939fa26
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-integrate-with-tableau.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-integrate-with-tableau
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-integrate-with-tableau.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 6310a789-27f1-9b5d-8df9-6c633f917938
---

# Microsoft Entra application proxy and Tableau - Microsoft Entra ID | Microsoft Learn

## Overview

Microsoft and Tableau worked together so you can use application proxy to provide remote access for your Tableau deployment.

## Prerequisites

- Configure [Tableau](https://help.tableau.com/current/server/en-us/proxy.htm#azure).
- Install a [private network connector](application-proxy-add-on-premises-application).

## Enabling application proxy for Tableau

Application proxy supports the OAuth 2.0 Grant Flow, which is required for Tableau to work properly. This means that there are no longer any special steps required to enable this application, other than configuring it by following the publishing steps.

## Publish your applications in Microsoft Entra

To publish Tableau, you need to publish an application in the Microsoft Entra admin center.

- Steps 1 through 8 are detailed in the application proxy tutorial. For more information, see [Publish applications using Microsoft Entra application proxy](application-proxy-add-on-premises-application).
- Information about how to find Tableau values for the application proxy fields, see the Tableau documentation.

**To publish your app**:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Select **New application** at the top of the page.
4. Select **On-premises application**.
5. Fill out the required fields with information about the new app.
    - **Internal URL**: This application should have an internal URL that is the Tableau URL itself. For example, `https://adventure-works.tableau.com`.
    - **Pre-authentication method**: Microsoft Entra ID (recommended but not required).
6. Select **Add** at the top of the page. Your application is added, and the quick start menu opens.
7. In the quick start menu, select **Assign a user for testing**, and add at least one user to the application. Make sure this test account has access to the on-premises application.
8. Select **Assign** to save the test user assignment.
9. (Optional) On the app management page, select **Single sign-on**. Choose **Integrated Windows Authentication** from the drop-down menu, and fill out the required fields based on your Tableau configuration. Select **Save**.

## Testing

Your application is now ready to test. Access the external URL you used to publish Tableau, and sign in as a user assigned to both applications.
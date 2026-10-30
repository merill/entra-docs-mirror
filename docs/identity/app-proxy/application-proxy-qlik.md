---
layout: Conceptual
title: Microsoft Entra application proxy and Qlik Sense - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-qlik
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Integrate Microsoft Entra application proxy with Qlik Sense.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
locale: en-us
document_id: 6aa42942-653d-70c6-427b-c6b541652ee0
document_version_independent_id: c2156850-bc1d-c3f1-9e3b-5e3ba2e30cdc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-qlik.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-qlik
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-qlik.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 190f9d63-135f-6e63-e106-1525ff0208e0
---

# Microsoft Entra application proxy and Qlik Sense - Microsoft Entra ID | Microsoft Learn

## Overview

Microsoft and Qlik Sense worked together to provide remote access using Microsoft Entra application proxy.

## Prerequisites

- Set up [Qlik Sense](https://community.qlik.com/docs/DOC-19822).
- [Install a private network connector](application-proxy-add-on-premises-application).

## Publish your applications in Microsoft Entra

To publish Qlik Sense, publish two applications in Azure.

### Application 1: Qlik Sense Hub

Publish your application in Microsoft Entra. For a more detailed walkthrough of steps 1-8, see [Publish applications using Microsoft Entra application proxy](application-proxy-add-on-premises-application).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Select **New application** at the top of the page.
4. Select **On-premises application**.
5. Fill out the required fields with information about your new app.
    - **Internal URL**: This application should have an internal URL that is the Qlik Sense URL itself. For example, `https//demo.qlikemm.com:4244`.
    - **Pre-authentication method**: Microsoft Entra ID (recommended but not required).
6. Select **Add** at the bottom of the page. Your application is added, and the quick start menu opens.
7. In the quick start menu, select **Assign a user for testing**, and add at least one user to the application. Make sure this test account has access to the on-premises application.
8. Select **Assign** to save the test user assignment.
9. (Optional) On the app management page, select single sign-on. Choose **Kerberos Constrained Delegation** from the drop-down menu, and fill out the required fields based on your Qlik Sense configuration. Select **Save**.

### Application 2: Qlik Sense virtual proxy

Follow the same steps as for Application #1, with the following exceptions:

**Step #5** (required fields): The Internal URL should now be the Qlik Sense URL with the authentication port used by the application. The default is **4244** for HTTPS, and **4248** for HTTP for Qlik Sense releases before April 2018. The default for Qlik Sense releases after April 2018 is **443** for HTTPS and **80** for HTTP. For example, `https//demo.qlik.com:4244`.

**Step #8** (single sign-on): Don't set up single sign-on. Leave the **single sign-on** option disabled.

## Testing

Your application is now ready to test. Access the external URL you used to publish Qlik Sense in Application #1, and sign in as a user assigned to both applications.

## References

For more information about publishing Qlik Sense with application proxy, see the following Qlik Community Articles:

- [Microsoft Entra ID with integrated Windows authentication using a Kerberos Constrained Delegation with Qlik Sense](https://community.qlik.com/docs/DOC-20183)
- [Qlik Sense integration with Microsoft Entra application proxy](https://community.qlik.com/t5/Technology-Partners-Ecosystem/Azure-AD-Application-Proxy/ta-p/1528396)
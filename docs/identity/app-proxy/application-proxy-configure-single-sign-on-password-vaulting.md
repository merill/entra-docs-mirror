---
layout: Conceptual
title: Password vaulting for single sign-on with application proxy - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-configure-single-sign-on-password-vaulting
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Turn on single sign-on for your published on-premises applications with Microsoft Entra application proxy in the Microsoft Entra admin center.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
locale: en-us
document_id: 0129f50a-a0cd-cc81-4610-dccb929bccf8
document_version_independent_id: 7a63c519-3031-aa41-7041-6225b786f036
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-configure-single-sign-on-password-vaulting.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-configure-single-sign-on-password-vaulting
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-configure-single-sign-on-password-vaulting.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: e96b0816-5687-1461-a6af-efce8c82451c
---

# Password vaulting for single sign-on with application proxy - Microsoft Entra ID | Microsoft Learn

## Overview

Microsoft Entra application proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them. In the Microsoft Entra admin center, you can also set up single sign-on (SSO) to these apps. Your users only need to authenticate with Microsoft Entra ID, and they can access your enterprise application without having to sign in again.

Application proxy supports several [single sign-on modes](../enterprise-apps/plan-sso-deployment#choosing-a-single-sign-on-method). Password-based sign-on is intended for applications that use a username and password combination for authentication. Microsoft Entra ID stores the sign-in information and automatically provides it to the application when your users access it remotely.

## Prerequisites

This article requires that an app is published and tested with application proxy. For more information, see [Publish applications using Microsoft Entra application proxy](application-proxy-add-on-premises-application).

## Set up password vaulting for your application

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. From the list, select the app that you want to set up with SSO.
4. Select **application proxy**.
5. Change the **Pre Authentication type** to **Passthrough** and select **Save**. Later you can switch back to **Microsoft Entra ID** type again.
6. Select **Single sign-on**.
7. For the SSO mode, choose **Password-based Sign-on**.
8. For the Sign-on URL, enter the URL for the page where users enter their username and password to sign in to your app outside of the corporate network. The page could be the External URL that you created when you published the app through application proxy.

    ![Screenshot that shows the password-based sign-on configuration with URL entry.](media/application-proxy-configure-single-sign-on-password-vaulting/password-sso.png)
9. Select **Save**.
10. Select **application proxy**.
11. Change the **Pre Authentication type** to **Microsoft Entra ID** and select **Save**.
12. Select **Users and Groups**.
13. Assign users to the application.
14. Select **Add user**.
15. If you want to predefine credentials for a user, check the box in front of the user name and select **Update credentials**.
16. Browse to **Entra ID** &gt; **App registrations** &gt; **All applications**.
17. From the list, select the app that you configured with Password SSO.
18. Select **Branding**.
19. Update the **Home page URL** with the **Sign on URL** from the password SSO page and select **Save**.

## Test your app

Go to the My Apps portal. Sign in with your credentials (or the credentials for a test account that you set up with access). After you sign in, select the icon of the app. Opening the My Apps portal might trigger the installation of the My Apps Secure Sign-in browser extension. If credentials are predefined, the authentication to the app happens automatically. Otherwise, you must specify the user name or password for the first time.
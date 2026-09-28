---
layout: Conceptual
title: Security Assertion Markup Language (SAML) single sign-on (SSO) for on-premises apps with Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/conceptual-sso-apps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Configure SAML-based single sign-on for on-premises applications published through Microsoft Entra application proxy. Covers SAML claim mapping and remote access configuration.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: f496092e-dd14-80c2-2a42-b1a3a82c3805
document_version_independent_id: f496092e-dd14-80c2-2a42-b1a3a82c3805
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/conceptual-sso-apps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/conceptual-sso-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/conceptual-sso-apps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: b11d169e-79b6-5f01-1cc0-225caca6b111
---

# Security Assertion Markup Language (SAML) single sign-on (SSO) for on-premises apps with Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn

## Overview

Provide single sign-on (SSO) to on-premises applications secured with Security Assertion Markup Language (SAML) authentication. Provide remote access to SAML-based SSO applications through application proxy. With SAML single sign-on, Microsoft Entra authenticates to the application using the user's Microsoft Entra account. Microsoft Entra ID communicates the sign-on information to the application through a connection protocol. You can also map users to specific application roles based on rules you define in your SAML claims. By enabling application proxy in addition to SAML SSO, your users have external access to the application and a seamless SSO experience.

The applications must be able to consume SAML tokens issued by **Microsoft Entra ID**. This configuration doesn't apply to applications using an on-premises identity provider. For these scenarios, review [Resources for migrating applications to Microsoft Entra ID](../enterprise-apps/migration-resources).

SAML SSO with application proxy also works with the SAML token encryption feature. For more info, see [Configure Microsoft Entra SAML token encryption](../enterprise-apps/howto-saml-token-encryption).

The protocol diagrams describe the single sign-on sequence for both a service provider-initiated (SP-initiated) flow and an identity provider-initiated (IdP-initiated) flow. Application proxy works with SAML SSO by caching the SAML request and response to and from the on-premises application.

![Diagram shows interactions of Application, application proxy, Client, and Microsoft Entra ID for S P-Initiated single sign-on.](media/application-proxy-configure-single-sign-on-on-premises-apps/saml-sp-initiated-flow.png)

![Diagram shows interactions of Application, application proxy, Client, and Microsoft Entra ID for I d P-Initiated single sign-on.](media/application-proxy-configure-single-sign-on-on-premises-apps/saml-idp-initiated-flow.png)

## Create an application and set up SAML SSO

1. In the Microsoft Entra admin center, select **Microsoft Entra ID &gt; Enterprise applications** and select **New application**.
2. Enter the display name for your new application. Select **Integrate any other application you don't find in the gallery**, then select **Create**.
3. On the app's **Overview** page, select **Single sign-on**.
4. Select **SAML** as the single sign-on method.
5. First, set up SAML SSO to work while on the corporate network. See the basic SAML configuration section of [Configure SAML-based single sign-on](../../identity-platform/single-sign-on-saml-protocol) to configure SAML-based authentication for the application.
6. Add at least one user to the application and make sure the test account has access to the application. While connected to the corporate network, use the test account to verify that single sign-on works for the application.

    Note

    After you set up application proxy, you'll come back and update the SAML **Reply URL**.

## Publish the on-premises application with application proxy

Before you provide SSO for on-premises applications, enable application proxy and install a connector. For more information, see [how to prepare your on-premises environment, install and register a connector, and test the connector](application-proxy-add-on-premises-application). After you set up the connector, follow these steps to publish your new application with application proxy.

1. With the application still open in the Microsoft Entra admin center, select **application proxy**. Provide the **Internal URL** for the application. If you're using a custom domain, you also need to upload the Transport Layer Security (TLS) certificate for your application.

    Note

    As a best practice, use custom domains whenever possible for an optimized user experience. Learn more about [Working with custom domains in Microsoft Entra application proxy](how-to-configure-custom-domain).
2. Select **Microsoft Entra ID** as the **Pre Authentication** method for your application.
3. Copy the **External URL** for the application. You need this URL to complete the SAML configuration.
4. Using the test account, try to open the application with the **External URL** to validate that application proxy is set up correctly. If there are issues, see [Troubleshoot application proxy problems and error messages](application-proxy-troubleshoot).

## Update the SAML configuration

1. With the application still open in the Microsoft Entra admin center, select **Single sign-on**.
2. In the **Set up Single Sign-On with SAML** page, go to the **Basic SAML Configuration** heading and select its **Edit** icon (a pencil). Make sure the **External URL** you configured in application proxy is populated in the **Identifier**, **Reply URL**, and **Logout URL** fields. These URLs are required for application proxy to work correctly.
3. Edit the **Reply URL** configured earlier so that its domain is reachable on the internet via application proxy. For example, if your **External URL** is `https://contosotravel-f128.msappproxy.net` and the original **Reply URL** was `https://contosotravel.com/acs`, you need to update the original **Reply URL** to `https://contosotravel-f128.msappproxy.net/acs`.
4. Select the checkbox next to the updated **Reply URL** to mark it as the default.

    - After marking the required **Reply URL** as default, you can also delete the previously configured **Reply URL** that used the internal URL.
    - For an SP-initiated flow, make sure the back-end application specifies the correct **Reply URL** or Assertion Consumer Service URL for receiving the authentication token.

    Note

    If the back-end application expects the **Reply URL** to be the Internal URL, you need to either use [custom domains](how-to-configure-custom-domain) to have matching internal and external URLs or install the My Apps secure sign-in extension on users' devices. This extension will automatically redirect to the appropriate application proxy service. To install the extension, see [My Apps secure sign-in extension](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510#download-and-install-the-my-apps-secure-sign-in-extension).

## Test your app

Your app is up and running. To test the app:

1. Open a browser and navigate to the **External URL** that you created when you published the app.
2. Sign in with the test account that you assigned to the app. You should be able to load the application and have SSO into the application.
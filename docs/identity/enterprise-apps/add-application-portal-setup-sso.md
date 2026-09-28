---
layout: Conceptual
title: Enable SAML single sign-on for an enterprise application - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/add-application-portal-setup-sso
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Enable single sign-on for an enterprise application in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-07-10T00:00:00.0000000Z
ms.reviewer: ergleenl
ms.custom: mode-other, enterprise-apps, sfi-image-nochange
locale: en-us
document_id: 6ea1437d-a485-ed34-7706-c5be45ff3d8f
document_version_independent_id: f265f582-1894-bef9-9b81-a6bbd34b4381
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/add-application-portal-setup-sso.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/add-application-portal-setup-sso
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/add-application-portal-setup-sso.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: e51504da-e7e5-8544-0403-0b1652dcebef
---

# Enable SAML single sign-on for an enterprise application - Microsoft Entra ID | Microsoft Learn

In this article, you use the Microsoft Entra admin center to enable single sign-on (SSO) for an enterprise application that you added to your Microsoft Entra tenant. After you configure SSO, your users can sign in by using their Microsoft Entra credentials.

Microsoft Entra ID has a gallery that contains thousands of preintegrated applications that use SSO. This article uses an enterprise application named **Microsoft Entra SAML Toolkit 1** as an example, but the concepts apply for most preconfigured enterprise applications in the Microsoft Entra application gallery.

If your application doesn't integrate directly with Microsoft Entra ID for single sign-on, and instead tokens are provided to the application by a relying party Security Token Service (STS), then see the article [Enable single sign-on for an enterprise application with a relying party security token service](add-application-portal-setup-sso-rpsts).

We recommend that you use a nonproduction environment to test the steps in this article.

## Prerequisites

To configure SSO, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: Cloud Application Administrator, Application Administrator, or owner of the service principal.
- Completion of the steps in [Quickstart: Create and assign a user account](add-application-portal-assign-users).

Note

SAML SSO is only configurable on single tenant applications or gallery applications. Multi-tenant applications will show SAML SSO configurations greyed out.

## Enable single sign-on

To enable SSO for an application:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Enter the name of the existing application in the search box, and then select the application from the search results. For example, **Microsoft Entra SAML Toolkit 1**.
4. In the **Manage** section of the left menu, select **Single sign-on** to open the **Single sign-on** pane for editing.
5. Select **SAML** to open the SSO configuration page. After the application is configured, users can sign in to it by using their credentials from the Microsoft Entra tenant.
6. The process of configuring an application to use Microsoft Entra ID for SAML-based SSO varies depending on the application. For any of the enterprise applications in the gallery, use the **configuration guide** link to find information about the steps needed to configure the application. The steps for the **Microsoft Entra SAML Toolkit 1** are listed in this article.

    ![Screenshot showing how to configure single sign-on for an enterprise application.](media/add-application-portal-setup-sso/saml-configuration.png)
7. In the **Set up Microsoft Entra SAML Toolkit 1** section, record the values of the **Login URL**, **Microsoft Entra Identifier**, and **Logout URL** properties to be used later.

## Configure single sign-on in the tenant

You add sign-in and reply URL values, and you download a certificate to begin the configuration of SSO in Microsoft Entra ID.

To configure SSO in Microsoft Entra ID:

1. In the Microsoft Entra admin center, select **Edit** in the **Basic SAML Configuration** section on the **Set up Single Sign-On with SAML** pane.
2. For **Reply URL (Assertion Consumer Service URL)**, enter `https://samltoolkit.azurewebsites.net/SAML/Consume`.
3. For **Sign on URL**, enter `https://samltoolkit.azurewebsites.net/`. The **Identifier (Entity ID)** is typically a URL specific to the application you're integrating with. For the **Microsoft Entra SAML Toolkit 1** application in this example, the value is automatically generated once you input the **Sign on** URL and **Reply URL** values. Follow the specific configuration guide for the application you're integrating with to determine the correct value.
4. Select **Save**.
5. In the **SAML Certificates** section, select **Download** for **Certificate (Raw)** to download the SAML signing certificate and save it to be used later.

## Configure single sign-on in the application

Using single sign-on in the application requires you to register the user account with the application and to add the SAML configuration values that you previously recorded.

### Register the user account

To register a user account with the application:

1. Open a new browser window and browse to the sign-in URL for the application. For the **Microsoft Entra SAML Toolkit** application, the address is `https://samltoolkit.azurewebsites.net`.
2. Select **Register** in the upper right corner of the page.
3. For **Email**, enter the email address of the user that can access the application. Ensure that the user account is already assigned to the application.
4. Enter a **Password** and confirm it.
5. Select **Register**.

### Configure SAML settings

To configure SAML settings for the application:

1. On the application's sign-in page, sign in with the credentials of the user account that you already assigned to the application, select **SAML Configuration** at the upper-left corner of the page.
2. Select **Create** in the middle of the page.
3. For **Login URL**, **Microsoft Entra Identifier**, and **Logout URL**, enter the values that you recorded earlier.
4. Select **Choose file** to upload the certificate that you previously downloaded.
5. Select **Create**.
6. Copy the values of the **SP Initiated Login URL** and the **Assertion Consumer Service (ACS) URL** to be used later.

## Update single sign-on values

Use the values that you recorded for **SP Initiated Login URL** and **Assertion Consumer Service (ACS) URL** to update the single sign-on values in your tenant.

To update the single sign-on values:

1. In the Microsoft Entra admin center, select **Edit** in the **Basic SAML Configuration** section on the **Set up single sign-on** pane.
2. For **Reply URL (Assertion Consumer Service URL)**, enter the **Assertion Consumer Service (ACS) URL** value that you previously recorded.
3. For **Sign on URL**, enter the **SP Initiated Login URL** value that you previously recorded.
4. Select **Save**.

## Test single sign-on

You can test the single sign-on configuration from the **Set up single sign-on** pane.

To test SSO:

1. In the **Test single sign-on with Microsoft Entra SAML Toolkit 1** section, on the **Set up single sign-on with SAML** pane, select **Test**.
2. Sign in to the application using the Microsoft Entra credentials of the user account that you assigned to the application.
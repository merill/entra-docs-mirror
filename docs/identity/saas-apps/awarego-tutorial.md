---
layout: Conceptual
title: Configure AwareGo for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/awarego-tutorial
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jeevansd
ms.author: jeedes
ms.reviewer: jomondi
ms.service: entra-id
ms.subservice: saas-apps
manager: pmwongera
description: Learn how to configure single sign-on between Microsoft Entra ID and AwareGo.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 0144788e-c35a-359d-ffaa-b09057aa4ba0
document_version_independent_id: 64347976-1512-0989-1afb-183724c0803c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/awarego-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/awarego-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/awarego-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 3f52c169-3539-a178-bc42-6b584e59d6d3
---

# Configure AwareGo for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate AwareGo with Microsoft Entra ID. When you integrate AwareGo with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to AwareGo.
- Enable your users to be automatically signed in to AwareGo with their Microsoft Entra accounts.
- Manage your accounts in one central location, the Azure portal.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- An AwareGo single sign-on (SSO)-enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment. AwareGo supports a service provider (SP)-initiated SSO.

## Adding AwareGo from the gallery

To configure the integration of AwareGo into Microsoft Entra ID, you need to add AwareGo from the gallery to your list of managed software as a service (SaaS) apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **AwareGo** in the search box.
4. In the results pane, select **AwareGo**, and then add the app. In a few seconds, the app is added to your tenant.

## Configure and test Microsoft Entra SSO for AwareGo

Configure and test Microsoft Entra SSO with AwareGo by using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in AwareGo.

To configure and test Microsoft Entra SSO with AwareGo, do the following:

1. **Configure Microsoft Entra SSO** to enable your users to use this feature.

    a. **Create a Microsoft Entra test user** to test Microsoft Entra single sign-on with user B.Simon. b. **Assign the Microsoft Entra test user** to enable user B.Simon to use Microsoft Entra single sign-on.
2. **Configure AwareGo SSO** to configure the single sign-on settings on the application side.

    a. **Create an AwareGo test user** to have a counterpart of B.Simon in AwareGo that's linked to the Microsoft Entra representation of the user. b. **Test SSO** to verify that the configuration works.

## Configure Microsoft Entra SSO

To enable Microsoft Entra SSO in the Azure portal, do the following:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **AwareGo** application integration page, under **Manage**, select **single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. To edit the settings, on the **Set up Single Sign-On with SAML** pane, select the **Edit** button.

    ![Screenshot of the Edit button for Basic SAML Configuration.](common/edit-urls.png)
5. On the edit pane, under **Basic SAML Configuration**, do the following:

    a. In the **Sign on URL** box, enter either of the following URLs:

    - `https://lms.awarego.com/auth/signin/`
    - `https://my.awarego.com/auth/signin/`

    b. In the **Identifier (Entity ID)** box, enter a URL in the following format: `https://<SUBDOMAIN>.awarego.com`

    c. In the **Reply URL** box, enter a URL in the following format: `https://<SUBDOMAIN>.awarego.com/auth/sso/callback`

    Note

    The preceding values aren't real. Update them with the actual identifier and reply URLs. To obtain the values, contact the [AwareGo client support team](mailto:support@awarego.com). You can also refer to the examples in the **Basic SAML Configuration** section.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, next to **Certificate (Base64)**, select **Download** to download the certificate and save it to your computer.

    ![Screenshot of the certificate &quot;Download&quot; link on the SAML Signing Certificate pane.](common/certificatebase64.png)
7. In the **Set up AwareGo** section, copy one or more URLs, depending on your requirements.

    ![Screenshot of the &quot;Set up AwareGo&quot; pane for copying configuration URLs.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure AwareGo SSO

To configure single sign-on on the **AwareGo** side, send the **Certificate (Base64)** certificate you downloaded earlier and the URLs you copied earlier to the [AwareGo support team](mailto:support@awarego.com). The support team creates this setting to establish the SAML SSO connection properly on both sides.

### Create an AwareGo test user

In this section, you create a user called Britta Simon in AwareGo. Work with the [AwareGo support team](mailto:support@awarego.com) to add the users in the AwareGo platform. You must create and activate the users before you can use single sign-on.

## Test SSO

In this section, you can test your Microsoft Entra single sign-on configuration by doing any of the following:

- In the Azure portal, select **Test this application**. This redirects you to the AwareGo sign-in page, where you can initiate the sign-in flow.
- Go to the AwareGo sign-in page directly, and initiate the sign-in flow from there.
- Go to Microsoft My Apps. When you select the **AwareGo** tile in My Apps, you're redirected to the AwareGo sign-in page. For more information, see [Sign in and start apps from the My Apps portal](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
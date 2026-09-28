---
layout: Conceptual
title: Configure Prezi for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/prezi-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Prezi.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: ba70bcfe-2e87-6f65-1974-c7f44a2514ec
document_version_independent_id: afb917e4-360c-47ed-e7b1-4e7f0efd48b6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/prezi-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/prezi-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/prezi-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: dbb54ec9-77fd-9537-7015-3f01d412114c
---

# Configure Prezi for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Prezi with Microsoft Entra ID. When you integrate Prezi with Microsoft Entra ID, you can:

- Control who has access to Prezi in Microsoft Entra ID.
- Enable your users to be automatically signed in to Prezi with their Microsoft Entra accounts.
- Manage your accounts.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A Prezi subscription enabled with single sign-on (SSO).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Prezi supports SP and IDP initiated SSO.
- Prezi supports just-in-time user provisioning.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Prezi from the gallery

To configure the integration of Prezi into Microsoft Entra ID, you need to add Prezi from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, enter **Prezi** in the search box.
4. Select **Prezi** from the results panel, and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Prezi

Configure and test Microsoft Entra SSO with Prezi by using a test user called B.Simon. For SSO to work, you establish a link relationship between a Microsoft Entra user and the related user in Prezi.

To configure and test Microsoft Entra SSO with Prezi, perform the following steps:

1. Configure Microsoft Entra SSOto enable your users to use this feature.
    1. Create a Microsoft Entra test user to test Microsoft Entra SSO with B.Simon.
    2. Assign the Microsoft Entra test user to enable B.Simon to use Microsoft Entra SSO.
2. Configure Prezi SSOto configure the SSO settings on the application side.
    1. Create a Prezi test user to have a counterpart of B.Simon in Prezi that's linked to the Microsoft Entra representation of the user.
3. Test SSO to verify whether the configuration works.

## Configure Microsoft Entra SSO

To enable Microsoft Entra SSO in the Azure portal:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Prezi** application integration page, find the **Manage** section and select **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon to edit the settings on **Basic SAML Configuration**.

    ![Edit Basic SAML Configuration settings](common/edit-urls.png)
5. In the **Basic SAML Configuration** section, the user doesn't have to do any step because the app is already preintegrated with Azure.
6. Select **Set additional URLs**, and do the following step if you want to configure the application in **SP**-initiated mode:

    In the **Sign-on URL** box, type the URL: `https://prezi.com/login/sso/`.
7. Select **Save**.
8. The Prezi application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![User Attributes &amp; Claims](common/default-attributes.png)
9. The Prezi application also expects a few more attributes to be passed back in SAML response, as shown here. These attributes are also prepopulated, but you can review them based on your requirements.

    | Name | Source attribute |
    | --- | --- |
    | given\_name | user.givenname |
    | family\_name | user.surname |
10. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)**. Select **Download** to download the certificate and save it on your computer.

    ![The certificate download link](common/certificatebase64.png)
11. In the **Set up Prezi** section, copy the appropriate URLs based on your requirements.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Prezi SSO

1. In a different web browser window, sign in to Prezi with your team account and go to the [Admin Console](https://prezi.com/organizations/manage).
2. From the **Admin Console**, select the **Settings** tab.

    ![Settings tab](media/prezi-tutorial/settings-image.png)
3. Go to the **Single Sign-On (SSO)** section, and turn on the toggle to enable SSO.

    ![Single Sign-On (SSO) toggle](media/prezi-tutorial/single-sign-on.png)
4. In the **Single sign-on (SSO)** section, follow these steps:

    ![Single sign-on (SSO) section](media/prezi-tutorial/configuration.png)

    1. In the **Identifier or Issuer URL** box, paste the **Microsoft Entra Identifier** value, which you copied.
    2. In the **SAML 2.0 Endpoint (HTTP)** box, paste the **Login URL** value, which you copied.
    3. Open the downloaded **Certificate (Base64)** into Notepad. Copy the contents of the certificate, and paste the contents into the **Certificate (X.509)** box.
    4. Select **Save**.

### Create a Prezi test user

In this section, a user called Britta Simon is created in Prezi. Prezi supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Prezi, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Prezi Sign on URL where you can initiate the login flow.
- Go to Prezi Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Prezi for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Prezi tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Prezi for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
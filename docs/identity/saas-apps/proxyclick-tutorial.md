---
layout: Conceptual
title: Configure Proxyclick for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/proxyclick-tutorial
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
description: In this article,  you learn how to configure single sign-on between Microsoft Entra ID and Proxyclick.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 91e96964-bd40-fd4c-5276-2d5e3db111e7
document_version_independent_id: 1c033fac-0336-08b7-8ee2-6c8c06e6eb43
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/proxyclick-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/proxyclick-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/proxyclick-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 48f48a8d-aed5-75a0-9653-53b971cf1aa0
---

# Configure Proxyclick for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Proxyclick with Microsoft Entra ID. When you integrate Proxyclick with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Proxyclick.
- Enable your users to be automatically signed-in to Proxyclick with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Proxyclick single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Proxyclick supports SP-initiated and IdP-initiated SSO.
- Proxyclick supports [Automated user provisioning](proxyclick-provisioning-tutorial).

## Add Proxyclick from the gallery

To configure the integration of Proxyclick into Microsoft Entra ID, you need to add Proxyclick from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Proxyclick** in the search box.
4. Select **Proxyclick** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Proxyclick

Configure and test Microsoft Entra SSO with Proxyclick using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Proxyclick.

To configure and test Microsoft Entra SSO with Proxyclick, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Proxyclick SSO**- to configure the single sign-on settings on application side.
    1. **Create Proxyclick test user** - to have a counterpart of B.Simon in Proxyclick that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Proxyclick** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. In the **Basic SAML Configuration** dialog box, if you want to configure the application in IdP-initiated mode, perform the following steps.

    a. In the **Identifier** box, type a URL using the following pattern: `https://saml.proxyclick.com/init/<COMPANY_ID>`

    b. In the **Reply URL** box, type a URL using the following pattern: `https://saml.proxyclick.com/consume/<COMPANY_ID>`
6. If you want to configure the application in SP-initiated mode, select **Set additional URLs**. In the **Sign on URL** textbox, type a URL using the following pattern:

    `https://saml.proxyclick.com/init/<COMPANY_ID>`

    Note

    These values are placeholders. You need to use the actual Identifier,Reply URL and Sign on URL. Steps for getting these values are described later in this article.
7. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select the **Download** link next to **Certificate (Base64)**, per your requirements, and save the certificate on your computer:

    ![Certificate download link](common/certificatebase64.png)
8. In the **Set up Proxyclick** section, copy the appropriate URLs, based on your requirements:

    ![Copy the configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Proxyclick SSO

1. In a new web browser window, sign in to your Proxyclick company site as an admin.
2. Select **Account & Settings**.

    ![Select Account &amp; Settings.](media/proxyclick-tutorial/account.png)
3. Scroll down to the **Integrations** section and select **SAML**.

    ![Select SAML.](media/proxyclick-tutorial/settings.png)
4. In the **SAML** section, take the following steps.

    ![SAML section](media/proxyclick-tutorial/configuration.png)

    1. Copy the **SAML Consumer URL** value and paste it into the **Reply URL** box in the **Basic SAML Configuration** dialog box.
    2. Copy the **SAML SSO Redirect URL** value and paste it into the **Sign on URL** and **Identifier** boxes in the **Basic SAML Configuration** dialog box.
    3. In the **SAML Request Method** list, select **HTTP Redirect**.
    4. In the **Issuer** box, paste the **Microsoft Entra Identifier** value that you copied.
    5. In the **SAML 2.0 Endpoint URL** box, paste the **Login URL** value that you copied.
    6. In Notepad, open the certificate file that you downloaded. Paste the contents of this file into the **Certificate** box.
    7. Select **Save Changes**.

### Create Proxyclick test user

To enable Microsoft Entra users to sign in to Proxyclick, you need to add them to Proxyclick. You need to add them manually.

To create a user account, take these steps:

1. Sign in to your Proxyclick company site as an admin.
2. Select **Colleagues** at the top of the window.

    ![Select Colleagues.](media/proxyclick-tutorial/user.png)
3. Select **Add Colleague**.

    ![Select Add Colleague.](media/proxyclick-tutorial/add-user.png)
4. In the **Add a colleague** section, take the following steps.

    ![Add a colleague section.](media/proxyclick-tutorial/create-user.png)

    1. In the **Email** box, enter the email address of the user. In this case, **brittasimon@contoso.com**.
    2. In the **First Name** box, enter the first name of the user. In this case, **Britta**.
    3. In the **Last Name** box, enter the last name of the user. In this case, **Simon**.
    4. Select **Add User**.

Note

Proxyclick also supports automatic user provisioning, you can find more details [here](proxyclick-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Proxyclick Sign on URL where you can initiate the login flow.
- Go to Proxyclick Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Proxyclick for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Proxyclick tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Proxyclick for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
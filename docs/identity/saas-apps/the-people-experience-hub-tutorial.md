---
layout: Conceptual
title: Configure The People Experience Hub for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/the-people-experience-hub-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and The People Experience Hub.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 5d9f9470-d0d0-f4ff-b68c-95df47851c1f
document_version_independent_id: 0cc1434e-4e1a-f397-77f3-9731068adeab
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/the-people-experience-hub-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/the-people-experience-hub-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/the-people-experience-hub-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: cc85baa3-1477-218a-2a95-51b2df2781e0
---

# Configure The People Experience Hub for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate The People Experience Hub with Microsoft Entra ID. When you integrate The People Experience Hub with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to The People Experience Hub.
- Enable your users to be automatically signed-in to The People Experience Hub with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- The People Experience Hub single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- The People Experience Hub supports **SP and IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Adding The People Experience Hub from the gallery

To configure the integration of The People Experience Hub into Microsoft Entra ID, you need to add The People Experience Hub from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **The People Experience Hub** in the search box.
4. Select **The People Experience Hub** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for The People Experience Hub

Configure and test Microsoft Entra SSO with The People Experience Hub using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in The People Experience Hub.

To configure and test Microsoft Entra SSO with The People Experience Hub, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure The People Experience Hub SSO**- to configure the single sign-on settings on application side.
    1. **Create The People Experience Hub test user** - to have a counterpart of B.Simon in The People Experience Hub that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **The People Experience Hub** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type the URL: `https://app.pxhub.io`

    b. In the **Reply URL** textbox, type a URL using the following pattern: `https://auth.api.pxhub.io/v1/auth/saml/<COMPANY_ID>/assert`
6. Perform the following step, if you wish to configure the application in **SP** initiated mode:

    In the **Sign on URL** textbox, type a URL using the following pattern: `https://auth.api.pxhub.io/v1/auth/saml/<COMPANY_ID>/login`

    Note

    These values aren't real. Update these values with the actual Reply URL and Sign on URL. Contact [The People Experience Hub support team](mailto:it@pxhub.io) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section in the Microsoft Entra admin center.
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link](common/certificatebase64.png)
8. On the **Set up The People Experience Hub** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration appropriate URL.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure The People Experience Hub SSO

1. Log in to The People Experience Hub company site as an administrator.
2. Go to **Admin Settings** &gt; **Integrations** &gt; **Single Sign-On** and select **Manage**.

    ![Screenshot shows settings of the configuration.](media/the-people-experience-hub-tutorial/settings.png)
3. In the **SAML 2.0 Single sign-on** page, perform the following steps:

    ![Screenshot shows configuration of the page.](media/the-people-experience-hub-tutorial/values.png)

    1. **Enable SAML 2.0 Single sign-on** toggle on.
    2. Copy **EntityID** value, paste this value into the **Identifier** textbox in the **Basic SAML Configuration** section in Microsoft Entra admin center.
    3. Copy **Login URL** value, paste this value into the **Sign on URL** textbox in the **Basic SAML Configuration** section in Microsoft Entra admin center.
    4. Copy **Reply URL** value, paste this value into the **Reply URL** textbox in the **Basic SAML Configuration** section in Microsoft Entra admin center.
    5. In the **SSO Login URL** textbox, paste the **Login URL** value, which you copied from the Microsoft Entra admin center.
    6. Open the downloaded **Certificate (Base64)** into Notepad and paste the content into the **X509 Certificate** textbox.
    7. Select **Save Configuration**.

### Create The People Experience Hub test user

1. In a different web browser window, sign into The People Experience Hub website as an administrator.
2. Navigate to **Admin Settings** &gt; **Users** and select **Create**.

    ![Screenshot shows how to create users in application.](media/the-people-experience-hub-tutorial/create.png)
3. In the **Create a new admin users** section, perform the following steps:

    ![Screenshot shows how to create new users in the page.](media/the-people-experience-hub-tutorial/details.png)

    1. In the **Email** textbox, enter a valid email address of the user.
    2. In the **First Name** textbox, enter the first name of the user.
    3. In the **Last Name** textbox, enter the last name of the user.
    4. Select **Create User**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application** in Microsoft Entra admin center. this option redirects to The People Experience Hub Sign-on URL where you can initiate the login flow.
- Go to The People Experience Hub Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application** in Microsoft Entra admin center and you should be automatically signed in to The People Experience Hub for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select The People Experience Hub tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to The People Experience Hub for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
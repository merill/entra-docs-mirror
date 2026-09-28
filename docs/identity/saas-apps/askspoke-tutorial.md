---
layout: Conceptual
title: Configure askSpoke for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/askspoke-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and askSpoke.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: ab12a30a-395e-0508-2e90-4c23df557fe4
document_version_independent_id: b3dd8711-80ed-7c0c-690c-ae5a1f52b561
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/askspoke-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/askspoke-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/askspoke-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 3b85d518-6728-6aba-5a63-5c38a7a1b562
---

# Configure askSpoke for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate askSpoke with Microsoft Entra ID. When you integrate askSpoke with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to askSpoke.
- Enable your users to be automatically signed-in to askSpoke with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- askSpoke single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- askSpoke supports **SP and IDP** initiated SSO.
- askSpoke supports **Just In Time** user provisioning.
- askSpoke supports [Automated user provisioning](askspoke-provisioning-tutorial).

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add askSpoke from the gallery

To configure the integration of askSpoke into Microsoft Entra ID, you need to add askSpoke from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **askSpoke** in the search box.
4. Select **askSpoke** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for askSpoke

Configure and test Microsoft Entra SSO with askSpoke using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in askSpoke.

To configure and test Microsoft Entra SSO with askSpoke, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure askSpoke SSO**- to configure the single sign-on settings on application side.
    1. **Create askSpoke test user** - to have a counterpart of B.Simon in askSpoke that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **askSpoke** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, enter the values for the following fields:

    In the **Reply URL** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.askspoke.com/saml/callback`

    Note

    The Reply URL value isn't real. Update this value with the actual Reply URL. Contact [askSpoke Client support team](mailto:support@askspoke.com) to get this value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type the URL: `https://askspoke.com/login`
7. askSpoke application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
8. In addition to above, askSpoke application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | firstName | user.givenname |
    | lastName | user.surname |
9. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
10. On the **Set up askSpoke** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure askSpoke SSO

1. In a different web browser window, sign into askSpoke website as an administrator.
2. Select **Settings** tab from the left navigation pane.

    ![askSpoke settings tab](media/askspoke-tutorial/configure-1.png)
3. Scroll down to **SSO** and select **Connect**.

    ![askSpoke connect](media/askspoke-tutorial/configure-2.png)
4. On the **Enable SAML & SCIM** section, perform the following steps:

    ![askSpoke Enable SAML &amp; SCIM section](media/askspoke-tutorial/configure-3.png)

    1. In the **Sign-on URL** textbox, paste **Login URL** value, which you copied previously.
    2. In the **Issuer** textbox, paste **Microsoft Entra Identifier** value, which you copied previously.
    3. Open the downloaded **Certificate(Base64)** file into Notepad and copy content of certificate file and paste it into the **Public certificate** textbox.
    4. Copy **ACS URL** value and paste it into **Reply URL** textbox in the **Basic SAML Configuration** section.
    5. Select **Test SAML connection**.

### Create askSpoke test user

In this section, a user called B.Simon is created in askSpoke. askSpoke supports just-in-time provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in askSpoke, a new one is created when you attempt to access askSpoke.

askSpoke also supports automatic user provisioning, you can find more details [here](askspoke-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to askspoke Sign on URL where you can initiate the login flow.
- Go to askspoke Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the askspoke for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the askspoke tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the askspoke for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
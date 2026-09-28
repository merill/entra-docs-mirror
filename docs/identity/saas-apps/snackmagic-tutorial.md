---
layout: Conceptual
title: Configure Snackmagic for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/snackmagic-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Snackmagic.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: c315b4e7-238a-7f34-b7f7-6b84e0906113
document_version_independent_id: 123df56e-c17f-ce3e-2b59-4839f43b9aee
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/snackmagic-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/snackmagic-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/snackmagic-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 08e4dc27-7982-66e0-68f0-77baa4b726ad
---

# Configure Snackmagic for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Snackmagic with Microsoft Entra ID. When you integrate Snackmagic with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Snackmagic.
- Enable your users to be automatically signed-in to Snackmagic with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Snackmagic single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Snackmagic supports **SP and IDP** initiated SSO.
- Snackmagic supports **Just In Time** user provisioning.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Snackmagic from the gallery

To configure the integration of Snackmagic into Microsoft Entra ID, you need to add Snackmagic from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Snackmagic** in the search box.
4. Select **Snackmagic** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Snackmagic

Configure and test Microsoft Entra SSO with Snackmagic using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Snackmagic.

To configure and test Microsoft Entra SSO with Snackmagic, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Snackmagic SSO**- to configure the single sign-on settings on application side.
    1. **Create Snackmagic test user** - to have a counterpart of B.Simon in Snackmagic linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Snackmagic** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Relay State** text box, type the URL: `https://www.snackmagic.com/`

    b. In the **Logout Url** text box, type the URL: `https://sso.snackmagic.com/slo/callback`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    a. In the **Sign-on URL** text box, type the URL: `https://www.snackmagic.com/?modal=login`
7. Select **Save**.
8. Snackmagic application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
9. In addition to above, Snackmagic application expects few more attributes to be passed back in SAML response, which are shown below. These attributes are also prepopulated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | firstName | user.givenname |
    | lastName | user.surname |
    | company | user.companyname |
    | phone | user.telephonenumber |
    | email | user.userprincipalname |
10. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
11. On the **Set up Snackmagic** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Snackmagic SSO

1. Sign in to your Snackmagic company site as an administrator.
2. Go to **Account Settings** &gt; **SSO Preferences** and perform the following steps:

    ![Screenshot shows the SSO Settings.](media/snackmagic-tutorial/account.png)

    1. Select **Enable SSO** checkbox.
    2. In the **Service Provider Issuer/Identifier** textbox, paste the **Identifier URL** value, which you copied previously.
    3. In the **Identity Provider Single Sign-On URL** textbox, paste the **Login URL** value, which you copied previously.
    4. Open the downloaded **Certificate (Base64)** into Notepad and paste the content into the **X.509 Certificate** textbox.
    5. Select **Enable SLO** checkbox.
    6. In the **Identity Provider Single Logout URL** textbox, paste the **Logout URL** value, which you copied previously.
    7. Select **SUBMIT**.

### Create Snackmagic test user

In this section, a user called Britta Simon is created in Snackmagic. Snackmagic supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Snackmagic, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Snackmagic Sign on URL where you can initiate the login flow.
- Go to Snackmagic Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Snackmagic for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Snackmagic tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the sign-in flow and if configured in IDP mode, you should be automatically signed in to the Snackmagic for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
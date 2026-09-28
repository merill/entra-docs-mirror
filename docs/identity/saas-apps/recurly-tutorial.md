---
layout: Conceptual
title: Configure Recurly for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/recurly-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Recurly.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 40fd1bb5-5803-2780-a2f9-423ad6a79515
document_version_independent_id: b755078b-4165-03a6-4ff1-d11fbb8e09c9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/recurly-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/recurly-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/recurly-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 5ed4e54b-3386-3944-ec01-5583423d5eb8
---

# Configure Recurly for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Recurly with Microsoft Entra ID. When you integrate Recurly with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Recurly.
- Enable your users to be automatically signed-in to Recurly with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Recurly single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Recurly supports **SP and IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Recurly from the gallery

To configure the integration of Recurly into Microsoft Entra ID, you need to add Recurly from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Recurly** in the search box.
4. Select **Recurly** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Recurly

Configure and test Microsoft Entra SSO with Recurly using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Recurly.

To configure and test Microsoft Entra SSO with Recurly, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Recurly SSO**- to configure the single sign-on settings on application side.
    1. **Create Recurly test user** - to have a counterpart of B.Simon in Recurly that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Recurly** application integration page, find the **Manage** section and select **single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, the **Identifier** and **Reply URL** values are pre-configured with `https://app.recurly.com` and `https://app.recurly.com/login/sso` respectively. Perform the following step to complete the configuration:

    a. In the **Sign-on URL** text box, type the URL: `https://app.recurly.com/login/sso`
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, select **Edit**, select the `...` next to the thumbprint status, select **PEM certificate download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificate-base64-download.png)
7. Your Recurly application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows an example of this. The default value of **Unique User Identifier** is **user.userprincipalname** but Recurly expects this to be mapped with the user's email address. For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.

    ![image](common/default-attributes.png)
8. Recurly application expects to enable token encryption in order to make SSO work. To activate token encryption, Browse to **Entra ID** &gt; **Enterprise apps** &gt; select your application &gt; **Token encryption**. For more information see the article [Configure Microsoft Entra SAML token encryption](../enterprise-apps/howto-saml-token-encryption).

    1. Please contact [Recurly Support](mailto:support@recurly.com) to get a copy of the certificate to import.
    2. After importing the certificate, select the `...` next to the thumbprint status, select `Activate token encryption certificate`.
    3. For more information on configuring token encryption, please refer this [link](../enterprise-apps/howto-saml-token-encryption).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Recurly SSO

Follow these steps to configure single sign-on for your **Recurly** site.

1. Log into your Recurly company site as an administrator.
2. Navigate to **Admin** &gt; **Users**.

    ![Screenshot shows Navigating to Users menu](media/recurly-tutorial/menu.png)
3. Select the **Configure Single Sign on** button on the top right.

    ![Screenshot shows navigating to SSO configuration page](media/recurly-tutorial/configure-button.png)
4. In the **Single Sign-On** section, select the **Enabled** radio button and perform the following steps in the **Identity Provider** section:

    ![Screenshot shows complete SSO configuration](media/recurly-tutorial/configuration.png)

    a. In **PROVIDER NAME**, select **Azure**.

    b. In the **SAML ISSUER ID** textbox, paste the **Application(Client ID)** value.

    c. In the **LOGIN URL** textbox, paste the **Login URL** value which you copied previously.

    d. Open the downloaded Certificate (PEM) into Notepad and paste the content into the **CERTIFICATE** textbox.

    e. Select **Save Changes**.

### Create Recurly test user

In this section, you invite a new user to join your site and require them to use SSO to test the configuration.

1. Navigate to **Admin** &gt; **Users**, select **Invite User** and type the email address of the Azure test user that was previously created. Your invitation will default to requiring them to use SSO.

    ![Screenshot shows Navigating to Invite User page](media/recurly-tutorial/user-button.png)

    ![Screenshot shows Invite User page](media/recurly-tutorial/invite-user.png)
2. The test user will receive an email from Recurly inviting them to join your site.
3. After accepting the invite, the test user is listed under **Company Users** in your site and is able to log in using SSO.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Recurly Sign on URL where you can initiate the login flow.
- Go to Recurly Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Recurly for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Recurly tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Recurly for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
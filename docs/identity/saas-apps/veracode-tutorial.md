---
layout: Conceptual
title: Configure Veracode for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/veracode-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Veracode.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 2bc273c6-b406-1d93-d451-07c577cd0364
document_version_independent_id: 558be3a3-a111-f2a4-2a23-3e8e8462a699
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/veracode-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/veracode-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/veracode-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 98c35632-8126-5def-f3e4-62a6c45a937e
---

# Configure Veracode for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Veracode with Microsoft Entra ID. When you integrate Veracode with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Veracode.
- Enable your users to be automatically signed-in to Veracode with their Microsoft Entra accounts.
- Manage your accounts in one central location: the Azure portal.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A Veracode single sign-on (SSO)-enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment. Veracode supports identity provider initiated SSO and just-in-time user provisioning.

## Add Veracode from the gallery

To configure the integration of Veracode into Microsoft Entra ID, add Veracode from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type "Veracode" in the search box.
4. Select **Veracode** from the results panel, and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Veracode

Configure and test Microsoft Entra SSO with Veracode by using a test user called **B.Simon**. For SSO to work, you must establish a link between a Microsoft Entra user and the related user in Veracode.

To configure and test Microsoft Entra SSO with Veracode, perform the following steps:

1. **Configure Microsoft Entra SSO**to enable your users to use this feature.
    - **Create a Microsoft Entra test user** to test Microsoft Entra single sign-on with B.Simon.
    - **Assign the Microsoft Entra test user** to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Veracode SSO**to configure the single sign-on settings on the application side.
    - **Create a Veracode test user** to have a counterpart of B.Simon in Veracode linked to the Microsoft Entra representation of the user.
3. **Test SSO** to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. In the Microsoft Entra ID navigate to the **Veracode** application page under **Enterprise Applications**, scroll down to the **Manage** section, and select **single sign-on**.
2. Again under the **Manage** tab, select **Single sign-on**, then select **SAML**.
3. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic SAML Configuration.](common/edit-urls.png)
4. The Relay state field should be autopopulated with `https://web.analysiscenter.veracode.com/login/#/saml`. The rest of these fields will populate after setting up SAML within the Veracode Platform.
5. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)**. Select **Download** to download the certificate and save it on your computer.

    ![Screenshot of SAML Signing Certificate section, with Download link highlighted.](common/certificatebase64.png)
6. Veracode expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot of User Attributes &amp; Claims section.](common/default-attributes.png)
7. Veracode also expects a few more attributes to be passed back in the SAML response. These attributes are also pre-populated, but you can review them per your requirements.

    | Name | Source attribute |
    | --- | --- |
    | firstname | User.givenname |
    | lastname | User.surname |
    | email | User.mail |
8. On the **Set up Veracode** section, copy and save the provided URLs to use later in your Veracode Platform SAML setup.

    ![Screenshot of Set up Veracode section, with configuration URLs highlighted.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Veracode SSO

Notes:

- These instructions assume you're using the new [Single Sign On/Just-in-Time Provisioning feature from Veracode](https://docs.veracode.com/r/about_saml). To activate this feature if it isn't already active, please contact Veracode Support.
- These instructions are valid for all [Veracode regions](https://docs.veracode.com/r/Region_Domains_for_Veracode_APIs).

1. In a different web browser window, sign in to your Veracode company site as an administrator.
2. From the menu on the top, select **Settings** &gt; **Admin**.

    ![Screenshot of Veracode Administration, with Settings icon and Admin highlighted.](media/veracode-tutorial/admin.png)
3. Select the **SAML Certificate** tab.
4. In the **SAML Certificate** section, perform the following steps:

    ![Screenshot of Organization SAML Settings section.](media/veracode-tutorial/saml.png)

    a. For **Issuer**, paste the value of the **Microsoft Entra Identifier** that you've copied.

    b. For **Assertion Signing Certificate**, select **Choose File** to upload your downloaded certificate.

    c. Note the values of the three URLs (**SAML Assertion URL**, **SAML Audience URL**, **Relay state URL**).

    d. Select **Save**.
5. Take the values of the **SAML Assertion URL**, **SAML Audience URL** and **Relay state URL** and update them in the Microsoft Entra settings for the Veracode integration (follow the table below for proper conversions) NOTE: **Relay State** is NOT optional.

    | Veracode URL | Microsoft Entra ID Field |
    | --- | --- |
    | SAML Audience URL | Identifier (Entity ID) |
    | SAML Assertion URL | Reply URL (Assertion Consumer Service URL) |
    | Relay State URL | Relay State |
6. Select the **JIT Provisioning** tab.

    ![Screenshot of JIT Provisioning tab, with various options highlighted.](media/veracode-tutorial/just-in-time.png)
7. In the **Organization Settings** section, toggle the **Configure Default Settings for Just-in-Time user provisioning** setting to **On**.
8. In the **Basic Settings** section, for **User Data Updates**, select **Prefer Veracode User Data**. This will cause conflicts between data passed in the SAML assertion from Microsoft Entra ID and user data in the Veracode platform to be resolved using the Veracode user data.
9. In the **Access Settings** section, under **User Roles**, select from the following For more information about Veracode user roles, see the [Veracode Documentation](https://docs.veracode.com/r/c_role_permissions):

    ![Screenshot of JIT Provisioning User Roles, with various options highlighted.](media/veracode-tutorial/user-roles.png)

    - **Policy Administrator**
    - **Reviewer**
    - **Security Lead**
    - **Executive**
    - **Submitter**
    - **Creator**
    - **All Scan Types**

### Create Veracode test user

In this section, a user called B.Simon is created in Veracode. Veracode supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Veracode, a new one is created after authentication.

Note

You can use any other Veracode user account creation tools or APIs provided by Veracode to provision Microsoft Entra user accounts.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the Veracode for which you set up the SSO.
- You can use Microsoft My Apps. When you select the Veracode tile in the My Apps, you should be automatically signed in to the Veracode for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
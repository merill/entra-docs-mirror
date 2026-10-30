---
layout: Conceptual
title: Configure EverBridge for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/everbridge-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and EverBridge.
ms.topic: how-to
ms.date: 2026-04-17T00:00:00.0000000Z
locale: en-us
document_id: 6e2d66e3-fdd2-3567-b759-54c8a2d2ed5a
document_version_independent_id: a2321350-e67f-e1b2-a2a1-fb55f5c3dd51
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/everbridge-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/everbridge-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/everbridge-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 8ac07a8e-8bf1-ee55-f828-d50d5e056caa
---

# Configure EverBridge for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate EverBridge with Microsoft Entra ID. When you integrate EverBridge with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to EverBridge.
- Allow your users to be automatically signed in to EverBridge with their Microsoft Entra accounts. This access control is called single sign-on (SSO).
- Manage your accounts in one central location by using the Azure portal.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- An EverBridge subscription that uses single sign-on.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- EverBridge supports IDP-initiated SSO.
- EverBridge supports SP-initiated SSO.

## Add EverBridge from the Gallery

To configure the integration of EverBridge into Microsoft Entra ID, you need to add EverBridge from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **EverBridge** in the search box.
4. Select **EverBridge** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for EverBridge

Configure and test Microsoft Entra SSO with EverBridge using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in EverBridge.

To configure and test Microsoft Entra SSO with EverBridge, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure EverBridge SSO**- to configure the single sign-on settings on application side.
    1. **Create EverBridge test user** - to have a counterpart of B.Simon in EverBridge that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

### Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **EverBridge** application integration page, find the **Manage** section and select **Single sign-on**.
3. On the **Select a Single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)

    Note

    Configure the application either as the manager portal *or* as the member portal on both the Azure portal and the EverBridge portal. The URLs above illustrate a general pattern, not actual data. You need to update strings in &lt;&gt; with the actual Identifier. To get those values, check your SSO configuration in EverBridge Manager Portal.

    a. In the **Identifier** box, enter a URL that follows the pattern. `https://sso.everbridge.net/<API_Name>`

    b. In the **Reply URL** box, enter a URL that follows the pattern.

    - If you are configuring an account level SSO, use `https://manager.everbridge.net/saml/SSO/<API_Name>/alias/defaultAlias`
    - If you are configuring an organization level SSO, use `https://manager.everbridge.net/saml/SSO/<API_Name>/<Organization_ID>/alias/defaultAlias`

    Note

    The URLs above illustrate a general pattern, not actual data. You need to update strings in &lt;&gt; with the actual Identifier. To get those values, check your SSO configuration in Everbridge Manager Portal.
5. To configure the **EverBridge** application as the **EverBridge member portal**, in the **Basic SAML Configuration** section, follow these steps:

    - If you want to configure the application in IDP-initiated mode, follow these steps:

        a. In the **Identifier** box, enter a URL that follows the pattern `https://sso.everbridge.net/<API_Name>/<Organization_ID>`

        b. In the **Reply URL** box, enter a URL that follows the pattern `https://member.everbridge.net/saml/SSO/<API_Name>/<Organization_ID>/alias/defaultAlias`
    - If you want to configure the application in SP-initiated mode, select **Set additional URLs** and follow this step:

        a. In the **Sign on URL** box, enter a URL that follows the pattern `https://manager.everbridge.net/saml/login/<API_Name>`

        Note

        The URLs above illustrate a general pattern, not actual data. You need to update strings in &lt;&gt; with the actual value. To get those values, check your SSO configuration in Everbridge Manager Portal.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML**. Save it on your computer.

    ![Certificate download link](common/metadataxml.png)
7. In the **Set up EverBridge** section, copy the URLs you need for your requirements:

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure EverBridge SSO

To configure SSO on **EverBridge** as an **EverBridge manager portal** application, follow these steps.

1. In a different web browser window, sign in to EverBridge Manager Portal as an account or org administrator.
2. From the menu on the left, select the **Settings** menu. Under **Security**, select **Single Sign-On for Manager Portal**.

    ![Screenshot showing how to configure single sign-on.](media/everbridge-tutorial/sso-settings.png)

    a. In the **Name** box, enter the name of this setting. An example is your company name.

    b. In the **API Name** box, enter the name of the API. This is the unique identifier for your SSO configuration.

    c. Select the **Identity Provider** from the dropdown list. If not found, choose "Other" and provide the name.

    d. Choose the **Service Provider Certificate** you would like to use. The certificate of 3072 bit length is recommended.

    e. Select **Upload** to upload the metadata file that you downloaded from your IDP.

    f. For **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.

    g. In the **Identity Provider Login URL** box, paste the **Login URL** value that you copied.

    h. For **Service Provider initiated Request Binding**, select **HTTP Redirect**.

    i. Click **Save**.

### Create EverBridge test user

Create a test user in EverBridge. Ensure the **SSO User ID** field of the user matches the user's identifier in your IDP.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the EverBridge for which you set up the SSO.
- You can use Microsoft My Apps. When you select the EverBridge tile in the My Apps, you should be automatically signed in to the EverBridge for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
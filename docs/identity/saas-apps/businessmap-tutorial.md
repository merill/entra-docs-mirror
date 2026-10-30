---
layout: Conceptual
title: Configure Businessmap for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/businessmap-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Businessmap.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 20abc6ca-7add-befa-6553-dc199c8cf763
document_version_independent_id: 20abc6ca-7add-befa-6553-dc199c8cf763
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/businessmap-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/businessmap-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/businessmap-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f3ddfe9d-9937-dd21-a5d8-f0e1d901d2e2
---

# Configure Businessmap for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Businessmap with Microsoft Entra ID. When you integrate Businessmap with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Businessmap.
- Enable your users to be automatically signed-in to Businessmap with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Businessmap single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Businessmap supports **SP and IDP** initiated SSO.
- Businessmap supports **Just In Time** user provisioning.

## Add Businessmap from the gallery

To configure the integration of Businessmap into Microsoft Entra ID, you need to add Businessmap from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Businessmap** in the search box.
4. Select **Businessmap** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Businessmap

Configure and test Microsoft Entra SSO with Businessmap using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Businessmap.

To configure and test Microsoft Entra SSO with Businessmap, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Businessmap SSO**- to configure the single sign-on settings on application side.
    1. **Create Businessmap test user** - to have a counterpart of B.Simon in Businessmap that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Businessmap** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://<subdomain>.kanbanize.com/`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<subdomain>.kanbanize.com/saml/acs`

    c. Select **Set additional URLs**.

    d. In the **Relay State** textbox, type the value: `/ctrl_login/saml_login`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<subdomain>.kanbanize.com`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL, and Sign-on URL. Contact [Businessmap Client support team](mailto:support@businessmap.io) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. Businessmap application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes, whereas nameidentifier is mapped with **user.userprincipalname**. Businessmap application expects nameidentifier to be mapped with **user.mail**, so you need to edit the attribute mapping by selecting Edit icon and change the attribute mapping.

    ![image](common/edit-attribute.png)
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
9. On the **Set up Businessmap** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Businessmap SSO

1. In a different web browser window, sign in to your Businessmap company site as an administrator
2. Go to top right of the page, select **Settings** logo.

    ![Screenshot shows the Businessmap settings.](media/businessmap-tutorial/tutorial-businessmap-set.png)
3. On the Administration panel page, from the left side of menu select **Integrations** and then enable **Single Sign-On**.

    ![Screenshot shows the Administration panel with Integration selected.](media/businessmap-tutorial/tutorial-businessmap-admin.png)
4. Under Integrations section, select **CONFIGURE** to open **Single Sign-On Integration** page.

    ![Screenshot shows the Businessmap Integration.](media/businessmap-tutorial/configuration.png)
5. On the **Single Sign-On Integration** page under **Configurations**, perform the following steps:

    ![Screenshot shows the Single Sign-On Integration page where you enter the values in this step.](media/businessmap-tutorial/values.png)

    a. In the **Idp Entity ID** textbox, paste the value of **Microsoft Entra Identifier**, which you copied previously.

    b. In the **Idp Login Endpoint** textbox, paste the value of **Login URL**, which you copied previously.

    c. In the **Idp Logout Endpoint** textbox, paste the value of **Logout URL**, which you copied previously.

    d. In **Attribute name for Email** textbox, enter this value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`

    e. In **Attribute name for First Name** textbox, enter this value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`

    f. In **Attribute name for Last Name** textbox, enter this value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`

    Note

    You can get these values by combining namespace and name values of the respective attribute from the User attributes section in Azure portal.

    g. In Notepad, open the base-64 encoded certificate that you downloaded, copy its content (without the start and end markers), and then paste it into the **Idp X.509 Certificate** box.

    h. Check **Enable login with both SSO and Businessmap**.

    i. Select **Save Settings**.

### Create Businessmap test user

In this section, a user called B.Simon is created in Businessmap. Businessmap supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Businessmap, a new one is created after authentication. If you need to create a user manually, contact [Businessmap Client support team](mailto:support@businessmap.io).

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Businessmap Sign on URL where you can initiate the login flow.
- Go to Businessmap Sign-on URL directly and initiate the sign-in flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Businessmap for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Businessmap tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the sign-in flow and if configured in IDP mode, you should be automatically signed in to the Businessmap for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
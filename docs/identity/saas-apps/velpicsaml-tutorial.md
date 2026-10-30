---
layout: Conceptual
title: Configure Velpic SAML for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/velpicsaml-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Velpic SAML.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 2b91212b-0421-cd5d-d115-33369652fc9f
document_version_independent_id: 9147cdbd-f0da-1fc1-f908-692a5d3803dc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/velpicsaml-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/velpicsaml-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/velpicsaml-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 123ab157-5ffc-fa88-48b5-8d6550e65083
---

# Configure Velpic SAML for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Velpic SAML with Microsoft Entra ID. When you integrate Velpic SAML with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Velpic SAML.
- Enable your users to be automatically signed-in to Velpic SAML with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Velpic SAML single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Velpic SAML supports **SP** initiated SSO.
- Velpic SAML supports [Automated user provisioning](velpic-provisioning-tutorial).

## Adding Velpic SAML from the gallery

To configure the integration of Velpic SAML into Microsoft Entra ID, you need to add Velpic SAML from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Velpic SAML** in the search box.
4. Select **Velpic SAML** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Velpic SAML

Configure and test Microsoft Entra SSO with Velpic SAML using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Velpic SAML.

To configure and test Microsoft Entra SSO with Velpic SAML, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Velpic SAML SSO**- to configure the single sign-on settings on application side.
    1. **Create Velpic SAML test user** - to have a counterpart of B.Simon in Velpic SAML that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Velpic SAML** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Sign on URL** text box, type a URL using the following pattern: `https://<sub-domain>.velpicsaml.net`

    b. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://auth.velpic.com/saml/v2/<entity-id>/login`

    Note

    Please note that the Sign on URL is provided by the Velpic SAML team and Identifier value is available when you configure the SSO Plugin on Velpic SAML side. You need to copy that value from Velpic SAML application page and paste it here.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up Velpic SAML** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Velpic SAML SSO

1. In a different web browser window, sign in to your Velpic SAML company site as an administrator
2. Select **Manage** tab and go to **Integration** section where you need to select **Plugins** button to create new plugin for Sign-In.

    ![Screenshot shows the Integration page where you can select Plugins.](media/velpicsaml-tutorial/plugin.png)
3. Select the **Add plugin** button.

    ![Screenshot shows the Add Plugin button selected.](media/velpicsaml-tutorial/add-button.png)
4. Select the **SAML** tile in the Add Plugin page.

    ![Screenshot shows SAML selected in the Add Plugin page.](media/velpicsaml-tutorial/integration.png)
5. Enter the name of the new SAML plugin and select the **Add** button.

    ![Screenshot shows the Add new SAML plugin dialog box with Microsoft Entra ID entered.](media/velpicsaml-tutorial/new-plugin.png)
6. Enter the details as follows:

    ![Screenshot shows the Microsoft Entra ID page where you can enter the values described.](media/velpicsaml-tutorial/details.png)

    a. In the **Name** textbox, type the name of SAML plugin.

    b. In the **Issuer URL** textbox, paste the **Microsoft Entra Identifier** you copied from the **Configure sign-on** window.

    c. In the **Provider Metadata Config** upload the Metadata XML file which you downloaded previously.

    d. You can also choose to enable SAML just in time provisioning by enabling the **Auto create new users** checkbox. If a user doesn’t exist in Velpic and this flag isn't enabled, the login from Azure will fail. If the flag is enabled the user will automatically be provisioned into Velpic at the time of login.

    e. Copy the **Single sign on URL** from the text box and paste it.

    f. Select **Save**.

### Create Velpic SAML test user

This step is usually not required as the application supports just in time user provisioning. If the automatic user provisioning isn't enabled then manual user creation can be done as described below.

Sign into your Velpic SAML company site as an administrator and perform following steps:

1. Select Manage tab and go to Users section, then select New button to add users.

    ![Add user](media/velpicsaml-tutorial/new-user.png)
2. On the **“Create New User”** dialog page, perform the following steps.

    ![User](media/velpicsaml-tutorial/create-user.png)

    a. In the **First Name** textbox, type the first name of B.

    b. In the **Last Name** textbox, type the last name of Simon.

    c. In the **User Name** textbox, type the user name of B.Simon.

    d. In the **Email** textbox, type the email address of B.Simon@contoso.com account.

    e. Rest of the information is optional, you can fill it if needed.

    f. Select **SAVE**.

Note

Velpic SAML also supports automatic user provisioning, you can find more details [here](velpic-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration using the My Apps.

1. When you select the Velpic SAML tile in the My Apps, you should get login page of Velpic SAML application. You should see the **Log In With Microsoft Entra ID** button on the sign in page.

    ![Screenshot shows the Learning Portal with Log In With Microsoft Entra ID selected.](media/velpicsaml-tutorial/login.png)
2. Select the **Log In With Microsoft Entra ID** button to log in to Velpic using your Microsoft Entra account.
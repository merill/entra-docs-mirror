---
layout: Conceptual
title: Configure Banyan Security Zero Trust Remote Access Platform for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/banyan-command-center-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Banyan Security Zero Trust Remote Access Platform.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: a8249031-8232-e668-dfbb-0f9265cafbc5
document_version_independent_id: 069d09f8-5921-0abd-2afa-2ea6ea9eaab8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/banyan-command-center-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/banyan-command-center-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/banyan-command-center-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 4b4fe024-ee17-42a5-7e02-4d0ed1052fdc
---

# Configure Banyan Security Zero Trust Remote Access Platform for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Banyan Security Zero Trust Remote Access Platform with Microsoft Entra ID. When you integrate Banyan Security Zero Trust Remote Access Platform with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Banyan Security Zero Trust Remote Access Platform.
- Enable your users to be automatically signed-in to Banyan Security Zero Trust Remote Access Platform with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Banyan Security Zero Trust Remote Access Platform single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Banyan Security Zero Trust Remote Access Platform supports **SP and IDP** initiated SSO.
- Banyan Security Zero Trust Remote Access Platform supports **Just In Time** user provisioning.

## Add Banyan Security Zero Trust Remote Access Platform from the gallery

To configure the integration of Banyan Security Zero Trust Remote Access Platform into Microsoft Entra ID, you need to add Banyan Security Zero Trust Remote Access Platform from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Banyan Security Zero Trust Remote Access Platform** in the search box.
4. Select **Banyan Security Zero Trust Remote Access Platform** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Banyan Security Zero Trust Remote Access Platform

Configure and test Microsoft Entra SSO with Banyan Security Zero Trust Remote Access Platform using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Banyan Security Zero Trust Remote Access Platform.

To configure and test Microsoft Entra SSO with Banyan Security Zero Trust Remote Access Platform, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Banyan Security Zero Trust Remote Access Platform SSO**- to configure the single sign-on settings on application side.
    1. **Create Banyan Security Zero Trust Remote Access Platform test user** - to have a counterpart of B.Simon in Banyan Security Zero Trust Remote Access Platform that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Banyan Security Zero Trust Remote Access Platform** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://net.banyanops.com/api/v1/sso?orgname=<YOUR_ORG_NAME>`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://net.banyanops.com/api/v1/sso?orgname=<YOUR_ORG_NAME>`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://net.banyanops.com/api/v1/sso?orgname=<YOUR_ORG_NAME>`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [Banyan Security Zero Trust Remote Access Platform Client support team](mailto:support@banyansecurity.io) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![The Certificate download link](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Banyan Security Zero Trust Remote Access Platform SSO

1. Log in to your Banyan Security Zero Trust Remote Access Platform website as an administrator.
2. Go to **Admin Settings -&gt; Admin Sign-on**.
3. Perform the following steps in the **Sign-on Settings** page.

    ![Screenshot for Sign-on Settings.](media/banyan-command-center-tutorial/configuration.png)

    a. Select **Sign-On Method** as a **Single Sign On - SAML 2.0** from the dropdown.

    b. Copy **IDP Issuer** value, paste this value into the **Microsoft Entra Identifier** text box in the Basic SAML Configuration section.

    c. Paste the **App Federation Metadata Url** value in to the **IDP Metadata URL** textbox.

    d. Select the **Update** button.

### Create Banyan Security Zero Trust Remote Access Platform test user

In this section, a user called Britta Simon is created in Banyan Security Zero Trust Remote Access Platform. Banyan Security Zero Trust Remote Access Platform supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Banyan Security Zero Trust Remote Access Platform, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Banyan Security Zero Trust Remote Access Platform Sign on URL where you can initiate the login flow.
- Go to Banyan Security Zero Trust Remote Access Platform Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Banyan Security Zero Trust Remote Access Platform for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Banyan Security Zero Trust Remote Access Platform tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Banyan Security Zero Trust Remote Access Platform for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
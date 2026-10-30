---
layout: Conceptual
title: Configure Kendis for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/kendis-scaling-agile-platform-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Kendis - Microsoft Entra Integration.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: b4de27b6-0bbd-c9d3-f088-dd295e98d0ee
document_version_independent_id: 339147ec-cc78-3b00-3123-80cb4ef8389a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/kendis-scaling-agile-platform-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/kendis-scaling-agile-platform-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/kendis-scaling-agile-platform-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 81a59a82-35f1-d8f5-acae-1fc67bbdf04a
---

# Configure Kendis for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Kendis - Microsoft Entra Integration with Microsoft Entra ID. When you integrate Kendis - Microsoft Entra Integration with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Kendis - Microsoft Entra Integration.
- Enable your users to be automatically signed-in to Kendis - Microsoft Entra Integration with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Kendis - Microsoft Entra Integration single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Kendis - Microsoft Entra Integration supports **SP and IDP** initiated SSO
- Kendis - Microsoft Entra Integration supports **Just In Time** user provisioning

## Adding Kendis - Microsoft Entra Integration from the gallery

To configure the integration of Kendis - Microsoft Entra Integration into Microsoft Entra ID, you need to add Kendis - Microsoft Entra Integration from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Kendis - Microsoft Entra Integration** in the search box.
4. Select **Kendis - Microsoft Entra Integration** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Kendis - Microsoft Entra Integration

Configure and test Microsoft Entra SSO with Kendis - Microsoft Entra Integration using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Kendis - Microsoft Entra Integration.

To configure and test Microsoft Entra SSO with Kendis - Microsoft Entra Integration, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Kendis-Azure AD Integration SSO**- to configure the single sign-on settings on application side.
    1. **Create Kendis-Azure AD Integration test user** - to have a counterpart of B.Simon in Kendis - Microsoft Entra Integration that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Kendis - Microsoft Entra Integration** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, enter the values for the following fields:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.kendis.io`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.kendis.io/login/saml`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.kendis.io/login`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [Kendis - Microsoft Entra Integration Client support team](mailto:support@kendis.io) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
8. On the **Set up Kendis - Microsoft Entra Integration** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Kendis-Azure AD Integration SSO

1. In a different web browser window, sign in to your Kendis - Microsoft Entra Integration company site as an administrator
2. Go to the **Settings &gt; SAML Configurations**.

    ![settings to SAML Configurations](media/kendis-scaling-agile-platform-tutorial/settings.png)
3. Select **Edit** button at the bottom of the page and perform the following steps.

    ![SAML Configurations](media/kendis-scaling-agile-platform-tutorial/saml-configuration-settings.png)

    a. Copy **Callback URL** value, paste this value into the **Reply URL** text box in the Basic SAML Configuration section.

    b. In the **Identity Provider Single Sign On URL** textbox, paste the **Login URL** value which you copied previously.

    c. In the **Identity Provider Issuer** textbox, paste the **Microsoft Entra Identifier(Entity ID)** value which you copied previously.

    d. Open the downloaded **Certificate (Base64)** into Notepad and paste the content into the **X.509 Certificate** textbox.

    e. **Select Default Group** from the list of options.

    f. Select **Save**.

### Create Kendis-Azure AD Integration test user

In this section, a user called Britta Simon is created in Kendis - Microsoft Entra Integration. Kendis - Microsoft Entra Integration supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Kendis - Microsoft Entra Integration, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Kendis - Microsoft Entra Integration Sign on URL where you can initiate the login flow.
- Go to Kendis - Microsoft Entra Integration Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Kendis - Microsoft Entra Integration for which you set up the SSO

You can also use Microsoft My Apps to test the application in any mode. When you select the Kendis - Microsoft Entra Integration tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Kendis - Microsoft Entra Integration for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
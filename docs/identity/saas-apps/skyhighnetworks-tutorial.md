---
layout: Conceptual
title: Configure MVISION Cloud Microsoft Entra SSO Configuration for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/skyhighnetworks-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and MVISION Cloud Microsoft Entra SSO Configuration.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 9ec9f889-8da0-c318-866f-7a0c29914806
document_version_independent_id: a2f6aba3-ffba-2ca1-90d6-83a6409ae241
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/skyhighnetworks-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/skyhighnetworks-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/skyhighnetworks-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 4b414b85-b309-62c5-4095-49bf20b34fc8
---

# Configure MVISION Cloud Microsoft Entra SSO Configuration for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate MVISION Cloud Microsoft Entra SSO Configuration with Microsoft Entra ID. When you integrate MVISION Cloud Microsoft Entra SSO Configuration with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to MVISION Cloud Microsoft Entra SSO Configuration.
- Enable your users to be automatically signed-in to MVISION Cloud Microsoft Entra SSO Configuration with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- MVISION Cloud Microsoft Entra SSO Configuration single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- MVISION Cloud Microsoft Entra SSO Configuration supports **SP and IDP** initiated SSO.

## Add MVISION Cloud Microsoft Entra SSO Configuration from the gallery

To configure the integration of MVISION Cloud Microsoft Entra SSO Configuration into Microsoft Entra ID, you need to add MVISION Cloud Microsoft Entra SSO Configuration from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **MVISION Cloud Microsoft Entra SSO Configuration** in the search box.
4. Select **MVISION Cloud Microsoft Entra SSO Configuration** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for MVISION Cloud Microsoft Entra SSO Configuration

Configure and test Microsoft Entra SSO with MVISION Cloud Microsoft Entra SSO Configuration using a test user called **Britta Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in MVISION Cloud Microsoft Entra SSO Configuration.

To configure and test Microsoft Entra SSO with MVISION Cloud Microsoft Entra SSO Configuration, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with Britta Simon.
    2. **Assign the Microsoft Entra test user** - to enable Britta Simon to use Microsoft Entra single sign-on.
2. **Configure MVISION Cloud Microsoft Entra SSO Configuration SSO**- to configure the Single Sign-On settings on application side.
    1. **Create MVISION Cloud Microsoft Entra SSO Configuration test user** - to have a counterpart of Britta Simon in MVISION Cloud Microsoft Entra SSO Configuration that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

### Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Datadog** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, If you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://<ENV>.myshn.net/shndash/saml/Azure_SSO`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<ENV>.myshn.net/shndash/response/saml-postlogin`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<ENV>.myshn.net/shndash/saml/Azure_SSO`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [MVISION Cloud Microsoft Entra SSO Configuration Client support team](mailto:support@skyhighnetworks.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
8. On the **Set up MVISION Cloud Microsoft Entra SSO Configuration** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure MVISION Cloud Microsoft Entra SSO Configuration SSO

To configure single sign-on on **MVISION Cloud Microsoft Entra SSO Configuration** side, you need to send the downloaded **Certificate (Base64)** and appropriate copied URLs from the application configuration to [MVISION Cloud Microsoft Entra SSO Configuration support team](mailto:support@skyhighnetworks.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create MVISION Cloud Microsoft Entra SSO Configuration test user

In this section, you create a user called B.Simon in MVISION Cloud Microsoft Entra SSO Configuration. Work with [MVISION Cloud Microsoft Entra SSO Configuration support team](mailto:support@skyhighnetworks.com) to add the users in the MVISION Cloud Microsoft Entra SSO Configuration platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to MVISION Cloud Microsoft Entra SSO Configuration Sign on URL where you can initiate the login flow.
- Go to MVISION Cloud Microsoft Entra SSO Configuration Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the MVISION Cloud Microsoft Entra SSO Configuration for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the MVISION Cloud Microsoft Entra SSO Configuration tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the MVISION Cloud Microsoft Entra SSO Configuration for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
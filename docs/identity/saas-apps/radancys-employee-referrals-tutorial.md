---
layout: Conceptual
title: Configure Radancy's Employee Referrals for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/radancys-employee-referrals-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Radancy's Employee Referrals.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 2d6f75a4-791d-f0a5-32ae-c105d36b0843
document_version_independent_id: 85ac6c47-f0de-ce27-d9ea-5347a498e0bb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/radancys-employee-referrals-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/radancys-employee-referrals-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/radancys-employee-referrals-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 47a5735f-84f8-3ff4-84d6-924716df22d7
---

# Configure Radancy's Employee Referrals for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Radancy's Employee Referrals with Microsoft Entra ID. When you integrate Radancy's Employee Referrals with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Radancy's Employee Referrals.
- Enable your users to be automatically signed-in to Radancy's Employee Referrals with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Radancy's Employee Referrals single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Radancy's Employee Referrals supports **SP and IDP** initiated SSO.
- Radancy's Employee Referrals supports **Just In Time** user provisioning.

## Add Radancy's Employee Referrals from the gallery

To configure the integration of Radancy's Employee Referrals into Microsoft Entra ID, you need to add Radancy's Employee Referrals from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Radancy's Employee Referrals** in the search box.
4. Select **Radancy's Employee Referrals** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Radancy's Employee Referrals

Configure and test Microsoft Entra SSO with Radancy's Employee Referrals using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Radancy's Employee Referrals.

To configure and test Microsoft Entra SSO with Radancy's Employee Referrals, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Radancy's Employee Referrals SSO**- to configure the single sign-on settings on application side.
    1. **Create Radancy's Employee Referrals test user** - to have a counterpart of B.Simon in Radancy's Employee Referrals that are linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Radancy's Employee Referrals** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://<company-domain>.auth.1brd.com/saml/sp`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<company-domain>.auth.1brd.com/saml/callback`
6. Perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<company-domain>.1brd.com/login`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [Radancy's Employee Referrals Client support team](mailto:support@firstbird.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. Radancy's Employee Referrals application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows the image of token attributes configuration.](common/edit-attribute.png)
8. In addition to above, Radancy's Employee Referrals application expects few more attributes to be passed back in SAML response, which are shown below. These attributes are also pre populated but you can review them as per your requirement.

    | Name | Source Attribute |
    | --- | --- |
    | first\_name | user.givenname |
    | last\_name | user.surname |
    | email | user.mail |
9. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)
10. On the **Set up Radancy's Employee Referrals** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows how to copy configuration URL.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Radancy's Employee Referrals SSO

1. Log in to the Radancy's Employee Referrals website as an administrator.
2. Navigate to **Account Preferences** &gt; **Authentication** &gt; **Single Sign-On**.
3. In the **SAML IdP Metadata Configuration** section, perform the following steps:

    ![Screenshot shows how to upload the Federation Metadata.](media/radancys-employee-referrals-tutorial/certificate.png)

    1. In the **Entity ID** textbox, paste the **Microsoft Entra Identifier** value, which you've copied.
    2. In the **SSO-service URL** textbox, paste the **Login URL** value, which you've copied.
    3. In the **Signing certificate** textbox, paste the **Federation Metadata XML** file, which you've downloaded.
    4. **Save configuration** and verify the setup.

    Note

    You need to have the SSO option included in your contract.

### Create Radancy's Employee Referrals test user

In this section, a user called B.Simon is created in Radancy's Employee Referrals. Radancy's Employee Referrals supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Radancy's Employee Referrals, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Radancy's Employee Referrals Sign-on URL where you can initiate the login flow.
- Go to Radancy's Employee Referrals Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Radancy's Employee Referrals for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Radancy's Employee Referrals tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Radancy's Employee Referrals for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
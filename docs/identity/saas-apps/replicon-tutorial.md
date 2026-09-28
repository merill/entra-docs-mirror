---
layout: Conceptual
title: Configure Replicon for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/replicon-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Replicon.
ms.topic: how-to
ms.date: 2026-06-09T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 6bca8633-4880-720c-b11c-ce92dcd70b83
document_version_independent_id: 7dff3e70-8027-9400-513f-8e6ef6e68aae
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/replicon-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/replicon-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/replicon-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f6d483f2-8a2d-124b-e0d8-ab88522aa4e5
---

# Configure Replicon for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Replicon with Microsoft Entra ID. When you integrate Replicon with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Replicon.
- Enable your users to be automatically signed-in to Replicon with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Replicon is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Replicon single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Replicon supports **SP** initiated SSO.

## Add Replicon from the gallery

To configure the integration of Replicon into Microsoft Entra ID, you need to add Replicon from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Replicon** in the search box.
4. Select **Replicon** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Replicon

Configure and test Microsoft Entra SSO with Replicon using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Replicon.

To configure and test Microsoft Entra SSO with Replicon, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Replicon SSO**- to configure the single sign-on settings on application side.
    1. **Create Replicon test user** - to have a counterpart of B.Simon in Replicon that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Replicon** application integration page, find the **Manage** section and select **Single sign-on**.
3. On the **Select a Single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** page, perform the following steps:

    a. In the **Sign-on URL** text box, type a URL using the following pattern: `https://global.replicon.com/!/saml2/<client name>/sp-sso/post`

    b. In the **Identifier** box, type a URL using the following pattern: `https://global.replicon.com/!/saml2/<client name>`

    c. In the **Reply URL** text box, type a URL using the following pattern: `https://global.replicon.com/!/saml2/<client name>/sso/post`

    Note

    These values aren't real. Update these values with the actual Sign-On URL, Identifier and Reply URL. Contact [Replicon Client support team](https://www.replicon.com/customerzone/contact-support) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. Select the pencil icon for **SAML Signing Certificate** to edit the settings.

    ![Signing Algorithm](common/signing-algorithm.png)

    1. Select **Sign SAML assertion** as the **Signing Option**.
    2. Select **SHA-256** as the **Signing Algorithm**.
7. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Replicon SSO

1. In a different web browser window, sign into your Replicon company site as an administrator.
2. To configure SAML 2.0, perform the following steps:

    ![Enable SAML authentication](media/replicon-tutorial/authentication.png)

    a. To display the **EnableSAML Authentication2** dialog, append the following to your URL, after your company key: `/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2`

    1. The following shows the schema of the complete URL: `https://na2.replicon.com/<YourCompanyKey>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2`

    b. Select the **+** to expand the **v20Configuration** section.

    c. Select the **+** to expand the **metaDataConfiguration** section.

    d. Select **SHA256** for xmlSignatureAlgorithm

    e. Select **Choose File**, to select your identity provider metadata XML file, and select **Submit**.

### Create Replicon test user

The objective of this section is to create a user called B.Simon in Replicon.

**If you need to create user manually, perform following steps:**

1. In a web browser window, sign into your Replicon company site as an administrator.
2. Go to **Administration** &gt; **Users**.

    ![Users](media/replicon-tutorial/administration.png)
3. Select **+Add User**.

    ![Add User](media/replicon-tutorial/user.png)
4. In the **User Profile** section, perform the following steps:

    ![User profile](media/replicon-tutorial/profile.png)

    a. In the **Login Name** textbox, type the Microsoft Entra ID email address of the Microsoft Entra user you want to provision like `B.Simon@contoso.com`.

    Note

    Login Name needs to match the user's email address in Microsoft Entra ID

    b. As **Authentication Type**, select **SSO**.

    c. Set Authentication ID to the same value as Login Name (The Microsoft Entra ID email address of the user)

    d. In the **Department** textbox, type the user’s department.

    e. As **Employee Type**, select **Administrator**.

    f. Select **Save User Profile**.

Note

You can use any other Replicon user account creation tools or APIs provided by Replicon to provision Microsoft Entra user accounts.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Replicon Sign-on URL where you can initiate the login flow.
- Go to Replicon Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Replicon tile in the My Apps, this option redirects to Replicon Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
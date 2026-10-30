---
layout: Conceptual
title: Configure ScreenSteps for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/screensteps-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and ScreenSteps.
ms.topic: how-to
ms.date: 2024-05-08T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 3cea69f7-bd30-05b5-bcea-3ee38cb84e17
document_version_independent_id: ae8f1a95-2700-600c-a3af-ab2b6c863268
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/screensteps-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/screensteps-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/screensteps-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 12bb9909-7713-88f7-f965-ffd1bf26583c
---

# Configure ScreenSteps for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate ScreenSteps with Microsoft Entra ID. When you integrate ScreenSteps with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to ScreenSteps.
- Enable your users to be automatically signed-in to ScreenSteps with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- ScreenSteps single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- ScreenSteps supports **SP** initiated SSO.
- ScreenSteps supports [Automated user provisioning](screensteps-provisioning-tutorial).

## Add ScreenSteps from the gallery

To configure the integration of ScreenSteps into Microsoft Entra ID, you need to add ScreenSteps from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **ScreenSteps** in the search box.
4. Select **ScreenSteps** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for ScreenSteps

Configure and test Microsoft Entra SSO with ScreenSteps using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in ScreenSteps.

To configure and test Microsoft Entra SSO with ScreenSteps, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure ScreenSteps SSO**- to configure the single sign-on settings on application side.
    1. **Create ScreenSteps test user** - to have a counterpart of B.Simon in ScreenSteps that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **ScreenSteps** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<tenantname>.ScreenSteps.com`

    Note

    This value isn't real. Update this value with the actual Sign-On URL, which is explained later in this article.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
7. On the **Set up ScreenSteps** section, copy one or more appropriate URLs as per your requirement.

    ![Screenshot shows to copy configuration URLs.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure ScreenSteps SSO

1. Sign in to ScreenSteps company site as an administrator.
2. Go to **Account Settings** &gt; **Site Access**.

    ![Screenshot that shows the path.](media/screensteps-tutorial/path.png)
3. Select the pencil icon in the **Content Management and Admin Centers** and select **SAML** as identity provider from the drop-down.

    ![Screenshot that shows Configuration.](media/screensteps-tutorial/configure.png)

    a. In the **Remote Login URL** field, paste the **Login URL** which you copied from the Microsoft Entra admin center.

    b. Leave the **Logout URL** field blank

    c. Copy **SAML Consumer URL** value, paste this value into the **Sign-on URL** text box in the **Basic SAML Configuration** section in Microsoft Entra admin center.

    d. Copy **Entity ID** value, paste this value into the **Identifier (Entity ID)** text box in the **Basic SAML Configuration** section in Microsoft Entra admin center.

    e. Select **Save**.

Note

To configure Single Sign-on in Screen steps, Please refer [How to Set up Single Sign-on](https://help.screensteps.com/a/1097728-how-to-set-up-single-sign-on). This article guides you through the steps of setting up ScreenSteps to work with Microsoft Entra ID. After answering a few questions in the help article, you be asked to "Select how you set up SSO". Select Microsoft Entra ID and continue on with Configure Microsoft Entra SSO.

### Create ScreenSteps test user

In this section, you create a user called Britta Simon in ScreenSteps. Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add the users in the ScreenSteps platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Switch to the **Testing and Activation** tab in ScreenSteps.
- Select the **Save & Copy** button to copy the **SAML Test URL** to the clipboard.
- Open an Incognito browser window and paste the URL in.
- Sign in with the `B.Simon@contoso.com` test user you created in the previous step. You should be granted access to ScreenSteps and `B.Simon@contoso.com` should appear in the list of Users in ScreenSteps.
- You can use Microsoft My Apps. When you select the ScreenSteps tile in the My Apps, this option redirects to ScreenSteps Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
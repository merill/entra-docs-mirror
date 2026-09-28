---
layout: Conceptual
title: Configure Litmus for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/litmus-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Litmus.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 23be394f-8d06-d578-9752-7296128fd9d3
document_version_independent_id: 7af2c13a-916b-ad61-04df-145b6351d5be
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/litmus-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/litmus-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/litmus-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c8968617-729f-e796-7106-12433bbe3ef2
---

# Configure Litmus for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Litmus with Microsoft Entra ID. When you integrate Litmus with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Litmus.
- Enable your users to be automatically signed-in to Litmus with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Litmus single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Litmus supports **SP and IDP** initiated SSO

## Adding Litmus from the gallery

To configure the integration of Litmus into Microsoft Entra ID, you need to add Litmus from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Litmus** in the search box.
4. Select **Litmus** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Litmus

Configure and test Microsoft Entra SSO with Litmus using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Litmus.

To configure and test Microsoft Entra SSO with Litmus, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Litmus SSO**- to configure the single sign-on settings on application side.
    1. **Create Litmus test user** - to have a counterpart of B.Simon in Litmus that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Litmus** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the edit/pen icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, the user doesn't have to perform any step as the app is already pre-integrated with Azure.
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type the URL: `https://litmus.com/sessions/new`
7. Select **Save**.
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Raw)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificateraw.png)
9. On the **Set up Litmus** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Litmus SSO

1. In a different web browser window, sign in to your Litmus company site as an administrator
2. Select the **Security** from the left navigation panel.

    ![Screenshot shows the Security item selected.](media/litmus-tutorial/security-img.png)
3. On the **Configure SAML Authentication** section, perform the following steps:

    ![Screenshot shows the Configure SAML Authentication section where you can enter the values described.](media/litmus-tutorial/configure1.png)

    a. Switch on the **Enable SAML** toggle.

    b. Select **Generic** for the provider.

    c. Enter the name of **Identity Provider Name**. for ex. `Azure AD`
4. Perform the following steps:

    ![Screenshot shows the section where you can enter the values described.](media/litmus-tutorial/configure3.png)

    a. In the **SAML 2.0 Endpoint(HTTP)** textbox, paste the **Login URL** value, which you copied previously.

    b. Open downloaded **Certificate** file from Azure portal into Notepad and paste the content into **X.509 Certificate** textbox.

    c. Select **Save SAML settings**.

### Create Litmus test user

1. In a different web browser window, sign into Litmus application as an administrator.
2. Select the **Accounts** from the left navigation panel.

    ![Screenshot shows the Accounts item selected.](media/litmus-tutorial/accounts-img.png)
3. Select **Add New User** tab.

    ![Screenshot shows the Add New User item selected.](media/litmus-tutorial/add-new-user.png)
4. On the **Add User** section, perform the following steps:

    ![Screenshot shows the Add User section where you can enter the values described.](media/litmus-tutorial/user-profile.png)

    a. In the **Email** textbox, enter the email address of the user like **B.Simon@contoso.com**

    b. In the **First Name** textbox, enter the first name of the user like **B**.

    c. In the **Last Name** textbox, enter the last name of the user like **Simon**.

    d. Select **Create User**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Litmus Sign on URL where you can initiate the login flow.
- Go to Litmus Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Litmus for which you set up the SSO

You can also use Microsoft My Apps to test the application in any mode. When you select the Litmus tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Litmus for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
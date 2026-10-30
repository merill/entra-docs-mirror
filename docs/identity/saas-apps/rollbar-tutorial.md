---
layout: Conceptual
title: Configure Rollbar for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/rollbar-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Rollbar.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 27ab5c3d-5f1c-3c51-9e5e-220c7ba2d080
document_version_independent_id: 5af73a56-e8b1-419b-88a1-3ae4b693fbac
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/rollbar-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/rollbar-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/rollbar-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 9b2f43e9-b321-3709-db6a-3959e217e9e0
---

# Configure Rollbar for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Rollbar with Microsoft Entra ID. When you integrate Rollbar with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Rollbar.
- Enable your users to be automatically signed-in to Rollbar with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Rollbar single sign-on enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Rollbar supports **SP and IDP** initiated SSO.
- Rollbar supports [Automated user provisioning](rollbar-provisioning-tutorial).

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Rollbar from the gallery

To configure the integration of Rollbar into Microsoft Entra ID, you need to add Rollbar from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Rollbar** in the search box.
4. Select **Rollbar** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Rollbar

Configure and test Microsoft Entra SSO with Rollbar using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Rollbar.

To configure and test Microsoft Entra SSO with Rollbar, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Rollbar SSO**- to configure the single sign-on settings on application side.
    1. **Create Rollbar test user** - to have a counterpart of B.Simon in Rollbar that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Rollbar** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, type the URL: `https://saml.rollbar.com`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://rollbar.com/<ACCOUNT_NAME>/saml/sso/azure/`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://rollbar.com/<ACCOUNT_NAME>/saml/login/azure/`

    Note

    These values aren't real. Update these values with the actual Reply URL and Sign-On URL. Contact [Rollbar Client support team](mailto:support@rollbar.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
8. On the **Set up Rollbar** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Rollbar SSO

1. In a different web browser window, sign in to your Rollbar company site as an administrator.
2. Select the **Profile Settings** on the right top corner and then select **Account Name settings**.

    ![Screenshot shows an account name settings selected from Profile Settings.](media/rollbar-tutorial/general.png)
3. Select **Identity Provider** under SECURITY.

    ![Screenshot shows Identity Provider selected under SECURITY.](media/rollbar-tutorial/security.png)
4. In the **SAML Identity Provider** section, perform the following steps:

    ![Screenshot shows the SAML Identity Provider where you can enter the values described.](media/rollbar-tutorial/configure.png)

    a. Select **AZURE** from the **SAML Identity Provider** dropdown.

    b. Open your metadata file in notepad, copy the content of it into your clipboard, and then paste it to the **SAML Metadata** textbox.

    c. Select **Save**.
5. After selecting the save button, the screen is like this:

    ![Screenshot shows the results in the SAML Identity Provider page.](media/rollbar-tutorial/identity-provider.png)

    Note

    In order to complete the following step, you must first add yourself as a user to the Rollbar app in Azure.

    a. If you want to require all users to authenticate via Azure, then select **log in via your identity provider** to re-authenticate via Azure.

    b. Once you're returned to the screen, select the **Require login via SAML Identity Provider** checkbox.

    b. Select **Save**.

### Create Rollbar test user

To enable Microsoft Entra users to sign in to Rollbar, they must be provisioned into Rollbar. In the case of Rollbar, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Sign in to your Rollbar company site as an administrator.
2. Select the **Profile Settings** on the right top corner and then select **Account Name settings**.

    ![User](media/rollbar-tutorial/general.png)
3. Select **Users**.

    ![Add Employee](media/rollbar-tutorial/user.png)
4. Select **Invite Team Members**.

    ![Screenshot shows the Invite Team Members option selected.](media/rollbar-tutorial/invite-user.png)
5. In the textbox, enter the name of user like **brittasimon@contoso.com** and the select **Add/Invite**.

    ![Screenshot shows Add/Invite Members with an address provided.](media/rollbar-tutorial/add-user.png)
6. User receives an invitation and after accepting it they are created in the system.

Note

Rollbar also supports automatic user provisioning, you can find more details [here](rollbar-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Rollbar Sign on URL where you can initiate the login flow.
- Go to Rollbar Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Rollbar for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Rollbar tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Rollbar for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
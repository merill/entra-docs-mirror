---
layout: Conceptual
title: Configure Bonusly for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/bonus-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Bonusly.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: faddde3f-f71a-4a97-3424-2ff26ad3ed21
document_version_independent_id: 7a73a29a-60bc-79cd-5173-5c92603bcb50
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/bonus-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/bonus-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/bonus-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: fbd45de2-ce26-a886-9421-85b8b2f3ba48
---

# Configure Bonusly for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Bonusly with Microsoft Entra ID. When you integrate Bonusly with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Bonusly.
- Enable your users to be automatically signed-in to Bonusly with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Bonusly single sign-on enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Bonusly supports **IDP** initiated SSO.
- Bonusly supports [Automated user provisioning](bonusly-provisioning-tutorial).

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Bonusly from the gallery

To configure the integration of Bonusly into Microsoft Entra ID, you need to add Bonusly from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Bonusly** in the search box.
4. Select **Bonusly** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Bonusly

Configure and test Microsoft Entra SSO with Bonusly using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Bonusly.

To configure and test Microsoft Entra SSO with Bonusly, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Bonusly SSO**- to configure the single sign-on settings on application side.
    1. **Create Bonusly test user** - to have a counterpart of B.Simon in Bonusly that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Bonusly** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following step:

    In the **Reply URL** text box, type a URL using the following pattern: `https://Bonus.ly/saml/<TENANT_NAME>`

    Note

    The value isn't real. Update the value with the actual Reply URL. Contact [Bonusly Client support team](https://bonus.ly/contact) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. In the **SAML Signing Certificate** section, select **Edit** button to open **SAML Signing Certificate** dialog.

    ![Edit SAML Signing Certificate](common/edit-certificate.png)
7. In the **SAML Signing Certificate** section, copy the **THUMBPRINT** and save it on your computer.

    ![Copy Thumbprint value](common/copy-thumbprint.png)
8. On the **Set up Bonusly** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Bonusly SSO

1. In a different browser window, sign in to your **Bonusly** tenant.
2. In the toolbar on the top, select **Settings** and then select **Integrations and apps**.

    ![Bonusly Social Section](media/bonus-tutorial/settings.png)
3. Under **Single Sign-On**, select **SAML**.
4. On the **SAML** dialog page, perform the following steps:

    ![Bonusly Saml Dialog page](media/bonus-tutorial/dialog-page.png)

    a. In the **IdP SSO target URL** textbox, paste the value of **Login URL**.

    b. In the **IdP Login URL** textbox, paste the value of **Login URL**.

    c. In the **IdP Issuer** textbox, paste the value of **Microsoft Entra Identifier**.

    d. Paste the **Thumbprint** value into the **Cert Fingerprint** textbox.

    e. Select **Save**.

### Create Bonusly test user

In order to enable Microsoft Entra users to sign in to Bonusly, they must be provisioned into Bonusly. In the case of Bonusly, provisioning is a manual task.

Note

You can use any other Bonusly user account creation tools or APIs provided by Bonusly to provision Microsoft Entra user accounts.

**To configure user provisioning, perform the following steps:**

1. In a web browser window, sign in to your Bonusly tenant.
2. Select **Settings**.

    ![Settings](media/bonus-tutorial/users.png)
3. Select the **Users and bonuses** tab.

    ![Users and bonuses](media/bonus-tutorial/manage-user.png)
4. Select **Manage Users**.

    ![Manage Users](media/bonus-tutorial/new-users.png)
5. Select **Add User**.

    ![Screenshot shows Manage Users where you can select Add User.](media/bonus-tutorial/add-tab.png)
6. On the **Add User** dialog, perform the following steps:

    ![Screenshot shows the Add User dialog box where you can enter this information.](media/bonus-tutorial/select-user.png)

    a. In the **First name** textbox, enter the first name of user like **Britta**.

    b. In the **Last name** textbox, enter the last name of user like **Simon**.

    c. In the **Email** textbox, enter the email of user like `brittasimon@contoso.com`.

    d. Select **Save**.

    Note

    The Microsoft Entra account holder receives an email that includes a link to confirm the account before it becomes active.

Note

Bonusly also supports automatic user provisioning, you can find more details [here](bonusly-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the Bonusly for which you set up the SSO.
- You can use Microsoft My Apps. When you select the Bonusly tile in the My Apps, you should be automatically signed in to the Bonusly for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
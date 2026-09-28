---
layout: Conceptual
title: Configure UserVoice for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/uservoice-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and UserVoice.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 8a4483be-356d-5d3c-d7ae-30e8c95e51a9
document_version_independent_id: 8b324d39-857f-7e7f-0b71-1ebaff0e9e19
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/uservoice-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/uservoice-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/uservoice-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: bb7da9a3-da63-693f-316c-4604955631b2
---

# Configure UserVoice for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate UserVoice with Microsoft Entra ID. When you integrate UserVoice with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to UserVoice.
- Enable your users to be automatically signed-in to UserVoice with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- UserVoice single sign-on enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- UserVoice supports **SP** initiated SSO.

## Add UserVoice from the gallery

To configure the integration of UserVoice into Microsoft Entra ID, you need to add UserVoice from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **UserVoice** in the search box.
4. Select **UserVoice** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for UserVoice

Configure and test Microsoft Entra SSO with UserVoice using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in UserVoice.

To configure and test Microsoft Entra SSO with UserVoice, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure UserVoice SSO**- to configure the single sign-on settings on application side.
    1. **Create UserVoice test user** - to have a counterpart of B.Simon in UserVoice that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **UserVoice** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<TENANT_NAME>.UserVoice.com`

    b. In the **Sign on URL** text box, type a URL using the following pattern: `https://<TENANT_NAME>.UserVoice.com`

    Note

    These values aren't real. Update these values with the actual Identifier and Sign on URL. Contact [UserVoice Client support team](https://www.uservoice.com/) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. In the **SAML Signing Certificate** section, select **Edit** button to open **SAML Signing Certificate** dialog.

    ![Edit SAML Signing Certificate](common/edit-certificate.png)
7. In the **SAML Signing Certificate** section, copy the **Thumbprint** and save it on your computer.

    ![Copy Thumbprint value](common/copy-thumbprint.png)
8. On the **Set up UserVoice** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure UserVoice SSO

1. In a different web browser window, sign in to your UserVoice company site as an administrator.
2. In the toolbar on the top, select **Settings**, and then select **Web portal** from the menu.

    ![Settings Section On App Side](media/uservoice-tutorial/portal.png)
3. On the **Web portal** tab, in the **User authentication** section, select **Edit** to open the **Edit User Authentication** dialog page.

    ![Web portal Tab](media/uservoice-tutorial/user.png)
4. On the **Edit User Authentication** dialog page, perform the following steps:

    ![Edit user authentication](media/uservoice-tutorial/authentication.png)

    a. Select **Single Sign-On (SSO)**.

    b. Paste the **Login URL** value into the **SSO Remote Sign-In** textbox.

    c. Paste the **Logout URL** value into the **SSO Remote Sign-Out textbox**.

    d. Paste the **Thumbprint** value,. into the **Current certificate SHA1 fingerprint** textbox.

    e. Select **Save authentication settings**.

### Create UserVoice test user

To enable Microsoft Entra users to sign in to UserVoice, they must be provisioned into UserVoice. In the case of UserVoice, provisioning is a manual task.

### To provision a user account, perform the following steps:

1. Sign in to your **UserVoice** tenant.
2. Go to **Settings**.

    ![Settings](media/uservoice-tutorial/account.png)
3. Select **General**.
4. Select **Agents and permissions**.

    ![Agents and permissions](media/uservoice-tutorial/general.png)
5. Select **Add admins**.

    ![Add admins](media/uservoice-tutorial/admin.png)
6. On the **Invite admins** dialog, perform the following steps:

    ![Invite admins](media/uservoice-tutorial/invite.png)

    a. In the Emails textbox, type the email address of the account you want to provision, and then select **Add**.

    b. Select **Invite**.

Note

You can use any other UserVoice user account creation tools or APIs provided by UserVoice to provision Microsoft Entra user accounts.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to UserVoice Sign-on URL where you can initiate the login flow.
- Go to UserVoice Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the UserVoice tile in the My Apps, this option redirects to UserVoice Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
---
layout: Conceptual
title: Configure Teamphoria for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/teamphoria-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Teamphoria.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 83b18a79-c7cf-9cd7-f156-b670fcad9063
document_version_independent_id: 92c75205-6bed-59ea-57a6-6e7bcdbaad9d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/teamphoria-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/teamphoria-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/teamphoria-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 444d93bb-a3d2-d8dd-34e3-41f3d27854d1
---

# Configure Teamphoria for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Teamphoria with Microsoft Entra ID. When you integrate Teamphoria with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Teamphoria.
- Enable your users to be automatically signed-in to Teamphoria with their Microsoft Entra accounts.
- Manage your accounts in one central location.

To learn more about SaaS app integration with Microsoft Entra ID, see [What is application access and single sign-on with Microsoft Entra ID](../enterprise-apps/what-is-single-sign-on).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Teamphoria single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Teamphoria supports **SP** initiated SSO

## Adding Teamphoria from the gallery

To configure the integration of Teamphoria into Microsoft Entra ID, you need to add Teamphoria from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Teamphoria** in the search box.
4. Select **Teamphoria** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra single sign-on for Teamphoria

Configure and test Microsoft Entra SSO with Teamphoria using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Teamphoria.

To configure and test Microsoft Entra SSO with Teamphoria, complete the following building blocks:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Teamphoria SSO**- to configure the single sign-on settings on application side.
    1. **Create Teamphoria test user** - to have a counterpart of B.Simon in Teamphoria that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Teamphoria** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the edit/pen icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<sub-domain>.teamphoria.com/login`

    Note

    The value isn't real. Update the value with the actual Sign-On URL. Contact [Teamphoria Client support team](https://www.teamphoria.com/) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Teamphoria** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Teamphoria SSO

1. In a different web browser window, sign in to your Teamphoria company site as an administrator
2. Go to **ADMIN SETTINGS** option in the left toolbar and under the Configure Tab select **SINGLE SIGN-ON** to open the SSO configuration window.

    ![Screenshot shows ADMIN SETTINGS where you can select SINGLE SIGN-ON.](media/teamphoria-tutorial/admin_sso_configure.png)
3. Select **ADD NEW IDENTITY PROVIDER** option in the top right corner to open the form for adding the settings for SSO.

    ![Screenshot shows where you can select ADD NEW IDENTITY PROVIDER.](media/teamphoria-tutorial/add_new_identity_provider.png)
4. Enter the details in the fields as described below-

    ![Screenshot shows the page where you can enter the values described.](media/teamphoria-tutorial/teamphoria_sso_save.png)

    a. **DISPLAY NAME**: Enter the display name of the plugin on the admin page.

    b. **BUTTON NAME**: The name of the tab that will display on the login page for logging in via SSO.

    c. **CERTIFICATE**: Open the Certificate downloaded earlier in notepad, copy the contents of the same and paste it here in the box.

    d. **ENTRY POINT**: Paste the **Login URL** copied earlier.

    e. Switch the option to **ON** and select **SAVE**.

### Create Teamphoria test user

In order to enable Microsoft Entra users to sign in to Teamphoria, they must be provisioned into Teamphoria. In the case of Teamphoria, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Sign in to your Teamphoria company site as an administrator.
2. Select **ADMIN** settings on the left toolbar and under the **MANAGE** tab Select **USERS** to open the admin page for users.

    ![Add Employee](media/teamphoria-tutorial/admin_manage_users.png)
3. Select the **MANUAL INVITE** option.

    ![Screenshot shows the MANUAL INVITE option.](media/teamphoria-tutorial/admin_manage_add_users.png)
4. On this page, perform following action.

    ![Screenshot shows the MANUAL USER INVITE page where you can enter name and email address.](media/teamphoria-tutorial/manual_user_invite.png)

    a. In the **EMAIL ADDRESS** textbox, enter the **email address** of the user like B.Simon.

    b. In the **FIRST NAME** textbox, enter the first name of the user like **B**.

    c. In the **LAST NAME** textbox, enter the last name of the user like **Simon**.

    d. Select **INVITE 1 USER**. User needs to accept the invite to get created in the system.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration using the Access Panel.

When you select the Teamphoria tile in the Access Panel, you should be automatically signed in to the Teamphoria for which you set up SSO. For more information about the Access Panel, see [Introduction to the Access Panel](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
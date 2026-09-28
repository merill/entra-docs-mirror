---
layout: Conceptual
title: Configure Help Scout for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/helpscout-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Help Scout.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: fa3a8f91-a8d3-f3d3-4c24-e4b628de66c5
document_version_independent_id: 8372f584-37ee-bd8e-c4b2-f54a37f85887
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/helpscout-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/helpscout-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/helpscout-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: e3486d52-cfb1-dfb5-a919-cc925b09d9a8
---

# Configure Help Scout for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Help Scout with Microsoft Entra ID. When you integrate Help Scout with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Help Scout.
- Enable your users to be automatically signed-in to Help Scout with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Help Scout single sign-on enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Help Scout supports **SP and IDP** initiated SSO.
- Help Scout supports **Just In Time** user provisioning.

## Add Help Scout from the gallery

To configure the integration of Help Scout into Microsoft Entra ID, you need to add Help Scout from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Help Scout** in the search box.
4. Select **Help Scout** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Help Scout

Configure and test Microsoft Entra SSO with Help Scout using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Help Scout.

To configure and test Microsoft Entra SSO with Help Scout, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Help Scout SSO**- to configure the single sign-on settings on application side.
    1. **Create Help Scout test user** - to have a counterpart of B.Simon in Help Scout that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Help Scout** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, If you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. **Identifier** is the **Audience URI (Service Provider Entity ID)** from Help Scout, starts with `urn:`

    b. **Reply URL** is the **Post-back URL (Assertion Consumer Service URL)** from Help Scout, starts with `https://`

    Note

    The values in these URLs are for demonstration only. You need to update these values from actual Reply URL and Identifier. You get these values from the **Single Sign-On** tab under Authentication section, which is explained later in the article.
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** textbox, type the URL: `https://secure.helpscout.net/members/login/`
7. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
8. On the **Set up Help Scout** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create a Microsoft Entra test user

In this section, you create a test user called B.Simon.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **New user** &gt; **Create new user**, at the top of the screen.
4. In the **User**properties, follow these steps:
    1. In the **Display name** field, enter `B.Simon`.
    2. In the **User principal name** field, enter the username@companydomain.extension. For example, `B.Simon@contoso.com`.
    3. Select the **Show password** check box, and then write down the value that's displayed in the **Password** box.
    4. Select **Review + create**.
5. Select **Create**.

### Assign the Microsoft Entra test user

In this section, you enable B.Simon to use single sign-on by granting access to Help Scout.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Help Scout**.
3. In the app's overview page, select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Add Assignment**dialog.
    1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then select the **Select** button at the bottom of the screen.
    2. If you're expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
    3. In the **Add Assignment** dialog, select the **Assign** button.

## Configure Help Scout SSO

1. In a different web browser window, sign in to your Help Scout company site as an administrator
2. Select **Manage** from the top menu and then select **Company** from the dropdown menu.

    ![Screenshot shows the Manage menu with Company selected.](media/helpscout-tutorial/settings.png)
3. Select **Authentication** from the left navigation pane.

    ![Screenshot shows Authentication selected.](media/helpscout-tutorial/authentication.png)
4. This takes you to the SAML settings section and perform the following steps:

    ![Screenshot shows the Single Sign-On tab where you enter the specified information.](media/helpscout-tutorial/configuration.png)

    a. Copy the **Post-back URL (Assertion Consumer Service URL)** value and paste the value in the **Reply URL** text box in the **Basic SAML Configuration** section.

    b. Copy the **Audience URI (Service Provider Entity ID)** value and paste the value in the **Identifier** text box in the **Basic SAML Configuration** section.
5. Toggle **Enable SAML** on and perform the following steps:

    ![Screenshot shows the Single Sign-On tab where you enable SAML and add other information.](media/helpscout-tutorial/information.png)

    a. In **Single Sign-On URL** textbox, paste the value of **Login URL**.

    b. Select **Upload Certificate** to upload the **Certificate(Base64)** downloaded previously.

    c. Enter your organization's email domain(s) e.x.- `contoso.com` in the **Email Domains** textbox. You can separate multiple domains with a comma. Anytime a Help Scout User or Administrator who enters that specific domain on the [Help Scout log-in page](https://secure.helpscout.net/members/login/) is routed to Identity Provider to authenticate with their credentials.

    d. Lastly, you can toggle **Force SAML Sign-on** if you want Users to only log in to Help Scout via through this method. If you'd still like to leave the option for them to sign in with their Help Scout credentials, you can leave it toggled off. Even if this is enabled, an Account Owner will always be able to log in to Help Scout with their account password.

    e. Select **Save**.

### Create Help Scout test user

In this section, a user called B.Simon is created in Help Scout. Help Scout supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Help Scout, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Help Scout Sign on URL where you can initiate the login flow.
- Go to Help Scout Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Help Scout for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Help Scout tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Help Scout for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
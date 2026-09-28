---
layout: Conceptual
title: Configure Sprinklr for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/sprinklr-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Sprinklr.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 0116a89c-5e6a-17c5-200a-2295c3467eab
document_version_independent_id: ecc2bbb4-d033-d0f5-bd5f-8827ba2b4621
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/sprinklr-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/sprinklr-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/sprinklr-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: af2ce459-37a2-78ea-8b5f-b73031f69027
---

# Configure Sprinklr for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Sprinklr with Microsoft Entra ID. When you integrate Sprinklr with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Sprinklr.
- Enable your users to be automatically signed-in to Sprinklr with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Sprinklr single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Sprinklr supports **SP** initiated SSO.

## Add Sprinklr from the gallery

To configure the integration of Sprinklr into Microsoft Entra ID, you need to add Sprinklr from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Sprinklr** in the search box.
4. Select **Sprinklr** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Sprinklr

Configure and test Microsoft Entra SSO with Sprinklr using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Sprinklr.

To configure and test Microsoft Entra SSO with Sprinklr, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Sprinklr SSO**- to configure the single sign-on settings on application side.
    1. **Create Sprinklr test user** - to have a counterpart of B.Simon in Sprinklr that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Sprinklr** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    1. In the **Sign on URL** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.sprinklr.com`
    2. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.sprinklr.com`

    Note

    These values aren't real. Update these values with the actual Sign on URL and Identifier. Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Sprinklr** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Sprinklr SSO

1. In a different web browser window, log in to your Sprinklr company site as an administrator.
2. Go to **Administration** &gt; **Settings**.

    ![Administration](media/sprinklr-tutorial/settings.png)
3. Go to **Manage Partner** &gt; **Single Sign** on from the left pane.

    ![Manage Partner](media/sprinklr-tutorial/users.png)
4. Select **+Add Single Sign Ons**.

    ![Screenshot shows the Add Single Sign Ons button.](media/sprinklr-tutorial/add-user.png)
5. On the **Single Sign on** page, perform the following steps:

    ![Screenshot shows the Single Sign on page where you can enter the values described.](media/sprinklr-tutorial/configuration.png)

    1. In the **Name** textbox, type a name for your configuration (for example: **WAADSSOTest**).
    2. Select **Enabled**.
    3. Select **Use new SSO Certificate**.
    4. Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.
    5. Paste the **Microsoft Entra Identifier** value which you have into the **Entity Id** textbox.
    6. Paste the **Login URL** value which you have into the **Identity Provider Login URL** textbox.
    7. Paste the **Logout URL** value which you have into the **Identity Provider Logout URL** textbox.
    8. As **SAML User ID Type**, select **Assertion contains User’s sprinklr.com username**.
    9. As **SAML User ID Location**, select **User ID is in the Name Identifier element of the Subject statement**.
    10. Select **Save**.

    ![SAML](media/sprinklr-tutorial/save-configuration.png)

### Create Sprinklr test user

1. Log in to your Sprinklr company site as an administrator.
2. Go to **Administration** &gt; **Settings**.

    ![Administration](media/sprinklr-tutorial/settings.png)
3. Go to **Manage Client** &gt; **Users** from the left pane.

    ![Screenshot shows the Add User button in Settings/Users.](media/sprinklr-tutorial/client.png)
4. Select **Add User**.

    ![Screenshot shows the Edit user dialog box where you can enter the values described.](media/sprinklr-tutorial/search-users.png)
5. On the **Edit user** dialog, perform the following steps:

    ![Edit user](media/sprinklr-tutorial/update-users.png)

    1. In the **Email**, **First Name** and **Last Name** textboxes, type the information of a Microsoft Entra user account you want to provision.
    2. Select **Password Disabled**.
    3. Select **Language**.
    4. Select **User Type**.
    5. Select **Update**.

    Important

    **Password Disabled** must be selected to enable a user to log in via an Identity provider.
6. Go to **Role**, and then perform the following steps:

    ![Partner Roles](media/sprinklr-tutorial/role.png)

    1. From the **Global** list, select **ALL\_Permissions**.
    2. Select **Update**.

Note

You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr to provision Microsoft Entra user accounts.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Sprinklr Sign-on URL where you can initiate the login flow.
- Go to Sprinklr Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Sprinklr tile in the My Apps, this option redirects to Sprinklr Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
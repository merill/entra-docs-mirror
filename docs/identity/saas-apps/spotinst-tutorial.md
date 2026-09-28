---
layout: Conceptual
title: Configure Spotinst for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/spotinst-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Spotinst.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 19af48f7-b63f-e123-15a0-56fd4b7b1af6
document_version_independent_id: ef0df07b-3273-3a84-5dc2-ba8b3ed7cc0a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/spotinst-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/spotinst-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/spotinst-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 9dbf345b-4c46-7d1e-051d-f016d70e34ec
---

# Configure Spotinst for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Spotinst with Microsoft Entra ID. When you integrate Spotinst with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Spotinst.
- Enable your users to be automatically signed-in to Spotinst with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Spotinst single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Spotinst supports **SP and IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Spotinst from the gallery

To configure the integration of Spotinst into Microsoft Entra ID, you need to add Spotinst from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Spotinst** in the search box.
4. Select **Spotinst** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Spotinst

Configure and test Microsoft Entra SSO with Spotinst using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Spotinst.

To configure and test Microsoft Entra SSO with Spotinst, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Spotinst SSO**- to configure the single sign-on settings on application side.
    1. **Create Spotinst test user** - to have a counterpart of B.Simon in Spotinst that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Spotinst** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. In the **Basic SAML Configuration** section, if you want to configure the application in IDP initiated mode, perform the following steps:

    1. Make sure **Reply URL** is set to: https://console.spotinst.com/auth/saml.
    2. In **Relay State**, enter your Spotinst Organization ID, which you can also confirm on the **SSO** tab.
    3. **Sign-on URL** must be empty.
6. Select **Save**.
7. Spotinst application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
8. In addition to above, Spotinst application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | Email | user.mail |
    | FirstName | user.givenname |
    | LastName | user.surname |
9. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
10. On the **Set up Spotinst** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Spotinst SSO

1. In a different web browser window, sign in to Spotinst as a Security Administrator.
2. Select the **user icon** on the top right side of the screen and select **Settings**.

    ![Screenshot shows Settings selected from the User icon.](media/spotinst-tutorial/settings.png)
3. Select the **SECURITY** tab on the top and then select **Identity Providers** and perform the following steps:

    ![Spotinst security](media/spotinst-tutorial/security.png)

    a. Copy the **Relay State** value for your instance and paste it in **Relay State** textbox in **Basic SAML Configuration** section.

    b. Select **BROWSE** to upload the metadata xml file that you have downloaded from Azure portal

    c. Select **SAVE**.

### Create Spotinst test user

The objective of this section is to create a user called Britta Simon in Spotinst.

1. If you have configured the application in the **SP** initiated mode, perform the following steps:

    a. In a different web browser window, sign in to Spotinst as a Security Administrator.

    b. Select the **user icon** on the top right side of the screen and select **Settings**.

    ![Screenshot shows Settings selected from the User icon.](media/spotinst-tutorial/settings.png)

    c. Select **Users** and select **ADD USER**.

    ![Screenshot shows ADD USER selected from Users.](media/spotinst-tutorial/add-user.png)

    d. On the add user section, perform the following steps:

    ![Screenshot shows the Add user section where you can enter the values described.](media/spotinst-tutorial/new-user.png)

    1. In the **Full Name** textbox, enter the full name of user like `BrittaSimon`.
    2. In the **Email** textbox, enter the email address of the user like `brittasimon@contoso.com`.
    3. Select your organization-specific details for the **Organization Role, Account Role, and Accounts**.
2. If you have configured the application in the **IDP** initiated mode, There's no action item for you in this section. Spotinst supports just-in-time provisioning, which is by default enabled. A new user is created during an attempt to access Spotinst if it doesn't exist yet.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Spotinst Sign on URL where you can initiate the login flow.
- Go to Spotinst Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Spotinst for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Spotinst tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Spotinst for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
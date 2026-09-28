---
layout: Conceptual
title: Configure MOVEit Transfer for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/moveittransfer-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and MOVEit Transfer - Microsoft Entra integration.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 99ae594b-a2d3-4e47-527f-6ee05fe7df4b
document_version_independent_id: 1d778975-6ebf-6e37-f00e-afa823285423
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/moveittransfer-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/moveittransfer-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/moveittransfer-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 5b97070f-dde9-5a40-ffb9-01eb71be701b
---

# Configure MOVEit Transfer for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate MOVEit Transfer - Microsoft Entra integration with Microsoft Entra ID. When you integrate MOVEit Transfer - Microsoft Entra integration with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to MOVEit Transfer - Microsoft Entra integration.
- Enable your users to be automatically signed-in to MOVEit Transfer - Microsoft Entra integration with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- MOVEit Transfer - Microsoft Entra integration single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- MOVEit Transfer - Microsoft Entra integration supports **SP** initiated SSO.

## Add MOVEit Transfer - Microsoft Entra integration from the gallery

To configure the integration of MOVEit Transfer - Microsoft Entra integration into Microsoft Entra ID, you need to add MOVEit Transfer - Microsoft Entra integration from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **MOVEit Transfer - Microsoft Entra integration** in the search box.
4. Select **MOVEit Transfer - Microsoft Entra integration** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for MOVEit Transfer - Microsoft Entra integration

Configure and test Microsoft Entra SSO with MOVEit Transfer - Microsoft Entra integration using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in MOVEit Transfer - Microsoft Entra integration.

To configure and test Microsoft Entra SSO with MOVEit Transfer - Microsoft Entra integration, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure MOVEit Transfer - Microsoft Entra integration SSO**- to configure the single sign-on settings on application side.
    1. **Create MOVEit Transfer - Microsoft Entra integration test user** - to have a counterpart of B.Simon in MOVEit Transfer - Microsoft Entra integration that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **MOVEit Transfer - Microsoft Entra integration** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you have **Service Provider metadata file**, perform the following steps:

    a. Select **Upload metadata file**.

    ![Upload metadata file](common/upload-metadata.png)

    b. Select **folder logo** to select the metadata file and select **Upload**.

    ![choose metadata file](common/browse-upload-metadata.png)

    c. After the metadata file is successfully uploaded, the **Identifier** and **Reply URL** value gets auto populated in **Basic SAML Configuration** section.

    d. In the **Sign-on URL** text box, type the URL: `https://contoso.com`

    Note

    The **Sign-on URL** value isn't real. Update the value with the actual Sign-On URL. Contact [MOVEit Transfer - Microsoft Entra integration Client support](https://community.ipswitch.com/s/support) team to get the value. You can download the **Service Provider Metadata file** from the **Service Provider Metadata URL** which is explained later in the **Configure MOVEit Transfer - Microsoft Entra integration Single Sign-On** section of the article. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up MOVEit Transfer - Microsoft Entra integration** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure MOVEit Transfer - Microsoft Entra integration SSO

1. Sign on to your MOVEit Transfer tenant as an administrator.
2. On the left navigation pane, select **Settings**.

    ![Settings Section On App side.](media/moveittransfer-tutorial/settings.png)
3. Select **Single Signon** link, which is under **Security Policies -&gt; User Auth**.

    ![Security Policies On App side.](media/moveittransfer-tutorial/security.png)
4. Select the Metadata URL link to download the metadata document.

    ![Service Provider Metadata URL.](media/moveittransfer-tutorial/metadata.png)

    a. Verify that the **entityID** value in the **EntityDescriptor** matches **Identifier** in the **Basic SAML Configuration** section.

    b. Verify that the **AssertionConsumerService** **Location** URL matches **REPLY URL** in the **Basic SAML Configuration** section.
5. Select **Add Identity Provider** button to add a new Federated Identity Provider.

    ![Add Identity Provider.](media/moveittransfer-tutorial/provider.png)
6. Select **Browse...** to select the metadata file which you downloaded from Azure portal, then select **Add Identity Provider** to upload the downloaded file.

    ![SAML Identity Provider.](media/moveittransfer-tutorial/azure.png)
7. Select "**Yes**" as **Enabled** in the **Edit Federated Identity Provider Settings...** page and select **Save**.

    ![Federated Identity Provider Settings.](media/moveittransfer-tutorial/save.png)
8. In the **Edit Federated Identity Provider User Settings** page, perform the following actions:

    ![Edit Federated Identity Provider Settings.](media/moveittransfer-tutorial/attributes.png)

    a. Select **SAML NameID** as **Login name**.

    b. Select **Other** as **Full name** and in the **Attribute name** textbox put the value: `http://schemas.microsoft.com/identity/claims/displayname`.

    c. Select **Other** as **Email** and in the **Attribute name** textbox put the value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.

    d. Select **Yes** as **Auto-create account on signon**.

    e. Select **Save** button.

### Create MOVEit Transfer - Microsoft Entra integration test user

The objective of this section is to create a user called Britta Simon in MOVEit Transfer - Microsoft Entra integration. MOVEit Transfer - Microsoft Entra integration supports just-in-time provisioning, which you have enabled. There's no action item for you in this section. A new user is created during an attempt to access MOVEit Transfer - Microsoft Entra integration if it doesn't exist yet.

Note

If you need to create a user manually, you need to contact the [MOVEit Transfer - Microsoft Entra integration Client support team](https://community.ipswitch.com/s/support).

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to MOVEit Transfer - Microsoft Entra integration Sign-on URL where you can initiate the login flow.
- Go to MOVEit Transfer - Microsoft Entra integration Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the MOVEit Transfer - Microsoft Entra integration tile in the My Apps, you should be automatically signed in to the MOVEit Transfer - Microsoft Entra integration for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
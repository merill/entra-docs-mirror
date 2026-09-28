---
layout: Conceptual
title: Configure Beekeeper Microsoft Entra SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/beekeeper-azure-ad-data-connector-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Beekeeper Microsoft Entra SSO.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: b58cb583-d9df-8a8b-5388-14f55c1d5588
document_version_independent_id: f6efe825-62fe-5dc1-be55-959b7ec15a29
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/beekeeper-azure-ad-data-connector-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/beekeeper-azure-ad-data-connector-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/beekeeper-azure-ad-data-connector-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 38efe50a-a5fd-a1b7-addc-e75261a3c732
---

# Configure Beekeeper Microsoft Entra SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Beekeeper Microsoft Entra SSO with Microsoft Entra ID. When you integrate Beekeeper Microsoft Entra SSO with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Beekeeper Microsoft Entra SSO.
- Enable your users to be automatically signed-in to Beekeeper Microsoft Entra SSO with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Beekeeper Microsoft Entra SSO single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Beekeeper Microsoft Entra SSO supports **SP and IDP** initiated SSO.
- Beekeeper Microsoft Entra SSO supports **Just In Time** user provisioning.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Beekeeper Microsoft Entra SSO from the gallery

To configure the integration of Beekeeper Microsoft Entra SSO into Microsoft Entra ID, you need to add Beekeeper Microsoft Entra SSO from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Beekeeper Microsoft Entra SSO** in the search box.
4. Select **Beekeeper Microsoft Entra SSO** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Beekeeper Microsoft Entra SSO

Configure and test Microsoft Entra SSO with Beekeeper Microsoft Entra SSO using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Beekeeper Microsoft Entra SSO.

To configure and test Microsoft Entra SSO with Beekeeper Microsoft Entra SSO, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Beekeeper Microsoft Entra SSO**- to configure the single sign-on settings on application side.
    1. **Create Beekeeper Microsoft Entra SSO test user** - to have a counterpart of B.Simon in Beekeeper Microsoft Entra SSO that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Beekeeper Microsoft Entra SSO** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you have **Service Provider metadata file** and wish to configure in **IDP** initiated mode, perform the following steps:

    a. Select **Upload metadata file**.

    ![Upload metadata file](common/upload-metadata.png)

    b. Select **folder logo** to select the metadata file and select **Upload**.

    ![choose metadata file](common/browse-upload-metadata.png)

    c. After the metadata file is successfully uploaded, the **Identifier** and **Reply URL** values get auto populated in Basic SAML Configuration section.

    Note

    If the **Identifier** and **Reply URL** values don't get auto populated, then fill in the values manually according to your requirement.
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<YOUR_COMPANY>.beekeeper.io/login`

    Note

    The Sign-on URL value isn't real. Update this value with the actual Sign-on URL. Contact [Beekeeper Microsoft Entra SSO Client support team](mailto:support@beekeeper.io) to get this value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. Beekeeper Microsoft Entra SSO application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows Set additional U R Ls where you can enter a Sign on U R L.](common/default-attributes.png)
8. In addition to above, Beekeeper Microsoft Entra SSO application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | firstname | user.givenname |
    | lastname | user.surname |
    | email | user.mail |
    | username | user.principalname |
    | position | user.jobtitle |
9. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
10. On the **Set up Beekeeper Microsoft Entra SSO** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Beekeeper Microsoft Entra SSO

To configure single sign-on on **Beekeeper Microsoft Entra SSO** side, you need to send the downloaded **Federation Metadata XML** and appropriate copied URLs from the application configuration to [Beekeeper Microsoft Entra SSO support team](mailto:support@beekeeper.io). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Beekeeper Microsoft Entra SSO test user

In this section, a user called Britta Simon is created in Beekeeper Microsoft Entra SSO. Beekeeper Microsoft Entra SSO supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Beekeeper Microsoft Entra SSO, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Beekeeper Microsoft Entra SSO Sign on URL where you can initiate the login flow.
- Go to Beekeeper Microsoft Entra SSO Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Beekeeper Microsoft Entra SSO for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Beekeeper Microsoft Entra SSO tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Beekeeper Microsoft Entra SSO for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
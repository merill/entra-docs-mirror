---
layout: Conceptual
title: Configure TOPdesk - Public for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/topdesk-public-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and TOPdesk - Public.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: e1e4e6c3-5f9d-5779-2a1e-055ae4414dbc
document_version_independent_id: ce291bb5-5163-b50a-63dd-016b5b78bdff
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/topdesk-public-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/topdesk-public-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/topdesk-public-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 0d832e44-7398-729b-44e8-94bc38125083
---

# Configure TOPdesk - Public for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate TOPdesk - Public with Microsoft Entra ID. When you integrate TOPdesk - Public with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to TOPdesk - Public.
- Enable your users to be automatically signed-in to TOPdesk - Public with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- TOPdesk - Public single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- TOPdesk - Public supports **SP** initiated SSO.

## Add TOPdesk - Public from the gallery

To configure the integration of TOPdesk - Public into Microsoft Entra ID, you need to add TOPdesk - Public from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **TOPdesk - Public** in the search box.
4. Select **TOPdesk - Public** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for TOPdesk - Public

Configure and test Microsoft Entra SSO with TOPdesk - Public using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in TOPdesk - Public.

To configure and test Microsoft Entra SSO with TOPdesk - Public, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure TOPdesk - Public SSO**- to configure the single sign-on settings on application side.
    1. **Create TOPdesk - Public test user** - to have a counterpart of B.Simon in TOPdesk - Public that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **TOPdesk - Public** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you have **Service Provider metadata file**, perform the following steps:

    Note

    You get the **Service Provider metadata file** from the **Configure TOPdesk - Public Single Sign-On** section which is explained later in the article.

    a. Select **Upload metadata file**.

    ![Upload metadata file](common/upload-metadata.png)

    b. Select **folder logo** to select the metadata file and select **Upload**.

    ![choose metadata file](common/browse-upload-metadata.png)

    c. After the metadata file is successfully uploaded, the **Identifier** and **Reply URL** values get auto populated in Basic SAML Configuration section.

    d. In the **Sign-on URL** text box, type a URL using the following pattern: `https://<companyname>.topdesk.net`

    e. In the **Identifier URL** textbox, fill in the TOPdesk metadata URL that you can retrieve from the TOPdesk configuration. It should use the following pattern: `https://<companyname>.topdesk.net/saml-metadata/<identifier>`

    f. In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/verify`

    Note

    If the **Identifier** and **Reply URL** values don't get auto populated, you need to enter them manually. For Identifier, follow the pattern as mentioned above and you get Reply URL value from the **Configure TOPdesk - Public Single Sign-On** section which is explained later in the article. The **Sign-on URL** value isn't real, so you need to update the value with the actual Sign-On URL. Contact [TOPdesk - Public Client support team](https://www.topdesk.com/) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up TOPdesk - Public** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure TOPdesk - Public SSO

1. Sign on to your **TOPdesk - Public** company site as an administrator.
2. In the **TOPdesk** menu, select **Settings**.

    ![Settings](media/topdesk-public-tutorial/menu.png)
3. Select **Login Settings**.

    ![Login Settings](media/topdesk-public-tutorial/login.png)
4. Expand the **Login Settings** menu, and then select **General**.

    ![General Settings](media/topdesk-public-tutorial/general.png)
5. In the **Public** section of the **SAML login** configuration section, perform the following steps:

    ![Technical Settings](media/topdesk-public-tutorial/public.png)

    a. Select **Download** to download the public metadata file, and then save it locally on your computer.

    b. Open the downloaded metadata file, and then locate the **AssertionConsumerService** node.

    ![AssertionConsumerService](media/topdesk-public-tutorial/service.png)

    c. Copy the **AssertionConsumerService** value, paste this value in the **Reply URL** textbox in **Basic SAML Configuration** section.
6. To create a certificate file, perform the following steps:

    ![Certificate](media/topdesk-public-tutorial/certificate-file.png)

    a. Open the downloaded metadata file from Azure portal.

    b. Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.

    c. Copy the value of the **X509Certificate** node.

    d. Save the copied **X509Certificate** value locally on your computer in a file.
7. In the **Public** section, select **Add**.

    ![SAML Login](media/topdesk-public-tutorial/add.png)
8. On the **SAML configuration assistant** dialog page, perform the following steps:

    ![SAML Configuration Assistant](media/topdesk-public-tutorial/configuration.png)

    a. To upload your downloaded metadata file from Azure portal, under **Federation Metadata**, select **Browse**.

    b. To upload your certificate file, under **Certificate (RSA)**, select **Browse**.

    c. To upload the logo file you got from the TOPdesk support team, under **Logo icon**, select **Browse**.

    d. In the **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.

    e. In the **Display name** textbox, type a name for your configuration.

    f. Select **Save**.

### Create TOPdesk - Public test user

In order to enable Microsoft Entra users to sign into TOPdesk - Public, they must be provisioned into TOPdesk - Public. In the case of TOPdesk - Public, provisioning is a manual task.

### To configure user provisioning, perform the following steps:

1. Sign on to your **TOPdesk - Public** company site as administrator.
2. In the menu on the top, select **TOPdesk** &gt; **New** &gt; **Support Files** &gt; **Person**.

    ![Person](media/topdesk-public-tutorial/files.png)
3. On the New Person dialog, perform the following steps:

    ![New Person](media/topdesk-public-tutorial/new.png)

    a. Select the General tab.

    b. In the **Surname** textbox, type Surname of the user like Simon

    c. Select a **Site** for the account.

    d. Select **Save**.

Note

You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public to provision Microsoft Entra user accounts.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to TOPdesk - Public Sign-on URL where you can initiate the login flow.
- Go to TOPdesk - Public Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the TOPdesk - Public tile in the My Apps, this option redirects to TOPdesk - Public Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
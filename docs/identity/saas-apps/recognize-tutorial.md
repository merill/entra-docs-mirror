---
layout: Conceptual
title: Configure Recognize for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/recognize-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Recognize.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 55ec7747-37ba-c4be-403a-77d9f23055b1
document_version_independent_id: 88b911ad-f182-ff1d-4052-1a667c12f805
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/recognize-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/recognize-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/recognize-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 29ab8fd2-3e1f-30fe-6973-d6c3d9719239
---

# Configure Recognize for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Recognize with Microsoft Entra ID. When you integrate Recognize with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Recognize.
- Enable your users to be automatically signed-in to Recognize with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Recognize single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Recognize supports **SP** initiated SSO.

## Add Recognize from the gallery

To configure the integration of Recognize into Microsoft Entra ID, you need to add Recognize from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Recognize** in the search box.
4. Select **Recognize** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Recognize

Configure and test Microsoft Entra SSO with Recognize using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Recognize.

To configure and test Microsoft Entra SSO with Recognize, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Recognize SSO**- to configure the single sign-on settings on application side.
    1. **Create Recognize test user** - to have a counterpart of B.Simon in Recognize that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Recognize** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you have **Service Provider metadata file**, perform the following steps:

    Note

    You get the **Service Provider metadata file** from the **Configure Recognize Single Sign-On** section of the article.

    a. Select **Upload metadata file**.

    ![Upload metadata file](common/upload-metadata.png)

    b. Select **folder logo** to select the metadata file and select **Upload**.

    ![choose metadata file](common/browse-upload-metadata.png)

    c. After the metadata file is successfully uploaded, the **Identifier** value get auto populated in Basic SAML Configuration section.

    In the **Sign on URL** text box, type a URL using the following pattern: `https://recognizeapp.com/<YOUR_DOMAIN>/saml/sso`

    Note

    If the **Identifier** value don't get auto populated, you get the Identifier value by opening the Service Provider Metadata URL from the SSO Settings section that's explained later in the **Configure Recognize Single Sign-On** section of the article. The Sign-on URL value isn't real. Update the value with the actual Sign-on URL. Contact [Recognize Client support team](mailto:support@recognizeapp.com) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Recognize** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Recognize SSO

1. In a different web browser window, sign in to your Recognize tenant as an administrator.
2. On the upper right corner, select **Menu**. Go to **Company Admin**.

    ![Screenshot shows Company Admin selected from the Settings menu.](media/recognize-tutorial/menu.png)
3. On the left navigation pane, select **Settings**.

    ![Screenshot shows Settings selected from the navigation page.](media/recognize-tutorial/settings.png)
4. Perform the following steps on **SSO Settings** section.

    ![Screenshot shows S S O Settings where you can enter the values described.](media/recognize-tutorial/values.png)

    a. As **Enable SSO**, select **ON**.

    b. In the **IDP Entity ID** textbox, paste the value of **Microsoft Entra Identifier**..

    c. In the **Sso target url** textbox, paste the value of **Login URL**..

    d. In the **Slo target url** textbox, paste the value of **Logout URL**..

    e. Open your downloaded **Certificate (Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox.

    f. Select the **Save settings** button.
5. Beside the **SSO Settings** section, copy the URL under **Service Provider Metadata url**.

    ![Screenshot shows Notes, where you can copy the Service Provider Metadata.](media/recognize-tutorial/metadata.png)
6. Open the **Metadata URL link** under a blank browser to download the metadata document. Then copy the EntityDescriptor value(entityID) from the file and paste it in **Identifier** textbox in **Basic SAML Configuration** on Azure portal.

    ![Screenshot shows a text box with plain text X M L where you can get the entity I D.](media/recognize-tutorial/descriptor.png)

### Create Recognize test user

In order to enable Microsoft Entra users to log into Recognize, they must be provisioned into Recognize. In the case of Recognize, provisioning is a manual task.

This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.

**To provision a user account, perform the following steps:**

1. Sign into your Recognize company site as an administrator.
2. On the upper right corner, select **Menu**. Go to **Company Admin**.
3. On the left navigation pane, select **Settings**.
4. Perform the following steps on **User Sync** section.

    ![New User](media/recognize-tutorial/user.png)

    a. As **Sync Enabled**, select **ON**.

    b. As **Choose sync provider**, select **Microsoft / Office 365**.

    c. Select **Run User Sync**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Recognize Sign-on URL where you can initiate the login flow.
- Go to Recognize Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Recognize tile in the My Apps, this option redirects to Recognize Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
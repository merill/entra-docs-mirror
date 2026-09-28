---
layout: Conceptual
title: Configure Adra by Trintech for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/adra-by-trintech-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Adra by Trintech.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: c61866fc-71c3-e790-6005-d66e7f2e5217
document_version_independent_id: c4f2bee5-eab5-e13f-aaaa-d32c70d25d5d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/adra-by-trintech-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/adra-by-trintech-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/adra-by-trintech-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 8879eb89-368f-78d0-3ef3-fa7f13689567
---

# Configure Adra by Trintech for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Adra by Trintech with Microsoft Entra ID. When you integrate Adra by Trintech with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Adra by Trintech.
- Enable your users to be automatically signed-in to Adra by Trintech with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Adra by Trintech single sign-on (SSO) enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Adra by Trintech supports **SP** and **IDP** initiated SSO.

## Add Adra by Trintech from the gallery

To configure the integration of Adra by Trintech into Microsoft Entra ID, you need to add Adra by Trintech from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Adra by Trintech** in the search box.
4. Select **Adra by Trintech** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Adra by Trintech

Configure and test Microsoft Entra SSO with Adra by Trintech using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Adra by Trintech.

To configure and test Microsoft Entra SSO with Adra by Trintech, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Adra by Trintech SSO**- to configure the single sign-on settings on application side.
    1. **Create Adra by Trintech test user** - to have a counterpart of B.Simon in Adra by Trintech that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Adra by Trintech** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you have **Service Provider metadata file** and wish to configure in **IDP** initiated mode, perform the following steps:

    a. Select **Upload metadata file**.

    ![Screenshot shows to upload metadata file.](common/upload-metadata.png)

    b. Select **folder logo** to select the metadata file and select **Upload**.

    ![Screenshot shows to choose metadata file.](common/browse-upload-metadata.png)

    c. After the metadata file is successfully uploaded, the **Identifier** and **Reply URL** values get auto populated in **Basic SAML Configuration** section.

    d. In the **Sign-on URL** text box, type the URL: `https://login.adra.com`

    e. In the **Relay state** text box, type the URL: `https://setup.adra.com`

    f. In the **Logout URL** text box, type the URL: `https://login.adra.com/Saml/SLOServiceSP`

    Note

    You gets the **Service Provider metadata file** from the **Configure Adra by Trintech SSO** section, which is explained later in the article. If the **Identifier** and **Reply URL** values don't get auto populated, then fill in the values manually according to your requirement.
6. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Adra by Trintech SSO

1. Log in to your Adra by Trintech company site as an administrator.
2. Go to **Engagement** &gt; **Security** Tab &gt; **Security Policy** &gt; select **Use a federated identity provider** button.
3. Download the **Service Provider metadata file** by selecting **here** in the Adra page and upload this metadata file.

    [![Screenshot that shows the Configuration Settings.](media/adra-by-trintech-tutorial/settings.png)](media/adra-by-trintech-tutorial/settings.png#lightbox)
4. Select the **Add a new federated identity provider** button and enter the details for the required fields accordingly.

    a. Enter a valid **Name** and **Description** values in the textbox.

    b. In the **Metadata URL** textbox, paste the **App Federation Metadata Url** which you've copied and select the **Test URL** button.

    c. Select **Save** to save the SAML configuration..

### Create Adra by Trintech test user

In this section, you create a user called Britta Simon at Adra by Trintech. Work with [Adra by Trintech support team](mailto:support@adra.com) to add the users in the Adra by Trintech platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Adra by Trintech Sign-on URL where you can initiate the login flow.
- Go to Adra by Trintech Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Adra by Trintech for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Adra by Trintech tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Adra by Trintech for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
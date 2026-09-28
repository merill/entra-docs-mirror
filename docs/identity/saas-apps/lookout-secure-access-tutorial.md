---
layout: Conceptual
title: Configure Lookout Secure Access for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/lookout-secure-access-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Lookout Secure Access.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 18eae425-3c57-8b41-0916-ee906caf2041
document_version_independent_id: 18eae425-3c57-8b41-0916-ee906caf2041
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/lookout-secure-access-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/lookout-secure-access-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/lookout-secure-access-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: b58c7b61-8a20-8811-c69c-6329eb9106f1
---

# Configure Lookout Secure Access for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Lookout Secure Access with Microsoft Entra ID. When you integrate Lookout Secure Access with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Lookout Secure Access.
- Enable your users to be automatically signed-in to Lookout Secure Access with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Overview

Lookout Cloud Security Platform is a data-centric cloud security solution that protects your users from internet-based threats and protects data stored in cloud applications, private applications, and websites.

The solution supports these important components of cloud security:

- Lookout Secure Internet Access: Protection for web or nonweb internet-based traffic.
- Lookout Secure Private Access: Protection for private application traffic.
- Lookout Secure Cloud Access: Protection for cloud application traffic.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Lookout SSE subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Lookout Secure Access supports both **SP and IDP** initiated SSO.

## Add Lookout Secure Access from the gallery

To configure the integration of Lookout Secure Access into Microsoft Entra ID, you need to add Lookout Secure Access from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Lookout Secure Access** in the search box.
4. Select **Lookout Secure Access** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Lookout Secure Access

Configure and test Microsoft Entra SSO with Lookout Secure Access using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Lookout Secure Access.

To configure and test Microsoft Entra SSO with Lookout Secure Access, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Create a Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Lookout Secure Access SSO**- to configure the single sign-on settings on application side.
    1. **Create Lookout Secure Access test user** - to have a counterpart of B.Simon in Lookout Secure Access that's linked to the Microsoft Entra ID representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Lookout Secure Access** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    [![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)](common/edit-urls.png#lightbox)
5. On the **Basic SAML Configuration** section, if you have **Service Provider metadata file**, perform the following steps:

    a. Select **Upload metadata file**.

    [![Screenshot shows to Upload metadata file.](common/upload-metadata.png)](common/upload-metadata.png#lightbox)

    b. Select **folder logo** to select the metadata file and select **Upload**.

    [![Screenshot shows to choose metadata file.](common/browse-upload-metadata.png)](common/browse-upload-metadata.png#lightbox)

    c. After the metadata file is successfully uploaded, the **Identifier** and **Reply URL** values get auto populated in Basic SAML Configuration section.

    Note

    If the Identifier and Reply URL values aren't getting auto populated, then fill the values manually according to your requirement. You can get **Service Provider Metadata** file from the **Configure Lookout Secure Access** section.

    d. In the **Relay State** textbox, paste the value, which you have copied from the Lookout management console and select **Save**.
6. Lookout Secure Access application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. For the **Unique User Identifier (Name ID)** attribute, please set Name identifier format as **Unspecified** manually.

    [![Screenshot shows to manage claim.](media/lookout-secure-access-tutorial/claim.png)](media/lookout-secure-access-tutorial/claim.png#lightbox)
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    [![Screenshot shows the Certificate download link.](common/copy-metadataurl.png)](common/copy-metadataurl.png#lightbox)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Lookout Secure Access SSO

1. Log in to Lookout Secure Access company site as an administrator.
2. Go to **Administration** &gt; **Enterprise Integration** and select **Single Sign-On** from the left pane.
3. On the **SSO Groups** tab, select the download icon of the **SP Metadata** from the Default group. A pop-up appears with SP Metadata details. Select SP Metadata File button to download the file and upload in the **Basic SAML Configuration** section in the Microsoft Entra admin center.

    [![Screenshot shows to download metadata file.](media/lookout-secure-access-tutorial/metadata.png)](media/lookout-secure-access-tutorial/metadata.png#lightbox)
4. Navigate to **SSO Providers** tab and perform the following steps.

    [![Screenshot shows settings of the configuration.](media/lookout-secure-access-tutorial/settings.png)](media/lookout-secure-access-tutorial/settings.png#lightbox)

    1. Select **+New**.
    2. Enter a valid Name in the **Name** field and select Type as **Identity Provider**.
    3. Paste the **App Federation Metadata Url** in the **Metadata Link** textbox, which you have copied from the Microsoft Entra admin center.
    4. Select **Validate**.
    5. Select **Save**.
5. Navigate back to **Administration** &gt; **System Settings** &gt; **Enterprise Authentication** and perform the following steps:

    ![Screenshot shows the system settings of the Enterprise Authentication.](media/lookout-secure-access-tutorial/login.png)

    1. From the **Identity Provider** dropdown, choose the Identity Provider you created.
    2. Enable the **Management Console** and **Endpoint** by turning on the toggle.
    3. Copy the **Relay State** value by selecting the copy button and paste it in the **Relay State** textbox in **Basic SAML Configuration** section on Entra side.
    4. Select **Save**.

### Create Lookout Secure Access test user

In this section, a user called Britta Simon is created in Lookout Secure Access. Lookout Secure Access supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Lookout Secure Access, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated

- Go to Lookout SSE Management Console URL directly and initiate the login with IDP flow from there.

#### IDP initiated

- Select **Test this application** in Microsoft Entra admin center and you should be automatically signed in to the Lookout Secure Access for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Lookout Secure Access tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Lookout Secure Access for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
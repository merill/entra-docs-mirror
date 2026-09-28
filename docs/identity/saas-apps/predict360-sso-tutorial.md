---
layout: Conceptual
title: Configure Predict360 SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/predict360-sso-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Predict360 SSO.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 4a486e0e-6007-7894-7233-a513560ebc83
document_version_independent_id: 7a4d458d-2820-4b6d-9103-a3af971d4186
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/predict360-sso-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/predict360-sso-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/predict360-sso-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: e26ab9b7-1d35-d848-9d17-1bef2b5155f8
---

# Configure Predict360 SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Predict360 SSO with Microsoft Entra ID. Predict360 is a Governance, Risk and Compliance solution for mid-sized banks and other Financial Institutions. When you integrate Predict360 SSO with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Predict360 SSO.
- Enable your users to be automatically signed-in to Predict360 SSO with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You configure and test Microsoft Entra single sign-on for Predict360 SSO in a test environment. Predict360 SSO supports both **SP** and **IDP** initiated single sign-on.

## Prerequisites

To integrate Microsoft Entra ID with Predict360 SSO, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Predict360 SSO single sign-on (SSO) enabled subscription.

## Add application and assign a test user

Before you begin the process of configuring single sign-on, you need to add the Predict360 SSO application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the single sign-on configuration.

### Add Predict360 SSO from the Microsoft Entra gallery

Add Predict360 SSO from the Microsoft Entra application gallery to configure single sign-on with Predict360 SSO. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Predict360 SSO** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you have **Service Provider metadata file**, perform the following steps:

    a. Select **Upload metadata file**.

    ![Screenshot shows how to upload metadata file.](common/upload-metadata.png)

    b. Select **folder logo** to select the metadata file and select **Upload**.

    ![Screenshot shows to choose metadata file in folder.](common/browse-upload-metadata.png)

    c. After the metadata file is successfully uploaded, the **Identifier** and **Reply URL** values get auto populated in Basic SAML Configuration section.

    d. Enter the customer code/key provided by 360factors in **Relay State** textbox. Make sure the code is entered in lowercase. This is required for **IDP** initiated mode.

    Note

    You get the **Service Provider metadata file** from the [Predict360 SSO support team](mailto:support@360factors.com). If the **Identifier** and **Reply URL** values don't get auto populated, then fill in the values manually according to your requirement.

    e. If you wish to configure the application in **SP** initiated mode, then perform the following step:

    In the **Sign on URL** textbox, type your customer specific URL using the following pattern:`https://<customer-key>.360factors.com/predict360/login.do`

    Note

    This URL is shared by 360factors team. `<customer-key>` is replaced with your customer key, which is also provide by 360factors team.
6. On the **Set-up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)
7. Find **Certificate (Raw)** in the **SAML Signing Certificate** section, and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate Raw download link.](common/certificateraw.png)
8. On the **Set up Predict360 SSO** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration appropriate URL.](common/copy-configuration-urls.png)

## Configure Predict360 SSO

To configure single sign-on on **Predict360 SSO** side, you need to send the downloaded **Federation Metadata XML**, **Certificate (Raw)** and appropriate copied URLs from the application configuration to [Predict360 SSO support team](mailto:support@360factors.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Predict360 SSO test user

In this section, you create a user called Britta Simon at Predict360 SSO. Work with [Predict360 SSO support team](mailto:support@360factors.com) to add the users in the Predict360 SSO platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Predict360 SSO Sign-on URL where you can initiate the login flow.
- Go to Predict360 SSO Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Predict360 SSO for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Predict360 SSO tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Predict360 SSO for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
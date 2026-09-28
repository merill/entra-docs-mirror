---
layout: Conceptual
title: Configure tesma for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/tesma-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and tesma.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 81dfe242-6da6-10d6-5690-e0cdf5333342
document_version_independent_id: 008cfb2f-c2d0-aa8b-a4c5-3848a180943e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/tesma-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/tesma-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/tesma-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7ea97ec6-866b-7dd4-abb8-a6bb4e2fcb3f
---

# Configure tesma for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate tesma with Microsoft Entra ID. tesma provides SSO to tesma Essential and other tesma portals. When you integrate tesma with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to tesma.
- Enable your users to be automatically signed-in to tesma with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You'll configure and test Microsoft Entra single sign-on for tesma in a test environment. tesma supports both **SP** and **IDP** initiated single sign-on and **Just In Time** user provisioning.

## Prerequisites

To integrate Microsoft Entra ID with tesma, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- tesma single sign-on (SSO) enabled subscription.

## Add application and assign a test user

Before you begin the process of configuring single sign-on, you need to add the tesma application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the single sign-on configuration.

### Add tesma from the Microsoft Entra gallery

Add tesma from the Microsoft Entra application gallery to configure single sign-on with tesma. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **tesma** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type the value: `urn:identityprovider.chg-meridian.com`

    b. In the **Reply URL** textbox, type the URL: `https://identityprovider.chg-meridian.com`
6. If you want to configure **SP** initiated SSO, then perform the following step:

    In the **Sign on URL** textbox, type the URL: `https://qamajor.tesma.com`
7. On the **Set-up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)
8. On the **Set up tesma** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows how to copy configuration appropriate URL.](common/copy-configuration-urls.png)

## Configure tesma SSO

To configure single sign-on on **tesma** side, you need to send the downloaded **Federation Metadata XML** and appropriate copied URLs from the application configuration to [tesma support team](mailto:support@tesma.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create tesma test user

In this section, you create a user called Britta Simon in tesma. Work with [tesma support team](mailto:support@tesma.com) to add the users in the tesma platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to tesma Sign on URL where you can initiate the login flow.
- Go to tesma Sign on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the tesma for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the tesma tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the tesma for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
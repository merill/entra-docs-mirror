---
layout: Conceptual
title: Configure Yonyx Interactive Guides for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/yonyx-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Yonyx Interactive Guides.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: a6fc956c-63c6-1f96-009e-4d70121eb724
document_version_independent_id: 4f3709ae-5c6b-85ae-3292-91cf6632e928
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/yonyx-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/yonyx-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/yonyx-tutorial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 348f5ac4-b13c-648b-f2a7-f62491953c28
---

# Configure Yonyx Interactive Guides for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Yonyx Interactive Guides with Microsoft Entra ID. When you integrate Yonyx Interactive Guides with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Yonyx Interactive Guides.
- Enable your users to be automatically signed-in to Yonyx Interactive Guides with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Yonyx Interactive Guides single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Yonyx Interactive Guides supports **SP** initiated SSO.
- Yonyx Interactive Guides supports **Just In Time** user provisioning.

## Add Yonyx Interactive Guides from the gallery

To configure the integration of Yonyx Interactive Guides into Microsoft Entra ID, you need to add Yonyx Interactive Guides from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Yonyx Interactive Guides** in the search box.
4. Select **Yonyx Interactive Guides** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Yonyx Interactive Guides

Configure and test Microsoft Entra SSO with Yonyx Interactive Guides using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Yonyx Interactive Guides.

To configure and test Microsoft Entra SSO with Yonyx Interactive Guides, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Yonyx Interactive Guides SSO**- to configure the single sign-on settings on application side.
    1. **Create Yonyx Interactive Guides test user** - to have a counterpart of B.Simon in Yonyx Interactive Guides that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Yonyx Interactive Guides** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot for Edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    a. In the **Sign on URL** text box, type a URL using the following pattern: `https://<company name>.yonyx.com/y/conversation/?id=<guid number>`

    b. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<company name>.yonyx.com`

    Note

    These values aren't real. Update these values with the actual Sign on URL and Identifier. Contact [Yonyx Interactive Guides Client support team](mailto:support@yonyx.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![Screenshot for The Certificate download link.](common/certificatebase64.png)
7. On the **Set up Yonyx Interactive Guides** section, copy the appropriate URL(s) as per your requirement.

    ![Screenshot for Copy configuration URLs.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Yonyx Interactive Guides SSO

To configure single sign-on on **Yonyx Interactive Guides** side, you need to send the downloaded **Certificate (Base64)** and appropriate copied URLs from the application configuration to [Yonyx Interactive Guides support team](mailto:support@yonyx.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Yonyx Interactive Guides test user

In this section, a user called Britta Simon is created in Yonyx Interactive Guides. Yonyx Interactive Guides supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Yonyx Interactive Guides, a new one is created after authentication.

Note

If you need to create a user manually, you need to contact the [Yonyx Interactive Guides support team](mailto:support@yonyx.com).

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Yonyx Interactive Guides Sign-on URL where you can initiate the login flow.
- Go to Yonyx Interactive Guides Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Yonyx Interactive Guides tile in the My Apps, this option redirects to Yonyx Interactive Guides Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
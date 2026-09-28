---
layout: Conceptual
title: Configure TransPerfect GlobalLink Dashboard for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/transperfect-globallink-dashboard-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and TransPerfect GlobalLink Dashboard.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 05370277-634d-9f00-2b5d-1289ae86d3ef
document_version_independent_id: d3eebd8c-85c2-a5a2-f981-a7f16a7f75f8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/transperfect-globallink-dashboard-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/transperfect-globallink-dashboard-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/transperfect-globallink-dashboard-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 69c655a0-74d6-06a7-3e3b-561093ce3160
---

# Configure TransPerfect GlobalLink Dashboard for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate TransPerfect GlobalLink Dashboard with Microsoft Entra ID. When you integrate TransPerfect GlobalLink Dashboard with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to TransPerfect GlobalLink Dashboard.
- Enable your users to be automatically signed-in to TransPerfect GlobalLink Dashboard with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- TransPerfect GlobalLink Dashboard single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- TransPerfect GlobalLink Dashboard supports **SP and IDP** initiated SSO.
- TransPerfect GlobalLink Dashboard supports **Just In Time** user provisioning.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Adding TransPerfect GlobalLink Dashboard from the gallery

To configure the integration of TransPerfect GlobalLink Dashboard into Microsoft Entra ID, you need to add TransPerfect GlobalLink Dashboard from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **TransPerfect GlobalLink Dashboard** in the search box.
4. Select **TransPerfect GlobalLink Dashboard** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for TransPerfect GlobalLink Dashboard

Configure and test Microsoft Entra SSO with TransPerfect GlobalLink Dashboard using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in TransPerfect GlobalLink Dashboard.

To configure and test Microsoft Entra SSO with TransPerfect GlobalLink Dashboard, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure TransPerfect GlobalLink Dashboard SSO**- to configure the single sign-on settings on application side.
    1. **Create TransPerfect GlobalLink Dashboard test user** - to have a counterpart of B.Simon in TransPerfect GlobalLink Dashboard that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **TransPerfect GlobalLink Dashboard** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, the user doesn't have to perform any step as the app is already pre-integrated with Azure.
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type the URL: `https://sso.transperfect.com`
7. Select **Save**.
8. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![The Certificate download link](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure TransPerfect GlobalLink Dashboard SSO

To configure single sign-on on **TransPerfect GlobalLink Dashboard** side, you need to send the **App Federation Metadata Url** to [TransPerfect GlobalLink Dashboard support team](mailto:TechOps_Consulting@transperfect.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create TransPerfect GlobalLink Dashboard test user

In this section, a user called B.Simon is created in TransPerfect GlobalLink Dashboard. TransPerfect GlobalLink Dashboard supports just-in-time provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in TransPerfect GlobalLink Dashboard, a new one is created when you attempt to access TransPerfect GlobalLink Dashboard.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to TransPerfect GlobalLink Dashboard Sign on URL where you can initiate the login flow.
- Go to TransPerfect GlobalLink Dashboard Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the TransPerfect GlobalLink Dashboard for which you set up the SSO

You can also use Microsoft My Apps to test the application in any mode. When you select the TransPerfect GlobalLink Dashboard tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the TransPerfect GlobalLink Dashboard for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
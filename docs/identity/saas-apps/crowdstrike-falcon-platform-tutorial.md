---
layout: Conceptual
title: Configure CrowdStrike Falcon Platform for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/crowdstrike-falcon-platform-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and CrowdStrike Falcon Platform.
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
locale: en-us
document_id: 4d7647f4-9d8c-22f8-e564-975aaf4e6370
document_version_independent_id: e32468d5-ca67-da92-a165-719ee2f47e94
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/crowdstrike-falcon-platform-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/crowdstrike-falcon-platform-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/crowdstrike-falcon-platform-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 39224fad-2ed4-2c64-5583-d91b8f0653f9
---

# Configure CrowdStrike Falcon Platform for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate CrowdStrike Falcon Platform with Microsoft Entra ID. When you integrate CrowdStrike Falcon Platform with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to CrowdStrike Falcon Platform.
- Enable your users to be automatically signed-in to CrowdStrike Falcon Platform with their Microsoft Entra accounts.
- Manage your accounts in one central location.

CrowdStrike Falcon Platform is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A valid CrowdStrike Falcon subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- CrowdStrike Falcon Platform supports **SP and IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Adding CrowdStrike Falcon Platform from the gallery

To configure the integration of CrowdStrike Falcon Platform into Microsoft Entra ID, you need to add CrowdStrike Falcon Platform from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **CrowdStrike Falcon Platform** in the search box.
4. Select **CrowdStrike Falcon Platform** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for CrowdStrike Falcon Platform

Configure and test Microsoft Entra SSO with CrowdStrike Falcon Platform using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in CrowdStrike Falcon Platform.

To configure and test Microsoft Entra SSO with CrowdStrike Falcon Platform, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure CrowdStrike Falcon Platform SSO**- to configure the single sign-on settings on application side.
    1. **Create CrowdStrike Falcon Platform test user** - to have a counterpart of B.Simon in CrowdStrike Falcon Platform that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **CrowdStrike Falcon Platform** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** text box, type one of the following URLs:

    | Identifier |
    | --- |
    | `https://falcon.crowdstrike.com/saml/metadata` |
    | `https://falcon.us-2.crowdstrike.com/saml/metadata` |
    | `https://falcon.eu-1.crowdstrike.com/saml/metadata` |
    | `https://falcon.laggar.gcw.crowdstrike.com/saml/metadata` |
    |  |

    b. In the **Reply URL** text box, type one of the following URLs:

    | Reply URL |
    | --- |
    | `https://falcon.crowdstrike.com/saml/acs` |
    | `https://falcon.us-2.crowdstrike.com/saml/acs` |
    | `https://falcon.eu-1.crowdstrike.com/saml/acs` |
    | `https://falcon.laggar.gcw.crowdstrike.com/saml/acs` |
    |  |
6. Select **Set additional URLs** and perform the following step, if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type one of the following URLs:

    | Sign-on URL |
    | --- |
    | `https://falcon.crowdstrike.com/login/sso` |
    | `https://falcon.us-2.crowdstrike.com/login/sso` |
    | `https://falcon.eu-1.crowdstrike.com/login/sso` |
    | `https://falcon.laggar.gcw.crowdstrike.com/login/sso` |
    |  |
7. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure CrowdStrike Falcon Platform SSO

To configure single sign-on on **CrowdStrike Falcon Platform** side, you need to send the **App Federation Metadata Url** to [CrowdStrike Falcon Platform support team](mailto:support@crowdstrike.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create CrowdStrike Falcon Platform test user

In this section, you create a user called Britta Simon in CrowdStrike Falcon Platform. Work with [CrowdStrike Falcon Platform support team](mailto:support@crowdstrike.com) to add the users in the CrowdStrike Falcon Platform platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to CrowdStrike Falcon Platform Sign-on URL where you can initiate the login flow.
- Go to CrowdStrike Falcon Platform Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the CrowdStrike Falcon Platform for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the CrowdStrike Falcon Platform tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the CrowdStrike Falcon Platform for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
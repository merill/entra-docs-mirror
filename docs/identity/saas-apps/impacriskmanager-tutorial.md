---
layout: Conceptual
title: Configure IMPAC Risk Manager for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/impacriskmanager-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and IMPAC Risk Manager.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 33f222f4-b70c-9540-6440-f1d6f350162a
document_version_independent_id: 9583f3d2-ca5b-b107-b634-256695a780bf
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/impacriskmanager-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/impacriskmanager-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/impacriskmanager-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 3f10705f-8a90-eb2d-54a0-f234419e1412
---

# Configure IMPAC Risk Manager for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate IMPAC Risk Manager with Microsoft Entra ID. When you integrate IMPAC Risk Manager with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to IMPAC Risk Manager.
- Enable your users to be automatically signed-in to IMPAC Risk Manager with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- IMPAC Risk Manager single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- IMPAC Risk Manager supports **SP and IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add IMPAC Risk Manager from the gallery

To configure the integration of IMPAC Risk Manager into Microsoft Entra ID, you need to add IMPAC Risk Manager from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **IMPAC Risk Manager** in the search box.
4. Select **IMPAC Risk Manager** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for IMPAC Risk Manager

Configure and test Microsoft Entra SSO with IMPAC Risk Manager using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in IMPAC Risk Manager.

To configure and test Microsoft Entra SSO with IMPAC Risk Manager, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure IMPAC Risk Manager SSO**- to configure the single sign-on settings on application side.
    1. **Create IMPAC Risk Manager test user** - to have a counterpart of B.Simon in IMPAC Risk Manager that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **IMPAC Risk Manager** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, type a value provided by IMPAC.

    b. In the **Reply URL** text box, type a URL using one of the following patterns:

    | Environment | URL Pattern |
    | --- | --- |
    | For Production | `https://www.riskmanager.co.nz/DotNet/SSOv2/AssertionConsumerService.aspx?client=<ClientSuffix>` |
    | For Staging and Training | `https://staging.riskmanager.co.nz/DotNet/SSOv2/AssertionConsumerService.aspx?client=<ClientSuffix>` |
    | For Development | `https://dev.riskmanager.co.nz/DotNet/SSOv2/AssertionConsumerService.aspx?client=<ClientSuffix>` |
    | For QA | `https://QA.riskmanager.co.nz/DotNet/SSOv2/AssertionConsumerService.aspx?client=<ClientSuffix>` |
    | For Test | `https://test.riskmanager.co.nz/DotNet/SSOv2/AssertionConsumerService.aspx?client=<ClientSuffix>` |
    |  |  |
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using one of the following patterns:

    | Environment | URL Pattern |
    | --- | --- |
    | For Production | `https://www.riskmanager.co.nz/SSOv2/<ClientSuffix>` |
    | For Staging and Training | `https://staging.riskmanager.co.nz/SSOv2/<ClientSuffix>` |
    | For Development | `https://dev.riskmanager.co.nz/SSOv2/<ClientSuffix>` |
    | For QA | `https://QA.riskmanager.co.nz/SSOv2/<ClientSuffix>` |
    | For Test | `https://test.riskmanager.co.nz/SSOv2/<ClientSuffix>` |
    |  |  |

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [IMPAC Risk Manager Client support team](mailto:rmsupport@Impac.co.nz) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
8. On the **Set up IMPAC Risk Manager** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure IMPAC Risk Manager SSO

To configure single sign-on on **IMPAC Risk Manager** side, you need to send the downloaded **Certificate (Base64)** and appropriate copied URLs from the application configuration to [IMPAC Risk Manager support team](mailto:rmsupport@Impac.co.nz). They set this setting to have the SAML SSO connection set properly on both sides.

### Create IMPAC Risk Manager test user

In this section, you create a user called Britta Simon in IMPAC Risk Manager. Work with [IMPAC Risk Manager support team](mailto:rmsupport@Impac.co.nz) to add the users in the IMPAC Risk Manager platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to IMPAC Risk Manager Sign on URL where you can initiate the login flow.
- Go to IMPAC Risk Manager Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the IMPAC Risk Manager for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the IMPAC Risk Manager tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the IMPAC Risk Manager for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
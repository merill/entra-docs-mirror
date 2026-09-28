---
layout: Conceptual
title: Configure PoolParty Semantic Suite for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/poolparty-semantic-suite-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and PoolParty Semantic Suite.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 70d6c786-c537-ac2b-dbdc-baeeefa76f2f
document_version_independent_id: a42eae89-3236-7162-0f91-73b2d4946e12
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/poolparty-semantic-suite-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/poolparty-semantic-suite-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/poolparty-semantic-suite-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d25f3f64-951d-88ea-3810-a0f318f7462d
---

# Configure PoolParty Semantic Suite for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate PoolParty Semantic Suite with Microsoft Entra ID. When you integrate PoolParty Semantic Suite with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to PoolParty Semantic Suite.
- Enable your users to be automatically signed-in to PoolParty Semantic Suite with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- PoolParty Semantic Suite single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- PoolParty Semantic Suite supports **SP** initiated SSO

## Adding PoolParty Semantic Suite from the gallery

To configure the integration of PoolParty Semantic Suite into Microsoft Entra ID, you need to add PoolParty Semantic Suite from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **PoolParty Semantic Suite** in the search box.
4. Select **PoolParty Semantic Suite** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for PoolParty Semantic Suite

Configure and test Microsoft Entra SSO with PoolParty Semantic Suite using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in PoolParty Semantic Suite.

To configure and test Microsoft Entra SSO with PoolParty Semantic Suite, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure PoolParty Semantic Suite SSO**- to configure the single sign-on settings on application side.
    1. **Create PoolParty Semantic Suite test user** - to have a counterpart of B.Simon in PoolParty Semantic Suite that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **PoolParty Semantic Suite** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    a. In the **Sign-on URL** text box, type a URL using the following pattern: `https://<CustomerName>.poolparty.biz/PoolParty/`

    b. In the **Identifier** box, type a URL using the following pattern: `https://<CustomerName>.poolparty.biz/<ID>`

    c. In the **Reply URL** text box, type a URL using the following pattern: `https://<CustomerName>.poolparty.biz/<ID>`

    Note

    These values aren't real. Update these values with the actual Sign-On URL, Identifier and Reply URL. Contact [PoolParty Semantic Suite Client support team](mailto:support@poolparty.biz) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up PoolParty Semantic Suite** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure PoolParty Semantic Suite SSO

To configure single sign-on on **PoolParty Semantic Suite** side, you need to send the downloaded **Federation Metadata XML** and appropriate copied URLs from the application configuration to [PoolParty Semantic Suite support team](mailto:support@poolparty.biz). They set this setting to have the SAML SSO connection set properly on both sides.

### Create PoolParty Semantic Suite test user

In this section, you create a user called Britta Simon in PoolParty Semantic Suite. Work with [PoolParty Semantic Suite support team](mailto:support@poolparty.biz) to add the users in the PoolParty Semantic Suite platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to PoolParty Semantic Suite Sign-on URL where you can initiate the login flow.
- Go to PoolParty Semantic Suite Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the PoolParty Semantic Suite tile in the My Apps, this option redirects to PoolParty Semantic Suite Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
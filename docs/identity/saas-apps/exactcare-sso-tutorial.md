---
layout: Conceptual
title: Configure ExactCare SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/exactcare-sso-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and ExactCare SSO.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 19f857d0-8015-ae79-995d-bf0e886548b5
document_version_independent_id: 55d392cb-2c35-815d-8760-237117d959b3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/exactcare-sso-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/exactcare-sso-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/exactcare-sso-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 0cc124ae-d668-dc5f-054a-dcc4a2fabb12
---

# Configure ExactCare SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate ExactCare SSO with Microsoft Entra ID. When you integrate ExactCare SSO with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to ExactCare SSO.
- Enable your users to be automatically signed-in to ExactCare SSO with their Microsoft Entra accounts.
- Manage your accounts in one central location.

To learn more about SaaS app integration with Microsoft Entra ID, see [What is application access and single sign-on with Microsoft Entra ID](../enterprise-apps/what-is-single-sign-on).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- ExactCare SSO single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- ExactCare SSO supports **SP** initiated SSO

## Adding ExactCare SSO from the gallery

To configure the integration of ExactCare SSO into Microsoft Entra ID, you need to add ExactCare SSO from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **ExactCare SSO** in the search box.
4. Select **ExactCare SSO** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra single sign-on for ExactCare SSO

Configure and test Microsoft Entra SSO with ExactCare SSO using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in ExactCare SSO.

To configure and test Microsoft Entra SSO with ExactCare SSO, complete the following building blocks:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    - **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    - **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure ExactCare SSO**- to configure the single sign-on settings on application side.
    - **Create ExactCare SSO test user** - to have a counterpart of B.Simon in ExactCare SSO that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **ExactCare SSO** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the edit/pen icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    a. In the **Sign on URL** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.exactcarepharmacy.com/self-schedule/api/saml-response?idp=azure-sp`

    b. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.exactcarepharmacy.com`

    Note

    These values aren't real. Update these values with the actual Sign on URL and Identifier. Contact [ExactCare SSO Client support team](mailto:help@exactcarepharmacy.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up ExactCare SSO** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure ExactCare SSO

To configure single sign-on on **ExactCare SSO** side, you need to send the downloaded **Federation Metadata XML** and appropriate copied URLs from the application configuration to [ExactCare SSO support team](mailto:help@exactcarepharmacy.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create ExactCare SSO test user

In this section, you create a user called B.Simon in ExactCare SSO. Work with [ExactCare SSO support team](mailto:help@exactcarepharmacy.com) to add the users in the ExactCare SSO platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration using the Access Panel.

When you select the ExactCare SSO tile in the Access Panel, you should be automatically signed in to the ExactCare SSO for which you set up SSO. For more information about the Access Panel, see [Introduction to the Access Panel](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
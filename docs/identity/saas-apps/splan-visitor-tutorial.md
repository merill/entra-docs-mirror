---
layout: Conceptual
title: Configure Splan Visitor for Single sign-on in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/splan-visitor-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Splan Visitor.
ms.topic: how-to
ms.date: 2026-06-11T00:00:00.0000000Z
locale: en-us
document_id: fa477b40-d1bb-55a8-df12-ea67b166a9ee
document_version_independent_id: 2656b729-5493-8fcb-2d3f-06f2373cc8c4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/splan-visitor-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/splan-visitor-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/splan-visitor-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 3c439b44-f859-264c-08ee-9ac227076304
---

# Configure Splan Visitor for Single sign-on in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Splan Visitor with Microsoft Entra ID. When you integrate Splan Visitor with Microsoft Entra ID, you can:

- Use Microsoft Entra ID to control who has access to Splan Visitor.
- Enable users to be automatically signed in to Splan Visitor with their Microsoft Entra accounts.
- Manage your accounts in one central location, the Azure portal.

Splan Visitor is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A Splan Visitor single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Splan Visitor supports IdP-initiated SSO.

## Add Splan Visitor from the gallery

To configure the integration of Splan Visitor into Microsoft Entra ID, add Splan Visitor from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, enter **Splan Visitor** in the search box.
4. Select **Splan Visitor** from the results panel, and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Splan Visitor

Configure and test Microsoft Entra SSO with Splan Visitor by using a test user named **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Splan Visitor.

To configure and test Microsoft Entra SSO with Splan Visitor, perform the following steps:

1. **Configure Microsoft Entra SSO**to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** to test Microsoft Entra single sign-on with test user B.Simon.
    2. **Assign the Microsoft Entra test user** to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Splan Visitor SSO**to configure the single sign-on settings with Splan Visitor.
    1. **Create a Splan Visitor test user** to have a counterpart of B.Simon in Splan Visitor that's linked to the Microsoft Entra representation of user.
3. **Test SSO** to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Azure portal:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Splan Visitor** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the **pencil** icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot highlighting the edit/pen icon for Basic SAML Configuration.](common/edit-urls.png)
5. In the **Basic SAML Configuration** section, the application is preconfigured and the necessary URLs are prepopulated with Azure. Select the **Save** button to save the configuration.
6. On the **Set up Single Sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML**. Select **Download** to download the certificate and save it to your computer.

    ![Screenshot highlighting the Federation Metadata XML download link.](common/metadataxml.png)
7. On the **Set up Splan Visitor** section, copy the appropriate URL or URLs based on your requirement.

    ![Screenshot highlighting the configuration URLs section.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Splan Visitor SSO

To configure single sign-on with Splan Visitor, send the **Federation Metadata XML** that you downloaded and appropriate copied URLs to the [Splan Visitor support team](mailto:support@splan.com). This ensures that the SAML SSO connection is set properly on both sides.

### Create a Splan Visitor test user

Create a test user named **Britta Simon** in Splan Visitor. Work with the [Splan Visitor support team](mailto:support@splan.com) to add the user to Splan Visitor. You must create and activate the user before you use single sign-on.

## Test SSO

Test your Microsoft Entra single sign-on configuration with one of the following options:

- **Azure portal**: Select **Test this application** to automatically sign in to the Splan Visitor for which you set up SSO.
- **Microsoft My Apps portal**: Select the **Splan Visitor** tile to automatically sign in to the Splan Visitor for which you set up SSO. For more information about the My Apps portal, see [Sign in and start apps from the My Apps portal](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
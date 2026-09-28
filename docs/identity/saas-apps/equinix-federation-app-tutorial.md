---
layout: Conceptual
title: Configure Equinix Federation App for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/equinix-federation-app-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Equinix Federation App.
ms.topic: how-to
ms.date: 2024-06-19T00:00:00.0000000Z
locale: en-us
document_id: 3d1a17b9-4e62-6e92-4117-08f02b6838c5
document_version_independent_id: e1afcfae-edf1-f133-7d45-d477a84fe82b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/equinix-federation-app-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/equinix-federation-app-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/equinix-federation-app-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 9a1bddc7-e224-98bf-706c-f4d01237e50b
---

# Configure Equinix Federation App for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Equinix Federation App with Microsoft Entra ID. When you integrate Equinix Federation App with Microsoft Entra ID, you can do the following:

- Control in Microsoft Entra ID who has access to Equinix Federation App.
- Enable your users to be automatically signed-in to Equinix Federation App with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Equinix Federation App single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Equinix Federation App supports **SP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Adding Equinix Federation App from the gallery

To configure the integration of Equinix Federation App into Microsoft Entra ID, you need to add Equinix Federation App from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Equinix Federation App** in the search box.
4. Select **Equinix Federation App** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Equinix Federation App

Configure and test Microsoft Entra SSO with Equinix Federation App using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Equinix Federation App.

To configure and test Microsoft Entra SSO with Equinix Federation App, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Equinix Federation App SSO**- to configure the single sign-on settings on application side.
    1. **Create Equinix Federation App test user** - to have a counterpart of B.Simon in Equinix Federation App that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Equinix Federation App** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following step:

    In the **Sign on URL** text box, type a URL using the following pattern: `https://<customerprefix>customerportal.equinix.com`

    Note

    The Sign on URL value isn't real. Update the value with the actual Sign on URL. Contact [Equinix Federation App Client support team](mailto:FederationSupport@equinix.com) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up Equinix Federation App** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Equinix Federation App SSO

To configure Single Sign-On on **Equinix Federation App** side, please follow the [link](https://docs.equinix.com).

### Create Equinix Federation App test user

In this section, you create a user called Britta Simon in Equinix Federation App. Work with [Equinix Federation App support team](mailto:FederationSupport@equinix.com) to add the users in the Equinix Federation App platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

Go to Equinix Federation App Sign-on URL directly, and initiate the login flow from there.

Note

If you attempt to test your Azure application by using the **Test this application** link or by selecting the Equinix Federation App tile, it doesn't work, as that's IdP-initiated SSO, which Equinix doesn't support by default. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
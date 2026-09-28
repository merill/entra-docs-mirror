---
layout: Conceptual
title: Configure Netop Portal for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/netop-portal-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Netop Portal.
ms.topic: how-to
ms.date: 2026-06-09T00:00:00.0000000Z
locale: en-us
document_id: 6eb3df78-da19-07ed-67ff-f2c72d63bf64
document_version_independent_id: c731d90d-8132-27c4-b4ff-ccad70c3ec51
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/netop-portal-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/netop-portal-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/netop-portal-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 965643b5-b346-f8ed-5951-727c2a83bc6b
---

# Configure Netop Portal for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Netop Portal with Microsoft Entra ID. When you integrate Netop Portal with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Netop Portal.
- Enable your users to be automatically signed-in to Netop Portal with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Netop Portal is available in the following [national cloud deployments](/en-us/graph/deployments).

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

- Netop Portal single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Netop Portal supports **IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Netop Portal from the gallery

To configure the integration of Netop Portal into Microsoft Entra ID, you need to add Netop Portal from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Netop Portal** in the search box.
4. Select **Netop Portal** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Netop Portal

Configure and test Microsoft Entra SSO with Netop Portal using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Netop Portal.

To configure and test Microsoft Entra SSO with Netop Portal, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Netop Portal SSO**- to configure the single sign-on settings on application side.
    1. **Create Netop Portal test user** - to have a counterpart of B.Simon in Netop Portal that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Netop Portal** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set-up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, the application is pre-configured in **IDP** initiated mode and the necessary URLs are already pre-populated with Azure. The user needs to save the configuration by selecting the **Save** button.
6. Netop Portal application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/edit-attribute.png)
7. In addition to above, Netop Portal application expects few more attributes to be passed back in SAML response, which are shown below. These attributes are also pre populated but you can review them as per your requirement.

    | Name | Source Attribute |
    | --- | --- |
    | NRC-ACCOUNT-ID | "adfs-demo" |
    | NRC-EMAIL | user.userprincipalname |
    | NRC-GIVEN-NAME | user.givenname |
    | NRC-SURNAME | user.surname |
    | NRC-USERNAME | user.userprincipalname |
    | nameidentifier | user.userprincipalname |
    |  |  |
8. On the **Set-up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
9. On the **Set up Netop Portal** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Netop Portal SSO

To configure single sign-on on **Netop Portal** side, you need to the downloaded **Federation Metadata XML** and the Login URL from Azure portal. Follow the instructions in Step 3 of the documentation [here](https://support.netop.com/support/solutions/articles/205000041622-adfs-and-azure-ad-integration) to configure NetOp Portal for Microsoft Entra authentication.

### Create Netop Portal test user

In this section, you create a user called Britta Simon in Netop Portal. Work with [Netop Portal support team](mailto:support@netop.com) to add the users in the Netop Portal platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the Netop Portal for which you set up the SSO.
- You can use Microsoft My Apps. When you select the Netop Portal tile in the My Apps, you should be automatically signed in to the Netop Portal for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
---
layout: Conceptual
title: Configure Reprints Desk - Article Galaxy for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/reprints-desk-article-galaxy-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Reprints Desk - Article Galaxy.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: cac39259-898f-09ab-becd-f2e069ba07eb
document_version_independent_id: 3c3ff079-6392-87eb-986c-2e79e2ba193f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/reprints-desk-article-galaxy-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/reprints-desk-article-galaxy-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/reprints-desk-article-galaxy-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 032fed2c-9f95-964a-b548-d7160c113b14
---

# Configure Reprints Desk - Article Galaxy for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Reprints Desk - Article Galaxy with Microsoft Entra ID. When you integrate Reprints Desk - Article Galaxy with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Reprints Desk - Article Galaxy.
- Enable your users to be automatically signed-in to Reprints Desk - Article Galaxy with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Reprints Desk - Article Galaxy single sign-on (SSO) enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Reprints Desk - Article Galaxy supports **IDP** initiated SSO.
- Reprints Desk - Article Galaxy supports **Just In Time** user provisioning.

## Add Reprints Desk - Article Galaxy from the gallery

To configure the integration of Reprints Desk - Article Galaxy into Microsoft Entra ID, you need to add Reprints Desk - Article Galaxy from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Reprints Desk - Article Galaxy** in the search box.
4. Select **Reprints Desk - Article Galaxy** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Reprints Desk - Article Galaxy

Configure and test Microsoft Entra SSO with Reprints Desk - Article Galaxy using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Reprints Desk - Article Galaxy.

To configure and test Microsoft Entra SSO with Reprints Desk - Article Galaxy, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Reprints Desk - Article Galaxy SSO**- to configure the single sign-on settings on application side.
    1. **Create Reprints Desk - Article Galaxy test user** - to have a counterpart of B.Simon in Reprints Desk - Article Galaxy that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Reprints Desk - Article Galaxy** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic S A M L Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, the application is pre-configured and the necessary URLs are already pre-populated with Azure. The user needs to save the configuration by selecting the **Save** button.
6. Reprints Desk - Article Galaxy application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows the image of Reprints Desk application.](common/default-attributes.png)
7. In addition to above, Reprints Desk - Article Galaxy application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | firstname | user.givenname |
    | lastname | user.surname |
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)
9. On the **Set up Reprints Desk - Article Galaxy** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration appropriate U R L.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Reprints Desk - Article Galaxy SSO

To configure single sign-on on **Reprints Desk - Article Galaxy** side, you need to send the downloaded **Federation Metadata XML** and appropriate copied URLs from the application configuration to [Reprints Desk - Article Galaxy support team](mailto:customersupport@reprintsdesk.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Reprints Desk - Article Galaxy test user

In this section, a user called B.Simon is created in Reprints Desk - Article Galaxy. Reprints Desk - Article Galaxy supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Reprints Desk - Article Galaxy, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the Reprints Desk - Article Galaxy for which you set up the SSO.
- You can use Microsoft My Apps. When you select the Reprints Desk - Article Galaxy tile in the My Apps, you should be automatically signed in to the Reprints Desk - Article Galaxy for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
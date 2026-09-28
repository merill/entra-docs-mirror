---
layout: Conceptual
title: Configure Datto File Protection Single Sign On for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/datto-file-protection-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Datto File Protection Single Sign On.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: c0f70f95-1fc1-8338-17d1-d083952a9cf9
document_version_independent_id: d97461de-4d5e-bd04-3537-1b3a1fde3353
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/datto-file-protection-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/datto-file-protection-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/datto-file-protection-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c467d489-9fff-8663-8005-984a1068ab5e
---

# Configure Datto File Protection Single Sign On for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Datto File Protection Single Sign On with Microsoft Entra ID. When you integrate Datto File Protection Single Sign On with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Datto File Protection Single Sign On.
- Enable your users to be automatically signed-in to Datto File Protection Single Sign On with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Datto File Protection Single Sign On enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Datto File Protection Single Sign On supports **SP** and **IDP** initiated SSO.

## Add Datto File Protection Single Sign On from the gallery

To configure the integration of Datto File Protection Single Sign On into Microsoft Entra ID, you need to add Datto File Protection Single Sign On from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Datto File Protection Single Sign On** in the search box.
4. Select **Datto File Protection Single Sign On** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Datto File Protection Single Sign On

Configure and test Microsoft Entra SSO with Datto File Protection Single Sign On using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Datto File Protection Single Sign On.

To configure and test Microsoft Entra SSO with Datto File Protection Single Sign On, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Datto File Protection Single Sign On SSO**- to configure the single sign-on settings on application side.
    1. **Create Datto File Protection Single Sign On test user** - to have a counterpart of B.Simon in Datto File Protection Single Sign On that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Datto File Protection Single Sign On** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, the user doesn't have to perform any step as the app is already pre-integrated with Azure.
6. On the **Basic SAML Configuration** section, if you wish to configure the application in **SP** initiated mode then perform the following steps:

    a. In the **Identifier** textbox, type the URL: `https://saml.fileprotection.datto.com/singlesignon/saml/metadata`

    b. In the **Reply URL** textbox, type the URL: `https://saml.fileprotection.datto.com/singlesignon/saml/SSO`

    c. In the **Sign on URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.fileprotection.datto.com`

    Note

    This value isn't real. Update this value with the actual Sign on URL. Contact [Datto File Protection Single Sign On Client support team](mailto:ms-sso-support@ot.soonr.com) to get this value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Datto File Protection Single Sign On SSO

To configure single sign-on on **Datto File Protection Single Sign On** side, you need to send the **App Federation Metadata Url** to [Datto File Protection Single Sign On support team](mailto:ms-sso-support@ot.soonr.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Datto File Protection Single Sign On test user

In this section, you create a user called Britta Simon in Datto File Protection Single Sign On. Work with [Datto File Protection Single Sign On support team](mailto:ms-sso-support@ot.soonr.com) to add the users in the Datto File Protection Single Sign On platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Datto File Protection Single Sign On Sign on URL where you can initiate the login flow.
- Go to Datto File Protection Single Sign On Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Datto File Protection Single Sign On for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Datto File Protection Single Sign On tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Datto File Protection Single Sign On for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
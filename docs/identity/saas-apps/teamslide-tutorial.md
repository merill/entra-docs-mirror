---
layout: Conceptual
title: Configure TeamSlide for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/teamslide-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and TeamSlide.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: a5baa1ba-8f01-0cb2-fc87-858148e2b108
document_version_independent_id: 12fa40f7-dcfe-74ce-6a13-2815f750a406
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/teamslide-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/teamslide-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/teamslide-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c6fa7c6d-4b30-5545-9965-4ad9c6bb8cbe
---

# Configure TeamSlide for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate TeamSlide with Microsoft Entra ID. When you integrate TeamSlide with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to TeamSlide.
- Enable your users to be automatically signed-in to TeamSlide with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- TeamSlide single sign-on (SSO) enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- TeamSlide supports **SP** initiated SSO.
- TeamSlide supports **Just In Time** user provisioning.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add TeamSlide from the gallery

To configure the integration of TeamSlide into Microsoft Entra ID, you need to add TeamSlide from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **TeamSlide** in the search box.
4. Select **TeamSlide** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for TeamSlide

Configure and test Microsoft Entra SSO with TeamSlide using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in TeamSlide.

To configure and test Microsoft Entra SSO with TeamSlide, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure TeamSlide SSO**- to configure the single sign-on settings on application side.
    1. **Create TeamSlide test user** - to have a counterpart of B.Simon in TeamSlide that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **TeamSlide** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

![Screenshot shows to edit Basic SAML Configuration.](common/edit-urls.png)

1. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type the URL: `https://www.teamslide.io/AuthServices/`

    b. In the **Reply URL** textbox, type the URL: `https://www.teamslide.io/AuthServices/Acs`

    c. In the **Sign-on URL** text box, type a URL using the following pattern: `https://www.teamslide.io/ChooseSso?domain=<CustomerDomain>`

    Note

    The Sign-on URL isn't real. Update the value with the actual Sign-on URL. Contact [TeamSlide Client support team](mailto:support@aploris.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
2. TeamSlide application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot showing the list of default attributes.](common/default-attributes.png)
3. In addition to above, TeamSlide application expects few more attributes to be passed back in SAML response, which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | displayname | user.displayname |
    | groups | user.groups [All] |
4. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![Screenshot showing the Certificate download link](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure TeamSlide SSO

1. Log in to your TeamSlide company site as an administrator.
2. Go to **Global Settings** &gt; **SSO Settings** tab.
3. In the **Single sign-on settings** page, perform the following steps:

    ![Screenshot that shows the Configuration Settings.](media/teamslide-tutorial/settings.png)

    a. In the **Entity ID** textbox, paste the **Microsoft Entra Identifier** value which you copied previously.

    b. In the **Sign-On URL** textbox, paste the **Login URL** value which you copied previously.

    c. In the **Metadata location** textbox, paste the **App Federation Metadata Url** value which you copied previously.

    d. Select **Save Changes**.

### Create TeamSlide test user

In this section, a user called B.Simon is created in TeamSlide. TeamSlide supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in TeamSlide, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to TeamSlide Sign-on URL where you can initiate the login flow.
- Go to TeamSlide Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the TeamSlide tile in the My Apps, this option redirects to TeamSlide Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
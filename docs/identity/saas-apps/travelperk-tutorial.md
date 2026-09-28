---
layout: Conceptual
title: Configure TravelPerk for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/travelperk-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and TravelPerk.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 38576bb0-8f26-9727-b49c-3271d64f1905
document_version_independent_id: 5bc06b0a-7e25-a715-bf6a-1b1bd2ea5303
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/travelperk-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/travelperk-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/travelperk-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 63658738-7cee-d225-6389-15a3906f395c
---

# Configure TravelPerk for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate TravelPerk with Microsoft Entra ID. When you integrate TravelPerk with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to TravelPerk.
- Enable your users to be automatically signed-in to TravelPerk with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A TravelPerk account with Premium subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- TravelPerk supports **SP** initiated SSO.
- TravelPerk supports **Just In Time** user provisioning.
- TravelPerk supports [Automated user provisioning](travelperk-provisioning-tutorial).

## Add TravelPerk from the gallery

To configure the integration of TravelPerk into Microsoft Entra ID, you need to add TravelPerk from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **TravelPerk** in the search box.
4. Select **TravelPerk** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for TravelPerk

Configure and test Microsoft Entra SSO with TravelPerk using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in TravelPerk.

To configure and test Microsoft Entra SSO with TravelPerk, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure TravelPerk SSO**- to configure the single sign-on settings on application side.
    1. **Create TravelPerk test user** - to have a counterpart of B.Simon in TravelPerk that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **TravelPerk** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic S A M L Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<COMPANY>.travelperk.com/accounts/saml2/metadata/<APPLICATION_ID>`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<COMPANY>.travelperk.com/accounts/saml2/callback/<APPLICATION_ID>/?acs`

    c. In the **Sign on URL** text box, type a URL using the following pattern: `https://<COMPANY>.travelperk.com/`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign on URL. The values can be found inside your TravelPerk account: go to **Company Settings** &gt; **Integrations** &gt; **Single Sign On**. For assistance, visit the [TravelPerk helpcenter](https://support.travelperk.com/hc/articles/360052450271-How-can-I-setup-SSO-for-Azure-SAML).
6. Your TravelPerk application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes. In the default mapping, **emailaddress** is mapped with **user.mail**. However, the TravelPerk application expects **emailaddress** to be mapped with **user.userprincipalname**. For TravelPerk, you must edit the attribute mapping: select the **Edit** icon, and then change the attribute mapping. To edit an attribute, just select the attribute to open edit mode.

    ![Screenshot shows the image of TravelPerk application.](common/default-attributes.png)
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)
8. On the **Set up TravelPerk** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration appropriate U R L.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure TravelPerk SSO

To configure single sign-on on **TravelPerk** side, you need to set up the integration in the TravelPerk app.

1. Go to https://app.travelperk.com as an Admin user, and under **Account Settings** &gt; **Integrations** open **Single sign-on (SSO)**.
2. Select **SAML** as the option, and select **New Integration** then perform the following steps:

    a. In the **IdP entity ID** textbox, paste the **Microsoft Entra Identifier** value which you copied previously.

    b. In the **IdP SSO service URL** textbox, paste the **Login URL** value which you copied previously.

    c. In the **IdP x509 cert** textbox, paste the **Federation Metadata XML** file (Without the X509Certificate tag).

    d. Save and proceed with the testing.

### Create TravelPerk test user

In this section, a user called B.Simon is created in TravelPerk. TravelPerk supports just-in-time provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in TravelPerk, a new one is created when you attempt to access TravelPerk.

TravelPerk also supports automatic user provisioning, you can find more details [here](travelperk-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to TravelPerk Sign-on URL where you can initiate the login flow.
- Go to TravelPerk Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the TravelPerk tile in the My Apps, this option redirects to TravelPerk Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
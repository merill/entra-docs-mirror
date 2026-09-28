---
layout: Conceptual
title: Configure Pluto for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/pluto-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Pluto.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 98e09247-35af-9eba-6e02-4f78099d2830
document_version_independent_id: 47ec90a4-86bc-2e6f-e862-c0e2d9c30a0c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/pluto-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/pluto-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/pluto-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: bb51838f-7d78-8e8f-d375-fa494202501f
---

# Configure Pluto for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Pluto with Microsoft Entra ID. When you integrate Pluto with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Pluto.
- Enable your users to be automatically signed-in to Pluto with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Pluto single sign-on (SSO) enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Pluto supports **SP** initiated SSO.
- Pluto supports **Just In Time** user provisioning.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Pluto from the gallery

To configure the integration of Pluto into Microsoft Entra ID, you need to add Pluto from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Pluto** in the search box.
4. Select **Pluto** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Pluto

Configure and test Microsoft Entra SSO with Pluto using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Pluto.

To configure and test Microsoft Entra SSO with Pluto, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Pluto SSO**- to configure the single sign-on settings on application side.
    1. **Create Pluto test user** - to have a counterpart of B.Simon in Pluto that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Pluto** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** text box, type the URL: `https://api.pluto.bio`

    b. In the **Reply URL** text box, type the URL: `https://api.pluto.bio/auth/social/complete/saml/`

    c. In the **Sign-on URL** text box, type a URL using the following pattern: `https://pluto.bio/login/<organization-shortname>`

    Note

    This value isn't real. Update this value with the actual Sign-on URL. Contact [Pluto Client support team](mailto:support@pluto.bio) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. Pluto application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/edit-attribute.png)
7. In addition to above, Pluto application expects few more attributes to be passed back in SAML response, which are shown below. These attributes are also pre populated but you can review them as per your requirement.

    | Name | Source Attribute |
    | --- | --- |
    | email | user.mail |
    | first\_name | user.givenname |
    | last\_name | user.surname |
8. On the **Set-up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
9. On the **Set up Pluto** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Pluto SSO

To configure single sign-on on **Pluto** side, you need to send the downloaded **Federation Metadata XML** and appropriate copied URLs from the application configuration to [Pluto support team](mailto:support@pluto.bio). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Pluto test user

In this section, a user called Britta Simon is created in Pluto. Pluto supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Pluto, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Pluto Sign-on URL where you can initiate the login flow.
- Go to Pluto Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Pluto tile in the My Apps, this option redirects to Pluto Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
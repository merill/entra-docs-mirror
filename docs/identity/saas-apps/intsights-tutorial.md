---
layout: Conceptual
title: Configure IntSights for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/intsights-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and IntSights.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 5982606a-4f02-96af-1e7d-740c241957af
document_version_independent_id: d093db8f-893f-1171-bf75-2911f0a77f69
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/intsights-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/intsights-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/intsights-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7d1bcc33-9314-22dc-edb6-3935c97f9e86
---

# Configure IntSights for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate IntSights with Microsoft Entra ID. When you integrate IntSights with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to IntSights.
- Enable your users to be automatically signed-in to IntSights with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- IntSights single sign-on (SSO) enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- IntSights supports **SP and IDP** initiated SSO.
- IntSights supports **Just In Time** user provisioning.

## Add IntSights from the gallery

To configure the integration of IntSights into Microsoft Entra ID, you need to add IntSights from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **IntSights** in the search box.
4. Select **IntSights** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for IntSights

Configure and test Microsoft Entra SSO with IntSights using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in IntSights.

To configure and test Microsoft Entra SSO with IntSights, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure IntSights SSO**- to configure the single sign-on settings on application side.
    1. **Create IntSights test user** - to have a counterpart of B.Simon in IntSights that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **IntSights** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.ti.insight.rapid7.com/auth/saml-callback/azure`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.ti.insight.rapid7.com/auth/saml-callback/azure`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.ti.insight.rapid7.com/auth/saml-callback/azure`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign on URL. Contact [IntSights Client support team](mailto:supportteam@intsights.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. IntSights application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
8. In addition to above, IntSights application expects few more attributes to be passed back in SAML response, which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | firstName | user.givenname |
    | lastName | user.surname |
    | intsightsAccountId | &lt; intsightsAccountId &gt; |
    | intsightsRole | &lt; intsightsRole &gt; |

    Note

    **intsightsAccountId** and **intsightsRole** are the optional claims which aren't added by default and are to be added manually only when **Just In Time** user provisioning is enabled.
9. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
10. On the **Set up IntSights** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure IntSights SSO

To configure single sign-on on **IntSights** side, you need to send the downloaded **Certificate (Base64)** and appropriate copied URLs from the application configuration to [IntSights support team](mailto:supportteam@intsights.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create IntSights test user

In this section, a user called B.Simon is created in IntSights. IntSights supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in IntSights, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to IntSights Sign on URL where you can initiate the login flow.
- Go to IntSights Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the IntSights for which you set up the SSO

You can also use Microsoft Access Panel to test the application in any mode. When you select the IntSights tile in the Access Panel, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the IntSights for which you set up the SSO. For more information about the Access Panel, see [Introduction to the Access Panel](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
---
layout: Conceptual
title: Configure Dotcom-Monitor for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/dotcom-monitor-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Dotcom-Monitor.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 0a649173-1910-262a-d1cf-306e4ff5f41a
document_version_independent_id: 2726fde6-bd1b-98b3-3f2c-2717c4e11f6a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/dotcom-monitor-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/dotcom-monitor-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/dotcom-monitor-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ecd6a7ef-ebf5-939f-dc45-34f2bdcdf0dd
---

# Configure Dotcom-Monitor for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Dotcom-Monitor with Microsoft Entra ID. When you integrate Dotcom-Monitor with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Dotcom-Monitor.
- Enable your users to be automatically signed-in to Dotcom-Monitor with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Dotcom-Monitor single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Dotcom-Monitor supports **SP** initiated SSO
- Dotcom-Monitor supports **Just In Time** user provisioning

## Adding Dotcom-Monitor from the gallery

To configure the integration of Dotcom-Monitor into Microsoft Entra ID, you need to add Dotcom-Monitor from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Dotcom-Monitor** in the search box.
4. Select **Dotcom-Monitor** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Dotcom-Monitor

Configure and test Microsoft Entra SSO with Dotcom-Monitor using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Dotcom-Monitor.

To configure and test Microsoft Entra SSO with Dotcom-Monitor, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Dotcom Monitor SSO**- to configure the single sign-on settings on application side.
    1. **Create Dotcom Monitor test user** - to have a counterpart of B.Simon in Dotcom-Monitor that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Dotcom-Monitor** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://userauth.dotcom-monitor.com/Login.ashx?cidp=<CUSTOM_GUID>`

    Note

    The value isn't real. Update the value with the actual Sign-On URL. Contact [Dotcom-Monitor Client support team](mailto:vadimm@dana-net.com) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. Dotcom-Monitor application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
7. In addition to above, Dotcom-Monitor application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | Roles | user.assignedroles |

    Note

    You can find more guidance [here](../../identity-platform/howto-add-app-roles-in-apps#app-roles-ui) on how to create custom roles in Microsoft Entra ID.
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
9. On the **Set up Dotcom-Monitor** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Dotcom-Monitor SSO

To configure single sign-on on **Dotcom-Monitor** side, you need to send the downloaded **Federation Metadata XML** and appropriate copied URLs from the application configuration to [Dotcom-Monitor support team](mailto:vadimm@dana-net.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Dotcom-Monitor test user

In this section, a user called B.Simon is created in Dotcom-Monitor. Dotcom-Monitor supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Dotcom-Monitor, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Dotcom-Monitor Sign-on URL where you can initiate the login flow.
- Go to Dotcom-Monitor Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Dotcom-Monitor tile in the My Apps, this option redirects to Dotcom-Monitor Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
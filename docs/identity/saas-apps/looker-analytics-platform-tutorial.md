---
layout: Conceptual
title: Configure Looker Analytics Platform for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/looker-analytics-platform-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Looker Analytics Platform.
ms.topic: how-to
ms.date: 2026-06-09T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 393431cb-d443-013c-28a0-232cbacba42f
document_version_independent_id: f5a6ef16-4a1b-57e8-9e84-e0f9249269af
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/looker-analytics-platform-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/looker-analytics-platform-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/looker-analytics-platform-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: dfcd55bc-be78-a113-2870-33a6e98d2314
---

# Configure Looker Analytics Platform for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Looker Analytics Platform with Microsoft Entra ID. When you integrate Looker Analytics Platform with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Looker Analytics Platform.
- Enable your users to be automatically signed-in to Looker Analytics Platform with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Looker Analytics Platform is available in the following [national cloud deployments](/en-us/graph/deployments).

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

- Looker Analytics Platform single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Looker Analytics Platform supports **SP and IDP** initiated SSO
- Looker Analytics Platform supports **Just In Time** user provisioning

## Adding Looker Analytics Platform from the gallery

To configure the integration of Looker Analytics Platform into Microsoft Entra ID, you need to add Looker Analytics Platform from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Looker Analytics Platform** in the search box.
4. Select **Looker Analytics Platform** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Looker Analytics Platform

Configure and test Microsoft Entra SSO with Looker Analytics Platform using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Looker Analytics Platform.

To configure and test Microsoft Entra SSO with Looker Analytics Platform, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Looker Analytics Platform SSO**- to configure the single sign-on settings on application side.
    1. **Create Looker Analytics Platform test user** - to have a counterpart of B.Simon in Looker Analytics Platform that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Looker Analytics Platform** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the edit/pen icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, enter the values for the following fields:

    a. In the **SP Entity/IdP Audience** text box, type a URL using the following pattern: `<SPN>_looker`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.looker.com/samlcallback`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.looker.com`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [Looker Analytics Platform Client support team](mailto:support@looker.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
8. On the **Set up Looker Analytics Platform** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Looker Analytics Platform SSO

1. In a different web browser window, sign into Looker Analytics Platform website as an administrator.
2. Go to the **Admin** &gt; **Authentication** &gt; **SAML**

    ![screenshot for SAML option](media/looker-analytics-platform-tutorial/admin.png)
3. Paste the **Federation Metadata** information that you copied in to the **IDP Metadata** textbox and select **Load**.

    ![screenshot for metadata upload](media/looker-analytics-platform-tutorial/metadata.png)
4. Perform the following steps in the **User Attribute Settings** section.

    ![screenshot for User Attribute Settings](media/looker-analytics-platform-tutorial/user-attribute-settings.png)

    a. Add the following value in the Email Attr field: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`

    b. Add the following value to the Fname Attr field: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`

    c. Add the following value to the Lname Attr field: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`

    d. In the **Test User Authentication**, select **Test SAML Authentication**. If the page that loads say “Server Response Successfully Validated”, you have successfully set up the instance for SAML integration.

    e. In **Save and Apply Settings**, Check the box **I have confirmed the configuration above and want to enable applying it globally**.

    f. Select the **Update Settings** button.

### Create Looker Analytics Platform test user

In this section, a user called Britta Simon is created in Looker Analytics Platform. Looker Analytics Platform supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Looker Analytics Platform, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Looker Analytics Platform Sign-on URL where you can initiate the login flow.
- Go to Looker Analytics Platform Sign on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Looker Analytics Platform for which you set up the SSO

You can also use Microsoft Access Panel to test the application in any mode. When you select the Looker Analytics Platform tile in the Access Panel, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Looker Analytics Platform for which you set up the SSO. For more information about the Access Panel, see [Introduction to the Access Panel](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
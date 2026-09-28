---
layout: Conceptual
title: Configure Samsara for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/samsara-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Samsara.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: ee877713-e655-ea46-6f09-218044f4bafb
document_version_independent_id: 704aedb4-963c-e0f6-627c-74e848709e80
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/samsara-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/samsara-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/samsara-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d98d725d-9057-fd26-a64d-1201602f8517
---

# Configure Samsara for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Samsara with Microsoft Entra ID. When you integrate Samsara with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Samsara.
- Enable your users to be automatically signed-in to Samsara with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Samsara single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Samsara supports **SP** and **IDP** initiated SSO.
- Samsara supports **Just In Time** user provisioning.

## Add Samsara from the gallery

To configure the integration of Samsara into Microsoft Entra ID, you need to add Samsara from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Samsara** in the search box.
4. Select **Samsara** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Samsara

Configure and test Microsoft Entra SSO with Samsara using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Samsara.

To configure and test Microsoft Entra SSO with Samsara, perform the following steps:

1. **[Configure domain verification in Samsara](https://kb.samsara.com/hc/en-us/articles/31499789674893-Verify-Domains-for-Secure-SSO-Authentication#UUID-9e9af4f3-fa9a-e18c-723d-66e148c98140)** - to enable SSO within Samsara, domain verification is a prerequisite.
2. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
3. **Create Samsara test user** - to have a counterpart of B.Simon in Samsara that's linked to the Microsoft Entra representation of user.
4. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Samsara** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set-up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.
5. Open your Samsara dashboard and navigate to Settings &gt; Single Sign-On tab. If you want to create a user SSO connection, click **Add** in the user SSO box. If you want to create a driver SSO connection, click **Add** in the driver SSO box. You will need to copy over values from Samsara into Entra ID SAML Configuration.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
6. In Entra ID, on the **Basic SAML Configuration** section, perform the following steps:

    a. Copy the link from Service Provider Entity ID field in Samsara into the **Identifier (Entity ID)** text box in Entra ID.

    b. Copy the link from Post-back/ACS URL field in Samsara into the **Reply URL** text box in Entra ID.

    Note

    Update these values with the actual Reply URL and Identifier. Contact the [Samsara Client support team](mailto:support@samsara.com) to get these values, or in Samsara, go to **Settings** &gt; **single-sign-on** and select the connection you want to create in order to obtain the right ACS and Identifier URLs.
7. On the **Set-up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find and copy the **App Federation Metadata URL** or download the **Federation Metadata XML**. In the Samsara dashboard in Settings &gt; Single Sign-on in the relevant SSO configuration (user or driver), paste the metadata URL or upload the file. Click **Save** to apply the changes.

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

### Create Samsara test user

In this section, a user called B.Simon is created in Samsara. Samsara supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Samsara, a new one is created after authentication with a default role of Standard Admin (No Dash Cam Access) for Organization. The user's access can then be increased or decreased as needed in Samsara.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Samsara Sign on URL where you can initiate the login flow.
- Go to Samsara Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Samsara for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Samsara tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Samsara for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
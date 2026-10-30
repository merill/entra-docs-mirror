---
layout: Conceptual
title: Configure Zscaler B2B User Portal for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/zscaler-b2b-user-portal-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Zscaler B2B User Portal.
ms.topic: how-to
ms.date: 2026-06-11T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 524869cb-78a0-d965-3e55-75f3706c9eb1
document_version_independent_id: f4020617-3354-8578-9afd-c53608bb3862
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/zscaler-b2b-user-portal-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/zscaler-b2b-user-portal-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/zscaler-b2b-user-portal-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: fd7996db-cc1d-e932-b0cd-7a7dfa1f79c9
---

# Configure Zscaler B2B User Portal for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Zscaler B2B User Portal with Microsoft Entra ID. When you integrate Zscaler B2B User Portal with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Zscaler B2B User Portal.
- Enable your users to be automatically signed-in to Zscaler B2B User Portal with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Zscaler B2B User Portal is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ |  | ✅ |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Zscaler B2B User Portal single sign-on (SSO) enabled subscription.

Note

This integration is also available to use from Microsoft Entra US Government Cloud environment. You can find this application in the Microsoft Entra US Government Cloud Application Gallery and configure it in the same way as you do from public cloud.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Zscaler B2B User Portal supports **IDP** initiated SSO.
- Zscaler B2B User Portal supports **Just In Time** user provisioning.

## Add Zscaler B2B User Portal from the gallery

To configure the integration of Zscaler B2B User Portal into Microsoft Entra ID, you need to add Zscaler B2B User Portal from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Zscaler B2B User Portal** in the search box.
4. Select **Zscaler B2B User Portal** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Zscaler B2B User Portal

Configure and test Microsoft Entra SSO with Zscaler B2B User Portal using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Zscaler B2B User Portal.

To configure and test Microsoft Entra SSO with Zscaler B2B User Portal, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Zscaler B2B User Portal SSO**- to configure the single sign-on settings on application side.
    1. **Create Zscaler B2B User Portal test user** - to have a counterpart of B.Simon in Zscaler B2B User Portal that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Zscaler B2B User Portal** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Set up single sign-on with SAML** page, perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://samlsp.private.zscaler.com/auth/metadata/<UniqueID>`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://samlsp.private.zscaler.com/auth/login?domain=EXAMPLE`

    Note

    These values aren't real. Update these values with the actual Identifier and Reply URL. Contact [Zscaler B2B User Portal Client support team](https://help.zscaler.com/) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up Zscaler B2B User Portal** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Zscaler B2B User Portal SSO

1. Open a new web browser window and sign into your Zscaler B2B User Portal company site as an administrator and perform the following steps:
2. From the left side of menu, select **Administration** and navigate to **AUTHENTICATION** section select **IdP Configuration**.

    ![Zscaler Private Access Administrator administration](media/zscaler-b2b-user-tutorial/tutorial-zscaler-private-access-administration.png)
3. In the top right corner, select **Add IdP Configuration**.

    ![Zscaler Private Access Administrator idp](media/zscaler-b2b-user-tutorial/tutorial-zscaler-private-access-idp.png)
4. On the **Add IdP Configuration** page perform the following steps:

    ![Zscaler Private Access Administrator select](media/zscaler-b2b-user-tutorial/tutorial-zscaler-private-access-select.png)

    a. Select **Select File** to upload the downloaded Metadata file from Microsoft Entra ID in the **IdP Metadata File Upload** field.

    b. It reads the **IdP metadata** from Microsoft Entra ID and populates all the fields information as shown below.

    ![Zscaler Private Access Administrator config](media/zscaler-b2b-user-tutorial/config.png)

    c. Select your domain from **Domains** field.

    d. Select **Save**.

### Create Zscaler B2B User Portal test user

In this section, a user called Britta Simon is created in Zscaler B2B User Portal. Zscaler B2B User Portal supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Zscaler B2B User Portal, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the Zscaler B2B User Portal for which you set up the SSO.
- You can use Microsoft My Apps. When you select the Zscaler B2B User Portal tile in the My Apps, you should be automatically signed in to the Zscaler B2B User Portal for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
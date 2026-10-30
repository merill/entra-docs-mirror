---
layout: Conceptual
title: Configure Document360 for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/document360-tutorial
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
description: Learn how to configure single sign-on (SSO) between Microsoft Entra ID and Document360.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 450682ad-1180-6fe9-28c7-086c7d04b092
document_version_independent_id: 06cae7fd-4bbb-37ef-a66d-88b2844e8f9b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/document360-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/document360-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/document360-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d853b24d-f005-b09a-98dc-a958891f79a3
---

# Configure Document360 for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article teaches you how to integrate Document360 with Microsoft Entra ID. Document360 is an online self-service knowledge base software. When you integrate Document360 with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Document360.
- Enable your users to be automatically signed in to Document360 with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You configure and test Microsoft Entra single sign-on for Document360 in a test environment. Document360 supports **Service Provider (SP)** and **Identity Provider (IdP)** initiated SSO.

Note

Identifier of this application is a fixed string value, so only one instance can be configured in one tenant.

## Prerequisites

To integrate Microsoft Entra ID with Document360, you need the following:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can [get a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Document360 subscription with SSO enabled. If you don't have a subscription, you can [Sign up for a new account](https://document360.com/signup/).

## Add application and assign a test user

Before configuring SSO, add the Document360 application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the SSO configuration.

### Add Document360 from the Microsoft Entra gallery

Add Document360 from the Microsoft Entra application gallery to configure SSO with Document360. For more information on adding an application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Alternatively, you can use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Document360** application integration page, find the **Manage** section and select **single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps. Choose any one of the Identifiers, Reply URL, and Sign on URL based on your Data center region.

    a. In the **Identifier** textbox, type/copy & paste one of the following URLs:

    | **Identifier** |
    | --- |
    | `https://identity.document360.io/saml` |
    | **(or)** |
    | `https://identity.us.document360.io/saml` |

    b. In the **Reply URL** textbox, type/copy & paste a URL using one of the following patterns:

    | **Reply URL** |
    | --- |
    | `https://identity.document360.io/signin-saml-<ID>` |
    | **(or)** |
    | `https://identity.us.document360.io/signin-saml-<ID>` |
6. If you wish to configure the application in **SP** initiated mode, then perform the following step:

    In the **Sign on URL** textbox, type/copy & paste one of the following URLs:

    | **Sign on URL** |
    | --- |
    | `https://identity.document360.io` |
    | **(or)** |
    | `https://identity.us.document360.io` |

    Note

    The Reply URL isn't real. Update this value with the actual Reply URL. You can also refer to the patterns shown in the Azure portal's **Basic SAML Configuration** section.
7. On the **Set-up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
8. On the **Set up Document360** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration appropriate URL.](common/copy-configuration-urls.png)

## Configure Document360 SSO

1. In a different web browser window, log in to your Document360 portal as an administrator.
2. To configure SSO on the **Document360** portal, you need to navigate to **Settings** → **Users & Security** → **SAML/OpenID** → **SAML** and perform the following steps:

    [![Screenshot shows the Document360 configuration.](media/document360-tutorial/configuration.png)](media/document360-tutorial/configuration.png#lightbox)
3. Select the Edit icon in **SAML basic configuration** on the Document360 portal side and paste the values from Microsoft Entra admin center based on the below mentioned field associations.

    | Document360 portal fields | Microsoft Entra admin center values |
    | --- | --- |
    | Email domains | Domains of emails you have under active directory |
    | Sign On URL | Login URL |
    | Entity ID | Microsoft Entra identifier |
    | Sign Out URL | Logout URL |
    | SAML certificate | Download Certificate (Base64) from Microsoft Entra ID side and upload in Document360 |
4. Select the **Save** button when you’re done with the values.

### Create Document360 test user

1. In a different web browser window, log in to your Document360 portal as an administrator.
2. From the Document360 portal, go to **Settings → Users & Security → Team accounts & groups → Team account**. Select the **New team account** button and type in the required details, specify the roles, and follow the module steps to add a user to Document360.

    [![Screenshot shows the Document360 test user.](media/document360-tutorial/add-user.png)](media/document360-tutorial/add-user.png#lightbox)

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with the following options.

#### SP initiated:

- Select **Test this application**, this option redirects to the Document360 Sign-on URL, where you can initiate the login flow.
- Go to Document360 Sign-on URL directly and initiate the login flow.

#### IDP initiated:

- Select **Test this application**, in the Azure portal, and you should be automatically signed in to the Document360 for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Document360 tile in the My Apps if configured in SP mode, you be redirected to the application sign-on page for initiating the login flow. If configured in IDP mode, you should be automatically signed in to the Document360 for which you set up the SSO.

For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
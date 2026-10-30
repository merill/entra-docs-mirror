---
layout: Conceptual
title: Configure Microsoft Entra SAML Toolkit for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/saml-toolkit-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Microsoft Entra SAML Toolkit.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 0800632e-a9b3-5f96-f290-207c7ef6be88
document_version_independent_id: eaa3c7a0-76d5-433f-9ac3-bc72638c0ff3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/saml-toolkit-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/saml-toolkit-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/saml-toolkit-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 993bac0c-3365-0fba-bbc8-8e713f7d31d7
---

# Configure Microsoft Entra SAML Toolkit for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Microsoft Entra SAML Toolkit with Microsoft Entra ID. When you integrate Microsoft Entra SAML Toolkit with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Microsoft Entra SAML Toolkit.
- Enable your users to be automatically signed-in to Microsoft Entra SAML Toolkit with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Microsoft Entra SAML Toolkit single sign-on (SSO) enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Microsoft Entra SAML Toolkit supports **SP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Microsoft Entra SAML Toolkit from the gallery

To configure the integration of Microsoft Entra SAML Toolkit into Microsoft Entra ID, you need to add Microsoft Entra SAML Toolkit from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Microsoft Entra SAML Toolkit** in the search box.
4. Select **Microsoft Entra SAML Toolkit** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Microsoft Entra SAML Toolkit

Configure and test Microsoft Entra SSO with Microsoft Entra SAML Toolkit using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Microsoft Entra SAML Toolkit.

To configure and test Microsoft Entra SSO with Microsoft Entra SAML Toolkit, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    - **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    - **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Microsoft Entra SAML Toolkit SSO**- to configure the single sign-on settings on application side.
    - **Create Microsoft Entra SAML Toolkit test user** - to have a counterpart of B.Simon in Microsoft Entra SAML Toolkit that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Microsoft Entra SAML Toolkit** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Reply URL** text box, type the URL: `https://samltoolkit.azurewebsites.net/SAML/Consume`

    b. In the **Sign on URL** text box, type the URL: `https://samltoolkit.azurewebsites.net/`
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Raw)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificateraw.png)
7. On the **Set up Microsoft Entra SAML Toolkit** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Microsoft Entra SAML Toolkit SSO

1. Open a new web browser window, if you have not registered in the Microsoft Entra SAML Toolkit website, first register by selecting the **Register**. If you have registered already, sign into your Microsoft Entra SAML Toolkit company site using the registered sign-in credentials.

    ![Microsoft Entra SAML Toolkit Register](media/saml-toolkit-tutorial/register.png)
2. In the **SAML Toolkit** window, select **SAML Configuration**.
3. Select **Create**.

    ![Microsoft Entra SAML Toolkit](media/saml-toolkit-tutorial/createsso.png)
4. On the **SAML SSO Configuration** page, perform the following steps:

    ![Microsoft Entra SAML Toolkit Create SSO Configuration](media/saml-toolkit-tutorial/fill-details.png)

    1. In the **Login URL** textbox, paste the **Login URL** value, which you copied previously.
    2. In the **Microsoft Entra Identifier** textbox, paste the **Microsoft Entra Identifier** value, which you copied previously.
    3. In the **Logout URL** textbox, paste the **Logout URL** value, which you copied previously.
    4. Select **Choose File** and upload the **Certificate (Raw)** file which you have downloaded.
    5. Select **Create**.
    6. Copy Sign-on URL, Identifier and ACS URL values on SAML Toolkit SSO configuration page and paste into respected textboxes in the **Basic SAML Configuration section**.

### Create Microsoft Entra SAML Toolkit test user

In this section, a user called B.Simon is created in Microsoft Entra SAML Toolkit. Please create a test user in the tool by registering a new user and provide all the user details.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Microsoft Entra SAML Toolkit Sign-on URL where you can initiate the login flow.
- Go to Microsoft Entra SAML Toolkit Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Microsoft Entra SAML Toolkit tile in the My Apps, this option redirects to Microsoft Entra SAML Toolkit Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
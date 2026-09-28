---
layout: Conceptual
title: Configure Imagineer WebVision for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/imagineerwebvision-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Imagineer WebVision.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 53aa0012-71cd-dd21-2139-75e5c86bd7bd
document_version_independent_id: d3733741-71ce-7124-8dff-d953119ae23e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/imagineerwebvision-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/imagineerwebvision-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/imagineerwebvision-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 5954c5a2-81f2-c287-36ed-9f345b29b9fe
---

# Configure Imagineer WebVision for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Imagineer WebVision with Microsoft Entra ID. Integrating Imagineer WebVision with Microsoft Entra ID provides you with the following benefits:

- You can control in Microsoft Entra ID who has access to Imagineer WebVision.
- You can enable your users to be automatically signed-in to Imagineer WebVision (Single Sign-On) with their Microsoft Entra accounts.
- You can manage your accounts in one central location.

If you want to know more details about SaaS app integration with Microsoft Entra ID, see [What is application access and single sign-on with Microsoft Entra ID](../enterprise-apps/what-is-single-sign-on). If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Imagineer WebVision single sign-on enabled subscription

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Imagineer WebVision supports **SP** initiated SSO

## Adding Imagineer WebVision from the gallery

To configure the integration of Imagineer WebVision into Microsoft Entra ID, you need to add Imagineer WebVision from the gallery to your list of managed SaaS apps.

**To add Imagineer WebVision from the gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the search box, type **Imagineer WebVision**, select **Imagineer WebVision** from result panel then select **Add** button to add the application.

    ![Imagineer WebVision in the results list](common/search-new-app.png)

## Configure and test Microsoft Entra single sign-on

In this section, you configure and test Microsoft Entra single sign-on with Imagineer WebVision based on a test user called **Britta Simon**. For single sign-on to work, a link relationship between a Microsoft Entra user and the related user in Imagineer WebVision needs to be established.

To configure and test Microsoft Entra single sign-on with Imagineer WebVision, you need to complete the following building blocks:

1. **Configure Microsoft Entra Single Sign-On** - to enable your users to use this feature.
2. **Configure Imagineer WebVision Single Sign-On** - to configure the Single Sign-On settings on application side.
3. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with Britta Simon.
4. **Assign the Microsoft Entra test user** - to enable Britta Simon to use Microsoft Entra single sign-on.
5. **Create Imagineer WebVision test user** - to have a counterpart of Britta Simon in Imagineer WebVision that's linked to the Microsoft Entra representation of user.
6. **Test single sign-on** - to verify whether the configuration works.

### Configure Microsoft Entra single sign-on

In this section, you enable Microsoft Entra single sign-on.

To configure Microsoft Entra single sign-on with Imagineer WebVision, perform the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Imagineer WebVision** application integration page, select **Single sign-on**.

    ![Configure single sign-on link](common/select-sso.png)
3. On the **Select a Single sign-on method** dialog, select **SAML/WS-Fed** mode to enable single sign-on.

    ![Single sign-on select mode](common/select-saml-option.png)
4. On the **Set up Single Sign-On with SAML** page, select **Edit** icon to open **Basic SAML Configuration** dialog.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    ![Imagineer WebVision Domain and URLs single sign-on information](common/sp-identifier.png)

    a. In the **Sign on URL** text box, type a URL using the following pattern: `https://<YOUR SERVER URL>/<yourapplicationloginpage>`

    b. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<YOUR SERVER URL>/<yourapplicationloginpage>`

    Note

    These values aren't real. Update these values with the actual Sign on URL and Identifier. Contact [Imagineer WebVision Client support team](mailto:support@itgny.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![The Certificate download link](common/copy-metadataurl.png)

### Configure Imagineer WebVision Single Sign-On

To configure single sign-on on **Imagineer WebVision** side, you need to send the **App Federation Metadata Url** to [Imagineer WebVision support team](mailto:support@itgny.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

### Create Imagineer WebVision test user

In this section, you create a user called Britta Simon in Imagineer WebVision. Work with [Imagineer WebVision support team](mailto:support@itgny.com) to add the users in the Imagineer WebVision platform. Users must be created and activated before you use single sign-on.

### Test single sign-on

In this section, you test your Microsoft Entra single sign-on configuration using the Access Panel.

When you select the Imagineer WebVision tile in the Access Panel, you should be automatically signed in to the Imagineer WebVision for which you set up SSO. For more information about the Access Panel, see [Introduction to the Access Panel](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
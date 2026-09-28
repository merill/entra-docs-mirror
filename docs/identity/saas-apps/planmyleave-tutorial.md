---
layout: Conceptual
title: Configure PlanMyLeave for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/planmyleave-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and PlanMyLeave.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 72ebd8c1-057e-48fa-19e2-8eacc22aa9c2
document_version_independent_id: 89020ea0-2446-d4cc-d9ca-31c7d34cbb61
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/planmyleave-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/planmyleave-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/planmyleave-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 14a858d2-ca0f-3de0-86a6-86bbb738c1f1
---

# Configure PlanMyLeave for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate PlanMyLeave with Microsoft Entra ID. Integrating PlanMyLeave with Microsoft Entra ID provides you with the following benefits:

- You can control in Microsoft Entra ID who has access to PlanMyLeave.
- You can enable your users to be automatically signed-in to PlanMyLeave (Single Sign-On) with their Microsoft Entra accounts.
- You can manage your accounts in one central location.

If you want to know more details about SaaS app integration with Microsoft Entra ID, see [What is application access and single sign-on with Microsoft Entra ID](../enterprise-apps/what-is-single-sign-on). If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- PlanMyLeave single sign-on enabled subscription

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- PlanMyLeave supports **SP** initiated SSO
- PlanMyLeave supports **Just In Time** user provisioning

## Adding PlanMyLeave from the gallery

To configure the integration of PlanMyLeave into Microsoft Entra ID, you need to add PlanMyLeave from the gallery to your list of managed SaaS apps.

**To add PlanMyLeave from the gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the search box, type **PlanMyLeave**, select **PlanMyLeave** from result panel then select **Add** button to add the application.

    ![PlanMyLeave in the results list](common/search-new-app.png)

## Configure and test Microsoft Entra single sign-on

In this section, you configure and test Microsoft Entra single sign-on with PlanMyLeave based on a test user called **Britta Simon**. For single sign-on to work, a link relationship between a Microsoft Entra user and the related user in PlanMyLeave needs to be established.

To configure and test Microsoft Entra single sign-on with PlanMyLeave, you need to complete the following building blocks:

1. **Configure Microsoft Entra Single Sign-On** - to enable your users to use this feature.
2. **Configure PlanMyLeave Single Sign-On** - to configure the Single Sign-On settings on application side.
3. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with Britta Simon.
4. **Assign the Microsoft Entra test user** - to enable Britta Simon to use Microsoft Entra single sign-on.
5. **Create PlanMyLeave test user** - to have a counterpart of Britta Simon in PlanMyLeave that's linked to the Microsoft Entra representation of user.
6. **Test single sign-on** - to verify whether the configuration works.

### Configure Microsoft Entra single sign-on

In this section, you enable Microsoft Entra single sign-on.

To configure Microsoft Entra single sign-on with PlanMyLeave, perform the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **PlanMyLeave** application integration page, select **Single sign-on**.

    ![Configure single sign-on link](common/select-sso.png)
3. On the **Select a Single sign-on method** dialog, select **SAML/WS-Fed** mode to enable single sign-on.

    ![Single sign-on select mode](common/select-saml-option.png)
4. On the **Set up Single Sign-On with SAML** page, select **Edit** icon to open **Basic SAML Configuration** dialog.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    ![PlanMyLeave Domain and URLs single sign-on information](common/sp-identifier.png)

    a. In the **Sign on URL** text box, type a URL using the following pattern: `https://<company-name>.planmyleave.com/Login.aspx`

    b. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<company-name>.planmyleave.com`

    Note

    These values aren't real. Update these values with the actual Sign on URL and Identifier. Contact [PlanMyLeave Client support team](mailto:support@planmyleave.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up PlanMyLeave** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

    a. Login URL

    b. Microsoft Entra Identifier

    c. Logout URL

### Configure PlanMyLeave Single Sign-On

1. In a different web browser window, log into your PlanMyLeave tenant as an administrator.
2. Go to **System Setup**. Then on the **Security Management** section select **Company SAML settings** .

    ![Screenshot that shows the &quot;System setup&quot; page with the &quot;Security Management&quot; section highlighted and the &quot;Company S A M L Settings&quot; action selected.](media/planmyleave-tutorial/tutorial_planmyleave_002.png)
3. On the **SAML Settings** section, select editor icon.

    ![Screenshot that shows the &quot;S A M L Settings&quot; section with the &quot;editor&quot; icon selected in the top-right of the section.](media/planmyleave-tutorial/tutorial_planmyleave_003.png)
4. On the **Update SAML Settings** section, perform the following steps:

    ![Configure Single Sign-On On App Side](media/planmyleave-tutorial/tutorial_planmyleave_004.png)

    a. In the **Login URL** textbox, paste **Login URL**..

    b. Open your downloaded metadata, copy **X509Certificate** value and then paste it to the **Certificate** textbox.

    c. Set "**Is Enable**" to "**Yes**".

    d. Select **Save**.

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

### Create PlanMyLeave test user

In this section, a user called Britta Simon is created in PlanMyLeave. PlanMyLeave supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in PlanMyLeave, a new one is created after authentication.

Note

If you need to create a user manually, you need to contact [PlanMyLeave support team](mailto:support@planmyleave.com).

### Test single sign-on

In this section, you test your Microsoft Entra single sign-on configuration using the Access Panel.

When you select the PlanMyLeave tile in the Access Panel, you should be automatically signed in to the PlanMyLeave for which you set up SSO. For more information about the Access Panel, see [Introduction to the Access Panel](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
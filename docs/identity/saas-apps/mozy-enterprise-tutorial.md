---
layout: Conceptual
title: Configure Mozy Enterprise for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/mozy-enterprise-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Mozy Enterprise.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: caad1a82-cbb2-8402-1ab7-3871e4e0c85e
document_version_independent_id: a95b9ca7-b8b0-23df-b6a4-a57e7a39d4ca
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/mozy-enterprise-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/mozy-enterprise-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/mozy-enterprise-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 8f0bad80-e0a0-5c0a-a4fb-18ab112d8984
---

# Configure Mozy Enterprise for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Mozy Enterprise with Microsoft Entra ID. Integrating Mozy Enterprise with Microsoft Entra ID provides you with the following benefits:

- You can control in Microsoft Entra ID who has access to Mozy Enterprise.
- You can enable your users to be automatically signed-in to Mozy Enterprise (Single Sign-On) with their Microsoft Entra accounts.
- You can manage your accounts in one central location.

If you want to know more details about SaaS app integration with Microsoft Entra ID, see [What is application access and single sign-on with Microsoft Entra ID](../enterprise-apps/what-is-single-sign-on). If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Mozy Enterprise single sign-on enabled subscription

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Mozy Enterprise supports **SP** initiated SSO

## Adding Mozy Enterprise from the gallery

To configure the integration of Mozy Enterprise into Microsoft Entra ID, you need to add Mozy Enterprise from the gallery to your list of managed SaaS apps.

**To add Mozy Enterprise from the gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the search box, type **Mozy Enterprise**, select **Mozy Enterprise** from result panel then select **Add** button to add the application.

    ![Mozy Enterprise in the results list](common/search-new-app.png)

## Configure and test Microsoft Entra single sign-on

In this section, you configure and test Microsoft Entra single sign-on with Mozy Enterprise based on a test user called **Britta Simon**. For single sign-on to work, a link relationship between a Microsoft Entra user and the related user in Mozy Enterprise needs to be established.

To configure and test Microsoft Entra single sign-on with Mozy Enterprise, you need to complete the following building blocks:

1. **Configure Microsoft Entra Single Sign-On** - to enable your users to use this feature.
2. **Configure Mozy Enterprise Single Sign-On** - to configure the Single Sign-On settings on application side.
3. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with Britta Simon.
4. **Assign the Microsoft Entra test user** - to enable Britta Simon to use Microsoft Entra single sign-on.
5. **Create Mozy Enterprise test user** - to have a counterpart of Britta Simon in Mozy Enterprise that's linked to the Microsoft Entra representation of user.
6. **Test single sign-on** - to verify whether the configuration works.

### Configure Microsoft Entra single sign-on

In this section, you enable Microsoft Entra single sign-on.

To configure Microsoft Entra single sign-on with Mozy Enterprise, perform the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Mozy Enterprise** application integration page, select **Single sign-on**.

    ![Configure single sign-on link](common/select-sso.png)
3. On the **Select a Single sign-on method** dialog, select **SAML/WS-Fed** mode to enable single sign-on.

    ![Single sign-on select mode](common/select-saml-option.png)
4. On the **Set up Single Sign-On with SAML** page, select **Edit** icon to open **Basic SAML Configuration** dialog.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    ![Mozy Enterprise Domain and URLs single sign-on information](common/sp-signonurl.png)

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<tenantname>.Mozyenterprise.com`

    Note

    The value isn't real. Update the value with the actual Sign-On URL. Contact [Mozy Enterprise Client support team](https://www.safenames.net/about-us/contact-us) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Mozy Enterprise** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

    a. Login URL

    b. Microsoft Entra Identifier

    c. Logout URL

### Configure Mozy Enterprise Single Sign-On

1. In a different web browser window, log into your Mozy Enterprise company site as an administrator.
2. In the **Configuration** section, select **Authentication Policy**.

    ![Screenshot shows Authentication Policy selected from Configuration.](media/mozy-enterprise-tutorial/ic777314.png)
3. On the **Authentication Policy** section, perform the following steps:

    ![Screenshot shows the Authentication Policy section where you can enter the values described.](media/mozy-enterprise-tutorial/ic777315.png)

    a. Select **Directory Service** as **Provider**.

    b. Select **Use LDAP Push**.

    c. Select the **SAML Authentication** tab.

    d. Paste **Login URL** into the **Authentication URL** textbox.

    e. Paste **Microsoft Entra Identifier** into the **SAML Endpoint** textbox.

    f. Open your downloaded base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **SAML Certificate** textbox.

    g. Select **Enable SSO for Admins to log in with their network credentials**.

    h. Select **Save Changes**.

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

### Create Mozy Enterprise test user

In order to enable Microsoft Entra users to log into Mozy Enterprise, they must be provisioned into Mozy Enterprise. In the case of Mozy Enterprise, provisioning is a manual task.

Note

You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise to provision Microsoft Entra user accounts.

**To provision a user accounts, perform the following steps:**

1. Log in to your **Mozy Enterprise** tenant.
2. Select **Users**, and then select **Add New User**.

    ![Users](media/mozy-enterprise-tutorial/ic777317.png)

    Note

    The **Add New User** option is only displayed only if **Mozy** is selected as the provider under **Authentication policy**. If SAML Authentication is configured, then the users are added automatically on their first login through Single sign on.
3. On the new user dialog, perform the following steps:

    ![Add Users](media/mozy-enterprise-tutorial/ic777318.png)

    a. From the **Choose a Group** list, select a group.

    b. From the **What type of user** list, select a type.

    c. In the **Username** textbox, type the name of the Microsoft Entra user.

    d. In the **Email** textbox, type the email address of the Microsoft Entra user.

    e. Select **Send user instruction email**.

    f. Select **Add User(s)**.

    Note

    After creating the user, an email is sent to the Microsoft Entra user that includes a link to confirm the account before it becomes active.

### Test single sign-on

In this section, you test your Microsoft Entra single sign-on configuration using the Access Panel.

When you select the Mozy Enterprise tile in the Access Panel, you should be automatically signed in to the Mozy Enterprise for which you set up SSO. For more information about the Access Panel, see [Introduction to the Access Panel](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
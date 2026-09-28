---
layout: Conceptual
title: Configure Uberflip for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/uberflip-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Uberflip.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: d9f5a22c-5db8-2eea-b3f9-88d1f85760fb
document_version_independent_id: e8156a5d-0ac6-248e-f20b-635abf469ff4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/uberflip-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/uberflip-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/uberflip-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 744a4dad-1df4-0395-2636-339255ed801d
---

# Configure Uberflip for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Uberflip with Microsoft Entra ID.

Integrating Uberflip with Microsoft Entra ID provides you with the following benefits:

- You can control in Microsoft Entra ID who has access to Uberflip.
- You can enable your users to be automatically signed in to Uberflip (single sign-on) with their Microsoft Entra accounts.
- You can manage your accounts in one central location: the Azure portal.

For details about software as a service (SaaS) app integration with Microsoft Entra ID, see [What is application access and single sign-on with Microsoft Entra ID?](../enterprise-apps/what-is-single-sign-on).

## Prerequisites

To configure Microsoft Entra integration with Uberflip, you need the following items:

- A Microsoft Entra subscription. If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.
- An Uberflip subscription with single sign-on enabled.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

Uberflip supports the following features:

- SP-initiated and IDP-initiated single sign-on (SSO).
- Just-in-time user provisioning.

## Add Uberflip from the Azure Marketplace

To configure the integration of Uberflip into Microsoft Entra ID, you need to add Uberflip from the Azure Marketplace to your list of managed SaaS apps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.

    ![The New application option](common/add-new-app.png)
3. In the search box, enter **Uberflip**. In the search results, select **Uberflip**, and then select **Add** to add the application.

    ![Uberflip in the results list](common/search-new-app.png)

## Configure and test Microsoft Entra single sign-on

In this section, you configure and test Microsoft Entra single sign-on with Uberflip based on a test user named **B Simon**. For single sign-on to work, you need to establish a link between a Microsoft Entra user and a related user in Uberflip.

To configure and test Microsoft Entra single sign-on with Uberflip, you need to complete the following building blocks:

1. **Configure Microsoft Entra single sign-on** to enable your users to use this feature.
2. **Configure Uberflip single sign-on** to configure the single sign-on settings on the application side.
3. **Create a Microsoft Entra test user** to test Microsoft Entra single sign-on with B. Simon.
4. **Assign the Microsoft Entra test user** to enable B. Simon to use Microsoft Entra single sign-on.
5. **Create an Uberflip test user** so that there's a user named B. Simon in Uberflip who's linked to the Microsoft Entra user named B. Simon.
6. **Test single sign-on** to verify whether the configuration works.

### Configure Microsoft Entra single sign-on

In this section, you enable Microsoft Entra single sign-on.

To configure Microsoft Entra single sign-on with Uberflip, take the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Uberflip** application integration page, select **Single sign-on**.

    ![Configure single sign-on option](common/select-sso.png)
3. In the **Select a single sign-on method** pane, select **SAML/WS-Fed** mode to enable single sign-on.

    ![Single sign-on select mode](common/select-saml-option.png)
4. On the **Set up Single Sign-On with SAML** pane, select **Edit** (the pencil icon) to open the **Basic SAML Configuration** pane.

    ![Screenshot shows the Basic SAML Configuration, where you can enter a Reply U R L.](common/edit-urls.png)
5. On the **Basic SAML Configuration** pane, do one of the following steps, depending on which SSO mode you want to configure:

    - To configure the application in IDP-initiated SSO mode, in the **Reply URL (Assertion Consumer Service URL)** box, enter a URL by using the following pattern:

        `https://app.uberflip.com/sso/saml2/<IDPID>/<ACCOUNTID>`

        ![Uberflip domain and URLs single sign-on information](common/both-replyurl.png)

        Note

        This value isn't real. Update this value with the actual reply URL. To get the actual value, contact the [Uberflip support team](mailto:support@uberflip.com). You can also refer to the patterns shown in the **Basic SAML Configuration** pane.
    - To configure the application in SP-initiated SSO mode, select **Set additional URLs**, and in the **Sign-on URL** box, enter this URL:

        `https://app.uberflip.com/users/login`

        ![Screenshot shows Set additional U R Ls where you can enter a Sign on U R L.](common/both-signonurl.png)
6. On the **Set up Single Sign-On with SAML** pane, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options and save it on your computer.

    ![The Federation Metadata XML download option](common/metadataxml.png)
7. In the **Set up Uberflip** pane, copy the URL or URLs that you need:

    - **Login URL**
    - **Microsoft Entra Identifier**
    - **Logout URL**

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Configure Uberflip single sign-on

To configure single sign-on on the Uberflip side, you need to send the downloaded Federation Metadata XML and the appropriate copied URLs to the [Uberflip support team](mailto:support@uberflip.com). The Uberflip team will make sure the SAML SSO connection is set properly on both sides.

### Create a Microsoft Entra test user

In this section, you create a test user named B. Simon.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **New user** &gt; **Create new user**, at the top of the screen.
4. In the **User**properties, follow these steps:
    1. In the **Display name** field, enter `B.Simon`.
    2. In the **User principal name** field, enter the username@companydomain.extension. For example, `B.Simon@contoso.com`.
    3. Select the **Show password** check box, and then write down the value that's displayed in the **Password** box.
    4. Select **Review + create**.
5. Select **Create**.

### Assign the Microsoft Entra test user

In this section, you enable B. Simon to use Azure single sign-on by granting their access to Uberflip.

1. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Uberflip**.

    ![Enterprise applications pane](common/enterprise-applications.png)
2. In the applications list, select **Uberflip**.

    ![Uberflip in the applications list](common/all-applications.png)
3. In the left pane, under **MANAGE**, select **Users and groups**.

    ![The &quot;Users and groups&quot; option](common/users-groups-blade.png)
4. Select **+ Add user**, and then select **Users and groups** in the **Add Assignment** pane.

    ![The Add Assignment pane](common/add-assign-user.png)
5. In the **Users and groups** pane, select **B Simon** in the **Users** list, and then choose **Select** at the bottom of the pane.
6. If you're expecting a role value in the SAML assertion, then in the **Select Role** pane, select the appropriate role for the user from the list. At the bottom of the pane, choose **Select**.
7. In the **Add Assignment** pane, select **Assign**.

### Create an Uberflip test user

A user named B. Simon is now created in Uberflip. You don't have to do anything to create this user. Uberflip supports just-in-time user provisioning, which is enabled by default. If a user named B. Simon doesn't already exist in Uberflip, a new one is created after authentication.

Note

If you need to create a user manually, contact the [Uberflip support team](mailto:support@uberflip.com).

### Test single sign-on

In this section, you test your Microsoft Entra single sign-on configuration by using the My Apps portal.

When you select **Uberflip** in the My Apps portal, you should be automatically signed in to the Uberflip subscription for which you set up single sign-on. For more information about the My Apps portal, see [Access and use apps on the My Apps portal](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
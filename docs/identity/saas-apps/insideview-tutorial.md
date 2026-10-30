---
layout: Conceptual
title: Configure InsideView for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/insideview-tutorial
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
description: In this article,  you learn how to configure single sign-on between Microsoft Entra ID and InsideView.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 3a37e888-2a8d-44d3-0823-9fe221e00609
document_version_independent_id: f155b1f9-15fc-73ff-7de3-412861f8daca
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/insideview-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/insideview-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/insideview-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 0f4a1d9e-49b3-3733-be2b-43204900dd3b
---

# Configure InsideView for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate InsideView with Microsoft Entra ID. This integration provides these benefits:

- You can use Microsoft Entra ID to control who has access to InsideView.
- You can enable your users to be automatically signed in to InsideView (single sign-on) with their Microsoft Entra accounts.
- You can manage your accounts in one central location: the Azure portal.

To learn more about SaaS app integration with Microsoft Entra ID, see [Single sign-on to applications in Microsoft Entra ID](../enterprise-apps/what-is-single-sign-on).

If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

To configure Microsoft Entra integration with InsideView, you need to have:

- A Microsoft Entra subscription. If you don't have a Microsoft Entra environment, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- An InsideView subscription that has single sign-on enabled.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- InsideView supports IdP-initiated SSO.

## Add InsideView from the gallery

To set up the integration of InsideView into Microsoft Entra ID, you need to add InsideView from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.

    ![Enterprise applications blade](common/enterprise-applications.png)
3. To add an application, select **New application** at the top of the window:

    ![Select New application](common/add-new-app.png)
4. In the search box, enter **InsideView**. Select **InsideView** in the search results and then select **Add**.

    ![Search results](common/search-new-app.png)

## Configure and test Microsoft Entra single sign-on

In this section, you configure and test Microsoft Entra single sign-on with InsideView by using a test user named Britta Simon. To enable single sign-on, you need to establish a relationship between a Microsoft Entra user and the corresponding user in InsideView.

To configure and test Microsoft Entra single sign-on with InsideView, you need to complete these steps:

1. **Configure Microsoft Entra single sign-on** to enable the feature for your users.
2. **Configure InsideView single sign-on** on the application side.
3. **Create a Microsoft Entra test user** to test Microsoft Entra single sign-on.
4. **Assign the Microsoft Entra test user** to enable Microsoft Entra single sign-on for the user.
5. **Create an InsideView test user** that's linked to the Microsoft Entra representation of the user.
6. **Test single sign-on** to verify that the configuration works.

### Configure Microsoft Entra single sign-on

In this section, you enable Microsoft Entra single sign-on.

To configure Microsoft Entra single sign-on with InsideView, take these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **InsideView**
3. Select **Single sign-on**:

    ![Select single sign-on](common/select-sso.png)
4. In the **Select a single sign-on method** dialog box, select **SAML/WS-Fed** mode to enable single sign-on:

    ![Select a single sign-on method](common/select-saml-option.png)
5. On the **Set up Single Sign-On with SAML** page, select the **Edit** icon to open the **Basic SAML Configuration** dialog box:

    ![Edit icon](common/edit-urls.png)
6. In the **Basic SAML Configuration** dialog box, take the following steps.

    ![Basic SAML Configuration dialog box](common/idp-reply.png)

    In the **Reply URL** box, enter a URL in this pattern:

    `https://my.insideview.com/iv/<STS Name>/login.iv`

    Note

    This value is a placeholder. You need to use the actual reply URL. Contact the [InsideView support team](mailto:support@insideview.com) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** dialog box.
7. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select the **Download** link next to **Certificate (Raw)**, per your requirements, and save the certificate on your computer:

    ![Certificate download link](common/certificateraw.png)
8. In the **Set up InsideView** section, copy the appropriate URLs, based on your requirements:

    ![Copy the configuration URLs](common/copy-configuration-urls.png)

    1. **Login URL**.
    2. **Microsoft Entra Identifier**.
    3. **Logout URL**.

### Configure InsideView single sign-on

1. In a new web browser window, sign in to your InsideView company site as an admin.
2. At the top of the window, select **Admin**, **SingleSignOn Settings**, and then **Add SAML**.

    ![SAML single sign-on settings](media/insideview-tutorial/ic794135.png)
3. In the **Add a New SAML** section, take the following steps.

    ![Add a New SAML section](media/insideview-tutorial/ic794136.png)

    1. In the **STS Name** box, enter a name for your configuration.
    2. In the **SamlP/WS-Fed Unsolicited EndPoint** box, paste the **Login URL** value that you copied.
    3. Open the Raw certificate that you downloaded. Copy the contents of the certificate to the clipboard, and then paste the contents into the **STS Certificate** box.
    4. In the **Crm User Id Mapping** box, enter **`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`**.
    5. In the **Crm Email Mapping** box, enter **`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`**.
    6. In the **Crm First Name Mapping** box, enter **`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`**.
    7. In the **Crm lastName Mapping** box, enter **`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`**.
    8. Select **Save**.

### Create a Microsoft Entra test user

In this section, you create a test user named Britta Simon.

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

In this section, you enable Britta Simon to use Azure single sign-on by granting her access to InsideView.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **InsideView**.

    ![List of applications](common/all-applications.png)
3. In the left pane, select **Users and groups**:

    ![Select Users and groups](common/users-groups-blade.png)
4. Select **Add user**, and then select **Users and groups** in the **Add Assignment** dialog box.

    ![Select Add user](common/add-assign-user.png)
5. In the **Users and groups** dialog box, select **Britta Simon** in the users list, and then select the **Select** button at the bottom of the window.
6. If you expect a role value in the SAML assertion, in the **Select Role** dialog box, select the appropriate role for the user from the list. Select the **Select** button at the bottom of the window.
7. In the **Add Assignment** dialog box, select **Assign**.

### Create an InsideView test user

To enable Microsoft Entra users to sign in to InsideView, you need to add them to InsideView. You need to add them manually.

To create users or contacts in InsideView, contact the [InsideView support team](mailto:support@insideview.com).

Note

You can use any user account creation tool or API provided by InsideView to provision Microsoft Entra user accounts.

### Test single sign-on

Now you need to test your Microsoft Entra single sign-on configuration by using the Access Panel.

When you select the InsideView tile in the Access Panel, you should be automatically signed in to the InsideView instance for which you set up SSO. For more information about the Access Panel, see [Access and use apps on the My Apps portal](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
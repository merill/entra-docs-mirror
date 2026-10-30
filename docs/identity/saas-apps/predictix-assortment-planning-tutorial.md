---
layout: Conceptual
title: Configure Predictix Assortment Planning for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/predictix-assortment-planning-tutorial
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
description: In this article,  you learn how to configure single sign-on between Microsoft Entra ID and Predictix Assortment Planning.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 6efa17bf-f1fd-171c-5932-889fd8afefb6
document_version_independent_id: f96af962-417b-5027-1a26-aa99d40a2d2a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/predictix-assortment-planning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/predictix-assortment-planning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/predictix-assortment-planning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c7dc1c77-1353-b76b-99fe-954c5fa5855d
---

# Configure Predictix Assortment Planning for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Predictix Assortment Planning with Microsoft Entra ID. This integration provides these benefits:

- You can use Microsoft Entra ID to control who has access to Predictix Assortment Planning.
- You can enable your users to be automatically signed in to Predictix Assortment Planning (single sign-on) with their Microsoft Entra accounts.
- You can manage your accounts in one central location: the Azure portal.

To learn more about SaaS app integration with Microsoft Entra ID, see [Single sign-on to applications in Microsoft Entra ID](../enterprise-apps/what-is-single-sign-on).

If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you start.

## Prerequisites

To configure Microsoft Entra integration with Predictix Assortment Planning, you need to have:

- A Microsoft Entra subscription. If you don't have a Microsoft Entra environment, you can get a [free account](https://azure.microsoft.com/pricing/free-trial/).
- A Predictix Assortment Planning subscription that has single sign-on enabled.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Predictix Assortment Planning supports SP-initiated SSO.

## Add Predictix Assortment Planning from the gallery

To set up the integration of Predictix Assortment Planning into Microsoft Entra ID, you need to add Predictix Assortment Planning from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.

    ![The Enterprise applications blade](common/enterprise-applications.png)
3. To add an application, select **New application** at the top of the window:

    ![Select New application](common/add-new-app.png)
4. In the search box, enter **Predictix Assortment Planning**. Select **Predictix Assortment Planning** in the search results and then select **Add**.

    ![Search results](common/search-new-app.png)

## Configure and test Microsoft Entra single sign-on

In this section, you configure and test Microsoft Entra single sign-on with Predictix Assortment Planning by using a test user named Britta Simon. To enable single sign-on, you need to establish a relationship between a Microsoft Entra user and the corresponding user in Predictix Assortment Planning.

To configure and test Microsoft Entra single sign-on with Predictix Assortment Planning, you need to complete these steps:

1. **Configure Microsoft Entra single sign-on** to enable the feature for your users.
2. **Configure Predictix Assortment Planning single sign-on** on the application side.
3. **Create a Microsoft Entra test user** to test Microsoft Entra single sign-on.
4. **Assign the Microsoft Entra test user** to enable Microsoft Entra single sign-on for the user.
5. **Create a Predictix Assortment Planning test user** that's linked to the Microsoft Entra representation of the user.
6. **Test single sign-on** to verify that the configuration works.

### Configure Microsoft Entra single sign-on

In this section, you enable Microsoft Entra single sign-on.

To configure Microsoft Entra single sign-on with Predictix Assortment Planning, take these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Predictix Assortment Planning** application integration page, select **Single sign-on**:

    ![Select Single sign-on](common/select-sso.png)
3. In the **Select a single sign-on method** dialog box, select **SAML/WS-Fed** mode to enable single sign-on:

    ![Select a single sign-on method](common/select-saml-option.png)
4. On the **Set up Single Sign-On with SAML** page, select the **Edit** icon to open the **Basic SAML Configuration** dialog box:

    ![Edit icon](common/edit-urls.png)
5. In the **Basic SAML Configuration** dialog box, complete the following steps.

    ![Basic SAML Configuration dialog box](common/sp-identifier.png)

    1. In the **Sign on URL** box, enter a URL in this pattern:

        ```https
        https://<sub-domain>.ap.predictix.com/sso/request
        https://<sub-domain>.dev.ap.predictix.com/
        ```
    2. In the **Identifier (Entity ID)** box, enter a URL in this pattern:

        ```https
        https://<sub-domain>.ap.predictix.com
        https://<sub-domain>.dev.ap.predictix.com
        ```

    Note

    These values are placeholders. You need to use the actual sign-on URL and identifier. Contact the [Predictix Assortment Planning support team](https://www.infor.com/support) to get the values. You can also refer to the patterns shown in the **Basic SAML Configuration** dialog box.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select the **Download** link next to **Certificate (Base64)**, per your requirements, and save the certificate on your computer:

    ![Certificate download link](common/certificatebase64.png)
7. In the **Set up Predictix Assortment Planning** section, copy the appropriate URLs, based on your requirements:

    ![Copy the configuration URLs](common/copy-configuration-urls.png)

    1. **Login URL**.
    2. **Microsoft Entra Identifier**.
    3. **Logout URL**.

### Configure Predictix Assortment Planning single sign-on

To configure single sign-on on the Predictix Assortment Planning side, you need to send the certificate that you downloaded and the URLs that you copied to the [Predictix Assortment Planning support team](https://www.infor.com/support). This team ensures the SAML SSO connection is set properly on both sides.

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

In this section, you enable Britta Simon to use Microsoft Entra single sign-on by granting her access to Predictix Assortment Planning.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Predictix Assortment Planning**.

    ![List of applications](common/all-applications.png)
3. In the left pane, select **Users and groups**:

    ![Select Users and groups](common/users-groups-blade.png)
4. Select **Add user**, and then select **Users and groups** in the **Add Assignment** dialog box.

    ![Select Add user](common/add-assign-user.png)
5. In the **Users and groups** dialog box, select **Britta Simon** in the users list, and then select the **Select** button at the bottom of the screen.
6. If you expect a role value in the SAML assertion, in the **Select Role** dialog box, select the appropriate role for the user from the list. Select the **Select** button at the bottom of the screen.
7. In the **Add Assignment** dialog box, select **Assign**.

### Create a Predictix Assortment Planning test user

Next, you need to create a user named Britta Simon in Predictix Assortment Planning. Work with the [Predictix Assortment Planning support team](https://www.infor.com/support) to add users. Users need to be created and activated before you use single sign-on.

Note

The Microsoft Entra account holder receives an email and selects a link to confirm the account before it becomes active.

### Test single sign-on

Now you need to test your Microsoft Entra single sign-on configuration by using the Access Panel.

When you select the Predictix Assortment Planning tile in the Access Panel, you should be automatically signed in to the Predictix Assortment Planning instance for which you set up SSO. For more information, see [Access and use apps on the My Apps portal](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
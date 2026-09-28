---
layout: Conceptual
title: Configure Adaptive Insights for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/adaptivesuite-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Adaptive Insights.
ms.topic: how-to
ms.date: 2025-05-09T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 4b78648e-3c76-7f99-e405-9cef3ac14e5c
document_version_independent_id: ab241b85-57c8-fc32-c34d-904df5183d50
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/adaptivesuite-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/adaptivesuite-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/adaptivesuite-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: e482e245-00b6-4b62-73c5-083602e9ebc0
---

# Configure Adaptive Insights for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Adaptive Insights with Microsoft Entra ID. When you integrate Adaptive Insights with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Adaptive Insights.
- Enable your users to be automatically signed-in to Adaptive Insights with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Adaptive Insights single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Adaptive Insights supports **IDP** initiated SSO

## Add Adaptive Insights from the gallery

To configure the integration of Adaptive Insights into Microsoft Entra ID, you need to add Adaptive Insights from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Adaptive Insights** in the search box.
4. Select **Adaptive Insights** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Adaptive Insights

Configure and test Microsoft Entra SSO with Adaptive Insights using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Adaptive Insights.

To configure and test Microsoft Entra SSO with Adaptive Insights, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Adaptive Insights SSO**- to configure the single sign-on settings on application side.
    1. **Create Adaptive Insights test user** - to have a counterpart of B.Simon in Adaptive Insights that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

### Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Adaptive Insights** application integration page, find the **Manage** section and select **Single sign-on**.
3. On the **Select a Single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`

    Note

    You can get Identifier(Entity ID) and Reply URL values from the Adaptive Insights’s **SAML SSO Settings** page.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Adaptive Insights** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create a Microsoft Entra test user

In this section, you create a test user called B.Simon.

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

In this section, you enable B.Simon to use single sign-on by granting access to Adaptive Insights.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Adaptive Insights**.
3. In the app's overview page, select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Add Assignment**dialog.
    1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then select the **Select** button at the bottom of the screen.
    2. If you're expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
    3. In the **Add Assignment** dialog, select the **Assign** button.

### Configure Adaptive Insights SSO

1. In a different web browser window, sign in to your Adaptive Insights company site as an administrator.
2. Go to **Administration**.
3. In the **Users and Roles** section, select **SAML SSO Settings**.
4. On the **SAML SSO Settings** page, perform the following steps:

    ![SAML SSO Settings](media/adaptivesuite-tutorial/saml.png)

    a. In the **Identity provider name** textbox, type a name for your configuration.

    b. Paste the **Microsoft Entra Identifier** value into the **Identity provider Entity ID** textbox.

    c. Paste the **Login URL** value into the **Identity provider SSO URL** textbox.

    d. Paste the **Logout URL** value into the **Custom logout URL** textbox.

    e. To upload your downloaded certificate, select **Choose file**.

    f. Select the following, for:

    - **SAML user id**, select **User’s Adaptive Insights user name**.
    - **SAML user id location**, select **User id in NameID of Subject**.
    - **SAML NameID format**, select **Email address**.
    - **Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.

    g. Copy **Adaptive Insights SSO URL** and paste into the **Identifier(Entity ID)** and **Reply URL** textboxes in the **Basic SAML Configuration** section.

    h. Select **Save**.

### Create Adaptive Insights test user

To enable Microsoft Entra users to sign in to Adaptive Insights, they must be provisioned into Adaptive Insights. In the case of Adaptive Insights, provisioning is a manual task.

**To configure user provisioning, perform the following steps:**

1. Sign in to your **Adaptive Insights** company site as an administrator.
2. Go to **Administration** &gt; **Users and Roles** &gt; **Users**.
3. In the **New User** section, enter the details of the user you want to create. Ensure that the user names in Microsoft Entra ID match the corresponding user names in Adaptive Insights.
4. Select **Submit**.

Note

You can use any other Adaptive Insights user account creation tools or APIs provided by Adaptive Insights to provision Microsoft Entra user accounts.

### Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the Adaptive Insights for which you set up the SSO.
- You can use Microsoft My Apps. When you select the Adaptive Insights tile in the My Apps, you should be automatically signed in to the Adaptive Insights for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
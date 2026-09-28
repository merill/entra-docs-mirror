---
layout: Conceptual
title: Configure Harness for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/harness-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Harness.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 3fd52187-b9e9-5012-1086-3dc49fc24dea
document_version_independent_id: 0719f736-d460-c151-6c6d-f873e5cac967
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/harness-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/harness-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/harness-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 0b52e799-abe6-b0ea-a07a-ca5654967ccc
---

# Configure Harness for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Harness with Microsoft Entra ID. When you integrate Harness with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Harness.
- Enable your users to be automatically signed-in to Harness with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Harness single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Harness supports **SP and IDP** initiated SSO.
- Harness supports [Automated user provisioning](harness-provisioning-tutorial).

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Harness from the gallery

To configure the integration of Harness into Microsoft Entra ID, you need to add Harness from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Harness** in the search box.
4. Select **Harness** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Harness

Configure and test Microsoft Entra SSO with Harness using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Harness.

To configure and test Microsoft Entra SSO with Harness, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Harness SSO**- to configure the single sign-on settings on application side.
    1. **Create Harness test user** - to have a counterpart of B.Simon in Harness that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Harness** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following step:

    In the **Reply URL** text box, type a URL using the following pattern: `https://app.harness.io/gateway/api/users/saml-login?accountId=<harness_account_id>`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type the URL: `https://app.harness.io/`

    Note

    The Reply URL value isn't real. You get the actual Reply URL from the **Configure Harness SSO** section, which is explained later in the article. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
8. On the **Set up Harness** section, copy the appropriate URL(s) based on your requirement.

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

In this section, you enable B.Simon to use single sign-on by granting access to Harness.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Harness**.
3. In the app's overview page, select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Add Assignment**dialog.
    1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then select the **Select** button at the bottom of the screen.
    2. If you're expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
    3. In the **Add Assignment** dialog, select the **Assign** button.

## Configure Harness SSO

1. In a different web browser window, sign in to your Harness company site as an administrator
2. On the top-right of the page, select **Continuous Security** &gt; **Access Management** &gt; **Authentication Settings**.

    ![Screenshot that shows the &quot;Continuous Security&quot; menu with &quot;Access Management&quot; and &quot;Authentication Settings&quot; selected.](media/harness-tutorial/authentication.png)
3. On the **SSO Providers** section, select **+ Add SSO Providers** &gt; **SAML**.

    ![Screenshot that shows the &quot;S S O Providers&quot; with &quot;+ Add S S O Providers - S A M L&quot; selected.](media/harness-tutorial/providers.png)
4. On the **SAML Provider** pop-up, perform the following steps:

    ![Screenshot that shows the &quot;S A M L Provider&quot; pop-up with the &quot;U R L&quot; and &quot;Display Name&quot; fields highlighted, and the &quot;Choose File&quot; and &quot;Submit&quot; buttons selected.](media/harness-tutorial/file.png)

    a. Copy the **In your SSO Provider, please enable SAML-based login, then enter the following URL** instance and paste it in Reply URL textbox in **Basic SAML Configuration** section.

    b. In the **Display Name** text box, type your display name.

    c. Select **Choose file** to upload the Federation Metadata XML file, which you have downloaded from Microsoft Entra ID.

    d. Select **SUBMIT**.

### Create Harness test user

To enable Microsoft Entra users to sign in to Harness, they must be provisioned into Harness. In Harness, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Sign in to Harness as an Administrator.
2. On the top-right of the page, select **Continuous Security** &gt; **Access Management** &gt; **Users**.

    ![Screenshot that shows the &quot;Continuous Security&quot; menu with &quot;Access Management&quot; and &quot;Users&quot; selected.](media/harness-tutorial/users.png)
3. On the right side of page, select **+ Add User**.

    ![Screenshot that shows the &quot;Users&quot; page with the &quot;+ Add User&quot; action selected.](media/harness-tutorial/add-user.png)
4. On the **Add User** pop-up, perform the following steps:

    ![Harness configuration](media/harness-tutorial/configure.png)

    a. In **Email Address(es)** text box, enter the email of user like `B.simon@contoso.com`.

    b. Select your **User Groups**.

    c. Select **Submit**.

Harness also supports automatic user provisioning, you can find more details [here](harness-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Harness Sign on URL where you can initiate the login flow.
- Go to Harness Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Harness for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Harness tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Harness for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
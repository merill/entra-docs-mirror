---
layout: Conceptual
title: Configure Greenhouse for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/greenhouse-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Greenhouse.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: d9b260cc-3e08-e2a0-b478-30a745cd2c97
document_version_independent_id: 5f7d594b-b6ec-cee2-9a8c-d2e6e9c4783b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/greenhouse-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/greenhouse-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/greenhouse-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: b307eeb7-b2f1-0b70-dfa6-5fa8649184fd
---

# Configure Greenhouse for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Greenhouse with Microsoft Entra ID. When you integrate Greenhouse with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Greenhouse.
- Enable your users to be automatically signed-in to Greenhouse with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Greenhouse single sign-on (SSO) enabled subscription.

Note

This integration is also available to use from Microsoft Entra US Government Cloud environment. You can find this application in the Microsoft Entra US Government Cloud Application Gallery and configure it in the same way as you do from public cloud.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Greenhouse supports **SP and IDP** initiated SSO.

## Adding Greenhouse from the gallery

To configure the integration of Greenhouse into Microsoft Entra ID, you need to add Greenhouse from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Greenhouse** in the search box.
4. Select **Greenhouse** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Greenhouse

Configure and test Microsoft Entra SSO with Greenhouse using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Greenhouse.

To configure and test Microsoft Entra SSO with Greenhouse, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with Britta Simon.
    2. **Assign the Microsoft Entra test user** - to enable Britta Simon to use Microsoft Entra single sign-on.
2. **Configure Greenhouse SSO**- to configure the Single Sign-On settings on application side.
    1. **Create Greenhouse test user** - to have a counterpart of Britta Simon in Greenhouse that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Greenhouse** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)

Note

The [Greenhouse Client support team](https://www.greenhouse.io/contact) recommends configuring Entra ID side application settings for **IDP** initiated mode. Contact the Greenhouse Client support team for more details and to get the correct values mentioned below.

1. On the **Basic SAML Configuration** section enter the values for the following fields:

    a. In the **Identifier** text box, type the value: `greenhouse.io`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<COMPANYNAME>.greenhouse.io/<ENTITY ID>/users/saml/consume`
2. Leave the **Sign-on URL** text box empty.
3. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
4. On the **Set up Greenhouse** section, copy the appropriate URL(s) as per your requirement.

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

In this section, you enable B.Simon to use single sign-on by granting access to Greenhouse.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Greenhouse**.
3. In the app's overview page, select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Add Assignment**dialog.
    1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then select the **Select** button at the bottom of the screen.
    2. If you're expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
    3. In the **Add Assignment** dialog, select the **Assign** button.

## Configure Greenhouse SSO

1. In a different web browser window, sign into Greenhouse website as an administrator.
2. Go to the **Configure &gt; Dev Center &gt; Single Sign-On**.

    ![screenshot for the sso page](media/greenhouse-tutorial/configure.png)
3. Perform the following steps in the **Single Sign-On** page.

    ![screenshot for the sso configuration page](media/greenhouse-tutorial/sso-page.png)

    a. Copy **SSO Assertion Consumer URL** value, paste this value into the **Reply URL** text box in the **Basic SAML Configuration** section.

    b. In the **Entity ID/Issuer** textbox, paste the **Microsoft Entra Identifier** value which you copied previously.

    c. In the **Single Sign-On URL** textbox, paste the **Login URL** value which you copied previously.

    d. Open the downloaded **Federation Metadata XML** into Notepad and paste the content into the **IdP Certificate Fingerprint** textbox.

    e. Select the **Name Identifier Format** value from the dropdown.

    f. Select **Begin Testing**.

    Note

    Alternatively you can also upload the **Federation Metadata XML** file by selecting the **Choose File** option.

### Create Greenhouse test user

In order to enable Microsoft Entra users to log into Greenhouse, they must be provisioned into Greenhouse. In the case of Greenhouse, provisioning is a manual task.

Note

You can use any other Greenhouse user account creation tools or APIs provided by Greenhouse to provision Microsoft Entra user accounts.

**To provision a user accounts, perform the following steps:**

1. Log in to your **Greenhouse** company site as an administrator.
2. Go to the **Configure &gt; Users &gt; New Users**

    ![Users](media/greenhouse-tutorial/create-user-1.png)
3. In the **Add New Users** section, perform the following steps:

    ![Add New User](media/greenhouse-tutorial/create-user-2.png)

    a. In the **Enter user emails** textbox, type the email address of a valid Microsoft Entra account you want to provision.

    b. Select **Save**.

    Note

    The Microsoft Entra account holders will receive an email including a link to confirm the account before it becomes active.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Greenhouse Sign on URL where you can initiate the login flow.
- Go to Greenhouse Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Greenhouse for which you set up the SSO

You can also use Microsoft My Apps to test the application in any mode. When you select the Greenhouse tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Greenhouse for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
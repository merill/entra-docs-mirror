---
layout: Conceptual
title: Configure Zoho for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/zoho-mail-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Zoho.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 1c9ffbb0-a388-9cb7-087d-8b410aade465
document_version_independent_id: 30f1a617-c8fa-a36a-d684-f16f2c7b6dca
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/zoho-mail-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/zoho-mail-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/zoho-mail-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 5ee9ffc6-2ff1-db73-55c9-0bbf92c3fbac
---

# Configure Zoho for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Zoho with Microsoft Entra ID. When you integrate Zoho with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Zoho.
- Enable your users to be automatically signed-in to Zoho with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To configure Microsoft Entra integration with Zoho One, you need the following items:

- A Microsoft Entra subscription. If you don't have a Microsoft Entra environment, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Zoho single sign-on enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Zoho supports **SP** initiated SSO

## Add Zoho from the gallery

To configure the integration of Zoho into Microsoft Entra ID, you need to add Zoho from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Zoho** in the search box.
4. Select **Zoho** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Zoho

Configure and test Microsoft Entra SSO with Zoho using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Zoho.

To configure and test Microsoft Entra SSO with Zoho, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Zoho SSO**- to configure the single sign-on settings on application side.
    1. **Create Zoho test user** - to have a counterpart of B.Simon in Zoho that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

### Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Zoho** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<company name>.zohomail.com`

    Note

    The value isn't real. Update the value with the actual Sign-On URL. Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Zoho** section, copy the appropriate URL(s) as per your requirement.

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

In this section, you enable B.Simon to use single sign-on by granting access to Zoho.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Zoho**.
3. In the app's overview page, select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Add Assignment**dialog.
    1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then select the **Select** button at the bottom of the screen.
    2. If you're expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
    3. In the **Add Assignment** dialog, select the **Assign** button.

### Configure Zoho SSO

1. In a different web browser window, log into your Zoho Mail company site as an administrator.
2. Go to the **Control panel**.

    ![Control Panel](media/zoho-mail-tutorial/control-panel.png)
3. Select the **SAML Authentication** tab.

    ![SAML Authentication](media/zoho-mail-tutorial/saml-authentication.png)
4. In the **SAML Authentication Details** section, perform the following steps:

    ![SAML Authentication Details](media/zoho-mail-tutorial/details.png)

    a. In the **Login URL** textbox, paste **Login URL**..

    b. In the **Logout URL** textbox, paste **Logout URL**..

    c. In the **Change Password URL** textbox, paste **Change Password URL**..

    d. Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **PublicKey** textbox.

    e. As **Algorithm**, select **RSA**.

    f. Select **OK**.

### Create Zoho test user

In order to enable Microsoft Entra users to log into Zoho Mail, they must be provisioned into Zoho Mail. In the case of Zoho Mail, provisioning is a manual task.

Note

You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail to provision Microsoft Entra user accounts.

### To provision a user account, perform the following steps:

1. Log in to your **Zoho Mail** company site as an administrator.
2. Go to **Control Panel** &gt; **Mail & Docs**.
3. Go to **User Details** &gt; **Add User**.

    ![Screenshot shows the Zoho Mail site with User Details and Add User selected.](media/zoho-mail-tutorial/add-user-1.png)
4. On the **Add users** dialog, perform the following steps:

    ![Screenshot shows the Add users dialog box where you can enter the values described.](media/zoho-mail-tutorial/add-user-2.png)

    a. In the **First Name** textbox, type the first name of user like **Britta**.

    b. In the **Last Name** textbox, type the last name of user like **Simon**.

    c. In the **Email ID** textbox, type the email ID of user like **brittasimon@contoso.com**.

    d. In the **Password** textbox, enter password of user.

    e. Select **OK**.

    Note

    The Microsoft Entra account holder will receive an email with a link to confirm the account before it becomes active.

### Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Zoho Sign-on URL where you can initiate the login flow.
- Go to Zoho Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Zoho tile in the My Apps, you should be automatically signed in to the Zoho for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
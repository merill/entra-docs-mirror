---
layout: Conceptual
title: Configure Egnyte for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/egnyte-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Egnyte.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 9e29a931-f453-8ef9-fc72-5ec4a8e0c4e6
document_version_independent_id: 3c42090f-0745-1833-a84c-37802a304977
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/egnyte-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/egnyte-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/egnyte-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 0c4baca0-9fc6-882f-fd30-20a3bc111683
---

# Configure Egnyte for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Egnyte with Microsoft Entra ID. When you integrate Egnyte with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Egnyte.
- Enable your users to be automatically signed-in to Egnyte with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Egnyte single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Egnyte supports **SP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Egnyte from the gallery

To configure the integration of Egnyte into Microsoft Entra ID, you need to add Egnyte from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Egnyte** in the search box.
4. Select **Egnyte** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Egnyte

Configure and test Microsoft Entra SSO with Form.com using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Form.com.

To configure and test Microsoft Entra SSO with Form.com, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Egnyte SSO**- to configure the single sign-on settings on application side.
    1. **Create Egnyte test user** - to have a counterpart of B.Simon in Egnyte that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Egnyte** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Sign-on URL** text box, type a URL using the following pattern: `https://<companyname>.egnyte.com`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<companyname>.egnyte.com/samlconsumer/AzureAD`

    Note

    These values aren't real. Update the value with the actual Sign-On URL and Reply URL. Contact [Egnyte Client support team](https://www.egnyte.com/corp/contact_egnyte.html) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Egnyte** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Egnyte SSO

1. In a different web browser window, sign in to your Egnyte company site as an administrator.
2. Select **Settings**.

    ![Settings 1](media/egnyte-tutorial/settings-tab.png)
3. In the menu, select **Settings**.

    ![Menu 1](media/egnyte-tutorial/menu-tab.png)
4. Select the **Configuration** tab, and then select **Security**.

    ![Security](media/egnyte-tutorial/configuration.png)
5. In the **Single Sign-On Authentication** section, perform the following steps:

    ![Single Sign On Authentication](media/egnyte-tutorial/authentication.png)

    1. As **Single sign-on authentication**, select **SAML 2.0**.
    2. As **Identity provider**, select **Microsoft Entra ID**.
    3. Paste **Login URL** into the **Identity provider login URL** textbox.
    4. Paste **Microsoft Entra Identifier** which you have into the **Identity provider entity ID** textbox.
    5. Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.
    6. As **Default user mapping**, select **Email address**.
    7. As **Use domain-specific issuer value**, select **disabled**.
    8. Select **Save**.

### Create Egnyte test user

To enable Microsoft Entra users to sign in to Egnyte, they must be provisioned into Egnyte. In the case of Egnyte, provisioning is a manual task.

**To provision a user accounts, perform the following steps:**

1. Sign in to your **Egnyte** company site as administrator.
2. Go to **Settings** &gt; **Users & Groups**.
3. Select **Add New User**, and then select the type of user you want to add.

    ![Users](media/egnyte-tutorial/add-user.png)
4. In the **New Power User** section, perform the following steps:

    ![New Standard User](media/egnyte-tutorial/new-user.png)

    a. In **Email** text box, enter the email of user like **Brittasimon@contoso.com**.

    b. In **Username** text box, enter the username of user like **Brittasimon**.

    c. Select **Single Sign-On** as **Authentication Type**.

    d. Select **Save**.

    Note

    The Microsoft Entra account holder will receive a notification email.

Note

You can use any other Egnyte user account creation tools or APIs provided by Egnyte to provision Microsoft Entra user accounts.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Egnyte Sign-on URL where you can initiate the login flow.
- Go to Egnyte Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Egnyte tile in the My Apps, this option redirects to Egnyte Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
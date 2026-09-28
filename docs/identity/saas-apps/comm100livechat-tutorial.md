---
layout: Conceptual
title: Configure Comm100 Live Chat for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/comm100livechat-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Comm100 Live Chat.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 8c7eb8e3-edda-3202-3743-5bb4162a5fde
document_version_independent_id: a3d9ac9e-0caa-f71a-303d-b001e3e0367e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/comm100livechat-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/comm100livechat-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/comm100livechat-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: b67c0e6d-4020-8619-eb57-1add589b26f4
---

# Configure Comm100 Live Chat for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Comm100 Live Chat with Microsoft Entra ID. When you integrate Comm100 Live Chat with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Comm100 Live Chat.
- Enable your users to be automatically signed-in to Comm100 Live Chat with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Comm100 Live Chat single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Comm100 Live Chat supports **SP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Comm100 Live Chat from the gallery

To configure the integration of Comm100 Live Chat into Microsoft Entra ID, you need to add Comm100 Live Chat from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Comm100 Live Chat** in the search box.
4. Select **Comm100 Live Chat** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Comm100 Live Chat

Configure and test Microsoft Entra SSO with Comm100 Live Chat using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Comm100 Live Chat.

To configure and test Microsoft Entra SSO with Comm100 Live Chat, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Comm100 Live Chat SSO**- to configure the single sign-on settings on application side.
    1. **Create Comm100 Live Chat test user** - to have a counterpart of B.Simon in Comm100 Live Chat that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Comm100 Live Chat** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following step:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.comm100.com/AdminManage/LoginSSO.aspx?siteId=<SITEID>`

    Note

    The Sign-on URL value isn't real. You update the Sign-on URL value with the actual Sign-on URL, which is explained later in the article.
6. Comm100 Live Chat application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/edit-attribute.png)
7. In addition to above, Comm100 Live Chat application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirement.

    | Name | Source Attribute |
    | --- | --- |
    | email | user.mail |
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
9. On the **Set up Comm100 Live Chat** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Comm100 Live Chat SSO

1. In a different web browser window, sign in to Comm100 Live Chat as a Security Administrator.
2. On the top right side of the page, select **My Account**.

    ![Comm100 Live Chat my account.](media/comm100livechat-tutorial/account.png)
3. From the left side of menu, select **Security** and then select **Agent Single Sign-On**.

    ![Screenshot that shows the left-side account menu with &quot;Security&quot; and &quot;Agent Single Sign-On&quot; highlighted.](media/comm100livechat-tutorial/security.png)
4. On the **Agent Single Sign-On** page, perform the following steps:

    ![Comm100 Live Chat security.](media/comm100livechat-tutorial/certificate.png)

    a. Copy the first highlighted link and paste it in **Sign-on URL** textbox in **Basic SAML Configuration** section.

    b. In the **SAML SSO URL** textbox, paste the value of **Login URL**, which you copied previously.

    c. In the **Remote Logout URL** textbox, paste the value of **Logout URL**, which you copied previously.

    d. Select **Choose a File** to upload the base-64 encoded certificate that you have downloaded, into the **Certificate**.

    e. Select **Save Changes**.

### Create Comm100 Live Chat test user

To enable Microsoft Entra users to sign in to Comm100 Live Chat, they must be provisioned into Comm100 Live Chat. In Comm100 Live Chat, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Sign in to Comm100 Live Chat as a Security Administrator.
2. On the top right side of the page, select **My Account**.

    ![Comm100 Live Chat my account.](media/comm100livechat-tutorial/account.png)
3. From the left side of menu, select **Agents** and then select **New Agent**.

    ![Comm100 Live Chat agent.](media/comm100livechat-tutorial/agent.png)
4. On the **New Agent** page, perform the following steps:

    ![Comm100 Live Chat new agent.](media/comm100livechat-tutorial/new-agent.png)

    a. a. In **Email** text box, enter the email of user like **B.simon@contoso.com**.

    b. In **First Name** text box, enter the first name of user like **B**.

    c. In **Last Name** text box, enter the last name of user like **simon**.

    d. In the **Display Name** textbox, enter the display name of user like **B.simon**

    e. In the **Password** textbox, type your password.

    f. Select **Save**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Comm100 Live Chat Sign-on URL where you can initiate the login flow.
- Go to Comm100 Live Chat Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Comm100 Live Chat tile in the My Apps, this option redirects to Comm100 Live Chat Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
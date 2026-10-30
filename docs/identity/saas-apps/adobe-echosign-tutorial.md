---
layout: Conceptual
title: Configure Adobe Sign for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/adobe-echosign-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Adobe Sign.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 6769b869-58c7-a812-bda8-0ac1888d422a
document_version_independent_id: f2984995-4ff7-ed88-8650-27d880374d15
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/adobe-echosign-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/adobe-echosign-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/adobe-echosign-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 3b0bb828-03ff-e210-6ade-5eb541f1ef44
---

# Configure Adobe Sign for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Adobe Sign with Microsoft Entra ID. When you integrate Adobe Sign with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Adobe Sign.
- Enable your users to be automatically signed-in to Adobe Sign with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Adobe Sign single sign-on (SSO)-enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Adobe Sign supports **SP** initiated SSO.

## Add Adobe Sign from the gallery

To configure the integration of Adobe Sign into Microsoft Entra ID, you need to add Adobe Sign from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Adobe Sign** in the search box.
4. Select **Adobe Sign** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Adobe Sign

In this section, you configure and test Microsoft Entra single sign-on with Adobe Sign based on a test user called **Britta Simon**. For single sign-on to work, a link relationship between a Microsoft Entra user and the related user in Adobe Sign needs to be established.

To configure and test Microsoft Entra single sign-on with Adobe Sign, you need to perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with Britta Simon.
    2. **Assign the Microsoft Entra test user** - to enable Britta Simon to use Microsoft Entra single sign-on.
2. **Configure Adobe Sign SSO**- to configure the Single Sign-On settings on application side.
    1. **Create Adobe Sign test user** - to have a counterpart of Britta Simon in Adobe Sign that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

In this section, you enable Microsoft Entra single sign-on.

To configure Microsoft Entra single sign-on with Adobe Sign, perform the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Adobe Sign** application integration page, select **Single sign-on**.
3. On the **Select a Single sign-on method** dialog, select **SAML/WS-Fed** mode to enable single sign-on.
4. On the **Set up Single Sign-On with SAML** page, select pencil icon to open **Basic SAML Configuration** dialog.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Sign on URL** text box, type a URL using the following pattern: `https://<companyname>.echosign.com/`

    b. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<companyname>.echosign.com`

    Note

    These values aren't real. Update these values with the actual Sign on URL and Identifier. Contact [Adobe Sign Client support team](https://helpx.adobe.com/support.html) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Adobe Sign** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Adobe Sign SSO

1. Before configuration, contact the [Adobe Sign Client support team](https://helpx.adobe.com/support.html) to add your domain in the Adobe Sign allowlist. Here's how to add the domain:

    a. The [Adobe Sign Client support team](https://helpx.adobe.com/support.html) sends you a randomly generated token. For your domain, the token is like the following: **adobe-sign-verification= xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx**

    b. Publish the verification token in a DNS text record, and notify the [Adobe Sign Client support team](https://helpx.adobe.com/support.html).

    Note

    This can take a few days, or longer. Note that DNS propagation delays mean that a value published in DNS might not be visible for an hour or more. Your IT administrator should be knowledgeable about how to publish this token in a DNS text record.

    c. When you notify the [Adobe Sign Client support team](https://helpx.adobe.com/support.html) through the support ticket, after the token is published, they validate the domain and add it to your account.

    d. Generally, here's how to publish the token on a DNS record:

    - Sign in to your domain account
    - Find the page for updating the DNS record. This page might be called DNS Management, Name Server Management, or Advanced Settings.
    - Find the TXT records for your domain.
    - Add a TXT record with the full token value supplied by Adobe.
    - Save your changes.
2. In a different web browser window, sign in to your Adobe Sign company site as an administrator.
3. In the SAML menu, select **Account Settings** &gt; **SAML Settings**.

    ![Screenshot of Adobe Sign SAML Settings page.](media/adobe-echosign-tutorial/settings.png)
4. In the **SAML Settings** section, perform the following steps:

    ![Screenshot that highlights the SAML settings, including SAML Mandatory.](media/adobe-echosign-tutorial/profile.png)

    ![Screenshot of SAML Settings.](media/adobe-echosign-tutorial/certificate.png)

    a. Under **SAML Mode**, select **SAML Mandatory**.

    b. Select **Allow Echosign Account Administrators to log in using their Echosign Credentials**.

    c. Under **User Creation**, select **Automatically add users authenticated through SAML**.

    d. Paste **Microsoft Entra Identifier** into the **Idp Entity ID** text box.

    e. Paste **Login URL** into the **Idp Login URL** text box.

    f. Paste **Logout URL** into the **Idp Logout URL** text box.

    g. Open your downloaded **Certificate(Base64)** file in Notepad. Copy the content of it into your clipboard, and then paste it to the **IdP Certificate** text box.

    h. Select **Save Changes**.

### Create Adobe Sign test user

To enable Microsoft Entra users to sign in to Adobe Sign, they must be provisioned into Adobe Sign. This is a manual task.

Note

You can use any other Adobe Sign user account creation tools or APIs provided by Adobe Sign to provision Microsoft Entra user accounts.

1. Sign in to your **Adobe Sign** company site as an administrator.
2. In the menu on the top, select **Account**. Then, in the left pane, select **Users & Groups** &gt; **Create a new user**.

    ![Screenshot of Adobe Sign company site, with Account, Users &amp;Groups, and Create a new user highlighted](media/adobe-echosign-tutorial/account.png)
3. In the **Create New User** section, perform the following steps:

    ![Screenshot of Create New User section](media/adobe-echosign-tutorial/user.png)

    a. Type the **Email Address**, **First Name**, and **Last Name** of a valid Microsoft Entra account you want to provision into the related text boxes.

    b. Select **Create User**.

Note

The Microsoft Entra account holder receives an email that includes a link to confirm the account, before it becomes active.

### Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Adobe Sign Sign-on URL where you can initiate the login flow.
- Go to Adobe Sign Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Adobe Sign tile in the My Apps, you should be automatically signed in to the Adobe Sign for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
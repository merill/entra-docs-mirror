---
layout: Conceptual
title: Configure Evernote for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/evernote-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Evernote.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 841263bc-ea53-5b90-5e20-c512c11cca1f
document_version_independent_id: 191ddc34-bf98-3677-dc85-86b7866c4d5b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/evernote-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/evernote-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/evernote-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 8ef01151-1cab-975e-10b8-d6f41a7199c1
---

# Configure Evernote for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Evernote with Microsoft Entra ID. When you integrate Evernote with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Evernote.
- Enable your users to be automatically signed-in to Evernote with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Evernote single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Evernote supports **SP and IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Evernote from the gallery

To configure the integration of Evernote into Microsoft Entra ID, you need to add Evernote from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Evernote** in the search box.
4. Select **Evernote** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Evernote

Configure and test Microsoft Entra SSO with Evernote using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Evernote.

To configure and test Microsoft Entra SSO with Evernote, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Evernote SSO**- to configure the single sign-on settings on application side.
    1. **Create Evernote test user** - to have a counterpart of B.Simon in Evernote that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Evernote** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode,perform the following steps:

    In the **Identifier** text box, type the URL: `https://www.evernote.com/saml2`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type the URL: `https://www.evernote.com/Login.action`
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
8. To modify the **Signing** options, select the **Edit** button to open the **SAML Signing Certificate** dialog.

    ![Screenshot that shows the &quot;S A M L Signing Certificate&quot; dialog with the &quot;Edit&quot; button selected.](common/edit-certificate.png)

    a. Select the **Sign SAML response and assertion** option for **Signing Option**.

    b. Select **Save**
9. On the **Set up Evernote** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Evernote SSO

1. In a different web browser window, sign in to your Evernote company site as an administrator
2. Go to **'Admin Console'**

    ![Admin-Console](media/evernote-tutorial/admin.png)
3. From the **'Admin Console'**, go to **‘Security’** and select **‘Single Sign-On’**

    ![SSO-Setting](media/evernote-tutorial/security.png)
4. Configure the following values:

    ![Certificate-Setting](media/evernote-tutorial/certificate.png)

    a. **Enable SSO:** SSO is enabled by default (Select **Disable Single Sign-on** to remove the SSO requirement)

    b. Paste **Login URL** value into the **SAML HTTP Request URL** textbox.

    c. Open the downloaded certificate from Microsoft Entra ID in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE" and paste it into the **X.509 Certificate** textbox.

    d.Select **Save Changes**

### Create Evernote test user

In order to enable Microsoft Entra users to sign into Evernote, they must be provisioned into Evernote. In the case of Evernote, provisioning is a manual task.

**To provision a user accounts, perform the following steps:**

1. Sign in to your Evernote company site as an administrator.
2. Select the **'Admin Console'**.

    ![Admin-Console](media/evernote-tutorial/admin.png)
3. From the **'Admin Console'**, go to **‘Add users’**.

    ![Screenshot that shows the &quot;Users&quot; menu with &quot;Add Users&quot; selected.](media/evernote-tutorial/create-user.png)
4. **Add team members** in the **Email** textbox, type the email address of user account and select **Invite.**

    ![Add-testUser](media/evernote-tutorial/add-user.png)
5. After invitation is sent, the Microsoft Entra account holder will receive an email to accept the invitation.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Evernote Sign on URL where you can initiate the login flow.
- Go to Evernote Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Evernote for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Evernote tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Evernote for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
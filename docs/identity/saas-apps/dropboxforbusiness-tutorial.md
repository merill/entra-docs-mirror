---
layout: Conceptual
title: Configure Dropbox Business for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/dropboxforbusiness-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Dropbox Business.
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 6884bf55-8c3b-aa39-43e3-c0b44dcd6efb
document_version_independent_id: 9f606de5-73dd-8985-cf06-0bc9877c0352
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/dropboxforbusiness-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/dropboxforbusiness-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/dropboxforbusiness-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ef27c330-1a87-c5e6-fa78-bc412bc0a8f0
---

# Configure Dropbox Business for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Dropbox Business with Microsoft Entra ID. When you integrate Dropbox Business with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Dropbox Business.
- Enable your users to be automatically signed-in to Dropbox Business with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Dropbox Business is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Dropbox Business single sign-on (SSO) enabled subscription.

## Scenario description

- In this article, you configure and test Microsoft Entra SSO in a test environment. Dropbox Business supports **SP** initiated SSO.
- Dropbox Business supports [Automated user provisioning and deprovisioning](dropboxforbusiness-provisioning-tutorial).

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Dropbox Business from the gallery

To configure the integration of Dropbox Business into Microsoft Entra ID, you need to add Dropbox Business from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Dropbox Business** in the search box.
4. Select **Dropbox Business** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Dropbox Business

Configure and test Microsoft Entra SSO with Dropbox Business using a test user called **Britta Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Dropbox Business.

To configure and test Microsoft Entra SSO with Dropbox Business, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with Britta Simon.
    2. **Assign the Microsoft Entra test user** - to enable Britta Simon to use Microsoft Entra single sign-on.
2. **Configure Dropbox Business SSO**- to configure the Single Sign-On settings on application side.
    1. **Create Dropbox Business test user** - to have a counterpart of Britta Simon in Dropbox Business that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Dropbox Business** application integration page, find the **Manage** section and select **Single sign-on**.
3. On the **Select a Single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** page, enter the values for the following fields:

    a. In the **Sign on URL** text box, type a URL using the following pattern: `https://www.dropbox.com/sso/<id>`

    b. In the **Identifier (Entity ID)** text box, type the value: `Dropbox`

    c. In the **Reply URL** field, enter `https://www.dropbox.com/saml_login`

    Note

    The **Dropbox Sign SSO ID** can be found in the Dropbox site at Dropbox &gt; Admin console &gt; Settings &gt; Single sign-on &gt; SSO sign-in URL.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Dropbox Business** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Dropbox Business SSO

1. In a different web browser window, sign in to your Dropbox Business company site as an administrator

    ![Screenshot that shows the &quot;Dropbox Business Sign in&quot; page.](media/dropboxforbusiness-tutorial/account.png)
2. Select the **User Icon** and select **Settings** tab.

    ![Screenshot that shows the &quot;USER ICON&quot; action and &quot;Settings&quot; selected.](media/dropboxforbusiness-tutorial/user-icon.png)
3. In the navigation pane on the left side, select **Admin console**.

    ![Screenshot that shows &quot;Admin console&quot; selected.](media/dropboxforbusiness-tutorial/admin-console.png)
4. On the **Admin console**, select **Settings** in the left navigation pane.

    ![Screenshot that shows &quot;Settings&quot; selected.](media/dropboxforbusiness-tutorial/settings.png)
5. Select **Single sign-on** option under the **Authentication** section.

    ![Screenshot that shows the &quot;Authentication&quot; section with &quot;Single sign-on&quot; selected.](media/dropboxforbusiness-tutorial/authentication.png)
6. In the **Single sign-on** section, perform the following steps:

    ![Screenshot that shows the &quot;Single sign-on&quot; configuration settings.](media/dropboxforbusiness-tutorial/configure-sso.png)

    a. Select **Required** as an option from the dropdown for the **Single sign-on**.

    b. Select **Add sign-in URL** and in the **Identity provider sign-in URL** textbox, paste the **Login URL** value which you have copied and then select **Done**.

    ![Configure single sign-on](media/dropboxforbusiness-tutorial/sso.png)

    c. Select **Upload certificate**, and then browse to your **Base64 encoded certificate file** which you have downloaded.

    d. Select **Copy link** and paste the copied value into the **Sign-on URL** textbox of **Dropbox Business Domain and URLs** section on Azure portal.

    e. Select **Save**.

### Create Dropbox Business test user

1. Log in to the Dropbox Business website as an administrator.
2. Go to the **Admin Console** and select **Members** in the left menu.

    ![Screenshot for Invite member](media/dropboxforbusiness-tutorial/invite-member.png)
3. Enter the valid user email to add the user and select **Invite**.

    ![Screenshot for Invite](media/dropboxforbusiness-tutorial/invite-button.png)

This application also supports automatic user provisioning. See how to enable auto provisioning for [Dropbox Business](dropboxforbusiness-provisioning-tutorial).

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Dropbox Business Sign-on URL where you can initiate the login flow.
- Go to Dropbox Business Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Dropbox Business tile in the My Apps, this option redirects to Dropbox Business Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
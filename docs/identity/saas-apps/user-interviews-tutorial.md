---
layout: Conceptual
title: Configure User Interviews for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/user-interviews-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and User Interviews.
services: active-directory
ms.workload: identity
ms.topic: how-to
ms.date: 2024-04-05T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 2b88ef0b-a989-fe0c-d812-5930ccebd5bf
document_version_independent_id: 2b88ef0b-a989-fe0c-d812-5930ccebd5bf
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/user-interviews-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/user-interviews-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/user-interviews-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: aa389449-7eab-5e5a-a61d-b56ba62e2c57
---

# Configure User Interviews for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate User Interviews with Microsoft Entra ID. When you integrate User Interviews with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to User Interviews.
- Enable your users to be automatically signed-in to User Interviews with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- User Interviews single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- User Interviews supports both **SP and IDP** initiated SSO.
- User Interviews supports **Just In Time** user provisioning.

## Add User Interviews from the gallery

To configure the integration of User Interviews into Microsoft Entra ID, you need to add User Interviews from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **User Interviews** in the search box.
4. Select **User Interviews** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for User Interviews

Configure and test Microsoft Entra SSO with User Interviews using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in User Interviews.

To configure and test Microsoft Entra SSO with User Interviews, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Create a Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure User Interviews SSO**- to configure the single sign-on settings on application side.
    1. **Create User Interviews test user** - to have a counterpart of B.Simon in User Interviews that's linked to the Microsoft Entra ID representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **User Interviews** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** text box, type a URL using one of the following patterns:

    | **Identifier** |
    | --- |
    | `https://www.userinterviews.com/saml/metadata?team_id=<team_id>` |
    | `https://www.userinterviews.com/saml/metadata?<team_id>` |

    b. In the **Reply URL** text box, type one of the following URL/Pattern:

    | **Reply URL** |
    | --- |
    | `https://www.userinterviews.com/saml/consume?team_id=<team_id>` |
    | `https://www.userinterviews.com/saml/consume` |
6. Perform the following step, if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://www.userinterviews.com/saml/join?team_id=<team_id>`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign on URL. Contact [User Interviews support team](mailto:support@userinterviews.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section in the Microsoft Entra admin center.
7. User Interviews application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows the image of attributes configuration.](common/default-attributes.png)
8. In addition to above, User Interviews application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | first\_name | user.givenname |
    | last\_name | user.surname |
9. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
10. On the **Set up User Interviews** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration URLs.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure User Interviews SSO

1. Log in to User Interviews company site as an administrator.
2. Go to **Microsoft Entra Setup** &gt; **Team settings** &gt; **Advanced options** and perform the following steps:

    ![Screenshot shows the configuration.](media/user-interviews-tutorial/configuration.png#lightbox)

    a. Open the downloaded **Certificate (Base64)** into Notepad and paste the content into the **SSO Certificate** textbox.

    b. In the **SSO Entity ID** textbox, paste the **Microsoft Entra Identifier** which you have copied from the Microsoft Entra admin center.

    c. In the **SSO URL** textbox, paste the **Login URL** value which you copied from the Microsoft Entra admin center.

    d. Select **Save**.

    e. Copy the **ACS URL** and paste it in the **Reply URL** textbox in the **Basic SAML Configuration** section in the Microsoft Entra admin center.

    f. Copy the **Entity ID** and paste it in the **Identifier (Entity ID)** textbox in the **Basic SAML Configuration** section in the Microsoft Entra admin center.

### Create User Interviews test user

In this section, a user called Britta Simon is created in User Interviews. User Interviews supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in User Interviews, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application** in Microsoft Entra admin center. this option redirects to User Interviews Sign on URL where you can initiate the login flow.
- Go to User Interviews Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application** in Microsoft Entra admin center and you should be automatically signed in to the User Interviews for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the User Interviews tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the User Interviews for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
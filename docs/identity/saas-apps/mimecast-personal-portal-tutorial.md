---
layout: Conceptual
title: Configure Mimecast for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/mimecast-personal-portal-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Mimecast.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 2b85b077-78d6-8994-e5b2-14a05e6d8d2b
document_version_independent_id: 59db0a3a-b498-c417-fb17-6b7659a2f811
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/mimecast-personal-portal-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/mimecast-personal-portal-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/mimecast-personal-portal-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 0d0c93cc-72db-e47c-28ae-cba133342d04
---

# Configure Mimecast for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Mimecast with Microsoft Entra ID. When you integrate Mimecast with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Mimecast.
- Enable your users to be automatically signed-in to Mimecast with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Mimecast single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Mimecast supports **SP and IDP** initiated SSO.

## Add Mimecast from the gallery

To configure the integration of Mimecast into Microsoft Entra ID, you need to add Mimecast from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Mimecast** in the search box.
4. Select **Mimecast** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Mimecast

Configure and test Microsoft Entra SSO with Mimecast using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Mimecast.

To configure and test Microsoft Entra SSO with Mimecast, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Mimecast SSO**- to configure the single sign-on settings on application side.
    1. **Create Mimecast test user** - to have a counterpart of B.Simon in Mimecast that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Mimecast** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in IDP initiated mode, perform the following steps:

    a. In the **Identifier** textbox, type a URL using one of the following patterns:

    | Region | Value |
    | --- | --- |
    | Europe | `https://eu-api.mimecast.com/sso/<accountcode>` |
    | United States | `https://us-api.mimecast.com/sso/<accountcode>` |
    | South Africa | `https://za-api.mimecast.com/sso/<accountcode>` |
    | Australia | `https://au-api.mimecast.com/sso/<accountcode>` |
    | Offshore | `https://jer-api.mimecast.com/sso/<accountcode>` |

    Note

    You find the `accountcode` value in the Mimecast under **Account** &gt; **Settings** &gt; **Account Code**. Append the `accountcode` to the Identifier.

    b. In the **Reply URL** textbox, type one of the following URLs:

    | Region | Value |
    | --- | --- |
    | Europe | `https://eu-api.mimecast.com/login/saml` |
    | United States | `https://us-api.mimecast.com/login/saml` |
    | South Africa | `https://za-api.mimecast.com/login/saml` |
    | Australia | `https://au-api.mimecast.com/login/saml` |
    | Offshore | `https://jer-api.mimecast.com/login/saml` |
6. If you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** textbox, type one of the following URLs:

    | Region | Value |
    | --- | --- |
    | Europe | `https://eu-api.mimecast.com/login/saml` |
    | United States | `https://us-api.mimecast.com/login/saml` |
    | South Africa | `https://za-api.mimecast.com/login/saml` |
    | Australia | `https://au-api.mimecast.com/login/saml` |
    | Offshore | `https://jer-api.mimecast.com/login/saml` |
7. Select **Save**.
8. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![The Certificate download link](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Mimecast SSO

1. In a different web browser window, sign into Mimecast Administration Console.
2. Navigate to **Administration** &gt; **Services** &gt; **Applications**.

    ![Screenshot shows Mimecast window with Applications selected.](media/mimecast-personal-portal-tutorial/services.png)
3. Select **Authentication Profiles** tab.

    ![Screenshot shows the Application tab with Authentication Profiles selected.](media/mimecast-personal-portal-tutorial/authentication-profiles.png)
4. Select **New Authentication Profile** tab.

    ![Screenshot shows new Authentication Profile selected.](media/mimecast-personal-portal-tutorial/new-authenticatio-profile.png)
5. Provide a valid description in the **Description** textbox and select **Enforce SAML Authentication for Mimecast** checkbox.

    ![Screenshot shows New Authentication Profile selected.](media/mimecast-personal-portal-tutorial/selecting-personal-portal.png)
6. On the **SAML Configuration for Mimecast** page, perform the following steps:

    ![Screenshot shows where to select Enforce SAML Authentication for Administration Console.](media/mimecast-personal-portal-tutorial/sso-settings.png)

    a. For **Provider**, select **Microsoft Entra ID** from the Dropdown.

    b. In the **Metadata URL** textbox, paste the **App Federation Metadata URL** value, which you copied previously.

    c. Select **Import**. After importing the Metadata URL, the fields are populated automatically, no need to perform any action on these fields.

    d. Make sure you uncheck **Use Password protected Context** and **Use Integrated Authentication Context** checkboxes.

    e. Select **Save**.

### Create Mimecast test user

1. In a different web browser window, sign into Mimecast Administration Console.
2. Navigate to **Administration** &gt; **Directories** &gt; **Internal Directories**.

    ![Screenshot shows the SAML Configuration for Mimecast where you can enter the values described.](media/mimecast-personal-portal-tutorial/internal-directories.png)
3. Select your domain, if the domain is mentioned below, otherwise please create a new domain by selecting the **New Domain**.

    ![Screenshot shows Mimecast window with Internal Directories selected.](media/mimecast-personal-portal-tutorial/domain-name.png)
4. Select **New Address** tab.

    ![Screenshot shows the domain selected.](media/mimecast-personal-portal-tutorial/new-address.png)
5. Provide the required user information on the following page:

    ![Screenshot shows the page where you can enter the values described.](media/mimecast-personal-portal-tutorial/user-information.png)

    a. In the **Email Address** textbox, enter the email address of the user like `B.Simon@yourdomainname.com`.

    b. In the **Global Name** textbox, enter the **Full name** of the user.

    c. In the **Password** and **Confirm Password** textboxes, enter the password of the user.

    d. Select **Force Change at Login** checkbox.

    e. Select **Save**.

    f. To assign roles to the user, select **Role Edit** and assign the required role to user as per your organization requirement.

    ![Screenshot shows Address Settings where you can select Role Edit.](media/mimecast-personal-portal-tutorial/assign-role.png)

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Mimecast Sign on URL where you can initiate the login flow.
- Go to Mimecast Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Mimecast for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Mimecast tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Mimecast for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
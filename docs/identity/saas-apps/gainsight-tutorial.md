---
layout: Conceptual
title: Configure Gainsight for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/gainsight-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Gainsight.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: ed604438-ca77-d7a7-a1a6-5f12863650d8
document_version_independent_id: 10479091-e211-7117-6e02-6c3d560f5828
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/gainsight-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/gainsight-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/gainsight-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 90b3e18e-89d2-33e8-7c69-c30fd8b254aa
---

# Configure Gainsight for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Gainsight with Microsoft Entra ID. Use Microsoft Entra ID to manage user access and enable single sign-on with Gainsight. Requires an existing Gainsight subscription. When you integrate Gainsight with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Gainsight.
- Enable your users to be automatically signed-in to Gainsight with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You'll configure and test Microsoft Entra single sign-on for Gainsight in a test environment. Gainsight supports both **SP** and **IDP** initiated single sign-on.

## Prerequisites

To integrate Microsoft Entra ID with Gainsight, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Gainsight single sign-on (SSO) enabled subscription.

## Add application and assign a test user

Before you begin the process of configuring single sign-on, you need to add the Gainsight application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the single sign-on configuration.

### Add Gainsight SAML from the Microsoft Entra gallery

Add Gainsight SAML from the Microsoft Entra application gallery to configure single sign-on with Gainsight. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Gainsight** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. Provide any dummy url like (`https://gainsight.com`) in the **Identifier (Entity ID)** and **Reply URL (Assertion Consumer Service URL)** in **Basic SAML Configuration**.
5. On the **Set-up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
6. On the **Set up Gainsight SAML** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration appropriate URL.](common/copy-configuration-urls.png)
7. Now on the Gainsight Side, Navigate to **User Management** and select **Authentication** tab, create a new **SAML** Authentication.

## Setup SAML 2.0 Authentication in Gainsight

Note

SAML 2.0 Authentication allows the users to login to Gainsight via Microsoft Entra ID. Once Gainsight is configured to authenticate via SAML 2.0, users who want to access Gainsight will no longer be prompted to enter a username or password. Instead, an exchange between Gainsight and Microsoft Entra ID occurs that grants Gainsight access to the users.

**To configure SAML 2.0 Authentication:**

1. Log in to your **Gainsight** company site as an administrator.
2. Select **search bar** on the left side menu and select **User Management**.

    ![Screenshot shows the Gainsight Left Nav Search Bar.](media/gainsight-tutorial/search-bar.png)
3. In the **User Management** page, navigate to **Authentication** tab and select **Add Authentication** &gt; **SAML**.

    ![Screenshot shows the Gainsight User Management Authentication Page.](media/gainsight-tutorial/authentication.png)
4. In the **SAML Mechanism** page, perform the following steps:

    ![Screenshot shows how to edit SAML configuration in Gainsight.](media/gainsight-tutorial/connection.png)

    1. Enter a unique connection **Name** in the textbox.
    2. Enter a valid **Email Domain** in the textbox.
    3. In the **Sign In URL** textbox, paste the **Login URL** value, which you copied previously.
    4. In the **Sign Out URL** textbox, paste the **Logout URL** value, which you copied previously.
    5. Open the downloaded **Certificate (Base64)** and upload it into the **Certificate** by selecting **Browse** option.
    6. Select **Save**.
    7. Reopen the new **SAML** Authentication and select edit on the newly created connection, and download the **metadata**. Open the **metadata** file in your favorite Editor, and copy **entityID** and **Assertion Consumer Service Location URL**.

    Note

    For more information on SAML creation, please refer [GAINSIGHT SAML](https://support.gainsight.com/Gainsight_NXT/01Onboarding_and_Implementation/Onboarding_for_Gainsight_NXT/Login_and_Permissions/03Gainsight_Authentication).
5. Now back to Azure portal, On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
6. On the **Basic SAML Configuration** section, using the values obtained in the Step 4, perform the following steps:

    a. In the **Identifier (Entity ID)** textbox, type a value using one of the following patterns:

    | **Identifier** |
    | --- |
    | `urn:auth0:gainsight:<ID>` |
    | `urn:auth0:gainsight-eu:<ID>` |

    b. In the **Reply URL (Assertion Consumer Service URL)** textbox, type a URL using one of the following patterns:

    | **Reply URL** |
    | --- |
    | `https://secured.gainsightcloud.com/login/callback connection=<ID>` |
    | `https://secured.eu.gainsightcloud.com/login/callback?connection=<ID>` |
7. Perform the following step, if you wish to configure the application in **SP** initiated mode:

    In the **Sign on URL** textbox, type a URL using one of the following patterns:

    | **Sign on URL** |
    | --- |
    | `https://secured.gainsightcloud.com/samlp/<ID>` |
    | `https://secured.eu.gainsightcloud.com/samlp/<ID>` |

## Create Gainsight test user

1. In a different web browser window, sign in to your Gainsight website as an administrator.
2. In the **User Management** page, navigate to **Users** &gt; **Add User**.

    ![Screenshot shows how to add users in Gainsight.](media/gainsight-tutorial/user.png)
3. Fill required fields and select **Save**. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Gainsight Sign-on URL where you can initiate the login flow.
- Go to Gainsight Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Gainsight for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Gainsight tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Gainsight for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
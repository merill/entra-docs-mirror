---
layout: Conceptual
title: Configure New Relic by Account for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/new-relic-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and New Relic by Account.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 972b42e1-42bf-fbc6-2e9a-609ad655a955
document_version_independent_id: a76ded28-f72b-9d6d-2165-4f4d011052f3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/new-relic-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/new-relic-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/new-relic-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 73cc03d4-524f-c2d3-c3f3-cff2839ab32c
---

# Configure New Relic by Account for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate New Relic by Account with Microsoft Entra ID. When you integrate New Relic by Account with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to New Relic by Account.
- Enable your users to be automatically signed-in to New Relic by Account with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Note

This document is only relevant if you're using the [Original User Model](https://docs.newrelic.com/docs/accounts/original-accounts-billing/original-users-roles/overview-user-models/) in New Relic. Please refer to [New Relic (By Organization)](new-relic-limited-release-tutorial) if you're using New Relic's newer user model.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- New Relic by Account single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- New Relic by Account supports **SP** initiated SSO
- New Relic supports [**automated user provisioning and deprovisioning**](new-relic-by-organization-provisioning-tutorial) (recommended).

## Add New Relic by Account from the gallery

To configure the integration of New Relic by Account into Microsoft Entra ID, you need to add New Relic by Account from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **New Relic by Account** in the search box.
4. Select **New Relic by Account** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for New Relic by Account

Configure and test Microsoft Entra SSO with New Relic by Account using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in New Relic by Account.

To configure and test Microsoft Entra SSO with New Relic by Account, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    - **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    - **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure New Relic by Account SSO**- to configure the single sign-on settings on application side.
    - **Create New Relic by Account test user** - to have a counterpart of B.Simon in New Relic by Account that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New Relic by Account** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Sign on URL** text box, type the URL using the following pattern:

    `https://rpm.newrelic.com:443/accounts/{acc_id}/sso/saml/finalize` - Be sure to substitute `acc_id` with your own Account ID of New Relic by Account.

    b. In the **Identifier (Entity ID)** text box, type the URL: `rpm.newrelic.com`
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up New Relic by Account** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure New Relic by Account SSO

1. In a different web browser window, sign on to your **New Relic by Account** company site as administrator.
2. In the menu on the top, select **Account Settings**.

    ![Screenshot shows the Welcome page with Account settings selected.](media/new-relic-tutorial/settings.png)
3. Select the **Security and authentication** tab, and then select the **Single sign on** tab.

    ![Single Sign-On](media/new-relic-tutorial/single-sign-on-tab.png)
4. On the SAML dialog page, perform the following steps:

    ![SAML](media/new-relic-tutorial/save.png)

    a. Select **Choose File** to upload your downloaded Microsoft Entra certificate.

    b. In the **Remote login URL** textbox, paste the value of **Login URL**.

    c. In the **Logout landing URL** textbox, paste the value of **Logout URL**.

    d. Select **Save my changes**.

### Create New Relic by Account test user

1. Sign into your **New Relic by Account** company site as administrator.
2. In the menu on the top, select **Account Settings**.

    ![Screenshot shows Account settings selected from the Welcome page.](media/new-relic-tutorial/account.png)
3. In the **Account** pane on the left side, select **Summary**, and then select **Add user**.

    ![Screenshot shows the Summary pane where you can select Add user.](media/new-relic-tutorial/add.png)
4. On the **Active users** dialog, perform the following steps:

    ![Active Users](media/new-relic-tutorial/user.png)

    a. In the **Email** textbox, type the email address of a valid Microsoft Entra user you want to provision.

    b. As **Role** select **User**.

    c. Select **Add this user**.

Note

You can use any other New Relic by Account user account creation tools or APIs provided by New Relic by Account to provision Microsoft Entra user accounts.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to New Relic by Account Sign-on URL where you can initiate the login flow.
- Go to New Relic by Account Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the New Relic by Account tile in the My Apps, this option redirects to New Relic by Account Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
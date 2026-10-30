---
layout: Conceptual
title: Configure Timeclock 365 SAML for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/timeclock-365-saml-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Timeclock 365 SAML.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 3cb02b9c-e6f4-35f0-2a89-5d6056d2cd9c
document_version_independent_id: ebccbc65-b581-e30b-1252-f1e5662754a9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/timeclock-365-saml-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/timeclock-365-saml-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/timeclock-365-saml-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ea694065-8ca1-3d3a-b881-c4037eb5243e
---

# Configure Timeclock 365 SAML for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Timeclock 365 SAML with Microsoft Entra ID. When you integrate Timeclock 365 SAML with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Timeclock 365 SAML.
- Enable your users to be automatically signed-in to Timeclock 365 SAML with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Timeclock 365 SAML single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Timeclock 365 SAML supports **SP** initiated SSO.
- Timeclock 365 SAML supports [Automated user provisioning](timeclock-365-saml-provisioning-tutorial).

## Adding Timeclock 365 SAML from the gallery

To configure the integration of Timeclock 365 SAML into Microsoft Entra ID, you need to add Timeclock 365 SAML from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Timeclock 365 SAML** in the search box.
4. Select **Timeclock 365 SAML** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Timeclock 365 SAML

Configure and test Microsoft Entra SSO with Timeclock 365 SAML using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Timeclock 365 SAML.

To configure and test Microsoft Entra SSO with Timeclock 365 SAML, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Timeclock 365 SAML SSO**- to configure the single sign-on settings on application side.
    1. **Create Timeclock 365 SAML test user** - to have a counterpart of B.Simon in Timeclock 365 SAML that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Timeclock 365 SAML** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    In the **Sign-on URL** text box, type the URL: `https://live.timeclock365.com/login`
6. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![The Certificate download link](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Timeclock 365 SAML SSO

1. In a different web browser window, sign in to your up Timeclock 365 SAML company site as an administrator
2. Perform the below mentioned steps.

    ![Timeclock configuration](media/timeclock-365-saml-tutorial/saml-configuration.png)

    a. Go to the **Settings &gt; Company profile &gt; Settings** tab.

    b. In the **IDP metadata path**, paste the **App Federation Metadata Url** that you copied previously.

    c. Then, select **Update**.

### Create Timeclock 365 SAML test user

1. Open a new tab in your browser, and sign in to your Timeclock 365 SAML company site as an administrator.
2. Go to the **Users &gt; Add new user**.

    ![Create test user1](media/timeclock-365-saml-tutorial/add-user-1.png)
3. Provide all the required information in the **User information** page and select **Save**.

    ![Create test user2](media/timeclock-365-saml-tutorial/add-user-2.png)
4. Select **Create** button to create the test user.

Note

Timeclock 365 SAML also supports automatic user provisioning, you can find more details [here](timeclock-365-saml-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Timeclock 365 SAML Sign-on URL where you can initiate the login flow.
- Go to Timeclock 365 SAML Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Timeclock 365 SAML tile in the My Apps, this option redirects to Timeclock 365 SAML Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
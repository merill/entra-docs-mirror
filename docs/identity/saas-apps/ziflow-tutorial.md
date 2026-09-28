---
layout: Conceptual
title: Configure Ziflow for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/ziflow-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Ziflow.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 0dc802e9-f50a-908a-3311-d3e879f13a5b
document_version_independent_id: 081b7c21-51e5-eaf2-91b9-5f968beed1de
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/ziflow-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/ziflow-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/ziflow-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 8c6a23ea-9542-b008-6bd7-ecab837493cb
---

# Configure Ziflow for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Ziflow with Microsoft Entra ID. When you integrate Ziflow with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Ziflow.
- Enable your users to be automatically signed-in to Ziflow with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Ziflow single sign-on enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Ziflow supports **SP** initiated SSO.

## Add Ziflow from the gallery

To configure the integration of Ziflow into Microsoft Entra ID, you need to add Ziflow from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Ziflow** in the search box.
4. Select **Ziflow** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Ziflow

Configure and test Microsoft Entra SSO with Ziflow using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Ziflow.

To configure and test Microsoft Entra SSO with Ziflow, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Ziflow SSO**- to configure the single sign-on settings on application side.
    1. **Create Ziflow test user** - to have a counterpart of B.Simon in Ziflow that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Ziflow** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a value using the following pattern: `urn:auth0:ziflow-production:<UNIQUE_ID>`

    b. In the **Sign on URL** text box, type a URL using the following pattern: `https://ziflow-production.auth0.com/login/callback?connection=<UNIQUE_ID>`

    c. In the **Reply URL** text box, type a URL using the following pattern: `https://ziflow-production.auth0.com/login/callback?connection=<UNIQUE_ID>`

    Note

    The preceding values aren't real. You update the unique ID value in the Identifier, Sign on URL and Reply URL with actual value, which is explained later in the article.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Ziflow** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Ziflow SSO

1. In a different web browser window, sign in to Ziflow as a Security Administrator.
2. Select Avatar in the top right corner, and then select **Manage account**.

    ![Screenshot for Ziflow Configuration Manage](media/ziflow-tutorial/manage-account.png)
3. In the top left, select **Single Sign-On**.

    ![Screenshot for Ziflow Configuration Sign](media/ziflow-tutorial/configuration.png)
4. On the **Single Sign-On** page, perform the following steps:

    ![Screenshot for Ziflow Configuration Single](media/ziflow-tutorial/page.png)

    a. Select **Type** as **SAML2.0**.

    b. In the **Sign In URL** textbox, paste the value of **Login URL**, which you copied previously.

    c. Upload the base-64 encoded certificate that you have downloaded, into the **X509 Signing Certificate**.

    d. In the **Sign Out URL** textbox, paste the value of **Logout URL**, which you copied previously.

    e. From the **Configuration Settings for your Identifier Provider** section, copy the highlighted unique ID value and append it with the Identifier and Sign on URL in the **Basic SAML Configuration** on Azure portal.

### Create Ziflow test user

To enable Microsoft Entra users to sign in to Ziflow, they must be provisioned into Ziflow. In Ziflow, provisioning is a manual task.

To provision a user account, perform the following steps:

1. Sign in to Ziflow as a Security Administrator.
2. Navigate to **People** on the top.

    ![Screenshot for Ziflow Configuration people](media/ziflow-tutorial/people.png)
3. Select **Add** and then select **Add user**.

    ![Screenshot shows the Add user option selected.](media/ziflow-tutorial/add-tab.png)
4. On the **Add a user** pop-up, perform the following steps:

    ![Screenshot shows the Add a user dialog box where you can enter the values described.](media/ziflow-tutorial/add-user.png)

    a. In **Email** text box, enter the email of user like brittasimon@contoso.com.

    b. In **First name** text box, enter the first name of user like Britta.

    c. In **Last name** text box, enter the last name of user like Simon.

    d. Select your Ziflow role.

    e. Select **Add 1 user**.

    Note

    The Microsoft Entra account holder receives an email and follows a link to confirm their account before it becomes active.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Ziflow Sign-on URL where you can initiate the login flow.
- Go to Ziflow Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Ziflow tile in the My Apps, this option redirects to Ziflow Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
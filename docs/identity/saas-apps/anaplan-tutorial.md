---
layout: Conceptual
title: Configure Anaplan for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/anaplan-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Anaplan.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 75cc63ae-c2ed-63a8-f85a-da4fc1bc2eeb
document_version_independent_id: 1634b57b-f1bf-33b7-bc9a-3d33a0317cec
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/anaplan-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/anaplan-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/anaplan-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 6d017a56-f2c2-5c20-fbc3-36a2570f75fb
---

# Configure Anaplan for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Anaplan with Microsoft Entra ID. When you integrate Anaplan with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Anaplan.
- Enable your users to be automatically signed-in to Anaplan with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Anaplan single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Anaplan supports **SP** initiated SSO.

## Add Anaplan from the gallery

To configure the integration of Anaplan into Microsoft Entra ID, you need to add Anaplan from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Anaplan** in the search box.
4. Select **Anaplan** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Anaplan

Configure and test Microsoft Entra SSO with Anaplan using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Anaplan.

To configure and test Microsoft Entra SSO with Anaplan, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Anaplan SSO**- to configure the single sign-on settings on application side.
    1. **Create Anaplan test user** - to have a counterpart of B.Simon in Anaplan that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Anaplan** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select the copy icon to copy the **App Federation Metadata URL** and save this to use in the Anaplan SSO configuration.

    ![The Certificate download link.](common/copy-metadataurl.png)

## Configure Anaplan SSO

1. Log in to Anaplan website as an administrator.
2. In the Administration page, navigate to **Security &gt; Single Sign-On**.
3. Select **New**.
4. Perform the following steps in the **Metadata** tab:

    ![Screenshot for the security page.](media/anaplan-tutorial/security.png)

    a. Enter a **Connection Name**, should match the name of your connection in the identity provider interface.

    b. Select **Load from XML file** and paste the App Federation Metadata URL you into the **Metadata URL** textbox.

    c. Select **Save** to create the connection.

    d. Enable the connection by setting the **Enabled** toggle.
5. From the **Config** tab, copy the following values to save them back to the Azure portal:

    a. **Service Provider URL**. b. **Assertion Consumer Service URL**. c. **Entity ID**.

### Complete the Microsoft Entra SSO Configuration

1. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration.](common/edit-urls.png)
2. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, paste the Entity ID that you copied from above, in the format: `https://sdp.anaplan.com/<optional extension>`

    b. In the **Sign on URL** text box, paste the Service Provider URL that you copied from above, in the format: `https://us1a.app.anaplan.com/samlsp/<connection name>`

    c. In the **Reply URL (Assertion Consumer Service URL)** text box, paste the Assertion Consumer Service URL that you copied from above, in the format: `https://us1a.app.anaplan.com/samlsp/login/callback?connection=<connection name>`

### Complete the Anaplan SSO Configuration

1. Perform the following steps in the **Advanced** tab:

    ![Screenshot for the Advanced page.](media/anaplan-tutorial/advanced.png)

    a. Select **Name ID Format** as Email Address from the dropdown and keep the remaining values as default.

    b. Select **Save**.
2. In the **Workspaces** tab, specify the workspaces that use the identity provider from the dropdown and Select **Save**.

    ![Screenshot for the Workspaces page.](media/anaplan-tutorial/workspaces.png)

    Note

    Workspace connections are unique. If you have another connection already configured with a workspace, you can't associate that workspace with a new connection. To access the original connection and update it, remove the workspace from the connection and then reassociate it with the new connection.

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

### Create Anaplan test user

In this section, you create a user called Britta Simon in Anaplan. Work with [Anaplan support team](mailto:support@anaplan.com) to add the users in the Anaplan platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Anaplan Sign-on URL where you can initiate the login flow.
- Go to Anaplan Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Anaplan tile in the My Apps, this option redirects to Anaplan Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
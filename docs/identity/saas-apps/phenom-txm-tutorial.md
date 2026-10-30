---
layout: Conceptual
title: Configure Phenom TXM for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/phenom-txm-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Phenom TXM.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 857f5d85-c9ac-d4c9-2b06-7ca07676ae0a
document_version_independent_id: d0789aa5-2e4f-468e-224a-cc646f1bad33
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/phenom-txm-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/phenom-txm-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/phenom-txm-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 9df0aaaa-6127-574d-12e4-71f68bdac758
---

# Configure Phenom TXM for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Phenom TXM with Microsoft Entra ID. When you integrate Phenom TXM with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Phenom TXM.
- Enable your users to be automatically signed-in to Phenom TXM with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Phenom TXM single sign-on (SSO) enabled subscription and a user account with the Client Admin role in Service Hub.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Phenom TXM supports **SP** and **IDP** initiated SSO.

## Add Phenom TXM from the gallery

To configure the integration of Phenom TXM into Microsoft Entra ID, you need to add Phenom TXM from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Phenom TXM** in the search box.
4. Select **Phenom TXM** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Phenom TXM

Configure and test Microsoft Entra SSO with Phenom TXM using a test user called **B.Simon**. For SSO to work, you need to establish an assignment relationship between a Microsoft Entra user or group and the related Phenom TXM application, ensuring that Microsoft Entra ID passes the user's email address to Phenom TXM as a user identifier.

To configure and test Microsoft Entra SSO with Phenom TXM, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Phenom TXM SSO**- to configure the single sign-on settings on application side.
    1. **Create Phenom TXM test user** - to have a counterpart of B.Simon in Phenom TXM that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Phenom TXM** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** text box, enter the **ENTITY ID** copied from Service Hub.

    b. In the **Reply URL** text box, enter the **Redirect URI (ACS URL)** copied from Service Hub.

    1. In the first **Reply URL** text box, enter the **Redirect URI (ACS URL)** copied from Service Hub and set the Index value to **0**.
    2. In the second **Reply URL** text box, enter the **Redirect URI (ACS URL) SP Initiated Flow** copied from Service Hub and set the Index value to **1**

    Note

    Ensure that the first **Reply URL** is set as the **Default** using the checkbox.
6. Perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign on URL** text box, type one of the following URLs:

    | Environment | Sign on URL |
    | --- | --- |
    | Staging | `https://login-stg.phenompro.com` |
    | Production | `https://login.phenom.com` |
7. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Phenom TXM SSO

1. Log in to your Phenom TXM instance Service Hub as a user with the Client Admin role.
2. Go to **Settings** tab &gt; **Identity Provider**.
3. In the **Identity Provider** section, perform the following steps:

    ![Screenshot that shows the Configuration Settings.](media/phenom-txm-tutorial/input.png)

    ![Screenshot that shows the Identity Provider Metadata.](media/phenom-txm-tutorial/certificate.png)

    a. Choose **SAML** from the dropdown selector.

    b. Enter a valid name in the **Display Name** textbox.

    c. In the **Single SignOn URL** textbox, paste the **Login URL** value, which you've copied.

    d. In the **Meta data URL** textbox, paste the **App Federation Metadata Url** value, which you've copied.

    e. Copy **Entity ID** value, paste this value into the **Identifier** text box in the **Basic SAML Configuration** section.

    f. Copy **Redirect URI (ACS URL)** value, paste this value into the first **Reply URL** text box in the **Basic SAML Configuration** section.

    g. Copy **Redirect URI (ACS URL) SP Initiated Flow** value, paste this value into the second **Reply URL** text box in the **Basic SAML Configuration** section.

### Create Phenom TXM test user

1. In a different web browser window, log in to your Phenom TXM website as an administrator.
2. Go to **Users** tab and select **Create Users** &gt; **Create single new User**.
3. In the **Create User** page, perform the following steps:

    a. In the **User Information** section, enter a valid **First Name**, **Last Name** and **Work Email** in the textboxes and select **Continue**.

    ![Screenshot that shows the User Information fields.](media/phenom-txm-tutorial/name.png)

    b. In the **Assign Tenants** section, **Select Tenants** and select **Continue**.

    ![Screenshot that shows the Tenants Information fields.](media/phenom-txm-tutorial/details.png)

    c. In the **Assign Roles** section, **Select roles** from the dropdown and select **Continue**.

    ![Screenshot that shows the Roles Mapping for Users.](media/phenom-txm-tutorial/role.png)

    d. In the **Summary** section, review your selections and select **Finish** to create a user.

    ![Screenshot that shows the Phenom TXM Summary section.](media/phenom-txm-tutorial/finish.png)

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Phenom TXM Sign-on URL where you can initiate the login flow.
- Go to Phenom TXM Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Phenom TXM for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Phenom TXM tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Phenom TXM for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
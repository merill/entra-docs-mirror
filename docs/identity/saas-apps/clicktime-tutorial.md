---
layout: Conceptual
title: Configure ClickTime for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/clicktime-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and ClickTime.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: e9d7c0e2-5a9f-79c0-c3cb-f5a5bde69a59
document_version_independent_id: 5d9da1fb-0990-6ee9-08e0-d8bc65c210db
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/clicktime-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/clicktime-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/clicktime-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c0a5f0ec-8383-381d-bac4-33b5b47fe9bf
---

# Configure ClickTime for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate ClickTime with Microsoft Entra ID. When you integrate ClickTime with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to ClickTime.
- Enable your users to be automatically signed-in to ClickTime with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- ClickTime single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- ClickTime supports **IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add ClickTime from the gallery

To configure the integration of ClickTime into Microsoft Entra ID, you need to add ClickTime from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **ClickTime** in the search box.
4. Select **ClickTime** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for ClickTime

Configure and test Microsoft Entra SSO with ClickTime using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in ClickTime.

To configure and test Microsoft Entra SSO with ClickTime, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure ClickTime SSO**- to configure the single sign-on settings on application side.
    1. **Create ClickTime test user** - to have a counterpart of B.Simon in ClickTime that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **ClickTime** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Set up Single Sign-On with SAML** page, perform the following steps:

    a. In the **Identifier** text box, type the URL: `https://app.clicktime.com/sp/`

    b. In the **Reply URL** text box, type one of the following URLs:

    | **Reply URL** |
    | --- |
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up ClickTime** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure ClickTime SSO

1. In a different web browser window, log into your ClickTime company site as an administrator.
2. In the toolbar on the top, select **Preferences**, and then select **Security Settings**.
3. In the **Single Sign-On Preferences** configuration section, perform the following steps:

    ![Security Settings](media/clicktime-tutorial/toolbar.png)

    a. Select **Allow** sign-in using Single Sign-On (SSO) with **Microsoft Entra ID**.

    b. In the **Identity Provider Endpoint** textbox, paste **Login URL**..

    c. Open the **base-64 encoded certificate** downloaded from Azure portal in **Notepad**, copy the content, and then paste it into the **X.509 Certificate** textbox.

    d. Select **Save**.

### Create ClickTime test user

In order to enable Microsoft Entra users to log into ClickTime, they must be provisioned into ClickTime. In the case of ClickTime, provisioning is a manual task.

Note

You can use any other ClickTime user account creation tools or APIs provided by ClickTime to provision Microsoft Entra user accounts.

**To provision a user account, perform the following steps:**

1. Log in to your **ClickTime** tenant.
2. In the toolbar on the top, select **Company**, and then select **People**.

    ![Screenshot shows the ClickTime tenant with Company and People selected.](media/clicktime-tutorial/account.png)
3. Select **Add Person**.

    ![Add Person](media/clicktime-tutorial/company.png)
4. In the New Person section, perform the following steps:

    ![Screenshot shows the Add Person section where you can add the information in this step.](media/clicktime-tutorial/information.png)

    a. In the **full name** textbox, type full name of user like **Britta Simon**.

    b. In the **email address** textbox, type the email of user like **brittasimon@contoso.com**.

    Note

    If you want to, you can set additional properties of the new person object.

    c. Select **Save**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the ClickTime for which you set up the SSO.
- You can use Microsoft My Apps. When you select the ClickTime tile in the My Apps, you should be automatically signed in to the ClickTime for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
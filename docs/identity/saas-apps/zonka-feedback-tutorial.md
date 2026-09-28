---
layout: Conceptual
title: Configure Zonka Feedback for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/zonka-feedback-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Zonka Feedback.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 9507177d-38e3-291a-1a76-25c47663ca69
document_version_independent_id: 9507177d-38e3-291a-1a76-25c47663ca69
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/zonka-feedback-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/zonka-feedback-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/zonka-feedback-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 2033eb49-63d7-94bf-6d3f-88f4ba750d99
---

# Configure Zonka Feedback for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Zonka Feedback with Microsoft Entra ID. When you integrate Zonka Feedback with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Zonka Feedback.
- Enable your users to be automatically signed-in to Zonka Feedback with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Zonka Feedback single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Zonka Feedback supports **SP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Zonka Feedback from the gallery

To configure the integration of Zonka Feedback into Microsoft Entra ID, you need to add Zonka Feedback from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Zonka Feedback** in the search box.
4. Select **Zonka Feedback** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Zonka Feedback

Configure and test Microsoft Entra SSO with Zonka Feedback using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Zonka Feedback.

To configure and test Microsoft Entra SSO with Zonka Feedback, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Zonka Feedback SSO**- to configure the single sign-on settings on application side.
    1. **Create Zonka Feedback test user** - to have a counterpart of B.Simon in Zonka Feedback that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Zonka Feedback** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type the value: `zonkafeedback`

    b. In the **Reply URL** text box, type one of the following URLs:

    | **Reply URL** |
    | --- |
    | `https://us1.zonkafeedback.com/api/v1/sso/saml` |
    | `https://e.zonkafeedback.com/api/v1/sso/saml` |

    c. In the **Sign on URL** text box, type one of the following URLs:

    | **Sign on URL** |
    | --- |
    | `https://us1.zonkafeedback.com/api/v1/sso/saml` |
    | `https://e.zonkafeedback.com/api/v1/sso/saml` |
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
7. On the **Set up Zonka Feedback** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration URLs.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Zonka Feedback SSO

1. Log in to Zonka Feedback company site as an administrator.
2. Go to **Settings (gear icon)** &gt; **Account** &gt; and select **SSO**.
3. In the **Single Sign On** page, perform the following steps.

    ![Screenshot shows settings of the configuration.](media/zonka-feedback-tutorial/settings.png)

    1. In the **SSO Provider** section, select **Microsoft Entra ID** radio button.
    2. In the **SAML SSO URL** textbox, paste the **Login URL**, which you have copied from the Microsoft Entra admin center.
    3. In the **Identity Provider Issuer** textbox, paste the **Identifier (Entity ID)** value, which you have copied from the **Basic SAML Configuration** section in the Microsoft Entra admin center.
    4. Open the downloaded **Certificate (Base64)** into Notepad and paste the content into the **Public Certificate** textbox.
    5. Select **Save**.

### Create Zonka Feedback test user

1. In a different web browser window, sign into Zonka Feedback website as an administrator.
2. Navigate to **Settings** &gt; **Users** &gt; **All Users** and select **Add User**.

    ![Screenshot shows how to create users in application.](media/zonka-feedback-tutorial/create.png)
3. In the **Invite New Users** section, perform the following steps:

    ![Screenshot shows how to create new users in the page.](media/zonka-feedback-tutorial/details.png)

    1. Enter a valid email address in the textbox.
    2. Select **Invite**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application** in Microsoft Entra admin center. this option redirects to Zonka Feedback Sign-on URL where you can initiate the login flow.
- Go to Zonka Feedback Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Zonka Feedback tile in the My Apps, this option redirects to Zonka Feedback Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
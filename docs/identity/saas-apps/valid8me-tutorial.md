---
layout: Conceptual
title: Configure valid8Me for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/valid8me-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and valid8Me.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 5946641b-da00-6236-b2f9-6c3540529ccf
document_version_independent_id: deeb41eb-faba-bb20-e44e-df89b47ea697
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/valid8me-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/valid8me-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/valid8me-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 5fa38abf-8cab-87d4-403e-e15bc83341bf
---

# Configure valid8Me for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate valid8Me with Microsoft Entra ID. When you integrate valid8Me with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to valid8Me.
- Enable your users to be automatically signed-in to valid8Me with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- valid8Me single sign-on (SSO) enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- valid8Me supports **SP** and **IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add valid8Me from the gallery

To configure the integration of valid8Me into Microsoft Entra ID, you need to add valid8Me from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **valid8Me** in the search box.
4. Select **valid8Me** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for valid8Me

Configure and test Microsoft Entra SSO with valid8Me using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user at valid8Me.

To configure and test Microsoft Entra SSO with valid8Me, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure valid8Me SSO**- to configure the single sign-on settings on application side.
    1. **Create valid8Me test user** - to have a counterpart of B.Simon in valid8Me that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **valid8Me** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, the user doesn't have to perform any step as the app is already pre-integrated with Azure.
6. If you wish to configure the application in **SP** initiated mode:

    In the **Sign on URL (Optional)** text box, type a URL using the following pattern: `https://login.valid8me.com/?idp=https://sts.windows.net/${TenantID}/`

    Note

    This value isn't real. Update this value with the actual Sign on URL. Contact [valid8Me support team](mailto:support@valid8me.com) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
8. On the **Set up valid8Me** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration appropriate URL.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure valid8Me SSO

1. Log in to your valid8Me company site as an administrator.
2. From the left side menu, expand **Configuration** &gt; **Single Sign On** &gt; **Identity Management** tab and select **Create**.
3. In the **Microsoft Entra SAML settings** section, perform the following steps:

    a. In the **Login URL** textbox, paste the **Login URL** value, which you copied previously.

    b. In the **Microsoft Entra Identifier** textbox, paste the **Microsoft Entra Identifier** value, which you copied previously.

    c. In the **Logout URL** textbox, paste the **Logout URL** value, which you copied previously.

    d. Open the downloaded **Certificate (Base64)** into Notepad and upload file into the **Certificate (Base64)** textbox.

    e. Select **Create**.

### Create valid8Me test user

1. In a different web browser window, log in to your valid8Me website as an administrator.
2. Navigate to **Configuration** &gt; **Single Sign On** &gt; **Invitation** tab and select **Create**.
3. Perform the following steps in the **Create** page:

    ![Screenshot that shows the User Information fields.](media/valid8me-tutorial/user.png)

    1. Enter a valid email domain in the **Email Suffixes** textbox.

        Note

        the domain name should be same as Microsoft Entra account email domain.
    2. Select one of the **System Roles** according to your requirement.
    3. Select **Create**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to valid8Me Sign on URL where you can initiate the login flow.
- Go to valid8Me Sign on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the valid8Me for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the valid8Me tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the valid8Me for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
---
layout: Conceptual
title: Configure UserEcho for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/userecho-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and UserEcho.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 67dbf055-74e3-2712-41b4-e0b0fb4b7e05
document_version_independent_id: 0bea6377-273d-04bb-0928-6aac504f4ded
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/userecho-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/userecho-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/userecho-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 326d2ffb-eaf2-7d30-b135-b3590a0aff6f
---

# Configure UserEcho for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate UserEcho with Microsoft Entra ID. When you integrate UserEcho with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to UserEcho.
- Enable your users to be automatically signed-in to UserEcho with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To configure Microsoft Entra integration with UserEcho, you need the following items:

- A Microsoft Entra subscription. If you don't have a Microsoft Entra environment, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- UserEcho single sign-on enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- UserEcho supports **SP** initiated SSO.

## Add UserEcho from the gallery

To configure the integration of UserEcho into Microsoft Entra ID, you need to add UserEcho from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **UserEcho** in the search box.
4. Select **UserEcho** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for UserEcho

Configure and test Microsoft Entra SSO with UserEcho using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in UserEcho.

To configure and test Microsoft Entra SSO with UserEcho, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure UserEcho SSO**- to configure the single sign-on settings on application side.
    1. **Create UserEcho test user** - to have a counterpart of B.Simon in UserEcho that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **UserEcho** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic S A M L Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<companyname>.userecho.com/saml/metadata/`

    b. In the **Sign on URL** text box, type a URL using the following pattern: `https://<companyname>.userecho.com/`

    Note

    These values aren't real. Update these values with the actual Identifier and Sign on URL. Contact [UserEcho Client support team](https://feedback.userecho.com/) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
7. On the **Set up UserEcho** section, copy the appropriate URL(s) as per your requirement.

    ![Screenshot shows to copy configuration appropriate U R L.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure UserEcho SSO

1. In another browser window, sign on to your UserEcho company site as an administrator.
2. In the toolbar on the top, select your user name to expand the menu, and then select **Setup**.

    ![Screenshot shows Setup selected from the UserEcho site.](media/userecho-tutorial/profile.png)
3. Select **Integrations**.

    ![Screenshot shows Integrations selected from the Settings menu.](media/userecho-tutorial/menu.png)
4. Select **Website**, and then select **Single sign-on (SAML2)**.

    ![Screenshot shows Single sign-on SAML2 selected from the Integrations menu.](media/userecho-tutorial/website.png)
5. On the **Single sign-on (SAML)** page, perform the following steps:

    ![Screenshot shows the Single Sign-on SAML page where you can enter the values described.](media/userecho-tutorial/values.png)

    a. As **SAML-enabled**, select **Yes**.

    b. Paste **Login URL** into the **SAML SSO URL** textbox.

    c. Paste **Logout URL** into the **Remote Logout URL** textbox.

    d. Open your downloaded certificate in Notepad, copy the content, and then paste it into the **X.509 Certificate** textbox.

    e. Select **Save**.

### Create UserEcho test user

The objective of this section is to create a user called Britta Simon in UserEcho.

**To create a user called Britta Simon in UserEcho, perform the following steps:**

1. Sign-on to your UserEcho company site as an administrator.
2. In the toolbar on the top, select your user name to expand the menu, and then select **Setup**.

    ![Screenshot shows Setup selected from the UserEcho site.](media/userecho-tutorial/profile.png)
3. Select **Users**, to expand the **Users** section.

    ![Screenshot shows Users selected from the Settings menu.](media/userecho-tutorial/user.png)
4. Select **Users**.

    ![Screenshot shows Users selected button.](media/userecho-tutorial/new-user.png)
5. Select **Invite a new user**.

    ![Screenshot shows the Invite a new user control.](media/userecho-tutorial/control.png)
6. On the **Invite a new user** dialog, perform the following steps:

    ![Screenshot shows the Invite a new user dialog box where you can enter user information.](media/userecho-tutorial/name.png)

    a. In the **Name** textbox, type name of the user like Britta Simon.

    b. In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.

    c. Select **Invite**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to UserEcho Sign-on URL where you can initiate the login flow.
- Go to UserEcho Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the UserEcho tile in the My Apps, this option redirects to UserEcho Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
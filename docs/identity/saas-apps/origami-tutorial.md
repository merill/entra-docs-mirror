---
layout: Conceptual
title: Configure Origami for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/origami-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Origami.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 7eb9cad3-c7a6-a3f1-af1f-15fa15b0f43e
document_version_independent_id: 59e1bdbb-c2b6-f1fb-c112-f00f2f2514e2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/origami-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/origami-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/origami-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 31ee1002-8ad5-88c2-139a-0afc4b3e5822
---

# Configure Origami for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Origami with Microsoft Entra ID. When you integrate Origami with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Origami.
- Enable your users to be automatically signed-in to Origami with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Origami single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Origami supports **SP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Origami from the gallery

To configure the integration of Origami into Microsoft Entra ID, you need to add Origami from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Origami** in the search box.
4. Select **Origami** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Origami

Configure and test Microsoft Entra SSO with Origami using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Origami.

To configure and test Microsoft Entra SSO with Origami, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Origami SSO**- to configure the single sign-on settings on application side.
    1. **Create Origami test user** - to have a counterpart of B.Simon in Origami that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Origami** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://live.origamirisk.com/origami/account/login?account=<COMPANY_NAME>`

    Note

    The value isn't real. Update the value with the actual Sign-On URL. Contact [Origami Client support team](https://wordpress.org/support/theme/origami) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Origami** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Origami SSO

1. Log in to the Origami account with Admin rights.
2. In the menu on the top, select **Admin**.

    ![Screenshot that shows the Origami home page with &quot;Admin&quot; selected.](media/origami-tutorial/admin.png)
3. On the Single Sign On Setup dialog page, perform the following steps:

    ![Screenshot that shows the &quot;Single Sign On Setup&quot; page with &quot;Enable Single Sign-on&quot; selected, and the text boxes highlighted.](media/origami-tutorial/configuration.png)

    a. Select **Enable Single Sign On**.

    b. In the **Identity Provider's Sign-in Page URL** textbox, paste the value of **Login URL**.

    c. In the **Identity Provider's Sign-out Page URL** textbox, paste the value of **Logout URL**.

    d. Select **Browse** to upload the certificate you have downloaded.

    e. Select **Save Changes**.

### Create Origami test user

In this section, you create a user called Britta Simon in Origami.

1. Log in to the Origami account with Admin rights.
2. In the menu on the top, select **Admin**.

    ![Screenshot that shows the Origami account home page with &quot;Admin&quot; selected.](media/origami-tutorial/admin.png)
3. On the **Users and Security** dialog, select **Users**.

    ![Screenshot that shows the &quot;Users and Security&quot; dialog with &quot;Users&quot; selected.](media/origami-tutorial/user.png)
4. Select **Add New User**.

    ![Screenshot that shows the &quot;Add New User&quot; button selected.](media/origami-tutorial/add-user.png)
5. On the Add New User dialog, perform the following steps:

    ![Screenshot that shows the &quot;Add New User&quot; dialog with the &quot;User Name&quot;, &quot;First Name&quot;, and &quot;Last Name&quot; text boxes highlighted.](media/origami-tutorial/new-user.png)

    a. In the **User Name** textbox, enter the email of user like **brittasimon@contoso.com**.

    b. In the **Password** textbox, type a password.

    c. In the **Confirm Password** textbox, type the password again.

    d. In the **First Name** textbox, enter the first name of user like **Britta**.

    e. In the **Last Name** textbox, enter the last name of user like **Simon**.

    f. Select **Save**.

    ![Screenshot that shows the &quot;Save&quot; button selected.](media/origami-tutorial/save.png)
6. Assign **User Roles** and **Client Access** to the user.

    ![Configure Single Sign-On](media/origami-tutorial/user-roles.png)

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Origami Sign-on URL where you can initiate the login flow.
- Go to Origami Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Origami tile in the My Apps, this option redirects to Origami Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
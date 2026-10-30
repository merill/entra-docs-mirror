---
layout: Conceptual
title: Configure Small Improvements for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/smallimprovements-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Small Improvements.
ms.topic: how-to
ms.date: 2024-05-24T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: a852fa4d-5788-e7e1-d8c0-8b4905a76875
document_version_independent_id: 9cb1012e-b5f5-bc14-c934-9eaf798f3ba0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/smallimprovements-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/smallimprovements-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/smallimprovements-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: a376a8fb-9a3e-610d-490f-c701d82d3121
---

# Configure Small Improvements for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Small Improvements with Microsoft Entra ID. When you integrate Small Improvements with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Small Improvements.
- Enable your users to be automatically signed-in to Small Improvements with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Small Improvements single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Small Improvements supports **SP** initiated SSO.

## Add Small Improvements from the gallery

To configure the integration of Small Improvements into Microsoft Entra ID, you need to add Small Improvements from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Small Improvements** in the search box.
4. Select **Small Improvements** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Small Improvements

Configure and test Microsoft Entra SSO with Small Improvements using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Small Improvements.

To configure and test Microsoft Entra SSO with Small Improvements, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Small Improvements SSO**- to configure the single sign-on settings on application side.
    1. **Create Small Improvements test user** - to have a counterpart of B.Simon in Small Improvements that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Small Improvements** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<subdomain>.small-improvements.com`

    b. In the **Sign on URL** text box, type a URL using the following pattern: `https://<subdomain>.small-improvements.com`

    Note

    These values aren't real. Update these values with the actual Identifier and Sign on URL. Contact [Small Improvements Client support team](mailto:support@small-improvements.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Small Improvements** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Small Improvements SSO

1. In another browser window, sign on to your [Small Improvements](https://small-improvements.com) company site as an administrator.
2. From the main dashboard page, select **Admin** &gt; **Integrations** on the left.

    ![Screenshot shows the Integrations button selected.](media/smallimprovements-tutorial/admin.png)
3. Select the **SAML SSO** button from **Integrations** section.

    ![Screenshot shows the SAML S S O icon selected in Integrations.](media/smallimprovements-tutorial/menu.png)
4. On the SSO Setup page, perform the following steps:

    ![Screenshot shows the S S O Setup page where you can enter the values described.](media/smallimprovements-tutorial/certificate.png)

    a. Check **Enable SAML for SSO**.

    b. In the **Application Issuer URL** text box, enter the Small Improvements subdomain in the following format: `https://<yourcompany>.small-improvements.com`

    c. In the **HTTP Endpoint** textbox, paste the value of **Login URL**.

    d. Open your downloaded certificate in Notepad, copy the content, and then paste it into the **x509 Certificate** textbox.

    e. If you wish to have SSO and Login form authentication option available for users, then check the **Enable access via login/password too** option.

    f. Enter the appropriate value to Name the SSO Login button in the **SAML Prompt** textbox.

    g. Select **Save**.

### Create Small Improvements test user

To enable Microsoft Entra users to log in to Small Improvements, they must be provisioned into Small Improvements. In the case of Small Improvements, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Sign-on to your Small Improvements company site as an administrator.
2. From the Home page, go to the menu on the left, select **Admin** &gt; **Settings**.

    ![Screenshot shows the Settings button selected.](media/smallimprovements-tutorial/admin-settings.png)
3. Select the **Add Users** button from User Management section.

    ![Screenshot shows &quot;Add Users&quot; selected from Administration Overview.](media/smallimprovements-tutorial/user.png)
4. On the **Add Users** dialog, perform the following steps:

    ![Screenshot shows the Add users dialog box where you can enter the values described.](media/smallimprovements-tutorial/create-user.png)

    a. Enter the **first name** of user like **Britta**.

    b. Enter the **Last name** of user like **Simon**.

    c. Enter the **Email** of user like **brittasimon@contoso.com**.

    d. You can also choose to enter the personal message in the **Send notification email** box. If you don't wish to send the notification, then uncheck this checkbox.

    e. Select **Create Users**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Small Improvements Sign-on URL where you can initiate the login flow.
- Go to Small Improvements Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Small Improvements tile in the My Apps, this option redirects to Small Improvements Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
---
layout: Conceptual
title: Configure Silverback for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/silverback-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Silverback.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 83a3f680-8d3a-6560-6cbc-ae0ce25660cd
document_version_independent_id: 1ad0e8e7-9f23-51b6-9ce9-f96bb95f51c7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/silverback-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/silverback-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/silverback-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ad0e072c-dc1a-e6b5-6d40-cdb282688529
---

# Configure Silverback for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Silverback with Microsoft Entra ID. When you integrate Silverback with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Silverback.
- Enable your users to be automatically signed-in to Silverback with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Silverback single sign-on (SSO) enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Silverback supports **SP** initiated SSO.

## Add Silverback from the gallery

To configure the integration of Silverback into Microsoft Entra ID, you need to add Silverback from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Silverback** in the search box.
4. Select **Silverback** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Silverback

Configure and test Microsoft Entra SSO with Silverback using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Silverback.

To configure and test Microsoft Entra SSO with Silverback, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Silverback SSO**- to configure the single sign-on settings on application side.
    1. **Create Silverback test user** - to have a counterpart of B.Simon in Silverback that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Silverback** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic S A M L Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** box, type a URL using the following pattern: `<YOURSILVERBACKURL>.com`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<YOURSILVERBACKURL>.com/sts/authorize/login`

    c. In the **Sign-on URL** text box, type a URL using the following pattern: `https://<YOURSILVERBACKURL>.com/ssp`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign on URL. Contact [Silverback Client support team](mailto:helpdesk@matrix42.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Silverback SSO

1. In a different web browser, log in to your Silverback Server as an Administrator.
2. Navigate to **Admin** &gt; **Authentication Provider**.
3. On the **Authentication Provider Settings** page, perform the following steps:

    ![Screenshot shows the Authentication Provider Settings.](media/silverback-tutorial/admin.png)

    a. Select **Import from URL**.

    b. Paste the copied Metadata URL and select **OK**.

    c. Confirm with **OK** then the values are populated automatically.

    d. Enable **Show on Login Page**.

    e. Enable **Dynamic User Creation** if you want to add by Microsoft Entra authorized users automatically (optional).

    f. Create a **Title** for the button on the Self Service Portal.

    g. Upload an **Icon** by selecting **Choose File**.

    h. Select the background **color** for the button.

    i. Select **Save**.

### Create Silverback test user

To enable Microsoft Entra users to log in to Silverback, they must be provisioned into Silverback. In Silverback, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Log in to your Silverback Server as an Administrator.
2. Navigate to **Users** and **add a new device user**.
3. On the **Basic** page, perform the following steps:

    ![Screenshot shows the user account for Azure.](media/silverback-tutorial/user.png)

    a. In **Username** text box, enter the name of user like **Britta**.

    b. In **First Name** text box, enter the first name of user like **Britta**.

    c. In **Last Name** text box, enter the last name of user like **Simon**.

    d. In **E-mail Address** text box, enter the email of user like **Brittasimon@contoso.com**.

    e. In the **Password** text box, enter your password.

    f. In the **Confirm Password** text box, Reenter your password and confirm.

    g. Select **Save**.

Note

If you don’t want to create each user manually Enable the **Dynamic User Creation** Checkbox under **Admin** &gt; **Authentication Provider**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Silverback Sign on URL where you can initiate the login flow.
- Go to Silverback Sign on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Silverback tile in the My Apps, this option redirects to Silverback Sign on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
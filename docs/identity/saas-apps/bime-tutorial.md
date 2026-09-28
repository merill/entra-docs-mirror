---
layout: Conceptual
title: Configure Bime for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/bime-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Bime.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: f0decf6a-d089-0405-9940-3427e4359c84
document_version_independent_id: 174f6630-b524-9a68-19e9-d45ee133c0b6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/bime-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/bime-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/bime-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d9608466-7f46-18ca-c8c1-40777c19cd66
---

# Configure Bime for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Bime with Microsoft Entra ID. When you integrate Bime with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Bime.
- Enable your users to be automatically signed-in to Bime with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Bime single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Bime supports **SP** initiated SSO.

## Add Bime from the gallery

To configure the integration of Bime into Microsoft Entra ID, you need to add Bime from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Bime** in the search box.
4. Select **Bime** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Bime

Configure and test Microsoft Entra SSO with Bime using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Bime.

To configure and test Microsoft Entra SSO with Bime, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Bime SSO**- to configure the single sign-on settings on application side.
    1. **Create Bime test user** - to have a counterpart of B.Simon in Bime that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Bime** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<tenant-name>.Bimeapp.com`

    b. In the **Sign on URL** text box, type a URL using the following pattern: `https://<tenant-name>.Bimeapp.com`

    Note

    These values aren't real. Update these values with the actual Identifier and Sign on URL. Contact [Bime Client support team](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. In the **SAML Signing Certificate** section, select **Edit** button to open **SAML Signing Certificate** dialog.

    ![Edit SAML Signing Certificate](common/edit-certificate.png)
7. In the **SAML Signing Certificate** section, copy the **THUMBPRINT** and save it on your computer.

    ![Copy Thumbprint value](common/copy-thumbprint.png)
8. On the **Set up Bime** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Bime SSO

1. In a different web browser window, log into your Bime company site as an administrator.
2. In the toolbar, select **Admin**, and then **Account**.

    ![Screenshot shows the Admin item selected and Account selected.](media/bime-tutorial/account.png)
3. On the account configuration page, perform the following steps:

    ![Configure Single Sign-On](media/bime-tutorial/configuration.png)

    a. Select **Enable SAML authentication**.

    b. In the **Remote Login URL** textbox, paste the value of **Login URL**.

    c. In the **Certificate Fingerprint** textbox, paste the **THUMBPRINT** value..

    d. Select **Save**.

### Create Bime test user

In order to enable Microsoft Entra users to log in to Bime, they must be provisioned into Bime. In the case of Bime, provisioning is a manual task.

**To configure user provisioning, perform the following steps:**

1. Log in to your **Bime** tenant.
2. In the toolbar, select **Admin**, and then **Users**.

    ![Screenshot shows the Admin item selected and Users selected.](media/bime-tutorial/user.png)
3. In the **Users List**, select **Add New User** (“+”).

    ![Users](media/bime-tutorial/add-user.png)
4. On the **User Details** dialog page, perform the following steps:

    ![User Details](media/bime-tutorial/create-user.png)

    a. In the **First name** textbox, enter the first name of user like **Britta**.

    b. In the **Last name** textbox, enter the last name of user like **Simon**.

    c. In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.

    d. Select **Save**.

Note

You can use any other Bime user account creation tools or APIs provided by Bime to provision Microsoft Entra user accounts.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Bime Sign-on URL where you can initiate the login flow.
- Go to Bime Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Bime tile in the My Apps, this option redirects to Bime Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
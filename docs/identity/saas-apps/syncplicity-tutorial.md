---
layout: Conceptual
title: Configure Syncplicity for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/syncplicity-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Syncplicity.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: fe62d8ed-7a0c-99c2-bdfd-3c8c7b2df939
document_version_independent_id: 6798148c-2274-5af9-b182-fa21bdc78848
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/syncplicity-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/syncplicity-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/syncplicity-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: bcd5d2a2-ed8e-69b3-7832-75136762a7da
---

# Configure Syncplicity for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Syncplicity with Microsoft Entra ID. When you integrate Syncplicity with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Syncplicity.
- Enable your users to be automatically signed-in to Syncplicity with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Syncplicity single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Syncplicity supports **SP** initiated SSO.

## Add Syncplicity from the gallery

To configure the integration of Syncplicity into Microsoft Entra ID, you need to add Syncplicity from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Browse Microsoft Entra gallery** section, type **Syncplicity** in the search box.
4. Select **Syncplicity** from results panel and then select **Create** to add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Syncplicity

Configure and test Microsoft Entra SSO with Syncplicity using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Syncplicity.

To configure and test Microsoft Entra SSO with Syncplicity, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Syncplicity SSO**- to configure the single sign-on settings on application side.
    1. **Create Syncplicity test user** - to have a counterpart of B.Simon in Syncplicity that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.
4. **Update SSO** - to make the necessary changes in Syncplicity if you have changed the SSO settings in Microsoft Entra ID.

### Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Syncplicity** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. In the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<COMPANY_NAME>.syncplicity.com/sp`

    b. In the **Sign on URL** text box, type a URL using the following pattern: `https://<COMPANY_NAME>.syncplicity.com`

    c. In the **Reply URL (Assertion Consumer Service URL)** text box, type a URL using the following pattern: `https://<COMPANY_NAME>.syncplicity.com/Auth/AssertionConsumerService.aspx`

    Note

    These values aren't real. Update these values with the actual Reply URL,Sign on URL and Identifier. Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Edit**. Then in the dialog select the ellipsis button next to your active certificate and select **PEM certificate download**.

    ![The Certificate download link](common/certificatebase64.png)

    Note

    You need the PEM certificate, as Syncplicity doesn't accept certificates in CER format.
7. On the **Set up Syncplicity** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Syncplicity SSO

1. Sign in to your **Syncplicity** tenant.
2. In the menu on the top, select **Admin**, select **Settings**, and then select **Custom domain and single sign-on**.

    ![Syncplicity](media/syncplicity-tutorial/admin.png)
3. On the **Single Sign-On (SSO)** dialog page, perform the following steps:

    ![Single Sign-On (SSO)](media/syncplicity-tutorial/configuration.png)

    a. In the **Custom Domain** textbox, type the name of your domain.

    b. Select **Enabled** as **Single Sign-On Status**.

    c. In the **Entity Id** textbox, Paste the **Identifier (Entity ID)** value, which you have used in the **Basic SAML Configuration**.

    d. In the **Sign-in page URL** textbox, Paste the **Sign on URL** which you copied previously.

    e. In the **Logout page URL** textbox, Paste the **Logout URL** which you copied previously.

    f. In **Identity Provider Certificate**, select **Choose file**, and then upload the certificate which you have downloaded.

    g. Select **SAVE CHANGES**.

### Create Syncplicity test user

For Microsoft Entra users to be able to sign in, they must be provisioned to Syncplicity application. This section describes how to create Microsoft Entra user accounts in Syncplicity.

**To provision a user account to Syncplicity, perform the following steps:**

1. Sign in to your **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).
2. Select **Admin** and select **User Accounts**, then select **Add a User**.

    ![Manage Users](media/syncplicity-tutorial/users.png)
3. Type the **Email addresses** of a Microsoft Entra account you want to provision, select **User** as **Role**, and then select **Next**.

    ![Account Information](media/syncplicity-tutorial/roles.png)

    Note

    The Microsoft Entra account holder gets an email including a link to confirm and activate the account.
4. Select a group in your company that your new user should become a member of, and then select **Next**.

    ![Group Membership](media/syncplicity-tutorial/group.png)

    Note

    If there are no groups listed, select **Next**.
5. Select the folders you would like to place under Syncplicity’s control on the user’s computer, and then select **Next**.

    ![Syncplicity Folders](media/syncplicity-tutorial/folder.png)

Note

You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity to provision Microsoft Entra user accounts.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Syncplicity Sign-on URL where you can initiate the login flow.
- Go to Syncplicity Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Syncplicity tile in the My Apps, this option redirects to Syncplicity Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).

### Update SSO

Whenever you need to make changes to the SSO, you need to check the **SAML Signing Certificate** being used. If the certificate has changed, make sure to upload the new one to Syncplicity as described in **Configure Syncplicity SSO**.

If you're using the Syncplicity Mobile app, please contact the Syncplicity Customer Support (support@syncplicity.com) for assistance.
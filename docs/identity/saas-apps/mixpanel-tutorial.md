---
layout: Conceptual
title: Configure Mixpanel for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/mixpanel-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Mixpanel.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 501fd492-6b42-f364-ef9e-b46f771f2076
document_version_independent_id: a04c34bd-b8a9-cb01-07c7-74eeb7812310
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/mixpanel-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/mixpanel-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/mixpanel-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 76b3790b-445a-4760-c07b-9f05be5f705e
---

# Configure Mixpanel for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Mixpanel with Microsoft Entra ID. When you integrate Mixpanel with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Mixpanel.
- Enable your users to be automatically signed-in to Mixpanel with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Mixpanel single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Mixpanel supports **SP** initiated SSO.
- Mixpanel supports [Automated user provisioning](mixpanel-provisioning-tutorial).

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Mixpanel from the gallery

To configure the integration of Mixpanel into Microsoft Entra ID, you need to add Mixpanel from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Mixpanel** in the search box.
4. Select **Mixpanel** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Mixpanel

Configure and test Microsoft Entra SSO with Mixpanel using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Mixpanel.

To configure and test Microsoft Entra SSO with Mixpanel, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Mixpanel SSO**- to configure the single sign-on settings on application side.
    1. **Create Mixpanel test user** - to have a counterpart of B.Simon in Mixpanel that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Mixpanel** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following step:

    In the **Sign-on URL** text box, type the URL: `https://mixpanel.com/login/`

    Note

    Please register at https://mixpanel.com/register/ to set up your login credentials and contact the [Mixpanel support team](mailto:support@mixpanel.com) to enable SSO settings for your tenant. You can also get your Sign On URL value if necessary from your Mixpanel support team.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Mixpanel** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Mixpanel SSO

1. In a different browser window, sign-on to your Mixpanel application as an administrator.
2. On bottom of the page, select the little **gear** icon in the left corner.

    ![Mixpanel Single Sign-On](media/mixpanel-tutorial/gear-icon.png)
3. Select the **Access security** tab, and then select **Change settings**.

    ![Screenshot shows the Access security tab where you can change settings.](media/mixpanel-tutorial/settings.png)
4. On the **Change your certificate** dialog page, select **Choose file** to upload your downloaded certificate, and then select **NEXT**.

    ![Screenshot shows the Change your certificate dialog box where you can choose a certificate file.](media/mixpanel-tutorial/certificate.png)
5. In the authentication URL textbox on the **Change your authentication URL** dialog page, paste the value of **Login URL**., and then select **NEXT**.

    ![Screenshot shows the Change your authentication U R L pane where you can copy your Login U R L.](media/mixpanel-tutorial/authentication.png)
6. Select **Done**.

### Create Mixpanel test user

The objective of this section is to create a user called Britta Simon in Mixpanel.

1. Sign on to your Mixpanel company site as an administrator.
2. On the bottom of the page, select the little gear button on the left corner to open the **Settings** window.
3. Select the **Team** tab.
4. In the **team member** textbox, type Britta's email address in the Azure.

    ![Screenshot shows the Team tab where you add an address to Invite.](media/mixpanel-tutorial/member.png)
5. Select **Invite**.

Note

The user gets an email to set up the profile.

Note

Mixpanel also supports automatic user provisioning, you can find more details [here](mixpanel-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Mixpanel Sign-on URL where you can initiate the login flow.
- Go to Mixpanel Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Mixpanel tile in the My Apps, this option redirects to Mixpanel Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
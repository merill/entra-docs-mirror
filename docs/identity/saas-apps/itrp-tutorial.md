---
layout: Conceptual
title: Configure ITRP for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/itrp-tutorial
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
description: In this article,  you learn how to configure single sign-on between Microsoft Entra ID and ITRP.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 63cb78f9-2d85-ce33-87ac-c2a3b3d5e770
document_version_independent_id: 1aed0831-4d23-154f-40b6-2608d51c8952
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/itrp-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/itrp-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/itrp-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c9a22b65-c918-2f04-8ad4-b87eeda490f6
---

# Configure ITRP for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate ITRP with Microsoft Entra ID. When you integrate ITRP with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to ITRP.
- Enable your users to be automatically signed-in to ITRP with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- An ITRP subscription that has single sign-on enabled.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- ITRP supports SP-initiated SSO.

## Add ITRP from the gallery

To configure the integration of ITRP into Microsoft Entra ID, you need to add ITRP from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **ITRP** in the search box.
4. Select **ITRP** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for ITRP

Configure and test Microsoft Entra SSO with ITRP using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in ITRP.

To configure and test Microsoft Entra SSO with ITRP, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure ITRP SSO**- to configure the single sign-on settings on application side.
    1. **Create an ITRP test user** - to have a counterpart of B.Simon in ITRP that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **ITRP** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. In the **Basic SAML Configuration** dialog box, perform the following steps.

    1. In the **Identifier (Entity ID)** textbox, type a URL using the following pattern:

        `https://<tenant-name>.itrp.com`
    2. In the **Sign on URL** textbox, type a URL using the following pattern:

        `https://<tenant-name>.itrp.com`

    Note

    These values are placeholders. You need to use the actual Identifier and Sign on URL. Contact the [ITRP support team](https://www.4me.com/support/) to get the values. You can also refer to the patterns shown in the **Basic SAML Configuration** dialog box.
6. In the **SAML Signing Certificate** section, select the **Edit** icon to open the **SAML Signing Certificate** dialog box:

    ![Screenshot shows the SAML Signing Certificate page with the edit icon selected.](common/edit-certificate.png)
7. In the **SAML Signing Certificate** dialog box, copy the **Thumbprint** value and save it:

    ![Copy the Thumbprint value](common/copy-thumbprint.png)
8. In the **Set up ITRP** section, copy the appropriate URLs, based on your requirements:

    ![Copy the configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure ITRP SSO

1. In a new web browser window, sign in to your ITRP company site as an admin.
2. At the top of the window, select the **Settings** icon:

    ![Settings icon](media/itrp-tutorial/profile.png)
3. In the left pane, select **Single Sign-On**:

    ![Select Single Sign-On](media/itrp-tutorial/setting.png)
4. In the **Single Sign-On** configuration section, take the following steps.

    ![Screenshot shows the Single Sign-On section with Enabled selected.](media/itrp-tutorial/configuration.png)

    1. Select **Enabled**.
    2. In the **Remote logout URL** box, paste the **Logout URL** value that you copied.
    3. In the **SAML SSO URL** box, paste the **Login URL** value that you copied.
    4. In the **Certificate fingerprint** box, paste the **Thumbprint** value of the certificate, which you copied.
    5. Select **Save**.

### Create an ITRP test user

To enable Microsoft Entra users to sign in to ITRP, you need to add them to ITRP. You need to add them manually.

To create a user account, take these steps:

1. Sign in to your ITRP tenant.
2. At the top of the window, select the **Records** icon:

    ![Records icon](media/itrp-tutorial/account.png)
3. In the menu, select **People**:

    ![Select People](media/itrp-tutorial/user.png)
4. Select the plus sign (**+**) to add a new person:

    ![Select the plus sign](media/itrp-tutorial/people.png)
5. In the **Add New Person** dialog box, take the following steps.

    ![Add New Person dialog box](media/itrp-tutorial/details.png)

    1. Enter the name and email address of a valid Microsoft Entra account that you want to add.
    2. Select **Save**.

Note

You can use any user account creation tool or API provided by ITRP to provision Microsoft Entra user accounts.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to ITRP Sign-on URL where you can initiate the login flow.
- Go to ITRP Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the ITRP tile in the My Apps, this option redirects to ITRP Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
---
layout: Conceptual
title: Configure Showpad for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/showpad-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Showpad.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: ae4465bd-c942-02c8-77f5-227c1a56e455
document_version_independent_id: c5486bed-aedb-b1ef-4265-51ae1e4b34b2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/showpad-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/showpad-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/showpad-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 2f40bbdf-be49-4359-f748-990f0a87dafe
---

# Configure Showpad for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Showpad with Microsoft Entra ID. When you integrate Showpad with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Showpad.
- Enable your users to be automatically signed-in to Showpad with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Showpad single sign-on enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Showpad supports **SP** initiated SSO.
- Showpad supports **Just In Time** user provisioning.

## Add Showpad from the gallery

To configure the integration of Showpad into Microsoft Entra ID, you need to add Showpad from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Showpad** in the search box.
4. Select **Showpad** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Showpad

Configure and test Microsoft Entra SSO with Showpad using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Showpad.

To configure and test Microsoft Entra SSO with Showpad, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Showpad SSO**- to configure the single sign-on settings on application side.
    1. **Create Showpad test user** - to have a counterpart of B.Simon in Showpad that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Showpad** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<company-name>.showpad.biz`

    b. In the **Sign on URL** text box, type a URL using the following pattern: `https://<company-name>.showpad.biz/login`

    Note

    These values aren't real. Update these values with the actual Identifier and Sign on URL. Contact [Showpad Client support team](https://help.showpad.com/) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up Showpad** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Showpad SSO

1. Sign in to your Showpad tenant as an administrator.
2. In the menu on the top, select the **Settings**.

    ![Screenshot shows Settings selected from the Settings menu.](media/showpad-tutorial/settings.png)
3. Navigate to **Single Sign-On** and select **Enable**.

    ![Screenshot shows Single Sign-On selected with an Enable option.](media/showpad-tutorial/profile.png)
4. On the **Add a SAML 2.0 Service** dialog, perform the following steps:

    ![Screenshot shows the Add a SAML 2.0 Service dialog box where you can enter the values described.](media/showpad-tutorial/user.png)

    a. In the **Name** textbox, type the name of Identifier Provider (for example: your company name).

    b. As **Metadata Source**, select **XML**.

    c. Copy the content of metadata XML file, which you have downloaded, and then paste it into the **Metadata XML** textbox.

    d. Select **Auto-provision accounts for new users when they log in**.

    e. Select **Submit**.

### Create Showpad test user

In this section, a user called Britta Simon is created in Showpad. Showpad supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Showpad, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Showpad Sign-on URL where you can initiate the login flow.
- Go to Showpad Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Showpad tile in the My Apps, this option redirects to Showpad Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
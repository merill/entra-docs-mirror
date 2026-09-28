---
layout: Conceptual
title: Configure Infrascale Cloud Backup for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/infrascale-cloud-backup-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Infrascale Cloud Backup.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: c48e226e-1464-fea4-f415-fe8f57add35f
document_version_independent_id: 2b565b86-397a-5ff7-bcec-f43167564741
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/infrascale-cloud-backup-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/infrascale-cloud-backup-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/infrascale-cloud-backup-tutorial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 195c4a41-9098-6ac6-770a-eb776b5ed8d5
---

# Configure Infrascale Cloud Backup for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Infrascale Cloud Backup with Microsoft Entra ID. When you integrate Infrascale Cloud Backup with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Infrascale Cloud Backup.
- Enable your users to be automatically signed-in to Infrascale Cloud Backup with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Infrascale Cloud Backup single sign-on (SSO) enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Infrascale Cloud Backup supports **SP** initiated SSO.

## Add Infrascale Cloud Backup from the gallery

To configure the integration of Infrascale Cloud Backup into Microsoft Entra ID, you need to add Infrascale Cloud Backup from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Infrascale Cloud Backup** in the search box.
4. Select **Infrascale Cloud Backup** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Infrascale Cloud Backup

Configure and test Microsoft Entra SSO with Infrascale Cloud Backup using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Infrascale Cloud Backup.

To configure and test Microsoft Entra SSO with Infrascale Cloud Backup, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Infrascale Cloud Backup SSO**- to configure the single sign-on settings on application side.
    1. **Create Infrascale Cloud Backup test user** - to have a counterpart of B.Simon in Infrascale Cloud Backup that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Infrascale Cloud Backup** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic S A M L Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type a URL using the following pattern: `https://dashboard.sosonlinebackup.com/<ID>`

    b. In the **Reply URL** textbox, type the URL: `https://dashboard.managedoffsitebackup.net/Account/AssertionConsumerService`

    c. The **Sign-on URL** text box requires a specific URL for your company. The general pattern of the URL is: `https://[OptionalPrefix]dashboard[OptionalSuffix].CompanySpecificString.[com/net,etc]/Account/SingleSignOn`

    Note

    don't enter this in the Sign-on URL text box. The Identifier value isn't a real URL – just a general pattern. Update this value with the actual Identifier URL obtained from Infrascale. Contact [Infrascale Cloud Backup support team](mailto:support@infrascale.com) to get the value.
6. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Infrascale Cloud Backup SSO

1. Log in to your Infrascale Cloud Backup company site as an administrator.
2. Go to **Settings** &gt; **Single Sign-On** and select **Enable Single Sign-On (SSO)**.
3. In the **Single Sign-On Settings** page, perform the following steps:

    ![Screenshot that shows the Configuration Settings.](media/infrascale-cloud-backup-tutorial/settings.png)

    a. Copy **Service Provider EntityID** value, paste this value into the **Identifier** text box in the **Basic SAML Configuration** section.

    b. Copy **Reply URL** value, paste this value into the **Reply URL** text box in the **Basic SAML Configuration** section.

    c. Select **Via metadata URL** button under Identity Provider Settings section.

    d. Copy **App Federation Metadata Url** and paste it in the **Metadata URL** textbox.

    e. Select **Save**.

### Create Infrascale Cloud Backup test user

In this section, you create a user called Britta Simon in Infrascale Cloud Backup. Work with [Infrascale Cloud Backup support team](mailto:support@infrascale.com) to add the users in the Infrascale Cloud Backup platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Infrascale Cloud Backup Sign-On URL where you can initiate the login flow.
- Go to Infrascale Cloud Backup Sign-On URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Infrascale Cloud Backup tile in the My Apps, this option redirects to Infrascale Cloud Backup Sign-On URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
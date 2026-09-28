---
layout: Conceptual
title: Configure my.sdworx.com for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/mysdworxcom-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and my.sdworx.com.
ms.topic: how-to
ms.date: 2024-06-10T00:00:00.0000000Z
locale: en-us
document_id: 2e2f13fc-7944-1b29-e9f3-60ddea908d8b
document_version_independent_id: 93c244db-336c-1189-e8d8-eabd60d67ed5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/mysdworxcom-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/mysdworxcom-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/mysdworxcom-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
platformId: f6a2907c-f97b-863c-1d71-ea940f608701
---

# Configure my.sdworx.com for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate my.sdworx.com with Microsoft Entra ID. my.sdworx.com is an SD Worx portal. When you integrate my.sdworx.com with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to my.sdworx.com.
- Enable your users to be automatically signed-in to my.sdworx.com with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You configure and test Microsoft Entra single sign-on for my.sdworx.com in a test environment (my.acc.sdworx.com) but not by using this gallery app (import SP metadata, to be provided by your my.sdworx.com contact). my.sdworx.com supports **IDP** and **SP** initiated single sign-on.

When using **SP** initiated single sign-on, only “email domain” realm discovery is supported, which means only company/enterprise email addresses are allowed.

You can configure and test Microsoft Entra single sign-on for my.sdworx.com in a test environment (my.acc.sdworx.com) but not by using the gallery app (import SP metadata, to be provided by your my.sdworx.com contact). My.sdworx.com supports **IDP** and **SP** initiated single sign-on.

When using **SP** initiated single sign-on, only “email domain” realm discovery is supported, which means only company/enterprise email addresses are allowed.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Prerequisites

To integrate Microsoft Entra ID with my.sdworx.com, you need:

- Before adding the application in your Microsoft Entra tenant, please contact your SD Worx consultant first to start up the track to activate the SSO for your company. The SSO won’t work before it's implemented and activated on the SD Worx Service Provider.
- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- my.sdworx.com single sign-on (SSO) enabled subscription.

## Add application and assign a test user

Before you begin the process of configuring single sign-on, you need to add the my.sdworx.com application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the single sign-on configuration.

### Add my.sdworx.com from the Microsoft Entra gallery

Add my.sdworx.com from the Microsoft Entra application gallery to configure single sign-on with my.sdworx.com. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **my.sdworx.com** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, the application is preconfigured and the necessary URLs are already prepopulated with Microsoft Entra. The user needs to save the configuration by selecting the Save button.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/copy-metadataurl.png)

## Configure my.sdworx.com SSO

To configure single sign-on on **my.sdworx.com** side, you need to send the **App Federation Metadata Url** to [my.sdworx.com support team](mailto:prod_cloud&amp;busoper_middleware&amp;hostsol@sdworx.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create my.sdworx.com test user

In this section, you create a user called Britta Simon at my.sdworx.com. Work with [my.sdworx.com support team](mailto:prod_cloud&amp;busoper_middleware&amp;hostsol@sdworx.com) to add the users in the my.sdworx.com platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the my.sdworx.com for which you set up the SSO.
- You can use Microsoft My Apps. When you select the my.sdworx.com tile in the My Apps, you should be automatically signed in to the my.sdworx.com for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
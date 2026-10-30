---
layout: Conceptual
title: Configure Deem Mobile for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/deem-mobile-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Deem Mobile.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 4c5a20e3-f4c1-1fc8-27d9-2bedd7b68dfc
document_version_independent_id: 0b776105-0b99-e06c-df58-115b6f919b50
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/deem-mobile-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/deem-mobile-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/deem-mobile-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 72e5767e-14b8-e818-af25-618a45f461ba
---

# Configure Deem Mobile for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Deem Mobile with Microsoft Entra ID. Deem Mobile is designed for anyone who wants business travel to be fast and easy. With full functionality to book flights, hotels, rental cars, and even Uber for Business. When you integrate Deem Mobile with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Deem Mobile.
- Enable your users to be automatically signed-in to Deem Mobile with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You'll configure and test Microsoft Entra single sign-on for Deem Mobile in a test environment. Deem Mobile supports both **SP** and **IDP** initiated single sign-on.

## Prerequisites

To integrate Microsoft Entra ID with Deem Mobile, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Deem Mobile single sign-on (SSO) enabled subscription.

## Add application and assign a test user

Before you begin the process of configuring single sign-on, you need to add the Deem Mobile application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the single sign-on configuration.

### Add Deem Mobile from the Microsoft Entra gallery

Add Deem Mobile from the Microsoft Entra application gallery to configure single sign-on with Deem Mobile. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Deem Mobile** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    [![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)](common/edit-urls.png#lightbox)
5. On the **Basic SAML Configuration** section, perform the following steps:

    1. In the **Identifier** textDeem Mobile, type a value using one of the following patterns:

        | **Identifier** |
        | --- |
        | `<Deem_CustomerDomainName>-mobile` |
        | `<Deem_CustomerDomainName>:mobile` |
    2. In the **Reply URL** textbox, type the URL: `https://go.deem.com/idp/ACS.saml2`

    Note

    The Identifier value isn't real. Update this value with the actual Identifier. Contact [Deem Mobile support team](mailto:customer.success@deem.com) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. Your Deem Mobile application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows an example for this. The default value of **Unique User Identifier** is **user.userprincipalname** but Deem Mobile expects this to be mapped with the user's email address. For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.

    [![Screenshot shows the image of token attributes configuration.](common/default-attributes.png)](common/default-attributes.png#lightbox)
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    [![Screenshot shows the Certificate download link.](common/copy-metadataurl.png)](common/copy-metadataurl.png#lightbox)

## Configure Deem Mobile SSO

To configure single sign-on on **Deem Mobile** side, you need to send the **App Federation Metadata Url** to [Deem Mobile support team](mailto:customer.success@deem.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Deem Mobile test user

In this section, you create a user called Britta Simon in Deem Mobile. Work with [Deem Mobile support team](mailto:customer.success@deem.com) to add the users in the Deem Mobile platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the Deem Mobile for which you set up the SSO.
- You can use Microsoft My Apps. When you select the Deem Mobile tile in the My Apps, you should be automatically signed in to the Deem Mobile for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
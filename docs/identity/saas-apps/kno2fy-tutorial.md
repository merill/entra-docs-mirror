---
layout: Conceptual
title: Configure Kno2fy for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/kno2fy-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Kno2fy.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 940793a4-349e-a07a-32ab-ed35e56c8ca2
document_version_independent_id: c0c89aaf-b5f8-9773-1db4-5a1d2da0b67a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/kno2fy-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/kno2fy-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/kno2fy-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c586b798-8ce8-cc3a-1b47-c2985836788a
---

# Configure Kno2fy for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Kno2fy with Microsoft Entra ID. Kno2fy empowers healthcare organizations to send, receive, and find patient information across the healthcare ecosystem with just a few quick selects. When you integrate Kno2fy with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Kno2fy.
- Enable your users to be automatically signed-in to Kno2fy with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You'll configure and test Microsoft Entra single sign-on for Kno2fy in a test environment. Kno2fy supports only **SP** initiated single sign-on.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Prerequisites

To integrate Microsoft Entra ID with Kno2fy, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Kno2fy single sign-on (SSO) enabled subscription.

## Add application and assign a test user

Before you begin the process of configuring single sign-on, you need to add the Kno2fy application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the single sign-on configuration.

### Add Kno2fy from the Microsoft Entra gallery

Add Kno2fy from the Microsoft Entra application gallery to configure single sign-on with Kno2fy. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Access Microsoft Entra information in Kno2fy

1. Login to https://kno2fy.com as a Network Administrator.
2. Select the settings gear in the right-hand corner at the top of the screen.
3. Under Network, Select **Identity Provider**.
4. In the dropdown, Select **Microsoft Entra ID**.
5. Continue setup in Configure Microsoft Entra SSO section below.

Kno2fy will display the information needed to setup the **Basic SAML Configuration**

![Screenshot of Microsoft Entra Saml Setup Information.](media/kno2fy-tutorial/microsoft-entra-setup-data.png)

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Kno2fy** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)

    To access the information to setup **Basic SAML Configuration** review the Microsoft Entra Information Section above.
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, paste the value from: `Identifier (Entity ID)`

    b. In the **Reply URL** textbox, paste the URL from: `Reply URL (Assertion Consumer Service URL)`

    c. In the **Sign on URL** textbox:

    Note

    This value appears once the Kno2fy Identity Provider has been saved. For now leave it blank.
6. Save the **Basic SAML Configuration** section.
7. Scroll down and copy the **App Federation Metadata URL** generated.
8. Continue setup in the Configure Kno2fy SSO section

## Configure Kno2fy SSO

1. Paste the **App Federation Metadata URL** from Microsoft Entra ID SSO setup into the **App Federation Metadata URL** field inside Kno2fy.
2. In the **Authentication Settings**, login without SSO is off by default.

    To allow time to conduct a login test, the **Allow non-admins to bypass SSO and login with a Kno2 username and password** setting can be enabled temporarily. It's recommended this setting remain off once SSO is fully enabled and setup.
3. Select the **Save** button to complete the setup.

Once complete, an **SSO Integration Activated** banner appears at the top of the screen. Copy the URL and paste the URL into the **Sign on URL** section of the **Basic SAML Configuration**Configure Microsoft Entra SSO

### Create Kno2fy test user

In this section, you create a user called Britta Simon at Kno2fy. Work with [Kno2fy support team](mailto:support@kno2.com) to add the users in the Kno2fy platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Kno2fy Sign-on URL where you can initiate the login flow.
- Go to Kno2fy Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Kno2fy tile in the My Apps, this option redirects to Kno2fy Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
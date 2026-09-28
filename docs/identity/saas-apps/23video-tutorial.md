---
layout: Conceptual
title: Configure 23 Video for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/23video-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and 23 Video.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: aa5e94c4-ceb1-0245-735c-af209787eae8
document_version_independent_id: db01f9f5-e488-17da-326a-335a1da87ad3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/23video-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/23video-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/23video-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 07dfd811-6672-8aee-3a42-2e89ff4c2af7
---

# Configure 23 Video for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate 23 Video with Microsoft Entra ID. When you integrate 23 Video with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to 23 Video.
- Enable your users to be automatically signed-in to 23 Video with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- 23 Video single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- 23 Video supports **SP** initiated SSO.

## Add 23 Video from the gallery

To configure the integration of 23 Video into Microsoft Entra ID, you need to add 23 Video from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **23 Video** in the search box.
4. Select **23 Video** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for 23 Video

Configure and test Microsoft Entra SSO with 23 Video using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in 23 Video.

To configure and test Microsoft Entra SSO with 23 Video, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure 23 Video SSO**- to configure the single sign-on settings on application side.
    1. **Create 23 Video test user** - to have a counterpart of B.Simon in 23 Video that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **23 Video** application integration page, find the **Manage** section and select **Single sign-on**.
3. On the **Select a Single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://www.23video.com/saml/trust/<uniqueid>`

    b. In the **Sign on URL** text box, type a URL using the following pattern: `https://<subdomain>.23video.com`

    Note

    These values aren't real. Update these values with the actual Identifier and Sign on URL. Contact [23 Video Client support team](mailto:support@23company.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up 23 Video** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure 23 Video SSO

To configure single sign-on on **23 Video** side, you need to send the downloaded **Certificate (Base64)** and appropriate copied URLs from the application configuration to [23 Video support team](mailto:support@23company.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create 23 Video test user

The objective of this section is to create a user called B.Simon in 23 Video.

**To create a user called B.Simon in 23 Video, perform the following steps:**

1. Sign on to your 23 Video company site as administrator.
2. Go to **Settings**.
3. In **Users** section, select **Configure**.

    ![Screenshot that highlights the Users section.](media/23video-tutorial/settings.png)
4. Select **Add a new user**.

    ![Screenshot that highlights the Add a new user button.](media/23video-tutorial/user.png)
5. In the **Invite someone to join this site** section, perform the following steps:

    ![Assign User](media/23video-tutorial/invite-user.png)

    a. In the **E-mail addresses** textbox, type the email address of a user like B.Simon@contoso.com.

    b. Select **Add the user..**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to 23 Video Sign-on URL where you can initiate the login flow.
- Go to 23 Video Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the 23 Video tile in the My Apps, this option redirects to 23 Video Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
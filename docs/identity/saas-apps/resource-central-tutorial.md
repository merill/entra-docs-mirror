---
layout: Conceptual
title: Configure Resource Central – SAML SSO for Meeting Room Booking System for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/resource-central-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Resource Central – SAML SSO for Meeting Room Booking System.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 05e71fc5-e464-83ea-5dcf-6584adbd20d8
document_version_independent_id: 58ea7f32-ab95-b10f-0b55-485ad8a666f1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/resource-central-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/resource-central-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/resource-central-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7822fd9b-ecb6-674d-d421-44f4a2a3334c
---

# Configure Resource Central – SAML SSO for Meeting Room Booking System for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Resource Central – SAML SSO for Meeting Room Booking System with Microsoft Entra ID. When you integrate Resource Central – SAML SSO for Meeting Room Booking System with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Resource Central – SAML SSO for Meeting Room Booking System.
- Enable your users to be automatically signed-in to Resource Central – SAML SSO for Meeting Room Booking System with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Resource Central – SAML SSO for Meeting Room Booking System single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Resource Central – SAML SSO for Meeting Room Booking System supports **SP** initiated SSO
- Resource Central – SAML SSO for Meeting Room Booking System supports **Just In Time** user provisioning

## Add Resource Central – SAML SSO for Meeting Room Booking System from the gallery

To configure the integration of Resource Central – SAML SSO for Meeting Room Booking System into Microsoft Entra ID, you need to add Resource Central – SAML SSO for Meeting Room Booking System from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, in the search box, enter **Resource Central – SAML SSO for Meeting Room Booking System**.
4. Select **Resource Central – SAML SSO for Meeting Room Booking System** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Resource Central – SAML SSO for Meeting Room Booking System

Configure and test Microsoft Entra SSO with Resource Central – SAML SSO for Meeting Room Booking System using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Resource Central – SAML SSO for Meeting Room Booking System.

To configure and test Microsoft Entra SSO with Resource Central – SAML SSO for Meeting Room Booking System, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
    3. **Create Resource Central SAML SSO for Meeting Room Booking System test user** - to have a counterpart of B.Simon in Resource Central – SAML SSO for Meeting Room Booking System that's linked to the Microsoft Entra representation of user.
2. **Configure Resource Central SAML SSO for Meeting Room Booking System SSO** - to configure the single sign-on settings on application side.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Resource Central – SAML SSO for Meeting Room Booking System** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the edit/pen icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. In **Basic SAML Configuration**, enter the values for the following fields:

    1. In the **Sign on URL** text box, type a URL using the following pattern: `https://<DOMAIN_NAME>/ResourceCentral`
    2. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<DOMAIN_NAME>/ResourceCentral`
    3. In the **Reply URL** text box, type a URL using the following pattern: `https://<DOMAIN_NAME>/ResourceCentral/ExAuth/Saml2Authentication/Acs`

    Note

    These values aren't literal values. Update these values with the actual Sign-on URL, Identifier, and Reply URL values. Contact [Resource Central – SAML SSO for Meeting Room Booking System Client support team](mailto:st@aod.vn) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up single sign-on with SAML** page, in **SAML Signing Certificate**, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. In **Set up Resource Central – SAML SSO for Meeting Room Booking System**, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

### Create Resource Central SAML SSO for Meeting Room Booking System test user

In this section, a user called **B.Simon** is created in **Resource Central – SAML SSO for Meeting Room Booking System**.

1. In Resource Central – SAML SSO for Meeting Room Booking System, select **Security** &gt; **Persons** &gt; **New**.

    ![Screenshot that shows the Persons pane in Resource Central, with the New button highlighted.](media/resource-central/new-person.png)
2. In **Person Details**, for **Display name**, enter the user **B.Simon**. For **SMTP Address**, enter the user's Microsoft Entra user name. For example, `B.Simon@contoso.com`.

    ![Screenshot that shows the Person Details pane in Resource Central.](media/resource-central/person.png)

## Configure Resource Central SAML SSO for Meeting Room Booking System SSO

In this section, you configure single sign-on in **Resource Central System Administrator**.

1. In Resource Central – SAML SSO for Meeting Room Booking System System Administrator, select **External Authentication**.
2. For **Enable Configuration**, select **Yes**.

    ![Screenshot that shows the Enable Configuration option selected in the External Authentication pane in Resource Central – SAML SSO for Meeting Room Booking System.](media/resource-central/enable.png)
3. In **Authentication Protocol**, select **SAML2**.

    ![Screenshot that shows SAML2 selected for Authentication Protocol in Resource Central.](media/resource-central/protocol.png)
4. Under **SAML2 Configuration**, enter the values for the following fields:

    1. For **Identifier (Entity ID)**, **Login URL**, **Logout URL**, and **Microsoft Entra Identifier**, enter the relevant URLs:

        ![Screenshot of the SAML2 Configuration pane in Resource Central.](media/resource-central/auth.png)

        Copy the URLs from the **Set up Resource Central – SAML SSO for Meeting Room Booking System** pane:

        ![Screenshot of the Set up Resource Central pane in Resource Central.](media/resource-central/setup.png)
    2. For **Return URL**, enter `https://<DOMAIN_NAME>/ResourceCentral/ExAuth/Saml2Authentication/CallbackHandler`.
5. For **Certificate**, upload your certificate and enter your password.

    ![Screenshot of the certificate section in Resource Central – SAML SSO for Meeting Room Booking System.](media/resource-central/cert.png)
6. Select **Save**.
7. Return to the **Azure portal**. In **SAML Signing Certificate**, upload your certificate and enter your password.
8. Select **Add**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration. To test single sign-on, you have three options:

- In the Azure portal, select **Test this application**. The link redirects to the Resource Central – SAML SSO for Meeting Room Booking System sign-on URL, where you can initiate login.
- Go to the Resource Central – SAML SSO for Meeting Room Booking System sign-on URL directly and initiate login.

    ![Screenshot of the Resource Central single sign-on test webpage.](media/resource-central/test.png)
- Use the My Apps portal from Microsoft. In the My Apps portal, select the **Resource Central – SAML SSO for Meeting Room Booking System** tile to redirect to the Resource Central – SAML SSO for Meeting Room Booking System sign-on URL. For more information, see [Sign in and start apps from the My Apps portal](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
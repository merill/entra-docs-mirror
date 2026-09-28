---
layout: Conceptual
title: Configure Panorama9 for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/panorama9-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Panorama9.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 220ae7c5-cf42-2bb7-2748-5c83dac48dce
document_version_independent_id: 3e806d28-3a3f-dc0b-5157-e7f135a87cc5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/panorama9-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/panorama9-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/panorama9-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 1e689ed2-8a7e-a67c-e0eb-4a630f2b4322
---

# Configure Panorama9 for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Panorama9 with Microsoft Entra ID. When you integrate Panorama9 with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Panorama9.
- Enable your users to be automatically signed-in to Panorama9 with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Panorama9 single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Panorama9 supports **SP** initiated SSO.

## Add Panorama9 from the gallery

To configure the integration of Panorama9 into Microsoft Entra ID, you need to add Panorama9 from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Panorama9** in the search box.
4. Select **Panorama9** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Panorama9

Configure and test Microsoft Entra SSO with Panorama9 using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Panorama9.

To configure and test Microsoft Entra SSO with Panorama9, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Panorama9 SSO**- to configure the single sign-on settings on application side.
    1. **Create Panorama9 test user** - to have a counterpart of B.Simon in Panorama9 that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Panorama9** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Sign on URL** text box, type the URL: `https://dashboard.panorama9.com/saml/access/3262`

    b. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://www.panorama9.com/saml20/<TENANT_NAME>`

    Note

    These values aren't real. Update these values with the actual Sign on URL and Identifier. Contact the Panorama9 Client support team `https://support.panorama9.com` to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. In the **SAML Signing Certificate** section, select **Edit** button to open **SAML Signing Certificate** dialog.

    ![Edit SAML Signing Certificate](common/edit-certificate.png)
7. In the **SAML Signing Certificate** section, copy the **Thumbprint** and save it on your computer.

    ![Copy Thumbprint value](common/copy-thumbprint.png)
8. On the **Set up Panorama9** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Panorama9 SSO

1. In a different web browser window, sign in to your Panorama9 company site as an administrator.
2. Navigate to **Manage** &gt; **Extensions** &gt; **Single Sign-On**.
3. In the **Settings** section, perform the following steps:

    ![Settings](media/panorama9-tutorial/configuration.png)

    a. Enable the Single Sign-On.

    b. In **Identity URL** textbox, paste the value of **Identifier(Entity ID)**.

    c. In **Certificate fingerprint** textbox, paste the **Thumbprint** value of certificate.
4. Select **Save Changes**.

### Create Panorama9 test user

In order to enable Microsoft Entra users to sign in to Panorama9, they must be provisioned into Panorama9.

In the case of Panorama9, provisioning is a manual task.

**To configure user provisioning, perform the following steps:**

1. Sign in to your **Panorama9** company site as an administrator.
2. In the Users section, type the email address of a valid Microsoft Entra user you want to provision into the **Email** textbox and give a valid **Name**.

    ![Users](media/panorama9-tutorial/new-user.png)
3. Select **Create user**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Panorama9 Sign on URL where you can initiate the login flow.
- Go to Panorama9 Sign on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Panorama9 tile in the My Apps, this option redirects to Panorama9 Sign on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
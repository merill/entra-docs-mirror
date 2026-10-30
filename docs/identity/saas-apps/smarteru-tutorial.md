---
layout: Conceptual
title: Configure SmarterU for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/smarteru-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and SmarterU.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: a5fbf86f-3d17-fca2-5726-afae32afdc88
document_version_independent_id: a7d6e9dd-1276-90f3-f73c-5d8b3c9e0776
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/smarteru-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/smarteru-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/smarteru-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 118197bf-2559-9750-29bc-892a30b75d32
---

# Configure SmarterU for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Note

The process for integrating SmarterU with Microsoft Entra ID is also documented and maintained in the [SmarterU help system](https://support.smarteru.com/docs/sso-azure-active-directory).

In this article, you learn how to integrate SmarterU with Microsoft Entra ID. When you integrate SmarterU with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to SmarterU.
- Enable your users to be automatically signed-in to SmarterU with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- SmarterU single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- SmarterU supports **IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add SmarterU from the gallery

To configure the integration of SmarterU into Microsoft Entra ID, you need to add SmarterU from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **SmarterU** in the search box.
4. Select **SmarterU** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for SmarterU

Configure and test Microsoft Entra SSO with SmarterU using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in SmarterU.

To configure and test Microsoft Entra SSO with SmarterU, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure SmarterU SSO**- to configure the single sign-on settings on application side.
    1. **Create SmarterU test user** - to have a counterpart of B.Simon in SmarterU that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **SmarterU** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following step:

    In the **Identifier** text box, type the URL: `https://www.smarteru.com/`
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up SmarterU** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure SmarterU SSO

1. In a different web browser window, sign in to your SmarterU company site as an administrator.
2. In the toolbar on the top, select **Account Settings**.

    ![Account Settings](media/smarteru-tutorial/settings.png)
3. On the account configuration page, perform the following steps:

    ![External Authorization](media/smarteru-tutorial/configuration.png)

    a. Select **Enable External Authorization**.

    b. In the **Master Login Control** section, select the **SmarterU** tab.

    c. In the **User Default Login** section, select the **SmarterU** tab.

    d. Select **Enable SAML**.

    e. Copy the content of the downloaded metadata file, and then paste it into the **IdP Metadata** textbox.

    f. Select an **Identifier Attribute/Claim**.

    g. Select **Save**.

### Create SmarterU test user

To enable Microsoft Entra users to sign in to SmarterU, they must be provisioned into SmarterU. In the case of SmarterU, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. sign in to your **SmarterU** tenant.
2. Go to **Users**.
3. In the user section, perform the following steps:

    ![New User](media/smarteru-tutorial/add-user.png)

    a. Select **+User**.

    b. Type the related attribute values of the Microsoft Entra user account into the following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.

    c. Select **Active**.

    d. Select **Save**.

Note

You can use any other SmarterU user account creation tools or APIs provided by SmarterU to provision Microsoft Entra user accounts.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the SmarterU for which you set up the SSO.
- You can use Microsoft My Apps. When you select the SmarterU tile in the My Apps, you should be automatically signed in to the SmarterU for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
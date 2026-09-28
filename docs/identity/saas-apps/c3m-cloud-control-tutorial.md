---
layout: Conceptual
title: Configure C3M Cloud Control for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/c3m-cloud-control-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and C3M Cloud Control.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 68b81ee7-555d-2da1-4e77-f798a739af14
document_version_independent_id: 0b536184-fb5f-dd45-f3c0-d60207e7dc86
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/c3m-cloud-control-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/c3m-cloud-control-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/c3m-cloud-control-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: b2e80b53-7e51-bf43-9b0e-0d36d80c93af
---

# Configure C3M Cloud Control for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate C3M Cloud Control with Microsoft Entra ID. When you integrate C3M Cloud Control with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to C3M Cloud Control.
- Enable your users to be automatically signed-in to C3M Cloud Control with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- C3M Cloud Control single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- C3M Cloud Control supports **SP** initiated SSO.
- C3M Cloud Control supports **Just In Time** user provisioning.

## Add C3M Cloud Control from the gallery

To configure the integration of C3M Cloud Control into Microsoft Entra ID, you need to add C3M Cloud Control from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **C3M Cloud Control** in the search box.
4. Select **C3M Cloud Control** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for C3M Cloud Control

Configure and test Microsoft Entra SSO with C3M Cloud Control using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in C3M Cloud Control.

To configure and test Microsoft Entra SSO with C3M Cloud Control, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure C3M Cloud Control SSO**- to configure the single sign-on settings on application side.
    1. **Create C3M Cloud Control test user** - to have a counterpart of B.Simon in C3M Cloud Control that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **C3M Cloud Control** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<C3MCLOUDCONTROL_ACCESS_URL>/api/sso/saml`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<C3MCLOUDCONTROL_ACCESS_URL>/api/sso/saml`

    c. In the **Sign on URL** text box, type a URL using the following pattern: `https://<C3MCLOUDCONTROL_ACCESS_URL>`

    Note

    These values aren't real. Update these values with the actual Identifier,Reply URL and Sign on URL. Contact [C3M Cloud Control Client support team](mailto:support@c3m.io) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up C3M Cloud Control** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure C3M Cloud Control SSO

To configure SSO for C3M Cloud Control, please do follow the [documentation](https://c3m.freshdesk.com/support/solutions/articles/44001946272-configuring-sso-using-saml-azure).

### Create C3M Cloud Control test user

In this section, a user called B.Simon is created in C3M Cloud Control. C3M Cloud Control supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in C3M Cloud Control, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to C3M Cloud Control Sign-on URL where you can initiate the login flow.
- Go to C3M Cloud Control Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the C3M Cloud Control tile in the My Apps, this option redirects to C3M Cloud Control Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
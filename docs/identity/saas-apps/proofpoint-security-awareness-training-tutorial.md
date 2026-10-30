---
layout: Conceptual
title: Configure Proofpoint Security Awareness Training for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/proofpoint-security-awareness-training-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Proofpoint Security Awareness Training.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 6a2593f8-f8f9-0b45-0b42-545b4ccb131e
document_version_independent_id: c3a2172f-6d7e-921a-7129-4ec597991e0e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/proofpoint-security-awareness-training-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/proofpoint-security-awareness-training-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/proofpoint-security-awareness-training-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 1539bf99-d154-1e5b-dcbf-e255f59c68af
---

# Configure Proofpoint Security Awareness Training for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Proofpoint Security Awareness Training with Microsoft Entra ID. This application allows Microsoft Entra ID to act as SAML IdP for authenticating users to Proofpoint Security Awareness Training. When you integrate Proofpoint Security Awareness Training with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Proofpoint Security Awareness Training.
- Enable your users to be automatically signed-in to Proofpoint Security Awareness Training with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You configure and test Microsoft Entra single sign-on for Proofpoint Security Awareness Training in a test environment. Proofpoint Security Awareness Training supports both **SP** and **IDP** initiated single sign-on and **Just In Time** user provisioning.

## Prerequisites

To integrate Microsoft Entra ID with Proofpoint Security Awareness Training, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Proofpoint Security Awareness Training single sign-on (SSO) enabled subscription.

## Add application and assign a test user

Before you begin the process of configuring single sign-on, you need to add the Proofpoint Security Awareness Training application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the single sign-on configuration.

### Add Proofpoint Security Awareness Training from the Microsoft Entra gallery

Add Proofpoint Security Awareness Training from the Microsoft Entra application gallery to configure single sign-on with Proofpoint Security Awareness Training. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Proofpoint Security Awareness Training** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    [![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)](common/edit-urls.png#lightbox)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.<ENVIRONMENT>/api/auth/saml/metadata`

    b. In the **Reply URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.<ENVIRONMENT>/api/auth/saml/SSO`
6. If you wish to configure the application in **SP** initiated mode, then perform the following steps:

    a. In the **Sign on URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.<ENVIRONMENT>`

    b. In the **Relay State** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.<ENVIRONMENT>`

    c. In the **Logout Url** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.<ENVIRONMENT>/api/auth/saml/SingleLogout`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL, Sign on URL, Relay State and Logout Url. Contact [Proofpoint Security Awareness Training Client support team](mailto:wst-support@proofpoint.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    [![Screenshot shows the Certificate download link.](common/copy-metadataurl.png)](common/copy-metadataurl.png#lightbox)

## Configure Proofpoint Security Awareness Training SSO

To configure single sign-on on **Proofpoint Security Awareness Training** side, you need to send the **App Federation Metadata Url** to [Proofpoint Security Awareness Training support team](mailto:wst-support@proofpoint.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Proofpoint Security Awareness Training test user

In this section, a user called B.Simon is created in Proofpoint Security Awareness Training. Proofpoint Security Awareness Training supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Proofpoint Security Awareness Training, a new one is commonly created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Proofpoint Security Awareness Training Sign-on URL where you can initiate the login flow.
- Go to Proofpoint Security Awareness Training Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Proofpoint Security Awareness Training for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Proofpoint Security Awareness Training tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Proofpoint Security Awareness Training for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
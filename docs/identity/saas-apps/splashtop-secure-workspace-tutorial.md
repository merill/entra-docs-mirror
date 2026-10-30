---
layout: Conceptual
title: Configure Splashtop Secure Workspace for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/splashtop-secure-workspace-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Splashtop Secure Workspace.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 2acfc4d0-8c0b-b32d-8de4-bcb1dbf9e09a
document_version_independent_id: 8a5302b4-2e49-c66b-c2d6-6f176ceb6076
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/splashtop-secure-workspace-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/splashtop-secure-workspace-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/splashtop-secure-workspace-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 33a08eaf-e522-0e0e-60ca-bce22b9e5337
---

# Configure Splashtop Secure Workspace for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Splashtop Secure Workspace with Microsoft Entra ID. When you integrate Splashtop Secure Workspace with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Splashtop Secure Workspace.
- Enable your users to be automatically signed-in to Splashtop Secure Workspace with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Splashtop Secure Workspace single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Splashtop Secure Workspace supports **SP** initiated SSO.
- Splashtop Secure Workspace supports **Just In Time** user provisioning.

## Add Splashtop Secure Workspace from the gallery

To configure the integration of Splashtop Secure Workspace into Microsoft Entra ID, you need to add Splashtop Secure Workspace from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Splashtop Secure Workspace** in the search box.
4. Select **Splashtop Secure Workspace** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Splashtop Secure Workspace

Configure and test Microsoft Entra SSO with Splashtop Secure Workspace using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Splashtop Secure Workspace.

To configure and test Microsoft Entra SSO with Splashtop Secure Workspace, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Splashtop Secure Workspace SSO**- to configure the single sign-on settings on application side.
    1. **Create Splashtop Secure Workspace test user** - to have a counterpart of B.Simon in Splashtop Secure Workspace that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Splashtop Secure Workspace** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<ORG.ORG_NAME>.us.ssw.splashtop.com/realms/<ORG.ENTITY_ID>`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<ORG.ORG_NAME>.us.ssw.splashtop.com/realms/<ORG.ORG_NAME>/broker/<ORG.ENTITY_ID>/endpoint`

    c. In the **Sign on URL** text box, type a URL using the following pattern: `https://<ORG.ORG_NAME>.us.ssw.splashtop.com`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign on URL. Contact [Splashtop Secure Workspace support team](mailto:support-ssw@splashtop.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section in the Microsoft Entra admin center.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)
7. On the **Set up Splashtop Secure Workspace** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration URLs.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Splashtop Secure Workspace SSO

To configure single sign-on on **Splashtop Secure Workspace** side, you need to send the downloaded **Federation Metadata XML** and appropriate copied URLs from Microsoft Entra admin center to [Splashtop Secure Workspace support team](mailto:support-ssw@splashtop.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Splashtop Secure Workspace test user

In this section, a user called B.Simon is created in Splashtop Secure Workspace. Splashtop Secure Workspace supports just-in-time provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Splashtop Secure Workspace, a new one is created when you attempt to access Splashtop Secure Workspace.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application** in Microsoft Entra admin center. this option redirects to Splashtop Secure Workspace Sign-on URL where you can initiate the login flow.
- Go to Splashtop Secure Workspace Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Splashtop Secure Workspace tile in the My Apps, this option redirects to Splashtop Secure Workspace Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
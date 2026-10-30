---
layout: Conceptual
title: Configure SSO for Jama Connect® for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/sso-for-jama-connect-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and SSO for Jama Connect®.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 552c310c-727d-096e-16cc-6d51a3961aab
document_version_independent_id: 6eeb419f-0cb9-8041-4f46-0b2015b8687b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/sso-for-jama-connect-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/sso-for-jama-connect-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/sso-for-jama-connect-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f23c41c2-bb82-3225-69ac-4b264dafd791
---

# Configure SSO for Jama Connect® for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate SSO for Jama Connect® with Microsoft Entra ID. Jama Software®’s industry-leading platform helps teams manage requirements with Live Traceability™ through the systems development process for proven cycle time reduction and quality improvement. When you integrate SSO for Jama Connect® with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to SSO for Jama Connect®.
- Enable your users to be automatically signed-in to SSO for Jama Connect® with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You'll configure and test Microsoft Entra single sign-on for SSO for Jama Connect® in a test environment. SSO for Jama Connect® supports both **SP** and **IDP** initiated single sign-on and also **Just In Time** user provisioning.

## Prerequisites

To integrate Microsoft Entra ID with SSO for Jama Connect®, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- SSO for Jama Connect® single sign-on (SSO) enabled subscription.

## Add application and assign a test user

Before you begin the process of configuring single sign-on, you need to add the SSO for Jama Connect® application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the single sign-on configuration.

### Add SSO for Jama Connect® from the Microsoft Entra gallery

Add SSO for Jama Connect® from the Microsoft Entra application gallery to configure single sign-on with SSO for Jama Connect®. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **SSO for Jama Connect®** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type a value using the following pattern: `urn:auth0:<First_Part_of_Auth0_Domain>:<TenantID>`

    b. In the **Reply URL** textbox, type a URL using the following pattern: `https://<Auth0_Domain>/login/callback?connection=<TenantID>`
6. Perform the following step, if you wish to configure the application in **SP** initiated mode:

    In the **Sign on URL** textbox, type a URL using the following pattern: `https://<Tenant_Name>.jamacloud.com/login.req`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign on URL. Contact [SSO for Jama Connect® support team](mailto:support@jamasoftware.zendesk.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/copy-metadataurl.png)

## Configure SSO for Jama Connect® SSO

To configure single sign-on on **SSO for Jama Connect®** side, you need to send the **App Federation Metadata Url** to [SSO for Jama Connect® support team](mailto:support@jamasoftware.zendesk.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create SSO for Jama Connect® test user

In this section, a user called B.Simon is created in SSO for Jama Connect®. SSO for Jama Connect® supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in SSO for Jama Connect®, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to SSO for Jama Connect® Sign-on URL where you can initiate the login flow.
- Go to SSO for Jama Connect® Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the SSO for Jama Connect® for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the SSO for Jama Connect® tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the SSO for Jama Connect® for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
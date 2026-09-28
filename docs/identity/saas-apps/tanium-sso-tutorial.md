---
layout: Conceptual
title: Configure Tanium SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/tanium-sso-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Tanium SSO.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 65bfa0b5-3ea4-310e-60c1-8a826fe5076f
document_version_independent_id: c2bbe11b-8d30-fe42-56fb-e631d191cacb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/tanium-sso-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/tanium-sso-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/tanium-sso-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 466bcba1-304c-c84a-9ddd-397ab10dc24a
---

# Configure Tanium SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Tanium SSO with Microsoft Entra ID. Tanium, the industry’s only provider of converged endpoint management (XEM), leads the paradigm shift in legacy approaches to managing complex security and technology environments. When you integrate Tanium SSO with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Tanium SSO.
- Enable your users to be automatically signed-in to Tanium SSO with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You'll configure and test Microsoft Entra single sign-on for Tanium SSO in a test environment. Tanium SSO supports both **SP** and **IDP** initiated single sign-on and also **Just In Time** user provisioning. Tanium SSO also supports [Automated user provisioning](tanium-sso-provisioning-tutorial).

## Prerequisites

To integrate Microsoft Entra ID with Tanium SSO, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Tanium SSO single sign-on (SSO) enabled subscription.

## Add application and assign a test user

Before you begin the process of configuring single sign-on, you need to add the Tanium SSO application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the single sign-on configuration.

### Add Tanium SSO from the Microsoft Entra gallery

Add Tanium SSO from the Microsoft Entra application gallery to configure single sign-on with Tanium SSO. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Tanium SSO** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    [![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)](common/edit-urls.png#lightbox)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type a value using the following pattern: `urn:amazon:cognito:sp:<InstanceName>`

    b. In the **Reply URL** textbox, type a URL using the following pattern: `https://<InstanceName>-tanium.auth.<SUBDOMAIN>.amazoncognito.com/saml2/idpresponse`
6. If you wish to configure the application in **SP** initiated mode, then perform the following step:

    In the **Sign on URL** textbox, type a URL using the following pattern: `https://<InstanceName>.cloud.tanium.com`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign on URL. Contact [Tanium Support](https://community.tanium.com/s/contactsupport) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.

    Note

    If deploying Tanium in an on-premises configuration, your values may look different than those shown above. The values to use can be retrieved from the **Administration &gt; SAML Configuration** menu in the Tanium console. Details can be found in the [Tanium Console User Guide: Integrating with a SAML IdP](https://docs.tanium.com/platform_user/platform_user/console_using_saml.html?cloud=false).
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer. If deploying to Tanium in an on-premises configuration, select the edit button and set the **Response Signing Option** to "Sign response and assertion".

    [![Screenshot shows the Certificate download link.](common/copy-metadataurl.png)](common/copy-metadataurl.png#lightbox)

## Configure Tanium SSO

To configure single sign-on on **Tanium SSO** side, you need to send the **App Federation Metadata Url** to [Tanium Support](https://community.tanium.com/s/contactsupport). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Tanium SSO test user

In this section, a user called B.Simon is created in Tanium SSO. Tanium SSO supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Tanium SSO, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Tanium SSO Sign-on URL where you can initiate the login flow.
- Go to Tanium SSO Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Tanium SSO for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Tanium SSO tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Tanium SSO for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
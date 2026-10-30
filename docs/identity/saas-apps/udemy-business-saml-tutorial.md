---
layout: Conceptual
title: Configure Udemy Business SAML for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/udemy-business-saml-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Udemy Business SAML.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 669daf7a-ae87-960c-4311-2925ac80f859
document_version_independent_id: b2e7afb2-0e0c-a121-7b2e-6effe757455a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/udemy-business-saml-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/udemy-business-saml-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/udemy-business-saml-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 5f82d5b4-9422-2c60-9af6-6550580b3b28
---

# Configure Udemy Business SAML for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Udemy Business SAML with Microsoft Entra ID. Udemy for Business helps employees do whatever comes next - whether that’s the next project to tackle, skill to learn or role to master. When you integrate Udemy Business SAML with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Udemy Business SAML.
- Enable your users to be automatically signed-in to Udemy Business SAML with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You'll configure and test Microsoft Entra single sign-on for Udemy Business SAML in a test environment. Udemy Business SAML supports **SP** initiated single sign-on and **Just In Time** user provisioning.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Prerequisites

To integrate Microsoft Entra ID with Udemy Business SAML, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Udemy Business SAML single sign-on (SSO) enabled subscription.

## Add application and assign a test user

Before you begin the process of configuring single sign-on, you need to add the Udemy Business SAML application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the single sign-on configuration.

### Add Udemy Business SAML from the Microsoft Entra gallery

Add Udemy Business SAML from the Microsoft Entra application gallery to configure single sign-on with Udemy Business SAML. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Udemy Business SAML** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type the URL: `https://www.udemy.com/sso/saml`

    b. In the **Reply URL** textbox, type the URL: `https://sso.connect.pingidentity.com/sso/sp/ACS.saml2`

    c. In the **Sign on URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.udemy.com`

    Note

    This value isn't real. Update this value with the actual Sign-on URL. Contact [Udemy Business SAML Client support team](mailto:ufbsupport@udemy.com) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. Udemy Business SAML application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows the image of attributes configuration.](common/default-attributes.png)
7. In addition to above, Udemy Business SAML application expects few more attributes to be passed back in SAML response, which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | email | user.mail |
    | firstName | user.givenname |
    | lastName | user.surname |
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/copy-metadataurl.png)

## Configure Udemy Business SAML SSO

To configure single sign-on on **Udemy Business SAML** side, you need to send the **App Federation Metadata Url** to [Udemy Business SAML support team](mailto:ufbsupport@udemy.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Udemy Business SAML test user

In this section, a user called B.Simon is created in Udemy Business SAML. Udemy Business SAML supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Udemy Business SAML, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Udemy Business SAML Sign-on URL where you can initiate the login flow.
- Go to Udemy Business SAML Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Udemy Business SAML tile in the My Apps, this option redirects to Udemy Business SAML Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
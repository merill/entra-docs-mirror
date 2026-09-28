---
layout: Conceptual
title: Configure Elsevier SP for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/elsevier-sp-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Elsevier SP.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: d5c2ddee-04c3-25d3-478c-707f7d224e9c
document_version_independent_id: f0ebc1f6-f683-7b4f-a285-f816f9d4a95f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/elsevier-sp-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/elsevier-sp-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/elsevier-sp-tutorial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f8fe26d1-ff17-f001-7da9-22696c7775ca
---

# Configure Elsevier SP for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Elsevier SP with Microsoft Entra ID. Elsevier SP provides access to your organization's Elsevier subscriptions using your Microsoft Entra credentials. When you integrate Elsevier SP with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Elsevier SP.
- Enable your users to be automatically signed-in to Elsevier SP with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You'll configure and test Microsoft Entra single sign-on for Elsevier SP in a test environment. Elsevier SP supports only **SP** initiated single sign-on.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Prerequisites

To integrate Microsoft Entra ID with Elsevier SP, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Elsevier SP single sign-on (SSO) enabled subscription.

## Add application and assign a test user

Before you begin the process of configuring single sign-on, you need to add the Elsevier SP application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the single sign-on configuration.

### Add Elsevier SP from the Microsoft Entra gallery

Add Elsevier SP from the Microsoft Entra application gallery to configure single sign-on with Elsevier SP. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Elsevier SP** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type the URL: `https://sdauth.sciencedirect.com/`

    b. In the **Reply URL** textbox, type the URL: `https://auth.elsevier.com/SHIRE/SAML2/POST`

    c. In the **Sign on URL** textbox, type a URL using the following pattern: `https://auth.elsevier.com/ShibAuth/institutionLogin?entityID=<customer-URL-encoded-entityID>&appReturnURL=https%3A%2F%2Fwww.sciencedirect.com`
6. Your Elsevier SP application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the example. The default value of **Unique User Identifier** is **user.userprincipalname** but Elsevier SP expects to be mapped with a Persistent Name ID. For that you can use **user.objectid** attribute from the list or use the appropriate attribute value based on your organization configuration.

    ![Screenshot shows the image of token attributes.](common/default-attributes.png)
7. On the **Set-up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)
8. On the **Set up Elsevier SP** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows how to copy configuration appropriate URL.](common/copy-configuration-urls.png)

## Configure Elsevier SP SSO

To configure single sign-on on **Elsevier SP** side, you need to send the downloaded **Federation Metadata XML** and appropriate copied URLs from the application configuration to [Elsevier SP support team](mailto:iam_platform@elsevier.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Elsevier SP test user

In this section, you create a user called Britta Simon in Seculio. Work with [Elsevier SP support team](mailto:iam_platform@elsevier.com) to add the users in the Seculio platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Elsevier SP Sign-on URL where you can initiate the login flow.
- Go to Elsevier SP Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Elsevier SP tile in the My Apps, this option redirects to Elsevier SP Sign on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
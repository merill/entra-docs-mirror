---
layout: Conceptual
title: Configure CITI Program for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/citi-program-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and CITI Program.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 12000822-028e-ff3f-c4cf-dc850fb3358b
document_version_independent_id: e200d82a-c493-42fc-6319-0a8b6859962a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/citi-program-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/citi-program-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/citi-program-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 9ff4e891-94e5-181c-a0d7-f0c3a91c3fc0
---

# Configure CITI Program for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article teaches you how to integrate CITI Program with Microsoft Entra ID. CITI Program identifies education and training needs in the communities we serve and provides high-quality, peer-reviewed, web-based educational materials to meet those needs. When you integrate CITI Program with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to CITI Program.
- Enable your users to be automatically signed in to CITI Program with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You configure and test Microsoft Entra single sign-on for CITI Program in a test environment. CITI Program supports **SP-initiated** single sign-on and **Just-In-Time** user provisioning.

Note

The identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Prerequisites

To integrate Microsoft Entra ID with CITI Program, you need:

- CITI Program Single Sign-On (SSO) enabled subscription. Note that [SSO is a paid service with CITI Program](https://support.citiprogram.org/s/article/single-sign-on-sso-and-shibboleth-technical-specs#General).
- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Add application and assign a test user

Before configuring single sign-on, you need to add the CITI Program application from the Microsoft Entra gallery and assign a test user account. Then, you can test the single sign-on configuration.

### Add CITI Program from the Microsoft Entra gallery

Add CITI Program from the Microsoft Entra application gallery to configure single sign-on with CITI Program. For more information on how to add an application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **CITI Program** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** textbox, use the URL: `https://www.citiprogram.org/shibboleth`

    b. In the **Reply URL (Assertion Consumer Service URL)** textbox, use the URL: `https://www.citiprogram.org/Shibboleth.sso/SAML2/POST`

    c. In the **Sign on URL** textbox, use the URL: `https://www.citiprogram.org/portal`

    Note

    At the end of the configuration, you may update the **Sign on URL** with the SSO link provided by CITI Program Support.
6. The CITI Program application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows the image of attributes configuration.](common/default-attributes.png)
7. CITI Program application expects urn:oid named attributes to be passed back in the SAML response, shown below. These are all required. You may rename or remove the default attributes to configure them.

    | Name | Source Attribute |
    | --- | --- |
    | urn:oid:1.3.6.1.4.1.5923.1.1.1.6 | user.userprincipalname |
    | urn:oid:0.9.2342.19200300.100.1.3 | user.mail |
    | urn:oid:2.5.4.42 | user.givenname |
    | urn:oid:2.5.4.4 | user.surname |
8. If you wish to pass additional information in the SAML response, CITI Program can also accept the following optional attributes.

    | Name | Source Attribute |
    | --- | --- |
    | urn:oid:2.16.840.1.113730.3.1.241 | user.displayname |
    | urn:oid:2.16.840.1.113730.3.1.3 | user.employeeid |

    Note

    The Source Attribute is what is generally recommended but not necessarily a rule. For example, if user.mail is unique and scoped, it can also be passed as urn:oid:1.3.6.1.4.1.5923.1.1.1.6.
9. On the **Set-up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find the **App Federation Metadata Url** and copy it, or the **Federation Metadata XML** and select **Download** to download the certificate.

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)
10. On the **Set up CITI Program** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration appropriate URL.](common/copy-configuration-urls.png)

## Configure CITI Program SSO

To configure single sign-on on **CITI Program** side, you need to send the copied **App Federation Metadata Url** or the downloaded **Federation Metadata XML** to [CITI Program Support](mailto:shibboleth@citiprogram.org). This is required to have the SAML SSO connection set properly on both sides. Also, provide any additional scopes or domains for your integration.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with the following options.

- Select **Test this application**, this option redirects to CITI Program Sign-on URL, where you can initiate the login flow.
- Go to CITI Program Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. Selecting the CITI Program tile in the My Apps will redirect to CITI Program Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).

CITI Program supports just-in-time user provisioning. First-time SSO users are prompted to either:

- Link their existing CITI Program account in case they already have one ![SSOHaveAccount](https://user-images.githubusercontent.com/46728557/228357500-a74489c7-8c5f-4cbe-ad47-9757d3d9fbe6.PNG)
- Or Create a new CITI Program account, which is automatically provisioned ![SSONotHaveAccount](https://user-images.githubusercontent.com/46728557/228357503-f4eba4bb-f3fa-43e9-a98a-f0da87074eeb.PNG)
---
layout: Conceptual
title: Configure Autodesk SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/autodesk-sso-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Autodesk SSO.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: ed5f44ce-e73b-8890-74c2-8666a1085e51
document_version_independent_id: 093ec267-b53b-13e2-d99f-42926099090d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/autodesk-sso-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/autodesk-sso-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/autodesk-sso-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: a9b17be6-2dce-c0ff-eeee-2c535011a43c
---

# Configure Autodesk SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Autodesk SSO with Microsoft Entra ID. When you integrate Autodesk SSO with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Autodesk SSO.
- Enable your users to be automatically signed-in to Autodesk SSO with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Autodesk SSO single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Autodesk SSO supports **SP** initiated SSO.
- Autodesk SSO supports **Just In Time** user provisioning.
- Autodesk SSO supports [Automated user provisioning](autodesk-sso-provisioning-tutorial).

## Adding Autodesk SSO from the gallery

To configure the integration of Autodesk SSO into Microsoft Entra ID, you need to add Autodesk SSO from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Autodesk SSO** in the search box.
4. Select **Autodesk SSO** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Autodesk SSO

Configure and test Microsoft Entra SSO with Autodesk SSO using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Autodesk SSO.

To configure and test Microsoft Entra SSO with Autodesk SSO, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Autodesk SSO**- to configure the single sign-on settings on application side.
    1. **Create Autodesk SSO test user** - to have a counterpart of B.Simon in Autodesk SSO that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Autodesk SSO** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://www.okta.com/saml2/service-provider/<UNIQUE_ID>`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://autodesk-prod.okta.com/sso/saml2/<UNIQUE_ID>`

    c. In the **Sign on URL** text box, type the URL: `https://autodesk-prod.okta.com/sso/saml2/`

    Note

    These values aren't real. Update these values with the actual Identifier and Reply URL. Contact [Autodesk SSO Client support team](https://knowledge.autodesk.com/contact-support) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. Autodesk SSO application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
7. In addition to above, Autodesk SSO application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | firstName | user.givenname |
    | lastName | user.surname |
    | objectGUID | user.objectid |
    | email | user.mail |
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
9. On the **Set up Autodesk SSO** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Autodesk SSO

To configure single sign-on on **Autodesk SSO** side, you need to send the downloaded **Certificate (Base64)** and appropriate copied URLs from the application configuration to [Autodesk SSO support team](https://knowledge.autodesk.com/contact-support). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Autodesk SSO test user

In this section, a user called Britta Simon is created in Autodesk SSO. Autodesk SSO supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Autodesk SSO, a new one is created after authentication.

## Test SSO

To test the Autodesk SSO, open the Autodesk console and select **Test Connection** button and authenticate using the test account which you have created in the **Create a Microsoft Entra test user** section.
---
layout: Conceptual
title: Configure SAP Fieldglass for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/fieldglass-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and SAP Fieldglass.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: f97c243f-ca89-085a-4d18-40ba9b89bf90
document_version_independent_id: 960cf6d7-4433-9685-1c15-0e95d9faed9e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/fieldglass-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/fieldglass-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/fieldglass-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 8486aed1-969c-7534-bd8a-37d73ded1cae
---

# Configure SAP Fieldglass for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate SAP Fieldglass with Microsoft Entra ID. When you integrate Fieldglass with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Fieldglass via single-sign on.
- Enable your users to be automatically signed-in to Fieldglass with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Your Fieldglass implementation is ready to be configured for single sign-on (SSO). For more information, see [SAP Fieldglass Single-Sign on (SSO) Configuration Guide](https://help.sap.com/doc/eb7e719be14d4e3c9a4802a73f9b2f52/cloud/en-US/SAPFieldglassSSOConfigurationGuide.pdf).

## Scenario description

Before configuring single sign-on in a production deployment, we recommend you configure and test Microsoft Entra single sign-on in a test environment.

- This integration with Fieldglass supports **IDP** initiated SSO.

## Add Fieldglass from the gallery

To configure the integration of Fieldglass into Microsoft Entra ID, you need to add Fieldglass from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Fieldglass** in the search box.
4. Select **Fieldglass** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Fieldglass

Configure and test Microsoft Entra SSO with Fieldglass using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Fieldglass.

To configure and test Microsoft Entra SSO with Fieldglass, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Fieldglass SSO**- to configure the single sign-on settings on application side.
    1. **Create Fieldglass test user** - to have a counterpart of B.Simon in Fieldglass that's linked to the Microsoft Entra representation of that user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Fieldglass** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Set up Single Sign-On with SAML** page, perform the following steps:

    a. In the **Identifier** text box, type the URL as: `https://www.fieldglass.com` or follow the pattern: `https://<company name>.fgvms.com`

    b. In the **Reply URL** text box, type a URL using one of the following patterns:

    | Reply URL |
    | --- |
    | `https://www.fieldglass.net/<company name>` |
    | `https://<company name>.fgvms.com/<company name>` |
    |  |

    Note

    These values aren't real. Update these values with the actual Identifier and Reply URL. Contact [Fieldglass Client support team](https://www.fieldglass.com/customer-support) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Fieldglass** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Fieldglass SSO

To configure single sign-on on **Fieldglass** side, you need to send the downloaded **Certificate (Base64)** and appropriate copied URLs from the application configuration to [Fieldglass support team](https://www.fieldglass.com/customer-support). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Fieldglass test user

In this section, you create a user called Britta Simon in Fieldglass. If necessary, work with your [Fieldglass support team](https://www.fieldglass.com/customer-support) to generate a unique identifier for the user so you can create the user in the Fieldglass platform. Users must be created in Fieldglass before you use single sign-on.

Note

Fieldglass may require the user identifier sent to Fieldglass in the SAML assertion be different from the typical user account name in Microsoft Entra, in order to ensure uniqueness of user identifiers in Fieldglass.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the Fieldglass for which you set up the SSO.
- You can use Microsoft My Apps. When you select the Fieldglass tile in the My Apps, you should be automatically signed in to the Fieldglass for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
---
layout: Conceptual
title: Configure Cisco Intersight for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/cisco-intersight-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Cisco Intersight.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 4ca2c309-f31a-790f-2e48-cca7a99cc477
document_version_independent_id: 8b157640-e51c-5fc9-66a7-6b7abcf751ff
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/cisco-intersight-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/cisco-intersight-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/cisco-intersight-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: da164811-a8d5-0c95-cd31-93e491ddb3e3
---

# Configure Cisco Intersight for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Cisco Intersight with Microsoft Entra ID. When you integrate Cisco Intersight with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Cisco Intersight.
- Enable your users to be automatically signed-in to Cisco Intersight with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Cisco Intersight single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Cisco Intersight supports **SP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Adding Cisco Intersight from the gallery

To configure the integration of Cisco Intersight into Microsoft Entra ID, you need to add Cisco Intersight from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Cisco Intersight** in the search box.
4. Select **Cisco Intersight** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

For step-by-step guidance on adding enterprise applications, refer to [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Cisco Intersight

Configure and test Microsoft Entra SSO with Cisco Intersight using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Cisco Intersight.

To configure and test Microsoft Entra SSO with Cisco Intersight, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Cisco Intersight SSO** - to configure the single sign-on settings on application side.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Cisco Intersight** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    a. In the **Sign on URL** text box, type the URL: `https://intersight.com`

    b. In the **Identifier (Entity ID)** text box, type the URL: `www.intersight.com`
6. Your Cisco Intersight application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows an example for this. The default value of **Unique User Identifier** is **user.userprincipalname** but Cisco Intersight expects this to be mapped with the user's email address. For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration..

    ![image](common/default-attributes.png)
7. In addition to above, Cisco Intersight application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | First\_Name | user.givenname |
    | Last\_Name | user.surname |
    | memberOf | user.groups |
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
9. On the **Set up Cisco Intersight** section, copy one or more appropriate URLs based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Cisco Intersight SSO

To configure single sign-on on **Cisco Intersight** side, you need to send the downloaded **Federation Metadata XML** and appropriate copied URLs from the application configuration to [Cisco Intersight support team](mailto:intersight-feedback@cisco.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Cisco Intersight test user

### Configuring and Testing Microsoft Entra SSO for Cisco Intersight

The SSO configuration for Cisco Intersight is now self-service and managed directly through the Cisco Intersight platform. To complete the setup, visit the Cisco Intersight Help Center and follow their up-to-date guidance: [Cisco Intersight Help Documentation](https://www.intersight.com/help/saas)

#### Steps Overview:

1. Sign in to Cisco Intersight.
    1. Navigate to the **Settings** section.
    2. Access the **SSO Configuration** page.
2. Follow the self-service setup instructions provided in the Cisco Intersight Help documentation to configure the necessary SAML attributes, metadata, and certificate details.
3. Test the integration using the built-in testing tools available in both Microsoft Entra ID and Cisco Intersight to ensure seamless SSO.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Cisco Intersight Sign-on URL where you can initiate the sign in flow.
- Go to Cisco Intersight Sign on URL directly and initiate the sign in flow from there.
- You can use Microsoft My Apps. When you select the Cisco Intersight tile in the My Apps, this option redirects to Cisco Intersight Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
---
layout: Conceptual
title: Configure MS Azure SSO Access for Ethidex Compliance Office™ for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/ms-azure-sso-access-for-ethidex-compliance-office-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and MS Azure SSO Access for Ethidex Compliance Office™.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: caf79005-ae91-f853-b63b-a35d7428733e
document_version_independent_id: 689a61e9-5d49-13a7-8304-8cfb50fe1f18
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/ms-azure-sso-access-for-ethidex-compliance-office-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/ms-azure-sso-access-for-ethidex-compliance-office-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/ms-azure-sso-access-for-ethidex-compliance-office-tutorial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 3d6fd509-e186-5c73-a643-b124e62a123c
---

# Configure MS Azure SSO Access for Ethidex Compliance Office™ for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate MS Azure SSO Access for Ethidex Compliance Office™ with Microsoft Entra ID. When you integrate MS Azure SSO Access for Ethidex Compliance Office™ with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to MS Azure SSO Access for Ethidex Compliance Office™.
- Enable your users to be automatically signed-in to MS Azure SSO Access for Ethidex Compliance Office™ with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- MS Azure SSO Access for Ethidex Compliance Office™ single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- MS Azure SSO Access for Ethidex Compliance Office™ supports **IDP** initiated SSO.

## Adding MS Azure SSO Access for Ethidex Compliance Office™ from the gallery

To configure the integration of MS Azure SSO Access for Ethidex Compliance Office™ into Microsoft Entra ID, you need to add MS Azure SSO Access for Ethidex Compliance Office™ from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **MS Azure SSO Access for Ethidex Compliance Office™** in the search box.
4. Select **MS Azure SSO Access for Ethidex Compliance Office™** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for MS Azure SSO Access for Ethidex Compliance Office™

Configure and test Microsoft Entra SSO with MS Azure SSO Access for Ethidex Compliance Office™ using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in MS Azure SSO Access for Ethidex Compliance Office™.

To configure and test Microsoft Entra SSO with MS Azure SSO Access for Ethidex Compliance Office™, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure MS Azure SSO Access for Ethidex Compliance Office SSO**- to configure the single sign-on settings on application side.
    1. **Create MS Azure SSO Access for Ethidex Compliance Office test user** - to have a counterpart of B.Simon in MS Azure SSO Access for Ethidex Compliance Office™ that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **MS Azure SSO Access for Ethidex Compliance Office™** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    a. In the **Identifier** text box, type a URL using the following pattern: `com.ethidex.prod.<CLIENTID>`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://www.ethidex.com/saml2/sp/acs/<CLIENTID>`

    Note

    These values aren't real. Update these values with the actual Identifier and Reply URL. Contact [MS Azure SSO Access for Ethidex Compliance Office™ support team](mailto:support@ethidex.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. MS Azure SSO Access for Ethidex Compliance Office™ application application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes, whereas **nameidentifier** is mapped with **user.userprincipalname**. MS Azure SSO Access for Ethidex Compliance Office™ application expects **nameidentifier** to be mapped with **user.mail**, so you need to edit the attribute mapping by selecting **Edit** icon and change the attribute mapping.

    ![image](common/edit-attribute.png)
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
8. On the **Set up MS Azure SSO Access for Ethidex Compliance Office™** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure MS Azure SSO Access for Ethidex Compliance Office SSO

To configure single sign-on on **MS Azure SSO Access for Ethidex Compliance Office™** side, you need to send the downloaded **Certificate (Base64)** and appropriate copied URLs from the application configuration to [MS Azure SSO Access for Ethidex Compliance Office™ support team](mailto:support@ethidex.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create MS Azure SSO Access for Ethidex Compliance Office test user

In this section, you create a user called B.Simon in MS Azure SSO Access for Ethidex Compliance Office™. Work with [MS Azure SSO Access for Ethidex Compliance Office™ support team](mailto:support@ethidex.com) to add the users in the MS Azure SSO Access for Ethidex Compliance Office™ platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the Ethidex Compliance Office™ for which you set up the SSO
- You can use Microsoft My Apps. When you select the Ethidex Compliance Office™ tile in the My Apps, you should be automatically signed in to the Ethidex Compliance Office™ for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
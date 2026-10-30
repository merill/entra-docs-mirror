---
layout: Conceptual
title: Configure ContractSafe Saml2 SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/contractsafe-saml2-sso-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and ContractSafe Saml2 SSO.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 65c2eea2-cf3a-161f-e1bf-c6f41985921b
document_version_independent_id: b604cb9d-3b02-19d0-9f06-994be8bf7158
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/contractsafe-saml2-sso-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/contractsafe-saml2-sso-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/contractsafe-saml2-sso-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7189150b-62af-ccd5-eb16-b0b218bed1fc
---

# Configure ContractSafe Saml2 SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate ContractSafe Saml2 SSO with Microsoft Entra ID. When you integrate ContractSafe Saml2 SSO with Microsoft Entra ID, you can:

- Control who has access to ContractSafe Saml2 SSO in Microsoft Entra ID.
- Enable your users to automatically sign in to ContractSafe Saml2 SSO with their Microsoft Entra accounts.
- Manage your accounts in one central location: the Azure portal.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A ContractSafe Saml2 SSO subscription with SSO enabled.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- ContractSafe Saml2 SSO supports **IDP**-initiated SSO.

## Add ContractSafe Saml2 SSO from the gallery

To configure the integration of ContractSafe Saml2 SSO into Microsoft Entra ID, you need to add ContractSafe Saml2 SSO from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **ContractSafe Saml2 SSO** in the search box.
4. Select **ContractSafe Saml2 SSO** from the results panel, and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for ContractSafe Saml2 SSO

Configure and test Microsoft Entra SSO with ContractSafe Saml2 SSO by using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in ContractSafe Saml2 SSO.

To configure and test Microsoft Entra SSO with ContractSafe Saml2 SSO, perform the following steps:

1. Configure Microsoft Entra SSOto enable your users to use this feature.
    1. Create a Microsoft Entra test user to test Microsoft Entra SSO by using the **B.Simon** account.
    2. Assign the Microsoft Entra test user to enable **B.Simon** to use Microsoft Entra SSO.
2. Configure ContractSafe Saml2 SSOto configure the SSO settings on application side.
    1. Create a ContractSafe Saml2 SSO test user to have a counterpart of **B.Simon** in ContractSafe Saml2 SSO that's linked to the Microsoft Entra representation of the user.
3. Test SSO to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Azure portal:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **ContractSafe Saml2 SSO** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** text box, type a URL by using the following pattern: `https://app.contractsafe.com/saml2_auth/<UNIQUEID>/acs/`

    b. In the **Reply URL** text box, type a URL by using the following pattern: `https://app.contractsafe.com/saml2_auth/<UNIQUEID>/acs/`

    Note

    These values aren't real. Update these values with the actual Identifier and Reply URL. Contact the [ContractSafe Saml2 SSO Client support team](mailto:support@contractsafe.com) to get these values. You can also refer to the formats shown in the **Basic SAML Configuration** section.
6. ContractSafe Saml2 SSO expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Common default attributes](common/default-attributes.png)
7. In addition to the default attributes, the ContractSafe Saml2 SSO application expects a few more attributes to be passed back in the SAML response. These attributes are pre-populated, but you can review them according to your requirements. The following list shows the additional attributes.

    | Name | Source attribute |
    | --- | --- |
    | emailname | user.userprincipalname |
    | email | user.onpremisesuserprincipalname |
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML**. Select **Download** to download the certificate, and then save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
9. In the **Set up ContractSafe Saml2 SSO** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure ContractSafe Saml2 SSO

To configure SSO on the **ContractSafe Saml2 SSO** side, you need to send the downloaded **Federation Metadata XML** and appropriate copied URLs to the [ContractSafe Saml2 SSO support team](mailto:support@contractsafe.com). The team is responsible for setting the SAML SSO connection properly on both sides.

### Create a ContractSafe Saml2 SSO test user

Create a user called B.Simon in ContractSafe Saml2 SSO. Work with the [ContractSafe Saml2 SSO support team](mailto:support@contractsafe.com) to add the users in the ContractSafe Saml2 SSO platform. Users must be created and activated before you use SSO.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the ContractSafe Saml2 SSO for which you set up the SSO.
- You can use Microsoft My Apps. When you select the ContractSafe Saml2 SSO tile in the My Apps, you should be automatically signed in to the ContractSafe Saml2 SSO for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
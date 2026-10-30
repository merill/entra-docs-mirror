---
layout: Conceptual
title: Configure Keeper Password Manager for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/keeperpasswordmanager-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Keeper Password Manager.
ms.topic: how-to
ms.date: 2026-06-04T00:00:00.0000000Z
locale: en-us
document_id: 21d67f82-ae09-953c-50e5-3804eff71f74
document_version_independent_id: 0541c741-b36c-509b-3956-cb6530511803
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/keeperpasswordmanager-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/keeperpasswordmanager-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/keeperpasswordmanager-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c973485f-d528-9ad9-d33a-1a04842b7bf0
---

# Configure Keeper Password Manager for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Keeper Password Manager with Microsoft Entra ID. When you integrate Keeper Password Manager with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Keeper Password Manager.
- Enable your users to be automatically signed-in to Keeper Password Manager with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Keeper Password Manager is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Keeper Password Manager single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Keeper Password Manager supports SP-initiated SSO.
- Keeper Password Manager supports [**Automated** user provisioning and deprovisioning](keeper-password-manager-digitalvault-provisioning-tutorial) (recommended).
- Keeper Password Manager supports just-in-time user provisioning.

## Add Keeper Password Manager from the gallery

To configure the integration of Keeper Password Manager into Microsoft Entra ID, add the application from the gallery to your list of managed software as a service (SaaS) apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In **Add from the gallery**, type **Keeper Password Manager** in the search box.
4. Select **Keeper Password Manager** from results panel, and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Keeper Password Manager

Configure and test Microsoft Entra SSO with Keeper Password Manager by using a test user called **B.Simon**. For SSO to work, you need to establish a linked relationship between a Microsoft Entra user and the related user in Keeper Password Manager.

To configure and test Microsoft Entra SSO with Keeper Password Manager:

1. Configure Microsoft Entra SSO to enable your users to use this feature.

    1. Create a Microsoft Entra test user to test Microsoft Entra single sign-on with Britta Simon.
    2. Assign the Microsoft Entra test user to enable Britta Simon to use Microsoft Entra single sign-on.
2. Configure Keeper Password Manager SSO to configure the SSO settings on the application side.

    1. Create a Keeper Password Manager test user to have a counterpart of Britta Simon in Keeper Password Manager linked to the Microsoft Entra representation of the user.
3. Test SSO to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Keeper Password Manager** application integration page, find the **Manage** section. Select **single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot of Set up Single Sign-On with SAML, with pencil icon highlighted.](common/edit-urls.png)
5. In the **Basic SAML Configuration** section, perform the following steps:

    a. For **Identifier (Entity ID)**, type a URL using one of the following patterns:

    - For cloud SSO: `https://keepersecurity.com/api/rest/sso/saml/<CLOUD_INSTANCE_ID>`
    - For on-premises SSO: `https://<KEEPER_FQDN>/sso-connect`

    b. For **Reply URL**, type a URL using one of the following patterns:

    - For cloud SSO: `https://keepersecurity.com/api/rest/sso/saml/sso/<CLOUD_INSTANCE_ID>`
    - For on-premises SSO: `https://<KEEPER_FQDN>/sso-connect/saml/sso`

    c. For **Sign on URL**, type a URL using one of the following patterns:

    - For cloud SSO: `https://keepersecurity.com/api/rest/sso/ext_login/<CLOUD_INSTANCE_ID>`
    - For on-premises SSO: `https://<KEEPER_FQDN>/sso-connect/saml/login`

    d. For **Sign out URL**, type a URL using one of the following patterns:

    - For cloud SSO: `https://keepersecurity.com/api/rest/sso/saml/slo/<CLOUD_INSTANCE_ID>`
    - There's no configuration for on-premises SSO.

    Note

    These values aren't real. Update these values with the actual Identifier,Reply URL and Sign on URL. To get these values, contact the [Keeper Password Manager Client support team](https://keepersecurity.com/contact.html). You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. The Keeper Password Manager application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot of User Attributes &amp; Claims.](common/default-attributes.png)
7. In addition, the Keeper Password Manager application expects a few more attributes to be passed back in SAML response. These are shown in the following table. These attributes are also pre-populated, but you can review them per your requirements.

    | Name | Source attribute |
    | --- | --- |
    | First | user.givenname |
    | Last | user.surname |
    | Email | user.mail |
8. On **Set up Single Sign-On with SAML**, in the **SAML Signing Certificate** section, select **Download**. This downloads **Federation Metadata XML** from the options per your requirement, and saves it on your computer.

    ![Screenshot of SAML Signing Certificate with Download highlighted.](common/metadataxml.png)
9. On **Set up Keeper Password Manager**, copy the appropriate URLs, per your requirement.

    ![Screenshot of Set up Keeper Password Manager with URLs highlighted.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Keeper Password Manager SSO

To configure SSO for the app, see the guidelines in the [Keeper support guide](https://docs.keeper.io/sso-connect-cloud/identity-provider-setup/azure-o365-keeper).

### Create a Keeper Password Manager test user

To enable Microsoft Entra users to sign in to Keeper Password Manager, you must provision them. The application supports just-in-time user provisioning, and after authentication users are created in the application automatically. If you want to set up users manually, contact [Keeper support](https://keepersecurity.com/contact.html).

Note

Keeper Password Manager also supports automatic user provisioning, you can find more details [here](keeper-password-manager-digitalvault-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Keeper Password Manager Sign-on URL where you can initiate the login flow.
- Go to Keeper Password Manager Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Keeper Password Manager tile in the My Apps, this option redirects to Keeper Password Manager Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
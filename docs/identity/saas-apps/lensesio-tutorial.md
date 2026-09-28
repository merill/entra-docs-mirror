---
layout: Conceptual
title: Configure Lenses.io for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/lensesio-tutorial
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
description: In this article,  you learn how to configure single sign-on between Microsoft Entra ID and Lenses.io.
ms.topic: how-to
ms.date: 2026-06-04T00:00:00.0000000Z
locale: en-us
document_id: 3880688e-009c-c628-82f5-501ec8932c95
document_version_independent_id: 6b159255-e9c3-d2fa-9427-a2fe68fe8a73
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/lensesio-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/lensesio-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/lensesio-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 51c4ceba-c1c8-457d-0181-ee3597b0b468
---

# Configure Lenses.io for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate the [Lenses.io](https://lenses.io/) DataOps portal with Microsoft Entra ID. After you integrate Lenses.io with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to the Lenses.io portal.
- Enable your users to be automatically signed-in to Lenses with their Microsoft Entra accounts.
- Manage your accounts in one central location: the Azure portal.

Lenses.io is available in the following [national cloud deployments](/en-us/graph/deployments).

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

- An instance of a Lenses portal. You can choose from a number of [deployment options](https://lenses.io/product/deployment/).
- A Lenses.io [license](https://lenses.io/product/pricing/) that supports single sign-on (SSO).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Lenses.io supports service provider (SP) initiated SSO.

## Add Lenses.io from the gallery

To configure the integration of Lenses.io into Microsoft Entra ID, add Lenses.io to your list of managed SaaS apps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, enter **Lenses.io** in the search box.
4. From results panel, select **Lenses.io**, and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Lenses.io

You'll create a test user called *B.Simon* to configure and test Microsoft Entra SSO with your Lenses.io portal. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Lenses.io.

Perform the following steps:

1. Configure Microsoft Entra SSOto enable your users to use this feature.
    1. Create a Microsoft Entra test user and group to test Microsoft Entra SSO with B.Simon.
    2. Assign the Microsoft Entra test user to enable B.Simon to use Microsoft Entra SSO.
2. Configure Lenses.io SSOto configure the SSO settings on the application side.
    1. Create Lenses.io test group permissions to control what B.Simon can access in Lenses.io (authorization).
3. Test SSO to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Azure portal:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Lenses.io** application integration page, find the **Manage** section, and then select **single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot that shows the icon for editing basic SAML configuration.](common/edit-urls.png)
5. In the **Basic SAML Configuration** section, perform the following steps:

    a. **Identifier (Entity ID)**: Enter a URL that has the following pattern: `https://<CUSTOMER_LENSES_BASE_URL>`. An example is `https://lenses.my.company.com`.

    b. **Reply URL**: Enter a URL that has the following pattern: `https://<CUSTOMER_LENSES_BASE_URL>/api/v2/auth/saml/callback?client_name=SAML2Client`. An example is `https://lenses.my.company.com/api/v2/auth/saml/callback?client_name=SAML2Client`.

    c. **Sign on URL**: Enter a URL that has the following pattern: `https://<CUSTOMER_LENSES_BASE_URL>`. An example is `https://lenses.my.company.com`.

    Note

    These values aren't real. Update them with the actual Identifier,Reply URL and Sign on URL of the base URL of your Lenses portal instance. See the Lenses.io SSO documentation for more information.
6. On the **Set up single sign-on with SAML** page, go to the **SAML Signing Certificate** section. Find **Federation Metadata XML**, and then select **Download** to download and save the certificate on your computer.

    ![Screenshot that shows the Certificate download link.](common/metadataxml.png)
7. In the **Set up Lenses.io** section, use the XML file that you downloaded to configure Lenses against your Azure SSO.

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Lenses.io SSO

To configure SSO on the **Lenses.io** portal, install the downloaded **Federation Metadata XML** on your Lenses instance and configure Lenses to enable SSO.

### Create Lenses.io test group permissions

1. To create a group in Lenses, use the **Object ID** of the **LensesUsers** group. This is the ID that you copied in the user creation section.
2. Assign the desired permissions for B.Simon.

For more information, see Azure - Lenses group mapping.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Lenses.io Sign-on URL where you can initiate the login flow.
- Go to Lenses.io Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Lenses.io tile in the My Apps, this option redirects to Lenses.io Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
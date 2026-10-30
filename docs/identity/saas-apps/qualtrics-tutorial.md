---
layout: Conceptual
title: Configure Qualtrics for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/qualtrics-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Qualtrics.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: a19b96f1-9291-73c5-0dbe-b9c7008ba7b4
document_version_independent_id: c08afb2c-705f-ee69-7148-a528f3b4cb20
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/qualtrics-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/qualtrics-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/qualtrics-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: bc713a6f-7816-5b5a-a667-c04dadd67ccd
---

# Configure Qualtrics for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Qualtrics with Microsoft Entra ID. When you integrate Qualtrics with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Qualtrics.
- Enable your users to be automatically signed in to Qualtrics with their Microsoft Entra accounts.
- Manage your accounts in one central location: the Azure portal.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A Qualtrics subscription enabled for single sign-on (SSO).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Qualtrics supports **SP** and **IDP** initiated SSO.
- Qualtrics supports **Just In Time** user provisioning.

## Add Qualtrics from the gallery

To configure the integration of Qualtrics into Microsoft Entra ID, you need to add Qualtrics from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Qualtrics** in the search box.
4. Select **Qualtrics** from results, and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra single sign-on for Qualtrics

Configure and test Microsoft Entra SSO with Qualtrics, by using a test user called **B.Simon**. For SSO to work, you need to establish a linked relationship between a Microsoft Entra user and the related user in Qualtrics.

To configure and test Microsoft Entra SSO with Qualtrics, complete the following building blocks:

1. Configure Microsoft Entra SSOto enable your users to use this feature.
    1. Create a Microsoft Entra test user to test Microsoft Entra single sign-on with B.Simon.
    2. Assign the Microsoft Entra test user to enable B.Simon to use Microsoft Entra single sign-on.
2. Configure Qualtrics SSOto configure the single sign-on settings on the application side.
    1. Create a Qualtrics test user to have a counterpart of B.Simon in Qualtrics, linked to the Microsoft Entra representation of the user.
3. Test SSO to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Qualtrics** application integration page, find the **Manage** section. Select **single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Set up single sign-on with SAML** page, if you want to configure the application in **IDP** initiated mode, enter the values for the following fields:

    a. In the **Identifier** text box, type a URL that uses the following pattern:

    `https://< DATACENTER >.qualtrics.com`

    b. In the **Reply URL** text box, type a URL that uses the following pattern:

    `https://< DATACENTER >.qualtrics.com/login/v1/sso/saml2/default-sp`

    c. In the **Relay State** text box, type a URL that uses the following pattern:

    `https://< brandID >.< DATACENTER >.qualtrics.com`
6. Select **Set additional URLs**, and perform the following step if you want to configure the application in **SP** initiated mode:

    In the **Sign-on URL** textbox, type a URL that uses the following pattern:

    `https://< brandID >.< DATACENTER >.qualtrics.com`

    Note

    These values aren't real. Update these values with the actual Sign-on URL, Identifier, Reply URL, and Relay State. To get these values, contact the [Qualtrics Client support team](https://www.qualtrics.com/support/). You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, select the copy icon to copy **App Federation Metadata Url** and save it on your computer.

    ![The Certificate download link](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Qualtrics SSO

To configure single sign-on on the Qualtrics side, send the copied **App Federation Metadata Url** to the [Qualtrics support team](https://www.qualtrics.com/support/). The support team ensures that the SAML SSO connection is set properly on both sides.

### Create Qualtrics test user

Qualtrics supports just-in-time user provisioning, which is enabled by default. There's no additional action for you to take. If a user doesn't already exist in Qualtrics, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Qualtrics Sign on URL where you can initiate the login flow.
- Go to Qualtrics Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Qualtrics for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Qualtrics tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Qualtrics for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
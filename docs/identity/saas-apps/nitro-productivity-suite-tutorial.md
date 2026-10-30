---
layout: Conceptual
title: Configure Nitro Productivity Suite for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/nitro-productivity-suite-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Nitro Productivity Suite.
ms.topic: how-to
ms.date: 2025-03-03T00:00:00.0000000Z
locale: en-us
document_id: abe1e3e2-6128-8026-2373-24b7e354c19f
document_version_independent_id: 60dc1b58-b7eb-f7cd-df54-e7d073e5b9d1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/nitro-productivity-suite-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/nitro-productivity-suite-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/nitro-productivity-suite-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 6d42a2ad-5f03-8953-9750-18f00137b3fe
---

# Configure Nitro Productivity Suite for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Nitro Productivity Suite with Microsoft Entra ID. When you integrate Nitro Productivity Suite with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Nitro Productivity Suite.
- Enable your users to be automatically signed in to Nitro Productivity Suite with their Microsoft Entra accounts.
- Manage your accounts in one central location: The Microsoft Entra admin center.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A Nitro Productivity Suite [Enterprise subscription](https://www.gonitro.com/pricing).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Nitro Productivity Suite supports **SP** and **IDP** initiated SSO.
- Nitro Productivity Suite supports **Just In Time** user provisioning.

## Add Nitro Productivity Suite from the gallery

To configure the integration of Nitro Productivity Suite into Microsoft Entra ID, you need to add Nitro Productivity Suite from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Nitro Productivity Suite** in the search box.
4. Select **Nitro Productivity Suite** from the results, and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra single sign-on for Nitro Productivity Suite

Configure and test Microsoft Entra SSO with Nitro Productivity Suite, by using a test user called **B.Simon**. For SSO to work, you need to establish a linked relationship between a Microsoft Entra user and the related user in Nitro Productivity Suite.

To configure and test Microsoft Entra SSO with Nitro Productivity Suite, complete the following building blocks:

1. Configure Microsoft Entra SSO to enable your users to use this feature.

    a. Create a Microsoft Entra test user to test Microsoft Entra single sign-on with B.Simon.

    b. Assign the Microsoft Entra test user to enable B.Simon to use Microsoft Entra single sign-on.
2. Create a Nitro Productivity Suite test user to have a counterpart of B.Simon in Nitro Productivity Suite, linked to the Microsoft Entra representation of the user.
3. Test SSO to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Nitro Productivity Suite** application integration page, find the **Manage** section. Select **single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot of Set up Single Sign-On with SAML page, with pencil icon highlighted](common/edit-urls.png)
5. In the **Basic SAML Configuration** section, if you want to configure the application in **IDP** initiated mode, enter the values for the following fields:

    a. In the **Identifier** text box, copy and paste the **SAML Entity ID** field from the [Nitro Admin portal](https://admin.gonitro.com/). It should have the following pattern: `urn:auth0:gonitro-prod:<ENVIRONMENT>`

    b. In the **Reply URL** text box, copy and paste the **ACS URL** field from the [Nitro Admin portal](https://admin.gonitro.com/). It should have the following pattern: `https://gonitro-prod.eu.auth0.com/login/callback?connection=<ENVIRONMENT>`
6. Select **Set additional URLs**, and perform the following step if you want to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type the URL: `https://sso.gonitro.com/login`
7. Select **Save**.
8. In the **SAML Signing Certificate** section, find **Certificate (Base64)**. Select **Download** to download the certificate and save it on your computer.

    ![Screenshot of SAML Signing Certificate section, with Download link highlighted](common/certificatebase64.png)
9. In the **Set up Nitro Productivity Suite** section, select the copy icon beside **Login URL**.

    ![Screenshot of Set up Nitro Productivity Suite section, with URLs and copy icons highlighted](common/copy-configuration-urls.png)
10. In the [Nitro Admin portal](https://admin.gonitro.com/), on the **Enterprise Settings** page, find the **Single Sign-On** section. Select **Setup SAML SSO**.

    a. Paste the **Login URL** from step 9 into the **Sign In URL** field.

    b. Upload the **Certificate (Base64)** step 8 in the **X509 Signing Certificate** field.

    c. Select **Submit**.

    d. Select **Enable Single Sign-On**.
11. The Nitro Productivity Suite application expects the SAML assertions to be in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot of default attributes](common/default-attributes.png)
12. In addition to the preceding attributes, the Nitro Productivity Suite application expects a few more attributes to be passed back in the SAML response. These attributes are pre-populated, but you can review them per your requirements.

    | Name | Source attribute |
    | --- | --- |
    | employeeNumber | user.objectid |

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

### Create a Nitro Productivity Suite test user

Nitro Productivity Suite supports just-in-time user provisioning, which is enabled by default. There's no additional action for you to take. If a user doesn't already exist in Nitro Productivity Suite, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

### SP initiated:

1. Select **Test this application**, this option redirects to Nitro Productivity Suite Sign on URL where you can initiate the login flow.
2. Go to Nitro Productivity Suite Sign-on URL directly and initiate the login flow from there.

### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Nitro Productivity Suite for which you set up the SSO

You can also use Microsoft Access Panel to test the application in any mode. When you select the Nitro Productivity Suite tile in the Access Panel, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Nitro Productivity Suite for which you set up the SSO. For more information about the Access Panel, see [Introduction to the Access Panel](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
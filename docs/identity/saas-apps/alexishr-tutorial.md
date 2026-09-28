---
layout: Conceptual
title: Configure AlexisHR for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/alexishr-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and AlexisHR.
ms.topic: how-to
ms.date: 2026-06-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 2a9c5202-e122-0610-85d8-2cfdd5abcb75
document_version_independent_id: 38f7d96a-bf39-567a-f106-70f5718195ae
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/alexishr-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/alexishr-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/alexishr-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 8acf7f7f-8d49-a855-08ca-6ae794a707dd
---

# Configure AlexisHR for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate AlexisHR with Microsoft Entra ID. When you integrate AlexisHR with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to AlexisHR.
- Enable your users to be automatically signed-in to AlexisHR with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- AlexisHR single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test SAML SSO between Microsoft Entra ID and AlexisHR in a test environment.

- AlexisHR supports **IdP-initiated** SSO.
- You first create a **basic (mock) SAML configuration** in Microsoft Entra ID to obtain the Login URL and certificate, then configure SSO in AlexisHR, and finally return to Microsoft Entra ID to update the Identifier and Reply URL with the real values from AlexisHR.

## Add AlexisHR from the gallery

To configure the integration of AlexisHR into Microsoft Entra ID, you need to add AlexisHR from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Microsoft Entra ID** &gt; **Enterprise applications** &gt; **New application**.
3. In the **Add from the gallery** section, type **AlexisHR** in the search box.
4. Select **AlexisHR** from the results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for AlexisHR

Configure and test Microsoft Entra SSO with AlexisHR using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in AlexisHR.

To configure and test Microsoft Entra SSO with AlexisHR, perform the following steps:

1. **Configure Microsoft Entra SSO** – to enable your users to use this feature.
2. **Create and assign a Microsoft Entra test user** – to validate single sign-on.
3. **Configure AlexisHR SSO** – to configure single sign-on in AlexisHR.
4. **Update Microsoft Entra SSO with real values** – to replace the placeholder values with real ones.
5. **Test SSO** – to verify whether the configuration works.

## Configure Microsoft Entra SSO (initial mock setup)

Follow these steps to enable Microsoft Entra SSO with temporary values.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Microsoft Entra ID** &gt; **Enterprise applications** &gt; **AlexisHR** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. In the **Basic SAML Configuration** section, enter **placeholder values** for the first setup:

    - **Identifier (Entity ID)**: `urn:auth0:alexishr:<YOUR_CONNECTION_NAME>`
    - **Reply URL (Assertion Consumer Service URL)**: `https://auth.alexishr.com/login/callback?connection=<YOUR_CONNECTION_NAME>`

    Example:

    - Company: `acme`
    - Date: `20250901`
    - Identifier: `urn:auth0:alexishr:acme-20250901`
    - Reply URL: `https://auth.alexishr.com/login/callback?connection=acme-20250901`

    Note

    These values are placeholders only. After you configure AlexisHR SSO, you'll return to this page and replace them with the real **Audience URI** and **Assertion Consumer Service URL** values provided by AlexisHR.
6. In the **Attributes & Claims** section, set **Name ID format** to **Email address** and ensure the **Name ID** value is **user.email**.
7. In the **SAML Signing Certificate** section, select **Certificate (Base64)** and **Download**. This file has a .cer extension, is PEM-encoded, and is needed later during the AlexisHR setup.
8. In the **Set up AlexisHR** section, copy the **Login URL** and **Logout URL** values. These values will also be needed in the AlexisHR setup.

Important

Testing will only work **after** you complete the AlexisHR setup and update the Identifier and Reply URL in Microsoft Entra ID with the real values.

## Create and assign a Microsoft Entra test user

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure AlexisHR SSO

1. Log in to your AlexisHR company site as an Owner.
2. Go to **Settings** &gt; **SAML Single sign-on** and select **New identity provider**.
3. In the **New identity provider**section:
    - **Identity provider SSO URL**: paste the **Login URL** from Microsoft Entra ID.
    - **Identity provider sign out URL**: paste the **Logout URL** from Microsoft Entra ID.
    - **Public x509 certificate**: open the downloaded **Certificate (Base64)** file in a text editor and paste the **entire PEM content** (including the `-----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` lines) without modifying any line breaks.
4. Select **Create identity provider**.
5. After creating the identity provider, AlexisHR provides:
    - **Audience URI**
    - **Assertion Consumer Service URL** These values will be used to update Microsoft Entra ID.

## Update Microsoft Entra SSO with real values

1. Return to **Microsoft Entra admin center** &gt; **Enterprise applications** &gt; **AlexisHR** &gt; **Single sign-on**.
2. Edit the **Basic SAML Configuration** section.
3. Replace the temporary placeholder values with:
    - **Identifier (Entity ID)**: paste **Audience URI** from AlexisHR.
    - **Reply URL (Assertion Consumer Service URL)**: paste **Assertion Consumer Service URL** from AlexisHR.
4. Save the changes.

## Create AlexisHR test user

1. Work with [AlexisHR support team](mailto:support@alexishr.com) to add a test user (for example, Britta Simon) in the AlexisHR platform.
2. Ensure the user is created and activated before testing single sign-on.

## Test SSO

1. In the **Microsoft Entra admin center**, go to the **AlexisHR** app and select **Test this application**. You should be automatically signed in to AlexisHR.
2. Alternatively, open [My Apps](https://myapps.microsoft.com), select the **AlexisHR** tile, and confirm that you are automatically signed in. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
---
layout: Conceptual
title: Configure Trelica for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/trelica-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Trelica.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: a60b1478-96f0-08ab-ae2a-7678b24a5313
document_version_independent_id: 2739656e-4b77-b3a5-6216-c833825ae58b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/trelica-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/trelica-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/trelica-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 1feaac9a-7186-eae9-d0d6-c65c2ffd392c
---

# Configure Trelica for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Trelica with Microsoft Entra ID. When you integrate Trelica with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Trelica.
- Enable your users to be automatically signed in to Trelica with their Microsoft Entra accounts.
- Manage your accounts in one central location: the Azure portal.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A Trelica subscription with single sign-on (SSO) enabled.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Trelica supports IDP-initiated SSO.
- Trelica supports just-in-time user provisioning.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Trelica from the gallery

To configure the integration of Trelica into Microsoft Entra ID, you need to add Trelica from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, enter **Trelica** in the search box.
4. Select **Trelica** from the search results, and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Trelica

Configure and test Microsoft Entra SSO with Trelica by using a test user called **B.Simon**. For SSO to work, you must establish a linked relationship between a Microsoft Entra user and the related user in Trelica.

To configure and test Microsoft Entra SSO with Trelica, perform the following steps:

1. **Configure Microsoft Entra SSO**to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Trelica SSO**to configure the single sign-on settings on the application side.
    1. **Create a Trelica test user** to have a counterpart of B.Simon in Trelica. This counterpart is linked to the Microsoft Entra representation of the user.
3. **Test SSO** to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Azure portal:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Trelica** application integration page, go to the **Manage** section. Select **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![The Set up Single Sign-On with SAML page, with the pencil icon for Basic SAML Configuration highlighted](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    1. In the **Identifier** box, type the URL: `https://app.trelica.com`.
    2. In the **Reply URL** box, type a URL using the following pattern: `https://app.trelica.com/Id/Saml2/<CUSTOM_IDENTIFIER>/Acs`.

    Note

    The Reply URL value isn't real. Update this value with the actual Reply URL (also known as the ACS). You can find this by logging in to Trelica and going to the [SAML identity providers configuration page](https://app.trelica.com/Admin/Profile/SAML) (Admin &gt; Account &gt; SAML). Select the copy button next to the **Assertion Consumer Service (ACS) URL** to put this onto the clipboard, ready for pasting into the **Reply URL** text box in Microsoft Entra ID. Read the [Trelica help documentation](https://docs.trelica.com/admin/saml/azure-ad) or contact the [Trelica Client support team](mailto:support@trelica.com) if you have questions.
6. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select the copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![The SAML Signing Certificate section, with the copy button highlighted next to App Federation Metadata URL](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Trelica SSO

To configure single sign-on on the **Trelica** side, go to the [SAML identity providers configuration page](https://app.trelica.com/Admin/Profile/SAML) (Admin &gt; Account &gt; SAML). Select the **New** button. Enter **Microsoft Entra ID** as the Name and choose **Metadata from url** for the Metadata type. Paste the **App Federation Metadata Url** you took from Microsoft Entra ID into the **Metadata url** field in Trelica.

Read the [Trelica help documentation](https://docs.trelica.com/admin/saml/azure-ad) or contact the [Trelica Client support team](mailto:support@trelica.com) if you have questions.

### Create a Trelica test user

Trelica supports just-in-time user provisioning, which is enabled by default. There's no action for you to take in this section. If a user doesn't already exist in Trelica, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the Trelica for which you set up the SSO.
- You can use Microsoft My Apps. When you select the Trelica tile in the My Apps, you should be automatically signed in to the Trelica for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
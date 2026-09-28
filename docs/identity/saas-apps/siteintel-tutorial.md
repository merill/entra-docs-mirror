---
layout: Conceptual
title: Configure SiteIntel for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/siteintel-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and SiteIntel.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 2fd7d78b-3e2d-e453-89d9-2cac340bf729
document_version_independent_id: bdc48870-2ff6-6ee8-7811-f83f17e4dfa7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/siteintel-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/siteintel-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/siteintel-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 42b0e064-1884-1557-0a5e-2d1e6e5202fb
---

# Configure SiteIntel for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate SiteIntel with Microsoft Entra ID. When you integrate SiteIntel with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to SiteIntel.
- Enable your users to be automatically signed in to SiteIntel with their Microsoft Entra accounts.
- Manage your accounts in one central location, the Azure portal.

To learn more about software as a service (SaaS) app integration with Microsoft Entra ID, see [What is application access and single sign-on with Microsoft Entra ID?](../enterprise-apps/what-is-single-sign-on).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- SiteIntel single sign-on (SSO)-enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- SiteIntel supports SP-initiated and IdP-initiated SSO.
- After you configure SiteIntel, you can enforce session control, which protects exfiltration and infiltration of your organization’s sensitive data in real time. Session control extends from Conditional Access. [Learn how to enforce session control with Microsoft Defender for Cloud Apps](/en-us/cloud-app-security/proxy-deployment-any-app).

## Add SiteIntel from the gallery

To configure the integration of SiteIntel into Microsoft Entra ID, you need to add SiteIntel from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** box, enter **SiteIntel**.
4. In the results list, select **SiteIntel**, and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra single sign-on for SiteIntel

Configure and test Microsoft Entra SSO with SiteIntel by using a test user called *B.Simon*. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in SiteIntel.

To configure and test Microsoft Entra SSO with SiteIntel, complete the following building blocks:

1. **Configure Microsoft Entra SSO** to enable your users to use this feature.

    a. **Create a Microsoft Entra test user** to test Microsoft Entra single sign-on with user B.Simon.

    b. **Assign the Microsoft Entra test user** to enable user B.Simon to use Microsoft Entra single sign-on.
2. **Configure SiteIntel SSO** to configure the single sign-on settings on the application side.

    - **Create a SiteIntel test user** to have a counterpart of user B.Simon in SiteIntel that's linked to the Microsoft Entra representation of the user.
3. **Test SSO** to verify that the configuration works.

## Configure Microsoft Entra SSO

To enable Microsoft Entra SSO in the Azure portal, do the following:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **SiteIntel** application integration page, go to the **Manage** section, and then select **single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, next to **Basic SAML Configuration**, select **Edit** (pen icon).

    ![Screenshot of &quot;Set up Single-Sign-On with SAML&quot; pane](common/edit-urls.png)
5. To configure the application in IdP-initiated mode, in the **Basic SAML Configuration** section, do the following:

    a. In the **Identifier** box, type a URL in the following format: `urn:amazon:cognito:sp:<REGION>_<USERPOOLID>`

    b. In the **Reply URL** box, type a URL in the following format: `https://<CLIENT>.auth.siteintel.com/saml2/idpresponse`

    c. In the **Relay State** box, type a URL in the following format: `https://<CLIENT>.siteintel.com`
6. To configure the application in SP-initiated mode, select **Set additional URLs**, and then do the following:

    - In the **Sign-on URL** box, type a URL in the following format: `https://<CLIENT>.siteintel.com`

    Note

    These values aren't real. Update them with the actual Identifier, Reply URL, Sign-on URL, and Relay State. To get these values, contact [SiteIntel Client support team](mailto:support@intalytics.com). You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, select the **Copy** button to copy the URL in the **App Federation Metadata Url** box.

    ![Screenshot of the &quot;App Federation Metadata URL&quot; Copy button](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure SiteIntel SSO

To configure single sign-on on the SiteIntel side, send the URL you copied from the **App Federation Metadata Url** box to the [SiteIntel support team](mailto:support@intalytics.com). They set this value to establish the SAML SSO connection properly on both sides.

### Create a SiteIntel test user

In this section, you create a user called *Britta Simon* in SiteIntel. Work with [SiteIntel support team](mailto:support@intalytics.com) to add the users in the SiteIntel platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration by using the Access Panel.

When you select the **SiteIntel** tile in the Access Panel, you should be automatically signed in to the SiteIntel for which you set up SSO. For more information about the Access Panel, see [Introduction to the Access Panel](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
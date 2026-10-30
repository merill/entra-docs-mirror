---
layout: Conceptual
title: Configure Smart Global Governance for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/smart-global-governance-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Smart Global Governance.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: e0da3333-4886-ae4e-df15-647349ad3b1a
document_version_independent_id: 94c992ec-bfde-82de-16f9-2f5e5a73785e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/smart-global-governance-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/smart-global-governance-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/smart-global-governance-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: a15a9ae9-c866-625b-6fda-80944f7a0f09
---

# Configure Smart Global Governance for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Smart Global Governance with Microsoft Entra ID. When you integrate Smart Global Governance with Microsoft Entra ID, you can:

- Use Microsoft Entra ID to control who can access Smart Global Governance.
- Enable your users to be automatically signed in to Smart Global Governance with their Microsoft Entra accounts.
- Manage your accounts in one central location: the Azure portal.

To learn more about SaaS app integration with Microsoft Entra ID, see [Single sign-on to applications in Microsoft Entra ID](../enterprise-apps/what-is-single-sign-on).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A Smart Global Governance subscription with single sign-on (SSO) enabled.

## Article description

In this article, you configure and test Microsoft Entra SSO in a test environment.

Smart Global Governance supports SP-initiated and IDP-initiated SSO.

After you configure Smart Global Governance, you can enforce session control, which protects exfiltration and infiltration of your organization's sensitive data in real time. Session controls extend from Conditional Access. [Learn how to enforce session control with Microsoft Defender for Cloud Apps](/en-us/cloud-app-security/proxy-deployment-any-app).

## Add Smart Global Governance from the gallery

To configure the integration of Smart Global Governance into Microsoft Entra ID, you need to add Smart Global Governance from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, enter **Smart Global Governance** in the search box.
4. Select **Smart Global Governance** in the results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Smart Global Governance

You'll configure and test Microsoft Entra SSO with Smart Global Governance by using a test user named B.Simon. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the corresponding user in Smart Global Governance.

To configure and test Microsoft Entra SSO with Smart Global Governance, you take these high-level steps:

1. **Configure Microsoft Entra SSO**to enable your users to use the feature.
    1. **Create a Microsoft Entra test user** to test Microsoft Entra single sign-on.
    2. **Grant access to the test user** to enable the user to use Microsoft Entra single sign-on.
2. **Configure Smart Global Governance SSO**on the application side.
    1. **Create a Smart Global Governance test user** as a counterpart to the Microsoft Entra representation of the user.
3. **Test SSO** to verify that the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Azure portal:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Smart Global Governance** application integration page, in the **Manage** section, select **single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil button for **Basic SAML Configuration** to edit the settings:

    ![Pencil button for Basic SAML Configuration](common/edit-urls.png)
5. In the **Basic SAML Configuration** section, if you want to configure the application in IDP-initiated mode, take the following steps.

    a. In the **Identifier** box, enter one of these URLs:

    - `https://eu-fr-south.console.smartglobalprivacy.com/platform/authentication-saml2/metadata`
    - `https://eu-fr-south.console.smartglobalprivacy.com/dpo/authentication-saml2/metadata`

    b. In the **Reply URL** box, enter one of these URLs:

    - `https://eu-fr-south.console.smartglobalprivacy.com/platform/authentication-saml2/acs`
    - `https://eu-fr-south.console.smartglobalprivacy.com/dpo/authentication-saml2/acs`
6. If you want to configure the application in SP-initiated mode, select **Set additional URLs** and complete the following step.

    - In the **Sign-on URL** box, enter one of these URLs:
    - `https://eu-fr-south.console.smartglobalprivacy.com/dpo`
    - `https://eu-fr-south.console.smartglobalprivacy.com/platform`
7. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select the **Download** link for **Certificate (Raw)** to download the certificate and save it on your computer:

    ![Certificate download link](common/certificateraw.png)
8. In the **Set up Smart Global Governance** section, copy the appropriate URL or URLs, based on your requirements:

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create a Microsoft Entra test user

In this section, you create a test user called B.Simon.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **New user** &gt; **Create new user**, at the top of the screen.
4. In the **User**properties, follow these steps:
    1. In the **Display name** field, enter `B.Simon`.
    2. In the **User principal name** field, enter the username@companydomain.extension. For example, `B.Simon@contoso.com`.
    3. Select the **Show password** check box, and then write down the value that's displayed in the **Password** box.
    4. Select **Review + create**.
5. Select **Create**.

### Grant access to the test user

In this section, you enable B.Simon to use single sign-on by granting that user access to Smart Global Governance.

1. Browse to **Entra ID** &gt; **Enterprise apps**.
2. In the applications list, select **Smart Global Governance**.
3. In the app's overview page, in the **Manage** section, select **Users and groups**:

    ![Select Users and groups](common/users-groups-blade.png)
4. Select **Add user**, and then select **Users and groups** in the **Add Assignment** dialog box:

    ![Select Add user](common/add-assign-user.png)
5. In the **Users and groups** dialog box, select **B.Simon** in the **Users** list, and then select the **Select** button at the bottom of the screen.
6. If you're expecting any role value in the SAML assertion, in the **Select Role** dialog box, select the appropriate role for the user from the list and then select the **Select** button at the bottom of the screen.
7. In the **Add Assignment** dialog box, select **Assign**.

## Configure Smart Global Governance SSO

To configure single sign-on on the Smart Global Governance side, you need to send the downloaded raw certificate and the appropriate URLs that you copied from Azure portal to the [Smart Global Governance support team](mailto:support.tech@smartglobal.com). They configure the SAML SSO connection to be correct on both sides.

### Create a Smart Global Governance test user

Work with the [Smart Global Governance support team](mailto:support.tech@smartglobal.com) to add a user named B.Simon in Smart Global Governance. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra SSO configuration by using Access Panel.

When you select the Smart Global Governance tile in Access Panel, you should be automatically signed in to the Smart Global Governance instance for which you set up SSO. For more information about Access Panel, see [Introduction to Access Panel](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
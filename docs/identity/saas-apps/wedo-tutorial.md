---
layout: Conceptual
title: Configure WEDO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/wedo-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and WEDO.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: aa8805be-4386-dfea-7045-3568e45aa2d0
document_version_independent_id: d7948e0e-4d89-5ca1-5768-9b5619237b03
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/wedo-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/wedo-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/wedo-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 5f87b2bd-2dfe-8aff-88ec-26157d8534d1
---

# Configure WEDO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate WEDO with Microsoft Entra ID. When you integrate WEDO with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to WEDO.
- Enable your users to be automatically signed-in to WEDO with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- WEDO single sign-on (SSO) enabled subscription. Please contact [WEDO Client support team](mailto:info@wedo.swiss) to get a SSO subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- WEDO supports **SP and IDP** initiated SSO.
- WEDO supports [Automated user provisioning](wedo-provisioning-tutorial).

## Add WEDO from the gallery

To configure the integration of WEDO into Microsoft Entra ID, you need to add WEDO from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **WEDO** in the search box.
4. Select **WEDO** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for WEDO

Configure and test Microsoft Entra SSO with WEDO using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in WEDO.

To configure and test Microsoft Entra SSO with WEDO, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure WEDO SSO**- to configure the single sign-on settings on application side.
    1. **Create WEDO test user** - to have a counterpart of B.Simon in WEDO that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **WEDO** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.wedo.swiss/sp/acs`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.wedo.swiss/sp/acs`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.wedo.swiss/`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [WEDO Client support team](mailto:info@wedo.swiss) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. WEDO application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    | Name | Source Attribute |
    | --- | --- |
    | email | user.email |
    | firstName | user.firstName |
    | lastName | user.lastName |
    | userName | user.userName |
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
9. On the **Set up WEDO** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure WEDO SSO

Follow these steps to enable Microsoft Entra SSO in WEDO.

1. Log in [WEDO](https://login.wedo.swiss/). You need to have **administrator role**.
2. In the Profile settings, select the menu **Authentication** in the section **Network settings**.
3. On the **SAML Authentication** page, perform the following steps:

    ![SAML Authentication link](media/wedo-tutorial/network-security-authentification.png)

    a. Enable **SAML Authentication**.

    b. Select the **Identity Provider metadata (XML)** tab.

    c. Open the downloaded **Federation Metadata XML** from Azure portal into Notepad and copy the content of metadata XML and paste it into **X.509 Certificate** textbox.

    d. Select **Save**.

### Create WEDO test user

In this section, you create a test user in WEDO called Bob Simon. Information must matches from **Create a Microsoft Entra test user**.

1. From the Profile setting in WEDO, select **Users** from **Network settings** section.
2. Select **Add user**.
3. In the Add user pop-up, fill the user's information

    a. First name `B`.

    b. Last name `Simon`.

    c. Enter the email `username@companydomain.extension`. For example, `B.Simon@contoso.com`. It's mandatory to have email with the same domain as your company short name.

    d. User type `User`.

    e. Select **Create user**.

    f. In the **Select teams** page, select **Save**.

    g. In the **Invite user** page, select **Yes**.
4. Validate the user using the link you received by email

Note

If you want to create a fake user (email above doesn't exist in your network), contact [our support](mailto:info@wedo.swiss) to validate the user\*.

Note

WEDO also supports automatic user provisioning, you can find more details [here](wedo-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with the following options.

#### SP initiated:

- Select **Test this application** in Azure portal. this option redirects to WEDO Sign on URL where you can initiate the login flow.
- Go to WEDO Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application** and you should be automatically signed in to the WEDO for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the WEDO tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the WEDO for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
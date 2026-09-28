---
layout: Conceptual
title: Configure GitHub Enterprise Server for Single Sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/github-enterprise-server-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and GitHub Enterprise Server.
ms.topic: how-to
ms.date: 2026-02-13T00:00:00.0000000Z
locale: en-us
document_id: 5896feb4-c3f7-48e0-3a28-6c6d806ac243
document_version_independent_id: 5896feb4-c3f7-48e0-3a28-6c6d806ac243
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/github-enterprise-server-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/github-enterprise-server-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/github-enterprise-server-tutorial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: b9bc2815-bb07-9d70-1cf3-72ea814e8991
---

# Configure GitHub Enterprise Server for Single Sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate GitHub Enterprise Server with Microsoft Entra ID. When you integrate GitHub Enterprise Server with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to GitHub Enterprise Server.
- Enable your users to be automatically signed-in to GitHub Enterprise Server with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- GitHub Enterprise Server, ready for [initialization](https://docs.github.com/enterprise-server/admin/overview/about-github-enterprise-server).
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- GitHub Enterprise Server supports **SP** and **IDP** initiated SSO.
- GitHub Enterprise Server supports **Just In Time** user provisioning.
- GitHub Enterprise Server supports [Automated user provisioning](github-enterprise-server-provisioning-tutorial).

Note

The GitHub Enterprise Server application currently doesn't support SCIM provisioning in government cloud platforms. This limitation is due to GitHub Enterprise Server requiring the `User-Agent` header, which isn't included in provisioning requests sent from government cloud environments.

## Add GitHub Enterprise Server from the gallery

To configure the integration of GitHub Enterprise Server into Microsoft Entra ID, you need to add GitHub Enterprise Server from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **GitHub Enterprise Server** in the search box.
4. Select **GitHub Enterprise Server** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for GitHub Enterprise Server

Configure and test Microsoft Entra SSO with GitHub Enterprise Server using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in GitHub Enterprise Server.

To configure and test Microsoft Entra SSO with GitHub Enterprise Server, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure GitHub Enterprise Server SSO**- to configure the single sign-on settings on application side.
    1. **Create GitHub Enterprise Server test user** - to have a counterpart of B.Simon in GitHub Enterprise Server that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **GitHub Enterprise Server** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic S A M L Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<YOUR-GITHUB-ENTERPRISE-SERVER-HOSTNAME>`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<YOUR-GITHUB-ENTERPRISE-SERVER-HOSTNAME>/saml/consume`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign on URL** text box, type a URL using the following pattern: `https://<YOUR-GITHUB-ENTERPRISE-SERVER-HOSTNAME>/sso`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign on URL. Contact [GitHub Enterprise Server Client support team](mailto:support@github.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. GitHub Enterprise Server application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows the image of Enterprise Server application.](common/default-attributes.png)
8. Edit **User Attributes & Claims**.
9. Select **Add new claim** and enter the name as `administrator` in the textbox (the `administrator` value is case-sensitive).
10. Expand **Claim conditions** and select **Members** from **User type**.
11. Select **Select groups** and search for the **Group** you want to include this claim, where its members should be administrators for GHES.
12. Select **Attribute** for **Source** and enter `true` (without quotes) for the **Value**.
13. Select **Save**.

    ![Screenshot shows to manage claim for attributes.](media/github-ae-tutorial/administrator.png)
14. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
15. On the **Set up GitHub Enterprise Server** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy appropriate configuration U R L.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure GitHub Enterprise Server SSO

To configure SSO on GitHub Enterprise Server side, you need to follow the instructions mentioned [here](https://docs.github.com/enterprise-server/admin/managing-iam/using-saml-for-enterprise-iam/configuring-saml-single-sign-on-for-your-enterprise).

### Create GitHub Enterprise Server test user

In this section, a user called B.Simon is created in GitHub Enterprise Server. GitHub Enterprise Server supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in GitHub Enterprise Server, a new one is created after authentication.

GitHub Enterprise Server also supports automatic user provisioning. You can find more details [here](github-enterprise-server-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to GitHub Enterprise Server Sign-on URL where you can initiate the login flow.
- Go to GitHub Enterprise Server Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the GitHub Enterprise Server for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the GitHub Enterprise Server tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the GitHub Enterprise Server for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
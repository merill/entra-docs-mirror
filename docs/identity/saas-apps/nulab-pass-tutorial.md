---
layout: Conceptual
title: Configure Nulab Pass (Backlog and Cacoo) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/nulab-pass-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Nulab Pass (Backlog and Cacoo).
ms.topic: how-to
ms.date: 2024-07-01T00:00:00.0000000Z
locale: en-us
document_id: 214e8d7f-d33b-829c-1805-e843a99ff3d1
document_version_independent_id: 67b8d9e5-3ac8-2544-19b7-ed5517a37215
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/nulab-pass-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/nulab-pass-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/nulab-pass-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 87668fb9-e815-3c7b-a413-b6ec25a7787f
---

# Configure Nulab Pass (Backlog and Cacoo) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Nulab Pass (Backlog and Cacoo) with Microsoft Entra ID. By integrating, you can:

- Control in Microsoft Entra ID who has access to Nulab Pass in Microsoft Entra ID.
- Enable users to be automatically signed in to Nulab Pass with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Nulab Pass SSO-enabled subscription.

## Scenario description

In this article, you’ll configure and test Microsoft Entra SSO in a test environment. Nulab Pass supports both **SP and IDP**-initiated SSO.

## Add Nulab Pass from the gallery

To configure the integration of Nulab Pass into Microsoft Entra ID, add Nulab Pass from the gallery to your list of managed SaaS apps.

1. Go to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
2. In the **Add from the gallery** section, type **Nulab Pass** in the search box.
3. Select **Nulab Pass** from results panel and add the app.
4. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Nulab Pass

Configure and test Microsoft Entra SSO with Nulab Pass using a test user called B.Simon. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Nulab Pass.

To configure and test Microsoft Entra SSO with Nulab Pass:

1. **Configure Microsoft Entra SSO**to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** to test Microsoft Entra SSO with B.Simon.
    2. **Assign the Microsoft Entra test user** to enable B.Simon to use Microsoft Entra SSO.
2. **Configure Nulab Pass SSO**to configure the SSO settings on the application side.
    1. **Create Nulab Pass test user** to have a counterpart of B.Simon in Nulab Pass that’s linked to the Microsoft Entra representation of user.
3. **Test SSO** to verify whether the configuration works.

## Configure Microsoft Entra SSO

To enable Microsoft Entra SSO:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Go to **Entra ID** &gt; **Enterprise apps** &gt; **Nulab Pass (Backlog and Cacoo)** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. In the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://apps.nulab.com/signin/spaces/<Space_Key>/saml`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://apps.nulab.com/signin/spaces/<Space_Key>/saml/callback`
6. Perform the following step to configure the application in **SP** initiated mode:

    In the **Sign on URL** text box, type the URL: `https://apps.nulab.com/signin`

    Note

    These values aren't real and should be updated with the actual Identifier, Reply URL, and Sign on URL found in your Nulab Pass organization settings. In your organization settings:

    1. Select **Single Sign-On** from the menu on the left.
    2. Press the **Manage** button to display the **Manage SAML authentication** dialog.
    3. Copy **SP Entity ID** and **SP Endpoint URL (ACS)** values and paste in the Entra side configuration.
    4. For more information, please refer [how to set up SAML authentication](https://support.nulab.com/hc/en-us/articles/6478805477401) documentation.
7. Your Nulab Pass application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows an example for this. The default value of **Unique User Identifier** is **user.userprincipalname**, but Nulab Pass expects this to be mapped with the user's email. Use the **user.mail** attribute from the list or the appropriate attribute value based on your organization configuration.

    ![image](common/default-attributes.png)
8. On the **Set up single sign-on with SAML** page in the **SAML Signing Certificate** section, you find the **Certificate (Base64)**. Select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
9. In the **Set up Nulab Pass** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Nulab Pass SSO

You must configure **[Domain authentication](https://support.nulab.com/hc/en-us/articles/6558108028825)** before configure SSO.

To configure SSO in **Nulab Pass**, set the **Certificate (Base64)** and URLs from the application configuration to ensure that the SSO connection is set on both sides. To do this:

1. Go to your Nulab Pass organization settings.
2. Select **Single Sign-On** from the menu on the left.
3. Press the **Manage** button to display the **Manage SAML authentication** dialog.
4. Enter the following:
    - IdP Entity ID
    - IdP Endpoint URL
    - X.509 Certificate (Base64)

Please refer [how to set up SAML authentication](https://support.nulab.com/hc/en-us/articles/6478805477401) documentation for more details.

### Create Nulab Pass test user

Next, you’ll create a user called `Britta Simon` in Nulab Pass by [adding a Managed Account](https://support.nulab.com/hc/en-us/articles/6480291067801). Users must be created and activated before you use SSO.

## Test SSO

Now, you’ll test your Microsoft Entra SSO configuration using one of the following options:

#### SP initiated:

- Select **Test this application** to be redirected to Nulab Pass to sign in.
- Or, go to the Nulab Pass sign in page directly and initiate the flow from there.

#### IDP initiated:

- Select **Test this application** to be automatically signed in to SSO-enabled Nulab Pass.

You can also use Microsoft My Apps to test the application in any mode. When you select the Nulab Pass tile in My Apps, you’ll be redirected to the application sign on page for initiating the login flow if it was configured in SP mode. If configured in IDP mode, you’ll be automatically signed in to SSO-enabled Nulab Pass. [Learn more about My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
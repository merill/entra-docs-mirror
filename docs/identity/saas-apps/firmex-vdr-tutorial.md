---
layout: Conceptual
title: Configure Firmex VDR for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/firmex-vdr-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Firmex VDR.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 68c9a4aa-49aa-2427-7047-17de249cc0dc
document_version_independent_id: 47eaa817-12f6-8477-8a03-7b626dcae080
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/firmex-vdr-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/firmex-vdr-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/firmex-vdr-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: fd8dd2ae-ef24-5c7e-10dc-7bedfcca82eb
---

# Configure Firmex VDR for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Firmex VDR with Microsoft Entra ID. When you integrate Firmex VDR with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Firmex VDR.
- Enable your users to be automatically signed-in to Firmex VDR with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Firmex VDR single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Firmex VDR supports **SP and IDP** initiated SSO.

## Add Firmex VDR from the gallery

To configure the integration of Firmex VDR into Microsoft Entra ID, you need to add Firmex VDR from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Firmex VDR** in the search box.
4. Select **Firmex VDR** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Firmex VDR

Configure and test Microsoft Entra SSO with Firmex VDR using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Firmex VDR.

To configure and test Microsoft Entra SSO with Firmex VDR, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Firmex VDR SSO**- to configure the single sign-on settings on application side.
    1. **Create Firmex VDR test user** - to have a counterpart of B.Simon in Firmex VDR that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Firmex VDR** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set-up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, the user doesn't have to perform any step as the app is already pre-integrated with Azure.
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type the URL: `https://login.firmex.com`
7. Select **Save**.
8. Firmex VDR application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
9. In addition to above, Firmex VDR application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | email | user.mail |
10. On the **Set-up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
11. On the **Set-up Firmex VDR** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Firmex VDR SSO

### Before you get started

#### What you’ll need

- An active Firmex subscription.
- Microsoft Entra ID as your SSO service.
- Your IT administrator to configure SSO.
- Once SSO is enabled, all of your company’s users must log in to Firmex using SSO, and not using a login/password.

#### How long will this take?

Implementing SSO takes a few minutes. There's virtually no downtime between Firmex Support enabling SSO for your site, and your company’s users authenticating using SSO. Just follow the steps below.

### Step 1 - Identify your company’s domains

Identify the domains with which your company’s users are logging in.

For example:

- @firmex.com.
- @firmex.ca.

### Step 2 - Contact Firmex Support with your domains

Email [Firmex Support Team](mailto:support@firmex.com) or call 1888 688 4042 x.11 to speak to Firmex Support. Pass along your domain information. Firmex Support will add the domains to your VDR as **claimed domains**. Your admin must now configure SSO.

Warning: Until your site admin configures the claimed domains, your company’s users aren't able to log in to the VDR. Non-company users (that is, guest users) can still log in using their email/password. Configuration should take a few minutes.

### Step 3 - Configure the claimed domains

1. Log in to Firmex as a Site Administrator.
2. From the top-left corner, select your company logo.
3. Select the **SSO** tab. Then select **SSO Configuration**. Select the domain you want to configure.

    ![Claimed Domains](media/firmex-vdr-tutorial/domain.png)
4. Have your IT Administrator fill in the following fields. The fields should be taken from your identity provider:

    ![SSO Configuration](media/firmex-vdr-tutorial/admin.png)

    a. In the **Entity ID** textbox, paste the **Microsoft Entra Identifier** value, which you copied previously.

    b. In the **Identity Provider URL** textbox, paste the **Login URL** value, which you copied previously.

    c. **Public Key Certificate** - For authentication purposes, a SAML message may be digitally signed by the issuer. To verify the signature on the message, the message receiver uses a public key known to belong to the issuer. Similarly, to encrypt a message, a public encryption key belonging to the ultimate receiver must be known to the issuer. In both situations—signing and encryption—trusted public keys must be shared in advance. This is the **X509Certificate** from **Federation Metadata XML**

    d. Select **Save** to complete the SSO configuration. Changes take effect immediately.
5. At this time, SSO is enabled for your site.

### Create Firmex VDR test user

In this section, you create a user called B.Simon in Firmex. Work with [Firmex Support Team](mailto:support@firmex.com) to add the users in the Firmex platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with the following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Firmex VDR Sign on URL where you can initiate the login flow.
- Go to Firmex VDR Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Firmex VDR for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Firmex VDR tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Firmex VDR for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
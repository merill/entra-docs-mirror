---
layout: Conceptual
title: Configure Single Sign-on for Skytap for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/skytap-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Single Sign-on for Skytap.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: df3a7c0a-e4d3-192d-4b5c-a7c952fe58d3
document_version_independent_id: 8f929f42-dda7-c68d-5c84-7496267c8612
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/skytap-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/skytap-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/skytap-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 1f144db8-7bda-309b-0a9e-968e8b78263c
---

# Configure Single Sign-on for Skytap for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Single Sign-on for Skytap with Microsoft Entra ID. When you integrate Single Sign-on for Skytap with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Single Sign-on for Skytap.
- Enable your users to be automatically signed in to Single Sign-on for Skytap with their Microsoft Entra accounts.
- Manage your accounts in one central location, the Azure portal.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Single Sign-on for Skytap single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Single Sign-on for Skytap supports SP and IDP initiated SSO.

## Add Single Sign-on for Skytap from the gallery

To configure the integration of Single Sign-on for Skytap into Microsoft Entra ID, you need to add Single Sign-on for Skytap from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Single Sign-on for Skytap** in the search box.
4. Select **Single Sign-on for Skytap** from the results panel, and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Single Sign-on for Skytap

Configure and test Microsoft Entra SSO with Single Sign-on for Skytap by using a test user called **B.Simon**. For SSO to work, establish a linked relationship between a Microsoft Entra user and the related user in Single Sign-on for Skytap.

Here are the general steps to configure and test Microsoft Entra SSO with Single Sign-on for Skytap:

1. **Configure Microsoft Entra SSO**to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Single Sign-on for Skytap SSO**to configure the single sign-on settings on the application side.
    1. **Create a Single Sign-on for Skytap test user** to have a counterpart of B.Simon in Single Sign-on for Skytap. This counterpart is linked to the Microsoft Entra representation of the user.
3. **Test SSO** to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Single Sign-on for Skytap** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. In the **Basic SAML Configuration** section, if you want to configure the application in **IDP** initiated mode, enter the values for the following fields:

    a. In the **Identifier** text box, type a URL that uses the following pattern: `http://pingone.com/<custom EntityID>`

    b. In the **Reply URL** text box, type the URL: `https://sso.connect.pingidentity.com/sso/sp/ACS.saml2`
6. You can optionally select **Set additional URLs**, and perform the following steps to configure the application in **SP** initiated mode:

    a. In the **Sign-on URL** text box, type a URL that uses the following pattern: `https://sso.connect.pingidentity.com/sso/sp/initsso?saasid=<saasid>&idpid=<idpid>`

    b. In the **Relay State** text box, type a URL that uses the following pattern: `https://pingone.com/1.0/<custom ID>`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL, Sign-on URL and Relay State. Contact the [Single Sign-on for Skytap Client support team](mailto:support@skytap.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML**. Select **Download** to download the metadata file and save it on your computer.

    ![Screenshot of the certificate download link](common/metadataxml.png)
8. On the **Set up Single Sign-on for Skytap** section, copy the appropriate URL or URLs, based on your requirement.

    ![Screenshot of copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Single Sign-on for Skytap SSO

To configure single sign-on on the Single Sign-on for Skytap side, you need to send the downloaded **Federation Metadata XML**, and appropriate copied URLs, to the [Single Sign-on for Skytap Client support team](mailto:support@skytap.com). They configure this setting to have the SAML SSO connection set properly on both sides.

### Create Single Sign-on for Skytap test user

In this section, you create a user called B.Simon in Single Sign-on for Skytap. Work with the [Single Sign-on for Skytap Client support team](mailto:support@skytap.com) to add the users in the Single Sign-on for Skytap platform. You can't use single sign-on until you create and activate users.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Single Sign-on for Skytap Sign on URL where you can initiate the login flow.
- Go to Single Sign-on for Skytap Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Single Sign-on for Skytap for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Single Sign-on for Skytap tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Single Sign-on for Skytap for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
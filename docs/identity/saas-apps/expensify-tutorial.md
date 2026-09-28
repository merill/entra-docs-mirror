---
layout: Conceptual
title: Configure Expensify for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/expensify-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Expensify.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 569d7012-11db-454e-b237-2f7f18716bf1
document_version_independent_id: 183c1c26-26b4-af3f-3945-732e75e31a6d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/expensify-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/expensify-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/expensify-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 95aefe35-4ad4-fdf4-bb5e-46d527fc8087
---

# Configure Expensify for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Expensify with Microsoft Entra ID. When you integrate Expensify with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Expensify.
- Enable your users to be automatically signed-in to Expensify with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Expensify single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Expensify supports **SP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Expensify from the gallery

To configure the integration of Expensify into Microsoft Entra ID, you need to add Expensify from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Expensify** in the search box.
4. Select **Expensify** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Expensify

Configure and test Microsoft Entra SSO with Expensify using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Expensify.

To configure and test Microsoft Entra SSO with Expensify, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Expensify SSO**- to configure the Single Sign-On settings on application side.
    1. **Create Expensify test user** - to have a counterpart of B.Simon in Expensify that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Expensify** application integration page, find the **Manage** section and select **Single sign-on**.
3. On the **Select a Single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    a. In the **Identifier (Entity ID)** text box, type the URL: `https://www.expensify.com`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://www.expensify.com/authentication/saml/loginCallback?domain=<yourdomain>`

    c. In the **Sign on URL** text box, type the URL: `https://www.expensify.com/authentication/saml/login`

    Note

    The Reply URL value isn't real. Update this value with the actual Reply URL. Contact [Expensify Client support team](mailto:help@expensify.com) to get this value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, find **Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up Expensify** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Expensify SSO

To enable SSO in Expensify, you first need to enable **Domain Control** in the application. For additional support, work with [Expensify Client support team](mailto:help@expensify.com). Once you have Domain Control enabled, follow these steps:

![Configure Single Sign-On](media/expensify-tutorial/domain-control.png)

1. Sign on to your Expensify application.
2. In the left panel, hover over Settings, then select Domains and navigate to **SAML**.
3. Toggle the **SAML Login** option as **Enabled**.
4. Open the downloaded Federation Metadata from Microsoft Entra ID in notepad, copy the content, and then paste it into the **Identity Provider Metadata** textbox.

### Create Expensify test user

In this section, you create the same user called B.Simon (For example, B.Simon@contoso.com) in Expensify. Check their guide [here](https://community.expensify.com/discussion/4869/how-to-manage-domain-members) for inviting members, or work with the [Expensify Client support team](mailto:help@expensify.com) to add the users in the Expensify platform.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Expensify Sign-on URL where you can initiate the login flow.
- Go to Expensify Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Expensify tile in the My Apps, this option redirects to Expensify Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
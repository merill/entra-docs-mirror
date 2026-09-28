---
layout: Conceptual
title: Configure 123FormBuilder SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/123formbuilder-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and 123FormBuilder SSO.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 468e7ed9-b130-6b86-ee62-cd200392eeec
document_version_independent_id: 2b3ff255-b0f1-8313-1604-402fccf63ee8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/123formbuilder-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/123formbuilder-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/123formbuilder-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 4d9d805f-a47d-e942-d753-c214a1ccb870
---

# Configure 123FormBuilder SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate 123FormBuilder SSO with Microsoft Entra ID. When you integrate 123FormBuilder SSO with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to 123FormBuilder SSO.
- Enable your users to be automatically signed in to 123FormBuilder SSO with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- 123FormBuilder SSO single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- 123FormBuilder SSO supports **SP and IDP** initiated SSO.
- 123FormBuilder SSO supports **Just In Time** user provisioning.

## Add 123FormBuilder SSO from the gallery

To configure the integration of 123FormBuilder SSO into Microsoft Entra ID, you need to add 123FormBuilder SSO from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **123FormBuilder SSO** in the search box.
4. Select **123FormBuilder SSO** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for 123FormBuilder SSO

Configure and test Microsoft Entra SSO with 123FormBuilder SSO using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in 123FormBuilder SSO.

To configure and test Microsoft Entra SSO with 123FormBuilder SSO, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure 123FormBuilder SSO**- to configure the single sign-on settings on application side.
    1. **Create 123FormBuilder SSO test user** - to have a counterpart of B.Simon in 123FormBuilder SSO that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **123FormBuilder SSO** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, If you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://www.123formbuilder.com/saml/azure_ad/<TENANT_ID>/metadata`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://www.123formbuilder.com/saml/azure_ad/<TENANT_ID>/acs`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://www.123formbuilder.com/saml/azure_ad/<TENANT_ID>/sso`

    Note

    These values aren't real. You'll need to update these value from actual URLs and Identifier which is explained later in the article.
7. On the **Setup single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
8. On the **Set up 123FormBuilder SSO** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure 123FormBuilder SSO

1. To configure single sign-on on **123FormBuilder SSO** side, go to https://www.123formbuilder.com/form-2709121/ and perform the following steps:

    ![Screenshot that shows the SSO SAML - Identity Provider configuration screen.](media/123formbuilder-tutorial/submit.png)

    a. In the **Email** textbox, type the email of the user like `B.Simon@Contoso.com`.

    b. Select **Upload** and browse the downloaded Metadata XML file, which you have downloaded previously.

    c. Select **SUBMIT FORM**.
2. The **Microsoft Entra ID - Single sign-on - Configure App Settings** page includes the following values:

    - IDENTIFIER
    - REPLY URL
    - SIGN ON URL

    Perform the following steps:

    1. If you wish to configure the application in **IDP initiated mode**, copy the **IDENTIFIER** value for your instance and paste it in **Identifier** textbox in **Basic SAML Configuration** section.
    2. If you wish to configure the application in **IDP initiated mode**, copy the **REPLY URL** value for your instance and paste it in **Reply URL** textbox in **Basic SAML Configuration** section.
    3. If you wish to configure the application in **SP initiated mode**, copy the **SIGN ON URL** value for your instance and paste it in **Sign On URL** textbox in **Basic SAML Configuration** section.

### Create 123FormBuilder SSO test user

In this section, a user called Britta Simon is created in 123FormBuilder SSO. 123FormBuilder SSO supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in 123FormBuilder SSO, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to 123FormBuilder SSO Sign-on URL where you can initiate the login flow.
- Go to 123FormBuilder SSO Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the 123FormBuilder SSO for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the 123FormBuilder SSO tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the 123FormBuilder SSO for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
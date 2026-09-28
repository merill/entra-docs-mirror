---
layout: Conceptual
title: Configure Active Directory SSO for DoubleYou for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/entra-sso-for-doubleyou-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Active Directory SSO for DoubleYou.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 3052c4d3-308e-a8ae-35f2-56b275511f74
document_version_independent_id: 3052c4d3-308e-a8ae-35f2-56b275511f74
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/entra-sso-for-doubleyou-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/entra-sso-for-doubleyou-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/entra-sso-for-doubleyou-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: a5fbe20b-f287-8afd-863a-d28e55e2ca84
---

# Configure Active Directory SSO for DoubleYou for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Active Directory SSO for DoubleYou with Microsoft Entra ID. When you integrate Active Directory SSO for DoubleYou with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Active Directory SSO for DoubleYou.
- Enable your users to be automatically signed-in to Active Directory SSO for DoubleYou with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Active Directory SSO for DoubleYou single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Active Directory SSO for DoubleYou supports **SP and IDP** initiated SSO.

## Add Active Directory SSO for DoubleYou from the gallery

To configure the integration of Active Directory SSO for DoubleYou into Microsoft Entra ID, you need to add Active Directory SSO for DoubleYou from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Active Directory SSO for DoubleYou** in the search box.
4. Select **Active Directory SSO for DoubleYou** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Active Directory SSO for DoubleYou

Configure and test Microsoft Entra SSO with Active Directory SSO for DoubleYou using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Active Directory SSO for DoubleYou.

To configure and test Microsoft Entra SSO with Active Directory SSO for DoubleYou, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Active Directory SSO for DoubleYou SSO**- to configure the single sign-on settings on application side.
    1. **Create Active Directory SSO for DoubleYou test user** - to have a counterpart of B.Simon in Active Directory SSO for DoubleYou that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Active Directory SSO for DoubleYou** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** text box, type a value using the following pattern: `<company-id>.welfare.it`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<company-id>.welfare.it/<store-id>?`

    c. In the **Sign-on URL** text box, type a URL using the following pattern: `https://<company-id>.welfare.it/microsoft/`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [Active Directory SSO for DoubleYou Client support team](mailto:info@double-you.it) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. Your Active Directory SSO for DoubleYou application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows an example for this. The default value of **Unique User Identifier** is **user.userprincipalname** but Active Directory SSO for DoubleYou expects this to be mapped with the user's email address. For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.

    ![image](common/default-attributes.png)
7. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![The Certificate download link](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Active Directory SSO for DoubleYou SSO

To configure single sign-on on **Active Directory SSO for DoubleYou** side, you need to send the **App Federation Metadata Url** to [Active Directory SSO for DoubleYou support team](mailto:info@double-you.it). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Active Directory SSO for DoubleYou test user

In this section, you create a user called Britta Simon in Active Directory SSO for DoubleYou. Work with [Active Directory SSO for DoubleYou support team](mailto:info@double-you.it) to add the users in the Active Directory SSO for DoubleYou platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Active Directory SSO for DoubleYou Sign on URL where you can initiate the login flow.
- Go to Active Directory SSO for DoubleYou Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Active Directory SSO for DoubleYou for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Active Directory SSO for DoubleYou tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Active Directory SSO for DoubleYou for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
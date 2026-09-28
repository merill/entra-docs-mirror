---
layout: Conceptual
title: Configure Keystone for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/keystone-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Keystone.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 922e997f-511d-a05d-0d74-25f20676755f
document_version_independent_id: 90dd0d4d-5bae-4a85-216d-b59616730e15
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/keystone-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/keystone-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/keystone-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 94494877-91d6-f021-02c0-78f3a4f85a00
---

# Configure Keystone for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Keystone with Microsoft Entra ID. When you integrate Keystone with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Keystone.
- Enable your users to be automatically signed-in to Keystone with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Keystone single sign-on (SSO) enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Keystone supports **SP** initiated SSO.

## Add Keystone from the gallery

To configure the integration of Keystone into Microsoft Entra ID, you need to add Keystone from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Keystone** in the search box.
4. Select **Keystone** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Keystone

Configure and test Microsoft Entra SSO with Keystone using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user at Keystone.

To configure and test Microsoft Entra SSO with Keystone, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Keystone SSO**- to configure the single sign-on settings on application side.
    1. **Create Keystone test user** - to have a counterpart of B.Simon in Keystone that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Keystone** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type a value using the following pattern: `urn:amazon:cognito:sp:<UserPoolID>`

    b. In the **Reply URL** textbox, type a URL using the following pattern: `https://<UserPoolName>.auth.<Region>.amazoncognito.com/saml2/idpresponse`

    c. In the **Sign on URL** text box, type a URL using the following pattern: `https://irca.<Environment>.fm.ks.irdeto.com/`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign on URL. Contact [Keystone support team](mailto:soc@irdeto.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer

    ![Screenshot shows the Certificate download link.](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Keystone SSO

To configure single sign-on on **Keystone** side, you need to send the **App Federation Metadata Url** to [Keystone support team](mailto:soc@irdeto.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Keystone test user

In this section, you create a user called Britta Simon at Keystone. Work with [Keystone support team](mailto:soc@irdeto.com) to add the users in the Keystone platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Keystone Sign-On URL where you can initiate the login flow.
- Go to Keystone Sign-On URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Keystone tile in the My Apps, this option redirects to Keystone Sign-On URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
---
layout: Conceptual
title: Configure Loop Flow CRM for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/loop-flow-crm-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Loop Flow CRM.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 073dac88-557b-ad2e-feb7-8fb389ef8e70
document_version_independent_id: 3f3e04a5-6c63-69ab-232a-eb052a6cc6de
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/loop-flow-crm-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/loop-flow-crm-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/loop-flow-crm-tutorial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/0850fefd-e402-4507-ae98-46cfdfc2e16c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6ecf98a5-97c7-4249-b209-a9d9e42633a0
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 141b71cc-e0d6-a569-adbb-7aa3b7a2ad74
---

# Configure Loop Flow CRM for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Loop Flow CRM with Microsoft Entra ID. When you integrate Loop Flow CRM with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Loop Flow CRM.
- Enable your users to be automatically signed-in to Loop Flow CRM with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Loop Flow CRM single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Loop Flow CRM supports **SP and IDP** initiated SSO.

## Add Loop Flow CRM from the gallery

To configure the integration of Loop Flow CRM into Microsoft Entra ID, you need to add Loop Flow CRM from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Loop Flow CRM** in the search box.
4. Select **Loop Flow CRM** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Loop Flow CRM

Configure and test Microsoft Entra SSO with Loop Flow CRM using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Loop Flow CRM.

To configure and test Microsoft Entra SSO with Loop Flow CRM, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Loop Flow CRM SSO**- to configure the single sign-on settings on application side.
    1. **Create Loop Flow CRM test user** - to have a counterpart of B.Simon in Loop Flow CRM that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Loop Flow CRM** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://<CUSTOMER_NAME>.loopworks.com`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<CUSTOMER_NAME>.loopworks.com/sso/consume/<CUSTOMER_NAME>`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<CUSTOMER_NAME>.loopworks.com/sso/<CUSTOMER_NAME>`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [Loop Flow CRM Client support team](mailto:support@loopworks.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![The Certificate download link](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Loop Flow CRM SSO

To configure single sign-on on **Loop Flow CRM** side, you need to send the **App Federation Metadata Url** to [Loop Flow CRM support team](mailto:support@loopworks.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Loop Flow CRM test user

In this section, you create a user called Britta Simon in Loop Flow CRM. Work with [Loop Flow CRM support team](mailto:support@loopworks.com) to add the users in the Loop Flow CRM platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Loop Flow CRM Sign on URL where you can initiate the login flow.
- Go to Loop Flow CRM Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Loop Flow CRM for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Loop Flow CRM tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Loop Flow CRM for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
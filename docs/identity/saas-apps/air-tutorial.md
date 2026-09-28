---
layout: Conceptual
title: Configure Air for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/air-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Air.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 526400b6-92ed-e25e-2090-c57d06b5a5a1
document_version_independent_id: d2d5bfcc-28f6-9707-02ab-781715a5ccb4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/air-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/air-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/air-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 93491ada-1c44-cb31-d5bf-6b791d8c1eb3
---

# Configure Air for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Air with Microsoft Entra ID. When you integrate Air with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Air.
- Enable your users to be automatically signed-in to Air with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Air single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Air supports **SP and IDP** initiated SSO.

## Adding Air from the gallery

To configure the integration of Air into Microsoft Entra ID, you need to add Air from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Air** in the search box.
4. Select **Air** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Air

Configure and test Microsoft Entra SSO with Air using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Air.

To configure and test Microsoft Entra SSO with Air, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Air SSO**- to configure the single sign-on settings on application side.
    1. **Create Air test user** - to have a counterpart of B.Simon in Air that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Air** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, enter the values for the following fields:

    a. In the **Identifier** text box, type the value: `urn:amazon:cognito:sp:us-east-1_hFBg5izBk`

    b. In the **Reply URL** text box, type the URL: `https://auth.air.inc/saml2/idpresponse`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://api.air.inc/integrations/saml/login/<CustomerID>`

    Note

    The value isn't real. Update the value with the actual Sign-on URL. Contact [Air Client support team](mailto:dev@air.inc) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![The Certificate download link](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Air SSO

1. Log in to the Air website as an administrator.
2. Select the **Workspace** at the top left corner.
3. Go to the **Settings** &gt; **SECURITY &IDENTITY** tab and perform the perform the following steps:

    ![Screenshot for Air configuration](media/air-tutorial/integration.png)

    a. In the **Manage approved email domains** text box, add your organizations email domains to the approved domains list to allow users with these domains to authenticate using SAML SSO.

    b. Copy **Single sign-on URL** value, paste this value into the **Sign on URL** text box in the **Basic SAML Configuration** section.

    c. In the SAML metadata URL text box, paste the **App Federation Metadata Url** value which you have copied.

    d. Select **Enable SAML SSO**.

### Create Air test user

Log in to the Air website as an administrator.

1. Select the **Workspace** at the top left corner.
2. Go to the **Settings** &gt; **MEMBERS** tab and select **Add members**.
3. Give the Email address and select **Invite**.

    ![Screenshot for User creation](media/air-tutorial/user-new.png)

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Air Sign on URL where you can initiate the login flow.
- Go to Air Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Air for which you set up the SSO

You can also use Microsoft My Apps to test the application in any mode. When you select the Air tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Air for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
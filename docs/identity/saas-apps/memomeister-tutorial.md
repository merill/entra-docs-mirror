---
layout: Conceptual
title: Configure MemoMeister for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/memomeister-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and MemoMeister.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 7207cfdc-1f9c-c6ba-4562-f83c532cb30d
document_version_independent_id: 7207cfdc-1f9c-c6ba-4562-f83c532cb30d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/memomeister-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/memomeister-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/memomeister-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 0b12c267-7b94-d5e7-c611-28fe04d6359f
---

# Configure MemoMeister for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate MemoMeister with Microsoft Entra ID. When you integrate MemoMeister with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to MemoMeister.
- Enable your users to be automatically signed-in to MemoMeister with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- MemoMeister single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- MemoMeister supports only **SP** initiated SSO.

## Add MemoMeister from the gallery

To configure the integration of MemoMeister into Microsoft Entra ID, you need to add MemoMeister from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **MemoMeister** in the search box.
4. Select **MemoMeister** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for MemoMeister

Configure and test Microsoft Entra SSO with MemoMeister using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in MemoMeister.

To configure and test Microsoft Entra SSO with MemoMeister, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Create a Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure MemoMeister SSO**- to configure the single sign-on settings on application side.
    1. **Create MemoMeister test user** - to have a counterpart of B.Simon in MemoMeister that's linked to the Microsoft Entra ID representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **MemoMeister** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL: `urn:amazon:cognito:sp:eu-central-1_<ID>`

    b. In the **Reply URL** textbox, type the URL: `https://memomeister-production.auth.eu-central-1.amazoncognito.com/saml2/idpresponse`

    c. In the **Sign on URL** text box, type the URL: `https://web.memomeister.com/login`

    Note

    The Identifier value isn't real. Update the value with the actual Identifier. Contact [MemoMeister support team](mailto:support@memomeister.com) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section in the Microsoft Entra admin center.
6. MemoMeister application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows the image of attributes configuration.](common/default-attributes.png)
7. In addition to above, MemoMeister application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | address\_city | user.city |
    | address\_country | user.country |
    | mobile\_phone | user.mobilephone |
    | telephone\_number | user.telephonenumber |
    | address\_streetaddress | user.streetaddress |
    | preferred\_language | user.preferredlanguage |
    | address\_postalcode | user.postalcode |
    | company\_name | user.companyname |
    | groups | user.groups |
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure MemoMeister SSO

To configure single sign-on on **MemoMeister** side, you need to send the **App Federation Metadata Url** to [MemoMeister support team](mailto:support@memomeister.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create MemoMeister test user

In this section, you create a user called B.Simon in MemoMeister. Work with [MemoMeister support team](mailto:support@memomeister.com) to add the users in the MemoMeister platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application** in Microsoft Entra admin center. This option redirects to MemoMeister Sign-on URL where you can initiate the login flow.
- Go to MemoMeister Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the MemoMeister tile in the My Apps, this option redirects to MemoMeister Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
---
layout: Conceptual
title: Configure Campus Café for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/campus-cafe-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Campus Café.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 1b59ec0b-3e0e-279a-8865-ff14a8a24e43
document_version_independent_id: 17be32de-07ca-79c0-bedf-95ae56999b74
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/campus-cafe-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/campus-cafe-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/campus-cafe-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 115d1086-e3b8-579f-1c4e-fc1d0ebbab50
---

# Configure Campus Café for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Campus Café with Microsoft Entra ID. When you integrate Campus Café with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Campus Café.
- Enable your users to be automatically signed-in to Campus Café with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Campus Café single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Campus Café supports **SP** initiated SSO.

## Add Campus Café from the gallery

To configure the integration of Campus Café into Microsoft Entra ID, you need to add Campus Café from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Campus Café** in the search box.
4. Select **Campus Café** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Campus Café

Configure and test Microsoft Entra SSO with Campus Café using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Campus Café.

To configure and test Microsoft Entra SSO with Campus Café, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Campus Café SSO**- to configure the single sign-on settings on application side.
    1. **Create Campus Café test user** - to have a counterpart of B.Simon in Campus Café that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Campus Café** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you have **Service Provider metadata file**, perform the following steps:

    a. Select **Upload metadata file**.

    ![Upload metadata file](common/upload-metadata.png)

    b. Select **folder logo** to select the metadata file and select **Upload**.

    ![choose metadata file](common/browse-upload-metadata.png)

    c. After the metadata file is successfully uploaded, the **Identifier** value gets auto populated in **Basic SAML Configuration** section.

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://{SSO}-web.scansoftware.com/cafeweb/loginsso`

    Note

    If the **Identifier** value doesn't get auto populated, then please fill in the value manually according to your requirement. The Sign-on URL value isn't real. Update this value with the actual Sign-on URL. Contact [Campus Café Client support team](mailto:support@campuscafesoftware.com) to get this value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up Campus Café** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Campus Cafe SSO

To configure single sign-on on **Campus Café** side, you need to send the downloaded **Federation Metadata XML** and appropriate copied URLs from the application configuration to [Campus Café support team](mailto:support@campuscafesoftware.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Campus Cafe test user

In this section, you create a user called B.Simon in Campus Café. Work with [Campus Café support team](mailto:support@campuscafesoftware.com) to add the users in the Campus Café platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Campus Cafe Sign-on URL where you can initiate the login flow.
- Go to Campus Cafe Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Campus Cafe tile in the My Apps, this option redirects to Campus Cafe Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
---
layout: Conceptual
title: Configure Cisco Unified Communications Manager for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/cisco-unified-communications-manager-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Cisco Unified Communications Manager.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: f5dedd6b-ab42-2e0c-2c1d-d6ff7cac09e9
document_version_independent_id: dd2a170e-1834-0d53-463d-4a8f4db0843b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/cisco-unified-communications-manager-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/cisco-unified-communications-manager-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/cisco-unified-communications-manager-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 6c13d4ee-7f8f-3acf-a466-7b2e95aec48e
---

# Configure Cisco Unified Communications Manager for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Cisco Unified Communications Manager with Microsoft Entra ID. Cisco Unified Communications Manager (Unified CM) provides reliable, secure, scalable, and manageable call control and session management. When you integrate Cisco Unified Communications Manager with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Cisco Unified Communications Manager.
- Enable your users to be automatically signed-in to Cisco Unified Communications Manager with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You'll configure and test Microsoft Entra single sign-on for Cisco Unified Communications Manager in a test environment. Cisco Unified Communications Manager supports **SP** initiated single sign-on.

## Prerequisites

To integrate Microsoft Entra ID with Cisco Unified Communications Manager, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Cisco Unified Communications Manager single sign-on (SSO) enabled subscription.

## Add application and assign a test user

Before you begin the process of configuring single sign-on, you need to add the Cisco Unified Communications Manager application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the single sign-on configuration.

### Add Cisco Unified Communications Manager from the Microsoft Entra gallery

Add Cisco Unified Communications Manager from the Microsoft Entra application gallery to configure single sign-on with Cisco Unified Communications Manager. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Cisco Unified Communications Manager** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you have **Service Provider metadata file** then perform the following steps:

    a. Select **Upload metadata file**.

    ![Screenshot shows how to upload metadata file.](common/upload-metadata.png)

    b. Select **folder logo** to select the metadata file and select **Upload**.

    ![Screenshot shows to choose and browse metadata file.](common/browse-upload-metadata.png)

    c. After the metadata file is successfully uploaded, the **Identifier** and **Reply URL** values get auto populated in Basic SAML Configuration section.

    Note

    You get the **Service Provider metadata file** from the [Cisco Unified Communications Manager support team](mailto:email-in@cisco.com). If the **Identifier** and **Reply URL** values don't get auto populated, then fill in the values manually according to your requirement.
6. Cisco Unified Communications Manager application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows the image of attributes configuration.](common/default-attributes.png)
7. In addition to above, Cisco Unified Communications Manager application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | uid | user.onpremisessamaccountname |
8. On the **Set-up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)
9. On the **Set up Cisco Unified Communications Manager** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows how to copy configuration appropriate URL.](common/copy-configuration-urls.png)

## Configure Cisco Unified Communications Manager SSO

To configure single sign-on on **Cisco Unified Communications Manager** side, you need to send the downloaded **Federation Metadata XML** and appropriate copied URLs from the application configuration to [Cisco Unified Communications Manager support team](mailto:email-in@cisco.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Cisco Unified Communications Manager test user

In this section, you create a user called Britta Simon in Cisco Unified Communications Manager. Work with [Cisco Unified Communications Manager support team](mailto:email-in@cisco.com) to add the users in the Cisco Unified Communications Manager platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Cisco Unified Communications Manager Sign-on URL where you can initiate the login flow.
- Go to Cisco Unified Communications Manager Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Cisco Unified Communications Manager tile in the My Apps, this option redirects to Cisco Unified Communications Manager Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
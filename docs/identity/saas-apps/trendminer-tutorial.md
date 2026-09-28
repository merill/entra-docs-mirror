---
layout: Conceptual
title: Configure TrendMiner for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/trendminer-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and TrendMiner.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: eb2c02af-f307-ce64-6bd9-e7326c04c5c9
document_version_independent_id: 3c091231-723d-4b5a-cf12-cf7c5f52e20d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/trendminer-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/trendminer-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/trendminer-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7bf3212b-74c6-d0ee-a9d3-a187a230ed28
---

# Configure TrendMiner for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate TrendMiner with Microsoft Entra ID. When you integrate TrendMiner with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to TrendMiner.
- Enable your users to be automatically signed-in to TrendMiner with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- TrendMiner single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- TrendMiner supports **SP and IDP** initiated SSO

## Adding TrendMiner from the gallery

To configure the integration of TrendMiner into Microsoft Entra ID, you need to add TrendMiner from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **TrendMiner** in the search box.
4. Select **TrendMiner** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for TrendMiner

Configure and test Microsoft Entra SSO with TrendMiner using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in TrendMiner.

To configure and test Microsoft Entra SSO with TrendMiner, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure TrendMiner SSO**- to configure the single sign-on settings on application side.
    1. **Create TrendMiner test user** - to have a counterpart of B.Simon in TrendMiner that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **TrendMiner** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the edit/pen icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, enter the values for the following fields:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://<CUSTOMER>.trendminer.cloud/security/saml/metadata`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<CUSTOMER>.trendminer.cloud/security/saml/SSO`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<CUSTOMER>.trendminer.cloud/`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [TrendMiner Client support team](mailto:support@trendminer.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
8. On the **Set up TrendMiner** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure TrendMiner SSO

1. Open a new web browser window and sign into your TrendMiner company site as an administrator.
2. In the left menu, select **SECURITY &gt; Identity Provider**
3. In the **Identity Provider** page, select **SAML** and then select **Next step**.

    ![select SAML](media/trendminer-tutorial/saml.png)
4. Select **Next step** in **SAML Backup** page.

    ![select SAML Backup](media/trendminer-tutorial/saml-backup.png)
5. Select **Next step** for **Self-Signed certificates**.

    ![Self-Signed certificates page](media/trendminer-tutorial/self-signed-certificate.png)
6. You can **Skip** uploading a signing key.

    ![uploading a signing key](media/trendminer-tutorial/signing-key.png)
7. In the **SAML Configuration** screen in **Entity base URL**, enter domain URL like `https://trendminer.domain.com/`
8. In **Identity provider metadata**, upload the **Azure Metadata file** which you have copied and then select **Next step**.

    ![SAML Configuration](media/trendminer-tutorial/saml-configuration.png)
9. In the **SAML User mapping** section, enter usernames that you use to login and select **Finish**.

    ![SAML User mapping](media/trendminer-tutorial/user-mapping.png)

### Create TrendMiner test user

In this section, you create a user called Britta Simon in TrendMiner. Work with [TrendMiner support team](mailto:support@trendminer.com) to add the users in the TrendMiner platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to TrendMiner Sign on URL where you can initiate the login flow.
- Go to TrendMiner Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the TrendMiner for which you set up the SSO

You can also use Microsoft Access Panel to test the application in any mode. When you select the TrendMiner tile in the Access Panel, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the TrendMiner for which you set up the SSO. For more information about the Access Panel, see [Introduction to the Access Panel](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
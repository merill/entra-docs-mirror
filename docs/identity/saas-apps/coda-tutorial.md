---
layout: Conceptual
title: Configure Coda for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/coda-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Coda.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 5cfe0c12-836d-40fe-2e7d-cfe35b2770a2
document_version_independent_id: b859198f-9a17-1608-6066-24bd9ed55349
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/coda-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/coda-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/coda-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ef81e38b-896e-3d2b-34b9-ac12dd367339
---

# Configure Coda for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Coda with Microsoft Entra ID. When you integrate Coda with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Coda.
- Enable your users to be automatically signed-in to Coda with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Coda single sign-on (SSO) enabled subscription (Enterprise) with GDrive integration disabled. Contact [Coda support team](mailto:support@coda.io) to disable GDrive integration for your Organization if it's currently enabled.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Coda supports **IDP** initiated SSO.
- Coda supports **Just In Time** user provisioning.
- Coda supports [Automated user provisioning](coda-provisioning-tutorial).

## Add Coda from the gallery

To configure the integration of Coda into Microsoft Entra ID, you need to add Coda from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Coda** in the search box.
4. Select **Coda** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Coda

Configure and test Microsoft Entra SSO with Coda using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Coda.

To configure and test Microsoft Entra SSO with Coda, perform the following steps:

1. **Begin configuration of Coda SSO** - to begin configuration of SSO in Coda.
2. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
3. **Configure Coda SSO**- to complete configuration of single sign-on settings in Coda.
    1. **Create Coda test user** - to have a counterpart of B.Simon in Coda that's linked to the Microsoft Entra representation of user.
4. **Test SSO** - to verify whether the configuration works.

## Begin configuration of Coda SSO

Follow these steps in Coda to begin.

1. In Coda, open your **Organization settings** panel.

    ![Open Organization Settings](media/coda-tutorial/settings.png)
2. Ensure that your organization has GDrive Integration turned off. If it's currently enabled, contact the [Coda support team](mailto:support@coda.io) to help you migrate off GDrive.

    ![GDrive Disabled](media/coda-tutorial/gdrive-off.png)
3. Under **Authenticate with SSO (SAML)**, select the **Configure SAML** option.

    ![Saml Settings](media/coda-tutorial/settings-link.png)
4. Note the values for **Entity ID** and **SAML Response URL**, which you need in subsequent steps.

    ![Entity ID and SAML Response URL to use in Azure](media/coda-tutorial/azure-settings.png)

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Coda** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Set up single sign-on with SAML** page, perform the following steps:

    a. In the **Identifier** text box, enter the "Entity ID" from above. It should follow the pattern: `https://coda.io/samlId/<CUSTOMID>`

    b. In the **Reply URL** text box, enter the "SAML Response URL" from above. It should follow the pattern: `https://coda.io/login/sso/saml/<CUSTOMID>/consume`

    Note

    Your values will differ from the above; you can find your values in Coda's "Configure SAML" console. Update these values with the actual Identifier and Reply URL.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Coda** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Coda SSO

To complete the setup, you enter values from Microsoft Entra ID in the Coda **Configure Saml** panel.

1. In Coda, open your **Organization settings** panel.
2. Under **Authenticate with SSO (SAML)**, select the **Configure SAML** option.
3. Set **SAML Provider** to **Microsoft Entra ID**.
4. In **Identity Provider Login URL**, paste the **Login URL** from the Azure console.
5. In **Identity Provider Issuer**, paste the **Microsoft Entra Identifier** from the Azure console.
6. In **Identity Provider Public Certificate**, select the **Upload Certificate** option and select the certificate file you downloaded earlier.
7. Select **Save**.

This completes the work necessary for the SAML SSO connection setup.

### Create Coda test user

In this section, a user called Britta Simon is created in Coda. Coda supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Coda, a new one is created after authentication.

Coda also supports automatic user provisioning, you can find more details [here](coda-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the Coda for which you set up the SSO.
- You can use Microsoft My Apps. When you select the Coda tile in the My Apps, you should be automatically signed in to the Coda for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
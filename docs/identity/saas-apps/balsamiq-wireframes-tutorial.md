---
layout: Conceptual
title: Configure Balsamiq Wireframes for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/balsamiq-wireframes-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Balsamiq Wireframes.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: d564e314-1835-8ca5-7689-06e33470cd88
document_version_independent_id: 6fa16b66-abc8-ac28-1148-49f4750c9bce
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/balsamiq-wireframes-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/balsamiq-wireframes-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/balsamiq-wireframes-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 3f1c631a-0320-36d5-6dd4-994ebc6aa8f1
---

# Configure Balsamiq Wireframes for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Balsamiq Wireframes with Microsoft Entra ID. When you integrate Balsamiq Wireframes with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Balsamiq Wireframes.
- Enable your users to be automatically signed-in to Balsamiq Wireframes with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Balsamiq Wireframes single sign-on (SSO) enabled subscription.

Note

This feature is only available for users on the 200-projects Space plan.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Balsamiq Wireframes supports **SP and IDP** initiated SSO.
- Balsamiq Wireframes supports **Just In Time** user provisioning.

## Add Balsamiq Wireframes from the gallery

To configure the integration of Balsamiq Wireframes into Microsoft Entra ID, you need to add Balsamiq Wireframes from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Balsamiq Wireframes** in the search box.
4. Select **Balsamiq Wireframes** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Balsamiq Wireframes

Configure and test Microsoft Entra SSO with Balsamiq Wireframes using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Balsamiq Wireframes.

To configure and test Microsoft Entra SSO with Balsamiq Wireframes, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Balsamiq Wireframes SSO**- to configure the single sign-on settings on application side.
    1. **Create Balsamiq Wireframes test user** - to have a counterpart of B.Simon in Balsamiq Wireframes that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Balsamiq Wireframes** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://balsamiq.cloud/samlsso/<ID>`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://balsamiq.cloud/samlsso/<ID>`

    c. In the **Sign-on URL** text box, type a URL using the following pattern: `https://balsamiq.cloud/samlsso/<ID>`

    d. In the **Relay State** text box, type a URL using the following pattern: `https://balsamiq.cloud/<ID>/projects`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL, Sign-on URL and Relay State. Contact [Balsamiq Wireframes Client support team](mailto:support@balsamiq.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. Balsamiq Wireframes application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows list of attributes.](common/default-attributes.png)
7. In addition to above, Balsamiq Wireframes application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | Email | user.mail |
    | firstName | user.givenname |
    | lastName | user.surname |
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
9. On the **Set up Balsamiq Wireframes** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Balsamiq Wireframes SSO

1. Log in to your Balsamiq Wireframes company site as an administrator.
2. Go to **Settings** &gt; **Space Settings** and select **Configure SSO** under Single Sign-On Authentication.

    ![Screenshot shows the SSO Settings.](media/balsamiq-wireframes-tutorial/settings.png)
3. Copy all the required values and paste it in **Basic SAML Configuration** section in the Azure portal and select **Next**.

    ![Screenshot shows the Service Provider Details.](media/balsamiq-wireframes-tutorial/details.png)
4. In the **Configure IDp** section, perform the following steps:

    ![Screenshot shows the IDP Metadata.](media/balsamiq-wireframes-tutorial/certificate.png)

    1. In the **SAML 2.0 Endpoint(HTTP)** textbox, paste the value of **Login URL**, which you copied previously.
    2. In the **Identity Provider Issuer** textbox, paste the value of **Microsoft Entra Identifier**, which you copied previously.
    3. Open the downloaded **Federation Metadata XML** file and **Upload** the file into **Public Certificate** section.
    4. Select **Next**.

    Note

    If you have an IdP Metadata file to upload, the fields are automatically populated.
5. Verify your SAML configuration, select **Test SAML Login** button and select **Next**.

    ![Screenshot shows the SAML configuration.](media/balsamiq-wireframes-tutorial/configuration.png)
6. After the successful test configuration, select **Turn on SAML SSO Now**.

    ![Screenshot shows the Test SAML.](media/balsamiq-wireframes-tutorial/testing.png)

### Create Balsamiq Wireframes test user

In this section, a user called Britta Simon is created in Balsamiq Wireframes. Balsamiq Wireframes supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Balsamiq Wireframes, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Balsamiq Wireframes Sign on URL where you can initiate the login flow.
- Go to Balsamiq Wireframes Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Balsamiq Wireframes for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Balsamiq Wireframes tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Balsamiq Wireframes for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
---
layout: Conceptual
title: Configure Saba Cloud for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/saba-cloud-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Saba Cloud.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 696039ed-a27d-5d31-3007-b255fdd1d107
document_version_independent_id: 355eb5bc-2cde-a758-51ea-a9c0a9676ab6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/saba-cloud-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/saba-cloud-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/saba-cloud-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: dd253d95-16b1-ce70-3b3e-4f7fa7d81109
---

# Configure Saba Cloud for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Saba Cloud with Microsoft Entra ID. When you integrate Saba Cloud with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Saba Cloud.
- Enable your users to be automatically signed-in to Saba Cloud with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Saba Cloud single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Saba Cloud supports **SP and IDP** initiated SSO.
- Saba Cloud supports **Just In Time** user provisioning.
- Saba Cloud Mobile application can now be configured with Microsoft Entra ID for enabling SSO. In this article, you configure and test Microsoft Entra SSO in a test environment.

## Adding Saba Cloud from the gallery

To configure the integration of Saba Cloud into Microsoft Entra ID, you need to add Saba Cloud from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Saba Cloud** in the search box.
4. Select **Saba Cloud** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Saba Cloud

Configure and test Microsoft Entra SSO with Saba Cloud using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Saba Cloud.

To configure and test Microsoft Entra SSO with Saba Cloud, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Saba Cloud SSO**- to configure the single sign-on settings on application side.
    1. **Create Saba Cloud test user** - to have a counterpart of B.Simon in Saba Cloud that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.
4. **Test SSO for Saba Cloud (mobile)** to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Saba Cloud** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, enter the values for the following fields:

    a. In the **Identifier** text box, type a URL using the following pattern (you'll get this value in the Configure Saba Cloud SSO section on step 6, but it usually is in the format of `<CUSTOMER_NAME>_sp`): `<CUSTOMER_NAME>_sp`

    b. In the **Reply URL** text box, type a URL using the following pattern (ENTITY\_ID refers to the previous step, usually `<CUSTOMER_NAME>_sp`): `https://<CUSTOMER_NAME>.sabacloud.com/Saba/saml/SSO/alias/<ENTITY_ID>`

    Note

    If you specify the reply URL incorrectly, you might have to adjust it in the **App Registration** section of Microsoft Entra ID, not in the **Enterprise Application** section. Making changes to the **Basic SAML Configuration** section doesn't always update the Reply URL.
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    a. In the **Sign-on URL** text box, type a URL using the following pattern: `https://<CUSTOMER_NAME>.sabacloud.com`

    b. In the **Relay State** text box, type a URL using the following pattern: `IDP_INIT---SAML_SSO_SITE=<SITE_ID> `or in case SAML is configured for a microsite, type a URL using the following pattern: `IDP_INIT---SAML_SSO_SITE=<SITE_ID>---SAML_SSO_MICRO_SITE=<MicroSiteId>`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL, Sign-on URL and Relay State. Contact [Saba Cloud Client support team](mailto:support@saba.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.

    For more information about configuring the RelayState, see [IdP and SP initiated SSO for a microsite](https://help.sabacloud.com/sabacloud/help-system/topics/help-system-idp-and-sp-initiated-sso-for-a-microsite.html).
7. In the **User Attributes & Claims** section, adjust the Unique User Identifier to whatever you organization intends to use as the primary username for Saba users.

    This step is required only if you're attempting to convert from username/password to SSO. If this is a new Saba Cloud deployment that doesn't have existing users, you can skip this step.
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
9. On the **Set up Saba Cloud** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Saba Cloud SSO

1. In a different web browser window, sign in to your Saba Cloud company site as an administrator
2. Select **Menu** icon and select **Admin**, then select **System Admin** tab.

    ![screenshot for system admin](media/saba-cloud-tutorial/system.png)
3. In **Configure System**, select **SAML SSO Setup** and select **SETUP SAML SSO** button.

    ![screenshot for configuration](media/saba-cloud-tutorial/configure.png)
4. In the pop up window, select **Microsite** from the dropdown and select **ADD AND CONFIGURE**.

    ![screenshot for add site/microsite](media/saba-cloud-tutorial/microsite.png)
5. In the **Configure IDP** section, select **BROWSE** to upload the **Federation Metadata XML** file, which you have downloaded. Enable the **Site Specific IDP** checkbox and select **IMPORT**.

    ![screenshot for Certificate import](media/saba-cloud-tutorial/certificate.png)
6. In the **Configure SP** section, copy the **Entity Alias** value and paste this value into the **Identifier (Entity ID)** text box in the **Basic SAML Configuration** section. Select **GENERATE**.

    ![screenshot for Configure SP](media/saba-cloud-tutorial/generate-metadata.png)
7. In the **Configure Properties** section, verify the populated fields and select **SAVE**.

    ![screenshot for Configure Properties](media/saba-cloud-tutorial/configure-properties.png)

    You might need to set **Max Authentication Age (in seconds)** to **7776000** (90 days) to match the default max rolling age Microsoft Entra ID allows for a login. Failure to do so could result in the error `(109) Login failed. Please contact system administrator.`

### Create Saba Cloud test user

In this section, a user called Britta Simon is created in Saba Cloud. Saba Cloud supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Saba Cloud, a new one is created after authentication.

Note

For enabling SAML just in time user provisioning with Saba cloud, please refer to [this](https://help.sabacloud.com/sabacloud/help-system/topics/help-system-user-provisioning-with-saml.html) documentation.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Saba Cloud Sign on URL where you can initiate the login flow.
- Go to Saba Cloud Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Saba Cloud for which you set up the SSO

You can also use Microsoft My Apps to test the application in any mode. When you select the Saba Cloud tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Saba Cloud for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).

Note

If the sign-on URL isn't populated in Microsoft Entra ID then the application is treated as IDP initiated mode and if the sign-on URL is populated then Microsoft Entra ID will always redirect the user to the Saba Cloud application for service provider initiated flow.

## Test SSO for Saba Cloud (mobile)

1. Open Saba Cloud Mobile application, give the **Site Name** in the textbox and select **Enter**.

    ![Screenshot for Site name.](media/saba-cloud-tutorial/site-name.png)
2. Enter your **email address** and select **Next**.

    ![Screenshot for email address.](media/saba-cloud-tutorial/email-address.png)
3. Finally after successful sign in, the application page is displayed.

    ![Screenshot for successful sign in.](media/saba-cloud-tutorial/dashboard.png)
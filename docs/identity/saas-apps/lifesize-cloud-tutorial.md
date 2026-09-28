---
layout: Conceptual
title: Configure Lifesize Cloud for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/lifesize-cloud-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Lifesize Cloud.
ms.topic: how-to
ms.date: 2026-06-04T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: b7ee7496-1d94-0563-cf5a-f4d95bf17515
document_version_independent_id: 71807293-d60c-8bd0-38c9-f640b7ca0e7a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/lifesize-cloud-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/lifesize-cloud-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/lifesize-cloud-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: e21e754a-68af-270c-5e45-9a0275edc229
---

# Configure Lifesize Cloud for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Lifesize Cloud with Microsoft Entra ID. When you integrate Lifesize Cloud with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Lifesize Cloud.
- Enable your users to be automatically signed-in to Lifesize Cloud with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Lifesize Cloud is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Lifesize Cloud single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Lifesize Cloud supports **SP** initiated SSO.
- Lifesize Cloud supports **Automated** user provisioning.

## Add Lifesize Cloud from the gallery

To configure the integration of Lifesize Cloud into Microsoft Entra ID, you need to add Lifesize Cloud from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Lifesize Cloud** in the search box.
4. Select **Lifesize Cloud** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Lifesize Cloud

Configure and test Microsoft Entra SSO with Lifesize Cloud using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Lifesize Cloud.

To configure and test Microsoft Entra SSO with Lifesize Cloud, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Lifesize Cloud SSO**- to configure the single sign-on settings on application side.
    1. **Create Lifesize Cloud test user** - to have a counterpart of B.Simon in Lifesize Cloud that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Lifesize Cloud** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Sign-on URL** text box, type a URL using the following pattern: `https://login.lifesizecloud.com/ls/?acs`

    b. In the **Identifier** text box, type a URL using the following pattern: `https://login.lifesizecloud.com/<COMPANY_NAME>`

    c. Select **set additional URLs**.

    d. In the **Relay State** text box, type a URL using the following pattern: `https://webapp.lifesizecloud.com/?ent=<IDENTIFIER>`

    Note

    These values aren't real. Update these values with the actual Sign-on URL, Identifier and Relay State. Contact [Lifesize Cloud Client support team](https://support.lifesize.com/) to get Sign-On URL, and Identifier values and you can get Relay State value from SSO Configuration that's explained later in the article. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Lifesize Cloud** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Lifesize Cloud SSO

1. To get SSO configured for your application, login into the Lifesize Cloud application with Admin privileges.
2. In the top right corner select your name and then select the **Advance Settings**.

    ![Screenshot shows the Advanced Settings menu item.](media/lifesize-cloud-tutorial/settings.png)
3. In the Advance Settings now select the **SSO Configuration** link. It will open the SSO Configuration page for your instance.

    ![Screenshot shows Advanced Settings where you can select S S O Configuration.](media/lifesize-cloud-tutorial/configuration.png)
4. Now configure the following values in the SSO configuration UI.

    ![Screenshot shows the S S O Configuration page where you can enter the values described.](media/lifesize-cloud-tutorial/values.png)

    a. In **Identity Provider Issuer** textbox, paste the value of **Microsoft Entra Identifier**..

    b. In **Login URL** textbox, paste the value of **Login URL**..

    c. Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.

    d. In the SAML Attribute mappings for the First Name text box enter the value as `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`

    e. In the SAML Attribute mapping for the **Last Name** text box enter the value as `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`

    f. In the SAML Attribute mapping for the **Email** text box enter the value as `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`
5. To check the configuration you can select the **Test** button.

    Note

    For successful testing you need to complete the configuration wizard in Microsoft Entra ID and also provide access to users or groups who can perform the test.
6. Enable the SSO by checking on the **Enable SSO** button.
7. Now select the **Update** button so that all the settings are saved. This will generate the RelayState value. Copy the RelayState value, which is generated in the text box, paste it in the **Relay State** textbox under **Lifesize Cloud Domain and URLs** section.

### Create Lifesize Cloud test user

In this section, you create a user called Britta Simon in Lifesize Cloud. Lifesize cloud does support automatic user provisioning. After successful authentication at Microsoft Entra ID, the user is automatically provisioned in the application.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Lifesize Cloud Sign-on URL where you can initiate the login flow.
- Go to Lifesize Cloud Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Lifesize Cloud tile in the My Apps, this option redirects to Lifesize Cloud Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
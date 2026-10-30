---
layout: Conceptual
title: Configure SafetyCulture (formerly iAuditor) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/safety-culture-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and SafetyCulture (formerly iAuditor).
ms.topic: how-to
ms.date: 2026-06-09T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 3f0e617b-a62a-95ae-1ffb-1a226ebe799c
document_version_independent_id: 7f86a5c7-9587-cbb2-bebb-29066eae3277
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/safety-culture-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/safety-culture-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/safety-culture-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 11dee3cd-9503-0260-3946-a359bd7b2dfc
---

# Configure SafetyCulture (formerly iAuditor) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate SafetyCulture (formerly iAuditor) with Microsoft Entra ID. When you integrate SafetyCulture with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to SafetyCulture.
- Enable your users to be automatically logged in to SafetyCulture with their Microsoft Entra accounts.
- Manage your accounts in one central location.

SafetyCulture is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- [SafetyCulture paid plan](https://safetyculture.com/pricing/) - required for single sign-on.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- SafetyCulture supports **SP and IDP** initiated SSO.

## Add SafetyCulture from the gallery

To configure the integration of SafetyCulture into Microsoft Entra ID, you need to add SafetyCulture from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **SafetyCulture** in the search box.
4. Select **SafetyCulture** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for SafetyCulture

Configure and test Microsoft Entra SSO with SafetyCulture using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in SafetyCulture.

To configure and test Microsoft Entra SSO with SafetyCulture, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    - **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    - **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.]
    - **Create SafetyCulture test user** - to have a counterpart of B.Simon in SafetyCulture that's linked to the Microsoft Entra representation of user.
2. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **SafetyCulture** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic SAML Configuration.](common/edit-urls.png)
5. Go to the SafetyCulture web app:

    1. Log in to the [SafetyCulture](https://app.safetyculture.com) web app.
    2. Select your organization name on the lower-left corner of the page and select **Organization settings**.
    3. Select **Security** on the top of the page.
    4. Select **Set up** in the **Single sign-on (SSO)** box.
    5. Select **SAML**, ***not Microsoft Entra ID***, as the connection option.
    6. Perform the following steps on the below page.

        ![Screenshot shows sample SSO details from the SafetyCulture web app.](media/safety-culture-tutorial/connection-details.png)

        a. Copy **Service provider entity ID** value, paste this value into the **Identifier** text box in the **Basic SAML Configuration** section.

        b. Copy **Service provider assertion consumer service URL** value, paste this value into the **Reply URL** text box in the **Basic SAML Configuration** section.
6. Go back to the Azure portal. On the **Basic SAML Configuration** section, if you wish to configure the application in **IdP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, paste the **Service provider entity ID** from SafetyCulture.

    b. In the **Reply URL** text box, paste the **Service provider assertion consumer service URL** from SafetyCulture.
7. If you wish to configure the application in **SP** initiated mode, in the **Sign-on URL(optional)** text box, enter the **Service provider assertion consumer service URL** from SafetyCulture.
8. The SafetyCulture application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows the image of the SafetyCulture application.](common/default-attributes.png)
9. In addition to above, the SafetyCulture application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre-populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | firstname | user.givenname |
    | lastname | user.surname |
    | email | user.mail |
10. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (PEM)** and select **Download** to download the certificate and save it for the following steps.

    ![Screenshot shows the Certificate download link.](common/certificate-base64-download.png)
11. Go back to the SafetyCulture web app and select **Continue** and perform the below steps in the **Step 2: Login details** page.

    ![Screenshot shows the login details step of SafetyCulture's SSO setup.](media/safety-culture-tutorial/sso-configuration.png)

    a. In the **Login URL** textbox, paste the **Login URL** value which you copied previously.

    b. Upload the **Certificate (PEM)** you downloaded into the **Signing certificate** field.

    c. Select **Complete setup**.

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

### Create SafetyCulture test user

In this section, you create a user called Britta Simon in SafetyCulture. Work with your SafetyCulture organization's admin to add the test user. The user must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP-initiated

1. Select **Test this application**. This redirects you to the SafetyCulture Sign-on URL where you can initiate the login flow.
2. On the SafetyCulture login page, initiate the SSO login by entering the test user's email address.
3. Select **Log in with single sign-on (SSO)**.

    ![Screenshot shows the log in with SSO option on SafetyCulture.](media/safety-culture-tutorial/test-sso.png)

#### IDP-initiated

- Select **Test this application**, and you should be automatically logged in to SafetyCulture for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the SafetyCulture tile in My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IdP mode, you should be automatically logged in to SafetyCulture for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
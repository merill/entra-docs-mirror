---
layout: Conceptual
title: Configure Delivery Solutions for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/delivery-solutions-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Delivery Solutions.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 02ee39f3-554a-5ea2-bac2-24d1978a2755
document_version_independent_id: 083601f5-198b-dd74-8dec-f3b3e9740693
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/delivery-solutions-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/delivery-solutions-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/delivery-solutions-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: cc7ee979-4156-74b8-e9b7-93514e44f8bd
---

# Configure Delivery Solutions for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Delivery Solutions with Microsoft Entra ID. Delivery Solutions is an OXM platform that enables your omni channel strategy via same-day delivery, curbside, in-store pickup, shipping & post-purchase channels. When you integrate Delivery Solutions with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Delivery Solutions.
- Enable your users to be automatically signed-in to Delivery Solutions with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You'll configure and test Microsoft Entra single sign-on for Delivery Solutions in a test environment. Delivery Solutions supports both **SP** and **IDP** initiated single sign-on and **Just In Time** user provisioning.

## Prerequisites

To integrate Microsoft Entra ID with Delivery Solutions, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Delivery Solutions single sign-on (SSO) enabled subscription.

## Add application and assign a test user

Before you begin the process of configuring single sign-on, you need to add the Delivery Solutions application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the single sign-on configuration.

### Add Delivery Solutions from the Microsoft Entra gallery

Add Delivery Solutions from the Microsoft Entra application gallery to configure single sign-on with Delivery Solutions. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Delivery Solutions** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type a value using the following pattern: `<ENVIRONMENT>.portal.deliverysolutions.co`

    b. In the **Reply URL** textbox, type a URL using the following pattern: `https://<ENVIRONMENT>.api.deliverysolutions.co/authentications/saml/response/<Base64_Tenant_ID>`
6. If you wish to configure the application in **SP** initiated mode, then perform the following step:

    In the **Sign on URL** textbox, type a URL using the following pattern: `https://<ENVIRONMENT>.portal.deliverysolutions.co/#/login/saml/<Tenant_ID>`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign on URL. Contact [Delivery Solutions support team](mailto:support@deliverysolutions.co) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. Delivery Solutions application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows the image of attributes configuration.](common/default-attributes.png)
8. In addition to above, Delivery Solutions application expects few more attributes to be passed back in SAML response, which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | brandIds | user.jobtitle |
    | storeIds | user.department |
    | role | user.assignedroles |

    Note

    Please select [here](../../identity-platform/howto-add-app-roles-in-apps#app-roles-ui) to know how to configure Role in Microsoft Entra ID.
9. On the **Set-up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
10. On the **Set up Delivery Solutions** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration appropriate URL.](common/copy-configuration-urls.png)

## Configure Delivery Solutions SSO

1. Log in to your Delivery Solutions company site as an administrator.
2. Go to **Business** &gt; **Settings** &gt; **Authentication** and enable **Configure** button.

    ![Screenshot that shows the Settings and Business page.](media/delivery-solutions-tutorial/settings.png)
3. In the **SSO Configuration** page, perform the following steps:

    ![Screenshot that shows the Configuration Settings.](media/delivery-solutions-tutorial/configure.png)

    1. Select **SAML** type of SSO from the dropdown.
    2. Open the downloaded **Certificate (Base64)** into Notepad and paste the content into the **Idp Certificate** textbox.
    3. In the **Entity ID/Issuer Url** textbox, paste the **Microsoft Entra Identifier** value, which you copied previously.
    4. In the **Login URL/SSO Endpoint** textbox, paste the **Login URL**, which you copied previously.
    5. In the **Logout URL/SSO Endpoint** textbox, paste the **Logout URL**, which you copied previously.
    6. Select **User Role** from the dropdown and save the configuration.

### Create Delivery Solutions test user

In this section, a user called B.Simon is created in Delivery Solutions. Delivery Solutions supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Delivery Solutions, a new one is commonly created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Delivery Solutions Sign-on URL where you can initiate the login flow.
- Go to Delivery Solutions Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Delivery Solutions for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Delivery Solutions tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Delivery Solutions for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
---
layout: Conceptual
title: Configure Descartes for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/descartes-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Descartes.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 273f0536-3dc3-51df-919c-284b6dc9583e
document_version_independent_id: 7147286f-d1bb-3377-880b-c19b55855b7b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/descartes-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/descartes-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/descartes-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: fd6ae1a7-0e8a-67e8-9ea0-3cbeae83a2c3
---

# Configure Descartes for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Descartes with Microsoft Entra ID. The Descartes application provides logistics information services to delivery sensitive companies around the world. As an integrated suite it provides modules for various logistics business roles. When you integrate Descartes with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Descartes.
- Enable your users to be automatically signed-in to Descartes with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You'll configure and test Microsoft Entra single sign-on for Descartes in a test environment. Descartes supports both **SP** and **IDP** initiated single sign-on and also supports **Just In Time** user provisioning.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Prerequisites

To integrate Microsoft Entra ID with Descartes, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Descartes single sign-on (SSO) enabled subscription.

## Add application and assign a test user

Before you begin the process of configuring single sign-on, you need to add the Descartes application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the single sign-on configuration.

### Add Descartes from the Microsoft Entra gallery

Add Descartes from the Microsoft Entra application gallery to configure single sign-on with Descartes. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Descartes** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, the user doesn't have to perform any step as the app is already pre-integrated with Azure.
6. If you want to configure **IdP** initiated SSO, then perform the following step:

    In the **Relay State** textbox, type the URL: `https://auth.gln.com/Welcome`
7. Descartes application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows the image of attributes configuration.](common/default-attributes.png)
8. In addition to above, Descartes application expects few more attributes to be passed back in SAML response, which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | telephone | user.telephonenumber |
    | facsimiletelephonenumber | user.facsimiletelephonenumber |
    | ou | user.department |
    | assignedRoles | user.assignedroles |
    | Group | user.groups |
9. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/copy-metadataurl.png)
10. Compose a list of the Microsoft Entra groups you want the Descartes Application use for the Role-based configuration. A list of User Roles Descartes application modules can be found at https://www.gln.com/docs/Descartes_Application_User_Roles.pdf. You can find the Azure group GUIDs. Select **Download groups** from **Groups** in the Microsoft Entra admin center.

You can load this CSV file in Excel. Please select the groups that you want map to the Descartes application roles by list the ID in the first column and associating it with the Descartes Application User Role.

## Configure Descartes SSO

To configure single sign-on on **Descartes** side, you need to email the following values to the [Descartes support team](mailto:servicedesk@descartes.com). Please use the subject Microsoft Entra SSO Setup request as the subject.

1. The preferred identity domain suffix (often the same as the E-mail domain suffix).
2. The App Federation Metadata URL.
3. A list with the Microsoft Entra group GUIDs for users entitled to use the Descartes application.

Descartes will use the information in the E-mail to have the SAML SSO connection set properly on the application side.

An example of such a request below:

![Screenshot shows the example of the request.](media/descartes-tutorial/example.png)

### Create Descartes test user

In this section, a user called B.Simon is created in Descartes. Descartes supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Descartes, a new one is commonly created after authentication.

Descartes application use domain qualified usernames for your Microsoft Entra integrated users. The domain qualified usernames consist of the SAML claim subject and will always end with the domain suffix. Descartes recommends selecting your companies E-mail domain suffix all users in the domain have in common as the identity domain suffix (example B.Simon@contoso.com).

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Descartes Sign-on URL where you can initiate the login flow. Alternatively you can use a 'deep link' URL into a specific module of the Descartes application, and you be redirected to a page to provide your domain qualified username which will lead you to your Microsoft Entra login dialog.
- Go to Descartes application direct access URL provided and initiate the login flow by specifying your domain qualified username (B.Simon@contoso.com) in the application login window. This redirects the user automatically to Microsoft Entra ID.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Descartes application menu for which you set up the SSO.
- You can also use Microsoft My Apps to test the application in any mode. When you select the Descartes tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Descartes for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
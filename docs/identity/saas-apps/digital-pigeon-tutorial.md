---
layout: Conceptual
title: Configure Digital Pigeon for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/digital-pigeon-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Digital Pigeon.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: b3fd3033-cf33-83d5-4d99-4d0c981bb8b3
document_version_independent_id: 0b833091-0090-264b-8aa8-92505f5a52d8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/digital-pigeon-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/digital-pigeon-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/digital-pigeon-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
platformId: 993f8769-46a2-092f-b5f8-535188c2769b
---

# Configure Digital Pigeon for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Digital Pigeon with Microsoft Entra ID. Digital Pigeon helps creative people deliver their work, beautifully and quickly. Whatever your needs, Digital Pigeon makes sending and receiving large files seamless. When you integrate Digital Pigeon with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Digital Pigeon.
- Enable your users to be automatically signed-in to Digital Pigeon with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You'll configure and test Microsoft Entra single sign-on for Digital Pigeon in a test environment. Digital Pigeon supports both **SP** and **IDP** initiated single sign-on and also supports **Just In Time** user provisioning.

## Prerequisites

To integrate Microsoft Entra ID with Digital Pigeon, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Digital Pigeon single sign-on (SSO) enabled subscription (that is, Business or Enterprise plans)
- Digital Pigeon account owner access to the above subscription

## Add application and assign a test user

Before you begin the process of configuring single sign-on, you need to add the Digital Pigeon application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the single sign-on configuration.

### Add Digital Pigeon from the Microsoft Entra gallery

Add Digital Pigeon from the Microsoft Entra application gallery to configure single sign-on with Digital Pigeon. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Note

Please select [here](../../identity-platform/howto-add-app-roles-in-apps#app-roles-ui) to learn how to configure App Roles in Microsoft Entra ID. The Role value must be one of 'Digital Pigeon User', 'Digital Pigeon Power User', or 'Digital Pigeon Admin'. If a role claim isn't supplied, the default role is configurable in the Digital Pigeon app (`Account Settings > SSO > SAML Provisioning Settings`) by a Digital Pigeon Owner, as seen below: ![Screenshot shows how to configure SAML Provisioning Default Role.](media/digital-pigeon-tutorial/saml-default-role.png)

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Digital Pigeon** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic SAML Configuration.](common/edit-urls.png)
5. In another browser tab, log in to Digital Pigeon as an account administrator.
6. Navigate to **Account Settings &gt; SSO** and copy the **SP Entity ID** and **SP ACS URL** values.

    ![Screenshot shows Digital Pigeon SAML Service Provider Settings.](media/digital-pigeon-tutorial/saml-service-provider-settings.png)
7. Now in Microsoft Entra ID, in the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, paste the value from *Digital Pigeon &gt; Account Settings &gt; SSO &gt; **SP Entity ID***. It should match the following pattern: `https://digitalpigeon.com/saml2/service-provider-metadata/<CustomerID>`

    b. In the **Reply URL** textbox, paste the value from *Digital Pigeon &gt; Account Settings &gt; SSO &gt; **SP ACS URL***. It should match the following pattern: `https://digitalpigeon.com/login/saml2/sso/<CustomerID>`
8. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign on URL** textbox, type the URL: `https://digitalpigeon.com/login`
9. Digital Pigeon application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows the image of attributes configuration.](common/default-attributes.png)
10. In addition to above, Digital Pigeon application expects few more attributes to be passed back in SAML response, which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | user.firstName | user.givenname |
    | user.lastName | user.surname |
11. On the **Set-up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)
12. In Digital Pigeon, paste the content of downloaded **Federation Metadata XML** file into the **IDP Metadata XML** text field.

    ![Screenshot shows IDP Metadata XML.](media/digital-pigeon-tutorial/idp-metadata-xml.png)
13. In Microsoft Entra ID, on the **Set up Digital Pigeon** section, copy the Microsoft Entra Identifier URL.

    ![Screenshot shows to copy configuration appropriate U R L.](common/copy-configuration-urls.png)
14. In Digital Pigeon, paste this URL into the **IDP Entity ID** text field.

    ![Screenshot shows IDP Entity ID.](media/digital-pigeon-tutorial/idp-entity-id.png)
15. Select **Save** button to activate Digital Pigeon SSO.

### Create Digital Pigeon test user

In this section, a user called B.Simon is created in Digital Pigeon. Digital Pigeon supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Digital Pigeon, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Digital Pigeon Sign on URL where you can initiate the login flow.
- Go to Digital Pigeon Sign on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Digital Pigeon for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Digital Pigeon tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Digital Pigeon for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
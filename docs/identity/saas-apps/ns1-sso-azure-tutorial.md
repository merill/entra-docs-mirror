---
layout: Conceptual
title: Configure NS1 SSO for Azure for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/ns1-sso-azure-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and NS1 SSO for Azure.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 9d0ad66d-2d71-611e-250c-f6b2c366c45f
document_version_independent_id: 9e3c3344-c8cf-21c3-5093-9e83d0f40899
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/ns1-sso-azure-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/ns1-sso-azure-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/ns1-sso-azure-tutorial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 1d8677a9-eae3-966a-b237-e53865f48c1d
---

# Configure NS1 SSO for Azure for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate NS1 SSO for Azure with Microsoft Entra ID. When you integrate NS1 SSO for Azure with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to NS1 SSO for Azure.
- Enable your users to be automatically signed in to NS1 SSO for Azure with their Microsoft Entra accounts.
- Manage your accounts in one central location, the Azure portal.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- NS1 SSO for Azure single sign-on (SSO) enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- NS1 SSO for Azure supports SP and IDP initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add NS1 SSO for Azure from the gallery

To configure the integration of NS1 SSO for Azure into Microsoft Entra ID, you need to add NS1 SSO for Azure from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **NS1 SSO for Azure** in the search box.
4. Select **NS1 SSO for Azure** from the results panel, and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for NS1 SSO for Azure

Configure and test Microsoft Entra SSO with NS1 SSO for Azure by using a test user called **B.Simon**. For SSO to work, establish a linked relationship between a Microsoft Entra user and the related user in NS1 SSO for Azure.

Here are the general steps to configure and test Microsoft Entra SSO with NS1 SSO for Azure:

1. **Configure Microsoft Entra SSO** to enable your users to use this feature.

    a. **Create a Microsoft Entra test user** to test Microsoft Entra single sign-on with B.Simon.

    b. **Assign the Microsoft Entra test user** to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure NS1 SSO for Azure SSO** to configure the single sign-on settings on the application side.

    a. **Create an NS1 SSO for Azure test user** to have a counterpart of B.Simon in NS1 SSO for Azure. This counterpart is linked to the Microsoft Entra representation of the user.
3. **Test SSO** to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **NS1 SSO for Azure** application integration page, find the **Manage** section. Select **single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot of set up single sign-on with SAML page, with pencil icon highlighted.](common/edit-urls.png)
5. In the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** text box, type the following URL: `https://api.nsone.net/saml/metadata`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://api.nsone.net/saml/sso/<ssoid>`
6. Select **Set additional URLs**, and perform the following step if you want to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type the following URL: `https://my.nsone.net/#/login/sso`

    Note

    The Reply URL value isn't real. Update Reply URL value with the actual Reply URL. Contact the [NS1 SSO for Azure Client support team](mailto:techops@nsone.net) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. The NS1 SSO for Azure application expects the SAML assertions in a specific format. Configure the following claims for this application. You can manage the values of these attributes from the **User Attributes & Claims** section on the application integration page. On the **Set up Single Sign-On with SAML** page, select the pencil icon to open the **User Attributes** dialog box.

    ![Screenshot of User Attributes &amp; Claims section, with pencil icon highlighted.](media/ns1-sso-for-azure-tutorial/attribute-edit-option.png)
8. Select the attribute name to edit the claim.

    ![Screenshot of User Attributes &amp; Claims section, with attribute name highlighted.](media/ns1-sso-for-azure-tutorial/attribute-claim-edit.png)
9. Select **Transformation**.

    ![Screenshot of Manage claim section, with Transformation highlighted.](media/ns1-sso-for-azure-tutorial/prefix-edit.png)
10. In the **Manage transformation** section, perform the following steps:

    ![Screenshot of Manage transformation section, with various fields highlighted.](media/ns1-sso-for-azure-tutorial/prefix-added.png)

    1. Select **ExactMailPrefix()** as **Transformation**.
    2. Select **user.userprincipalname** as **Parameter 1**.
    3. Select **Add**.
    4. Select **Save**.
11. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, select the copy button. This copies the **App Federation Metadata Url** and saves it on your computer.

    ![Screenshot of the SAML Signing Certificate, with the copy button highlighted.](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure NS1 SSO for Azure SSO

To configure single sign-on on the NS1 SSO for Azure side, you need to send the App Federation Metadata URL to the [NS1 SSO for Azure support team](mailto:techops@nsone.net). They configure this setting to have the SAML SSO connection set properly on both sides.

### Create an NS1 SSO for Azure test user

In this section, you create a user called B.Simon in NS1 SSO for Azure. Work with the NS1 SSO for Azure support team to add the users in the NS1 SSO for Azure platform. You can't use single sign-on until you create and activate users.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to NS1 SSO for Azure Sign-on URL where you can initiate the login flow.
- Go to NS1 SSO for Azure Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the NS1 SSO for Azure for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the NS1 SSO for Azure tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the NS1 SSO for Azure for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
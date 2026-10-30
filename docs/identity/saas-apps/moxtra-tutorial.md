---
layout: Conceptual
title: Configure Moxtra for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/moxtra-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Moxtra.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 9ba0431d-8965-7959-ac4d-5f857a70f462
document_version_independent_id: 85239593-b691-6342-d204-72f86db319cc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/moxtra-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/moxtra-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/moxtra-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f83731d5-86e1-937d-1fc9-5e3f7be8468f
---

# Configure Moxtra for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Moxtra with Microsoft Entra ID. When you integrate Moxtra with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Moxtra.
- Enable your users to be automatically signed-in to Moxtra with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Moxtra single sign-on (SSO) enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Moxtra supports **SP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Moxtra from the gallery

To configure the integration of Moxtra into Microsoft Entra ID, you need to add Moxtra from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Moxtra** in the search box.
4. Select **Moxtra** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Moxtra

Configure and test Microsoft Entra SSO with Moxtra using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Moxtra.

To configure and test Microsoft Entra SSO with Moxtra, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Moxtra SSO**- to configure the single sign-on settings on application side.
    1. **Create Moxtra test user** - to have a counterpart of B.Simon in Moxtra that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Moxtra** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic S A M L Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following step:

    In the **Sign-on URL** text box, type the URL: `https://www.moxtra.com/service/#login`
6. Moxtra application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes. Select **Edit** icon to open User Attributes dialog.

    ![Screenshot shows the image of Moxtra application.](common/edit-attribute.png)
7. In addition to above, Moxtra application expects few more attributes to be passed back in SAML response. In the User Claims section on the User Attributes dialog, perform the following steps to add SAML token attribute as shown in the below table:

    | Name | Source Attribute |
    | --- | --- |
    | firstname | user.givenname |
    | lastname | user.surname |
    | idpid | &lt; Microsoft Entra Identifier &gt; |

    Note

    The value of **idpid** attribute isn't real. You can get the actual value from **Set up Moxtra** section from step#8.

    1. Select **Add new claim** to open the **Manage user claims** dialog.
    2. In the **Name** textbox, type the attribute name shown for that row.
    3. Leave the **Namespace** blank.
    4. Select Source as **Attribute**.
    5. From the **Source attribute** list, type the attribute value shown for that row.
    6. Select **Ok**
    7. Select **Save**.
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
9. On the **Set up Moxtra** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration appropriate U R L.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Moxtra SSO

1. In another browser window, sign on to your Moxtra company site as an administrator.
2. In the toolbar on the left, select **Admin Console &gt; SAML Single Sign-on**, and then select **New**.

    ![Screenshot shows the S A M L Single Sign-on page with the option to create a new S A M L Single Sign-on.](media/moxtra-tutorial/toolbar.png)
3. On the **SAML** page, perform the following steps:

    ![Screenshot shows the SAML page where you can enter the values described.](media/moxtra-tutorial/admin.png)

    a. In the **Name** textbox, type a name for your configuration (such as **SAML**).

    b. In the **IdP Entity ID** textbox, paste the value of **Microsoft Entra Identifier**..

    c. In **Login URL** textbox, paste the value of **Login URL**..

    d. In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.

    e. In the **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.

    f. Open certificate which you have downloaded from Azure portal in notepad, copy the content, and then paste it into the **Certificate** textbox.

    g. In the SAML email domain textbox, type your SAML email domain.

    Note

    To see the steps to verify the domain, select the "**i**" below.

    h. Select **Update**.

### Create Moxtra test user

The objective of this section is to create a user called B.simon in Moxtra.

**To create a user called B.simon in Moxtra, perform the following steps:**

1. Sign on to your Moxtra company site as an administrator.
2. In the toolbar on the left, select **Admin Console &gt; User Management**, and then **Add User**.

    ![Screenshot shows the User Management page with Add User selected.](media/moxtra-tutorial/user.png)
3. On the **Add User** dialog, perform the following steps:

    a. In the **First Name** textbox, type **B**.

    b. In the **Last Name** textbox, type **Simon**.

    c. In the **Email** textbox, type B.simon's email address same as on Azure portal.

    d. In the **Division** textbox, type **Dev**.

    e. In the **Department** textbox, type **IT**.

    f. Select **Administrator**.

    g. Select **Add**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Moxtra Sign-on URL where you can initiate the login flow.
- Go to Moxtra Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Moxtra tile in the My Apps, this option redirects to Moxtra Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
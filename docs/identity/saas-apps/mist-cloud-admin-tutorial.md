---
layout: Conceptual
title: Configure Mist Cloud Admin SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/mist-cloud-admin-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Mist Cloud Admin SSO.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 0df3ce70-acab-d5fe-84d1-e1c592a2929e
document_version_independent_id: 133f2b79-c242-0f06-0ae1-cf1562df3771
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/mist-cloud-admin-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/mist-cloud-admin-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/mist-cloud-admin-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 77c85e8e-5eec-2066-5a0a-105d96453eaa
---

# Configure Mist Cloud Admin SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Mist Cloud Admin SSO with Microsoft Entra ID. When you integrate Mist Cloud Admin SSO with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to the Mist dashboard.
- Enable your users to be automatically signed-in to the Mist dashboard with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Mist Cloud account, you can create an account [here](https://manage.mist.com/).
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Mist Cloud Admin SSO supports **SP** and **IDP** initiated SSO.

## Add Mist Cloud Admin SSO from the gallery

To configure the integration of Mist Cloud Admin SSO into Microsoft Entra ID, you need to add Mist Cloud Admin SSO from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Mist Cloud Admin SSO** in the search box.
4. Select **Mist Cloud Admin SSO** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Mist Cloud Admin SSO

Configure and test Microsoft Entra SSO with Mist Cloud Admin SSO using a test user called **B.Simon**. For SSO to work, you need to establish a link between your Microsoft Entra app and Mist organization SSO.

To configure and test Microsoft Entra SSO with Mist Cloud Admin SSO, perform the following steps:

1. **Perform initial configuration of the Mist Cloud SSO** - to generate ACS URL on the application side.
2. **Configure Microsoft Entra SSO** - to enable your users to use this feature.

    1. **Create Role for the SSO Application**
    2. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    3. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
3. **Complete configuration of the Mist Cloud**
4. **Create Roles to link roles sent by the Microsoft Entra ID**
5. **Test SSO** - to verify whether the configuration works.

## Perform Initial Configuration of the Mist Cloud SSO

1. Sign in to the Mist dashboard using a local account.
2. Go to **Organization &gt; Settings &gt; Single Sign-On &gt; Add IdP**.
3. Under **Single Sign-On** section select **Add IDP**.
4. In the **Name** field type `Azure AD` and select **Add**.

    ![Screenshot shows to add identity provider.](media/mist-cloud-admin-tutorial/identity-provider.png)
5. Copy **Reply URL** value, paste this value into the **Reply URL** text box in the **Basic SAML Configuration** section.

    ![Screenshot shows to Reply URL value.](media/mist-cloud-admin-tutorial/reply-url.png)

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Mist Cloud Admin SSO** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type a value using the following pattern: `https://api.<MISTCLOUDREGION>.mist.com/api/v1/saml/<SSOUNIQUEID>/login`

    b. In the **Reply URL** textbox, type a URL using the following pattern: `https://api.<MISTCLOUDREGION>.mist.com/api/v1/saml/<SSOUNIQUEID>/login`
6. Select **Set additional URLs** and perform the following step, if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type the URL: `https://manage.mist.com`

    Note

    These values aren't real. Update these values with the actual Identifier and Reply URL. Contact [Mist Cloud Admin SSO support team](mailto:support@mist.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. Mist Cloud Admin SSO application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows the image of attribute mappings.](common/default-attributes.png)
8. In addition to above, Mist Cloud Admin SSO application expects few more attributes to be passed back in SAML response, which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | FirstName | user.givenname |
    | LastName | user.surname |
    | Role | user.assignedroles |

    Note

    Please select [here](../../identity-platform/howto-add-app-roles-in-apps#app-roles-ui) to know how to configure Role in Microsoft Entra ID. Mist Cloud requires Role attribute to assign correct admin privileges to the user.
9. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
10. 1. On the **Set up Mist Cloud Admin SSO** section, copy the appropriate **Login URL** and **Microsoft Entra Identifier**.

    ![Screenshot shows to copy configuration appropriate URL.](common/copy-configuration-urls.png)

### Create Role for the SSO Application

In this section, you create a Superuser Role to later assign it to test user B.Simon.

1. In the Azure portal, select **App Registrations**, and then select **All Applications**.
2. In the applications list, select **Mist Cloud Admin SSO**.
3. In the app's overview page, find the **Manage** section and select **App Roles**.
4. Select **Create App Role**, then type **Mist Superuser** in the **Display Name** field.
5. Type **Superuser** in the **Value** field, then type **Mist Superuser Role** in the **Description** field, then select **Apply**.

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Complete configuration of the Mist Cloud

1. In the **Create Identity Provider** section, perform the following steps:

    ![Screenshot that shows the Organization Algorithm.](media/mist-cloud-admin-tutorial/configure-mist.png)

    1. In the **Issuer** textbox, paste the **Microsoft Entra Identifier** value which you copied previously.
    2. Open the downloaded **Certificate (Base64)** into Notepad and paste the content into the **Certificate** textbox.
    3. In the **SSO URL** textbox, paste the **Login URL** value which you copied previously.
    4. Select **Save**.

## Create Roles to link roles sent by the Microsoft Entra ID

1. In the Mist dashboard navigate to **Organization &gt; Settings**. Under **Single Sign-On** section, select **Create Role**.

    ![Screenshot that shows the Create Role section.](media/mist-cloud-admin-tutorial/create-role.png)
2. Role name must match Role claim value sent by Microsoft Entra ID, for example type `Superuser` in the **Name** field, specify desired admin privileges for the role and select **Create**.

    ![Screenshot that shows the Create Role button.](media/mist-cloud-admin-tutorial/create-button.png)

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Mist Cloud Admin SSO Sign-on URL where you can initiate the login flow.
- Go to Mist Cloud Admin SSO Sign-on URL directly and initiate the login flow from there.

    Note

    For each user first login must be performed from the IdP prior to using SP initiated flow.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Mist Cloud Admin SSO for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Mist Cloud Admin SSO tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Mist Cloud Admin SSO for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
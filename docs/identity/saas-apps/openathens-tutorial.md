---
layout: Conceptual
title: Configure OpenAthens for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/openathens-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and OpenAthens.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 1998e339-afaa-57b4-5417-a2d90fa3eb21
document_version_independent_id: b4ecd8b0-2474-060a-ecd5-3ef2abd37d60
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/openathens-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/openathens-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/openathens-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 228beac2-e90b-a27c-2032-cf2991aceade
---

# Configure OpenAthens for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate OpenAthens with Microsoft Entra ID. When you integrate OpenAthens with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to OpenAthens.
- Enable your users to be automatically signed-in to OpenAthens with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- OpenAthens single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- OpenAthens supports **IDP** initiated SSO
- OpenAthens supports **Just In Time** user provisioning

## Add OpenAthens from the gallery

To configure the integration of OpenAthens into Microsoft Entra ID, you need to add OpenAthens from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **OpenAthens** in the search box.
4. Select **OpenAthens** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for OpenAthens

Configure and test Microsoft Entra SSO with OpenAthens using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in OpenAthens.

To configure and test Microsoft Entra SSO with OpenAthens, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    - **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    - **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure OpenAthens SSO**- to configure the single sign-on settings on application side.
    - **Create OpenAthens test user** - to have a counterpart of B.Simon in OpenAthens that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **OpenAthens** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, upload the **Service Provider metadata file**, the steps for which are mentioned later in this article.

    a. Select **Upload metadata file**.

    ![openathens upload metadata](common/upload-metadata.png)

    b. Select **folder logo** to select the metadata file and select **Upload**.

    ![Openathens browse upload metadata](common/browse-upload-metadata.png)

    c. Once the metadata file is successfully uploaded, the **Identifier** value get auto populated in **Basic SAML Configuration** section textbox:

    ![OpenAthens Domain and URLs single sign-on information](common/idp-identifier.png)
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up OpenAthens** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure OpenAthens SSO

1. In a different web browser window, sign in to your OpenAthens company site as an administrator.
2. Select **Connections** from the list under the **Management** tab.
3. Select **SAML 1.1/2.0**, and then select the **Configure** button.

    ![Screenshot that shows the &quot;Select local authentication system type.&quot; dialog with &quot;S A M L 1.1/2.0&quot; and the &quot;Configure&quot; button selected.](media/openathens-tutorial/saml.png)
4. To add the configuration, select the **Browse** button to upload the metadata .xml file that you downloaded, and then select **Add**.

    ![Screenshot that shows the &quot;Add S A M L authentication system.&quot; dialog with the &quot;Browse&quot; action and &quot;Add button selected.](media/openathens-tutorial/configure.png)
5. Perform the following steps under the **Details** tab.

    ![Configure single sign-on](media/openathens-tutorial/add.png)

    a. In **Display name mapping**, select **Use attribute**.

    b. In the **Display name attribute** text box, enter the value `http://schemas.microsoft.com/identity/claims/displayname`.

    c. In **Unique user mapping**, select **Use attribute**.

    d. In the **Unique user attribute** text box, enter the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.

    e. In **Status**, select all the three check boxes.

    f. In **Create local accounts**, select **automatically**.

    g. Select **Save changes**.

    h. From the **&lt;/&gt; Relying Party** tab, copy the **Metadata URL** and open this in the browser to download the **SP metadata XML** file. Upload this SP metadata file on the **Basic SAML Configuration** section in Microsoft Entra ID.

    ![Screenshot that shows the &quot;Relying party&quot; tab selected and the &quot;Metadata U R L&quot; highlighted.](media/openathens-tutorial/metadata.png)

### Create OpenAthens test user

In this section, a user called Britta Simon is created in OpenAthens. OpenAthens supports **just-in-time user provisioning**, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in OpenAthens, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the OpenAthens for which you set up the SSO.
- You can use Microsoft My Apps. When you select the OpenAthens tile in the My Apps, you should be automatically signed in to the OpenAthens for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
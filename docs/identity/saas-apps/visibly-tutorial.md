---
layout: Conceptual
title: Configure Visibly for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/visibly-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Visibly.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: d85db35a-7812-7f7c-ce7a-1c818003c464
document_version_independent_id: f7c0a3bc-1176-d99b-c8cb-2370c78bfa51
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/visibly-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/visibly-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/visibly-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c870e10b-e017-ec62-934f-693a8259f5a8
---

# Configure Visibly for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Visibly with Microsoft Entra ID. When you integrate Visibly with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Visibly.
- Enable your users to be automatically signed-in to Visibly with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Visibly single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Visibly supports **SP** initiated SSO.
- Visibly supports [Automated user provisioning](visibly-provisioning-tutorial).

## Add Visibly from the gallery

To configure the integration of Visibly into Microsoft Entra ID, you need to add Visibly from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Visibly** in the search box.
4. Select **Visibly** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Visibly

Configure and test Microsoft Entra SSO with Visibly using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Visibly.

To configure and test Microsoft Entra SSO with Visibly, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Visibly SSO**- to configure the single sign-on settings on application side.
    1. **Create Visibly test user** - to have a counterpart of B.Simon in Visibly that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Visibly** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    a. In the **Sign-on URL** text box, type the URL: `https://app.visibly.io/`

    b. In the **Reply URL** text box, type the URL: `https://api.visibly.io/api/v1/verifyResponse`
6. Visibly application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
7. In addition to above, Visibly application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | city | user.city |
    | lastName | user.surname |
    | state | user.state |
    | department | user.department |
    | email | user.mail |
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
9. On the **Set up Visibly** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Visibly SSO

1. Sign in to Visibly using your credentials.
2. Navigate to the **Settings** option from the navigation menu.

    ![Screenshot shows the settings option selected.](media/visibly-tutorial/settings.png)
3. Select **Integrations** within Settings.

    ![Screenshot shows Integrations selected from the Settings menu.](media/visibly-tutorial/integrations.png)
4. In the **Integrations**, select **SSO**.

    ![Screenshot shows S S O selected from the Integrations.](media/visibly-tutorial/sso.png)
5. Perform the following steps in the following page.

    ![Screenshot shows S S O Integration page where you can enter the values described.](media/visibly-tutorial/configuration.png)

    a. In the **Entity ID** textbox, paste the **Entity ID** value which you copied previously.

    b. In the **SSO url** textbox, paste the **Login URL** value which you copied previously.

    c. In the **SSO name** textbox, give any valid name.

    d. Open the downloaded **Certificate (Base64)** into Notepad and paste the content into the **Certificate** textbox or you can also upload the **Certificate** by selecting the **Upload Certificate**.

    e. Select **Save**.

### Create Visibly test user

In this section, a user called B.Simon is created in Visibly. Visibly supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Visibly, a new one is created after authentication.

Visibly also supports automatic user provisioning, you can find more details [here](visibly-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application** in Azure portal. this option redirects to Visibly Sign-on URL where you can initiate the login flow.
- Go to Visibly Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Visibly tile in the My Apps, this option redirects to Visibly Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
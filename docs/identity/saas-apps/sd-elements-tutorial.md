---
layout: Conceptual
title: Configure SD Elements for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/sd-elements-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and SD Elements.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 69611e2c-6f0d-a30d-7f94-d5d5b2809a2a
document_version_independent_id: 0077bed4-4d82-e2df-52e0-fb669d964b1f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/sd-elements-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/sd-elements-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/sd-elements-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c9de1581-f7a0-7f1b-2dea-ddd83c337275
---

# Configure SD Elements for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate SD Elements with Microsoft Entra ID. When you integrate SD Elements with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to SD Elements.
- Enable your users to be automatically signed-in to SD Elements with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- SD Elements single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- SD Elements supports **IDP** initiated SSO.

## Add SD Elements from the gallery

To configure the integration of SD Elements into Microsoft Entra ID, you need to add SD Elements from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **SD Elements** in the search box.
4. Select **SD Elements** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for SD Elements

Configure and test Microsoft Entra SSO with SD Elements using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in SD Elements.

To configure and test Microsoft Entra SSO with SD Elements, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure SD Elements SSO**- to configure the single sign-on settings on application side.
    1. **Create SD Elements test user** - to have a counterpart of B.Simon in SD Elements that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **SD Elements** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Set up single sign-on with SAML** page, perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://<TENANT_NAME>.sdelements.com/sso/saml2/metadata`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<TENANT_NAME>.sdelements.com/sso/saml2/acs/`

    Note

    These values aren't real. Update these values with the actual Identifier and Reply URL. Contact [SD Elements Client support team](mailto:support@sdelements.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. SD Elements application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
7. In addition to above, SD Elements application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | email | user.mail |
    | firstname | user.givenname |
    | lastname | user.surname |
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
9. On the **Set up SD Elements** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure SD Elements SSO

1. To get single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with the downloaded certificate file.
2. In a different browser window, sign-on to your SD Elements tenant as an administrator.
3. In the menu on the top, select **System**, and then **Single Sign-on**.

    ![Screenshot that shows &quot;System&quot; selected and &quot;Single Sign-on&quot; selected from the drop-down.](media/sd-elements-tutorial/system.png)
4. On the **Single Sign-On Settings** dialog, perform the following steps:

    ![Configure Single Sign-On](media/sd-elements-tutorial/settings.png)

    a. As **SSO Type**, select **SAML**.

    b. In the **Identity Provider Entity ID** textbox, paste the value of **Microsoft Entra Identifier**.

    c. In the **Identity Provider Single Sign-On Service** textbox, paste the value of **Login URL**.

    d. Select **Save**.

### Create SD Elements test user

The objective of this section is to create a user called B.Simon in SD Elements. In the case of SD Elements, creating SD Elements users is a manual task.

**To create B.Simon in SD Elements, perform the following steps:**

1. In a web browser window, sign-on to your SD Elements company site as an administrator.
2. In the menu on the top, select **User Management**, and then **Users**.

    ![Screenshot that shows &quot;Users&quot; selected from the &quot;User Management&quot; drop-down.](media/sd-elements-tutorial/users.png)
3. Select **Add New User**.

    ![Screenshot that shows the &quot;Add New User&quot; button selected.](media/sd-elements-tutorial/add-user.png)
4. On the **Add New User** dialog, perform the following steps:

    ![Creating a SD Elements test user](media/sd-elements-tutorial/new-user.png)

    a. In the **E-mail** textbox, enter the email of user like **b.simon@contoso.com**.

    b. In the **First Name** textbox, enter the first name of user like **B.**.

    c. In the **Last Name** textbox, enter the last name of user like **Simon**.

    d. As **Role**, select **User**.

    e. Select **Create User**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the SD Elements for which you set up the SSO.
- You can use Microsoft My Apps. When you select the SD Elements tile in the My Apps, you should be automatically signed in to the SD Elements for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
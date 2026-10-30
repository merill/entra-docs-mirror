---
layout: Conceptual
title: Configure Kion (formerly cloudtamer.io) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/cloudtamer-io-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Kion (formerly cloudtamer.io).
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: adc3b40e-a630-f393-9f79-fefa53d5758f
document_version_independent_id: 10930e4c-543e-a4b5-290a-eedc2406ee21
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/cloudtamer-io-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/cloudtamer-io-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/cloudtamer-io-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ee88c8d3-eaab-3828-ea7c-152321daeac9
---

# Configure Kion (formerly cloudtamer.io) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Kion with Microsoft Entra ID. When you integrate Kion with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Kion.
- Enable your users to be automatically signed-in to Kion with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Kion single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Kion supports **IDP** initiated SSO.
- Kion supports **Just In Time** user provisioning.

## Add Kion (formerly cloudtamer.io) from the gallery

To configure the integration of Kion into Microsoft Entra ID, you need to add Kion from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Kion** in the search box.
4. Select **Kion** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Kion (formerly cloudtamer.io)

Configure and test Microsoft Entra SSO with Kion using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Kion.

To configure and test Microsoft Entra SSO with Kion, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Kion SSO**- to configure the single sign-on settings on application side.
    1. **Create Kion test user** - to have a counterpart of B.Simon in Kion that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.
4. **Group assertions** - to set group assertions for Microsoft Entra ID and Kion.

### Begin Kion SSO Configuration

1. Log in to Kion website as an administrator.
2. Select **+** plus icon at the top right corner and select **IDMS**.

    ![Screenshot for IDMS create.](media/cloudtamer-io-tutorial/idms-creation.png)
3. Select **SAML 2.0** as the IDMS Type.
4. Leave this screen open and copy values from this screen into the Microsoft Entra configuration.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Kion** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** text box, paste the **SERVICE PROVIDER ISSUER (ENTITY ID)** from Kion into this box.

    b. In the **Reply URL** text box, paste the **SERVICE PROVIDER ACS URL** from Kion into this box.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up Kion** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Kion SSO

1. Perform the following steps in the **Add IDMS** page:

    ![Screenshot for IDMS adding.](media/cloudtamer-io-tutorial/configuration.png)

    a. In the **IDMS Name** give a name that the users will recognize from the Login screen.

    b. In the **IDENTITY PROVIDER ISSUER (ENTITY ID)** textbox, paste the **Identifier** value which you copied previously.

    c. Open the downloaded **Federation Metadata XML** into Notepad and paste the content into the **IDENTITY PROVIDER METADATA** textbox.

    d. Copy **SERVICE PROVIDER ISSUER (ENTITY ID)** value, paste this value into the **Identifier** text box in the Basic SAML Configuration section.

    e. Copy **SERVICE PROVIDER ACS URL** value, paste this value into the **Reply URL** text box in the Basic SAML Configuration section.

    f. Under Assertion Mapping, enter the following values:

    | Field | Value |
    | --- | --- |
    | First Name | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname` |
    | Last Name | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname` |
    | Email | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name` |
    | Username | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name` |
2. Select **Create IDMS**.

### Create Kion test user

In this section, a user called Britta Simon is created in Kion. Kion supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Kion, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the Kion for which you set up the SSO.
- You can use Microsoft My Apps. When you select the Kion tile in the My Apps, you should be automatically signed in to the Kion for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).

## Group assertions

To easily manage Kion user permissions by using existing Microsoft Entra groups, complete these steps:

### Microsoft Entra configuration

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. In the list, select the enterprise application for Kion.
4. On **Overview**, in the left menu, select **Single sign-on**.
5. On **Single Sign-On**, under **User Attributes & Claims**, select **Edit**.
6. Select **Add a group claim**. 
    Note

    You can have only one group claim. If this option is disabled, you might already have a group claim defined.
7. On **Group Claims**, select the groups that should be returned in the claim:
    - If you always have every group you intend to use in Kion assigned to this enterprise application, select **Groups assigned to the application**.
    - If you want all groups to appear (this selection can cause a large number of group assertions and might be subject to limits), select **Groups assigned to the application**.
8. For **Source attribute**, leave the default **Group ID**.
9. Select the **Customize the name of the group claim** checkbox.
10. For **Name**, enter **memberOf**.
11. Select **Save** to complete the configuration with Microsoft Entra ID.

### Kion configuration

1. In Kion, go to **Users** &gt; **Identity Management Systems**.
2. Select the IDMS that you've created for Microsoft Entra ID.
3. On the overview page, select the **User Group Associations** tab.
4. For each user group mapping that you want, complete these steps:
    1. Select **Add** &gt; **Add New**.
    2. In the dialog that appears:
        1. For **Name**, enter **memberOf**.
        2. For **Regex**, enter the object ID (from Microsoft Entra ID) of the group you want to match.
        3. For **User Group**, select the Kion internal group you want to map to the group in **Regex**.
        4. Select the **Update on Login** checkbox.
    3. Select **Add** to add the group association.
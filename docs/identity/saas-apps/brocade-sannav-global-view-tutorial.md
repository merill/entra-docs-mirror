---
layout: Conceptual
title: Configure Brocade SANnav Global View for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/brocade-sannav-global-view-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Brocade SANnav Global View.
ms.topic: how-to
ms.date: 2026-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1012
ai-usage: ai-assisted
locale: en-us
document_id: a5d13582-b694-3305-70ac-b04a5a18e151
document_version_independent_id: a5d13582-b694-3305-70ac-b04a5a18e151
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/brocade-sannav-global-view-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/brocade-sannav-global-view-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/brocade-sannav-global-view-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 57dc13e7-f222-e149-308d-73f9e68b2cfb
---

# Configure Brocade SANnav Global View for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Brocade SANnav Global View with Microsoft Entra ID. When you integrate Brocade SANnav Global View with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Brocade SANnav Global View.
- Enable your users to be automatically signed-in to Brocade SANnav Global View with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- SANnav Global View application installed with a valid subscription license.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Brocade SANnav Global View supports both **SP and IDP** initiated SSO.

## Add Brocade SANnav Global View from the gallery

To configure the integration of Brocade SANnav Global View into Microsoft Entra ID, you need to add Brocade SANnav Global View from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Brocade SANnav Global View** in the search box.
4. Select **Brocade SANnav Global View** from the results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Brocade SANnav Global View

Configure and test Microsoft Entra SSO with Brocade SANnav Global View using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra group(s) and a Brocade Global view group.

To configure and test Microsoft Entra SSO with Brocade SANnav Global View, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Create SANnav Group and assign the user to the group** - to enable B.Simon to use Microsoft Entra single sign-on. Add importing the SANnav Global View metadata file.
2. **Configure Brocade SANnav Global View SSO**- to configure the single sign-on settings on application side.
    1. **Create Brocade SANnav Global View groups** - Assume B. Simon is part of the "SANnav Administrator" group in Microsoft Entra. Add importing the Microsoft Entra metadata.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Brocade SANnav Global View** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you have **Service Provider metadata file**, then perform the following steps:

    a. Select **Upload metadata file**.

    ![Screenshot shows how to upload metadata file.](common/upload-metadata.png)

    b. Select **folder logo** to select the metadata file and select **Upload**.

    ![Screenshot shows how to choose metadata file.](common/browse-upload-metadata.png)

    c. After the metadata file is successfully uploaded, the **Identifier** and **Reply URL** values get auto populated in **Basic SAML Configuration** section.

    Note

    You get the **Service Provider metadata file** from the **Configure Brocade SANnav Global View SSO** section, which is explained later in the article. If the **Identifier** and **Reply URL** values don't get auto populated, then fill in the values manually according to your requirement.
6. Brocade SANnav Global View application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows user attributes and claims with default values.](common/default-attributes.png)
7. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)

### Create a Microsoft Entra test user

In this section, you create a test user in the Microsoft Entra admin center called B.Simon.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **New user** &gt; **Create new user**, at the top of the screen.
4. In the **User**properties, follow these steps:
    1. In the **Display name** field, enter `B.Simon`.
    2. In the **User principal name** field, enter the username@companydomain.extension. For example, `B.Simon@contoso.com`.
    3. Select the **Show password** check box, and then write down the value that's displayed in the **Password** box.
    4. Select **Review + create**.
5. Select **Create**.

### Create SANnav Group and assign the user to the group

In this section, you enable B.Simon to use Microsoft Entra single sign-on by granting access to Brocade SANnav Global View.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Brocade SANnav Global View**.
3. In the app's overview page, select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Add Assignment**dialog.
    1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then select the **Select** button at the bottom of the screen.
    2. If you're expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
    3. In the **Add Assignment** dialog, select the **Assign** button.

## Configure Brocade SANnav Global View SSO

1. Log in to your Brocade SANnav Global View company site as an administrator.
2. Go to **SANnav** tab and perform the following steps in the SANnav Authentication and Authorization page:

    ![Screenshot shows settings of Identity Provider configuration.](media/brocade-sannav-global-view-tutorial/settings.png)

    1. Select Primary Authentication as **SAML**.
    2. Select **Import** to upload the downloaded **Federation Metadata XML** file from Microsoft Entra admin center.
    3. Select **Enable**.
3. Navigate to **SAML Service Provider (SP)** and select **Download the Service Provider Metadata XML** file and upload it in the **Basic SAML Configuration** section in Microsoft Entra admin center.

    ![Screenshot shows settings of Service Provider Metadata.](media/brocade-sannav-global-view-tutorial/values.png)

### Create Brocade SANnav Global View groups

In this section, you create a group called "SANnav\_Group" in the Brocade SANnav Global View as shown in the below screenshot.

![Screenshot shows how to create groups in brocade.](media/brocade-sannav-global-view-tutorial/groups.png)

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application** in Microsoft Entra admin center. this option redirects to Brocade SANnav Global View Sign-on URL where you can initiate the login flow.
- Go to Brocade SANnav Global View Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application** in Microsoft Entra admin center and you should be automatically signed in to the Brocade SANnav Global View for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Brocade SANnav Global View tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Brocade SANnav Global View for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
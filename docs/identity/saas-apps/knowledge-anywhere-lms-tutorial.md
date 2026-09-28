---
layout: Conceptual
title: Configure Knowledge Anywhere LMS for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/knowledge-anywhere-lms-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Knowledge Anywhere LMS.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: ed8e381d-99e5-06a5-4ac9-f697abd95178
document_version_independent_id: 57f4c63c-58a0-f5ff-0588-fd229d38f402
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/knowledge-anywhere-lms-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/knowledge-anywhere-lms-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/knowledge-anywhere-lms-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c5a7f2b4-5208-dbfc-0ce9-7ae88d70d2ac
---

# Configure Knowledge Anywhere LMS for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Knowledge Anywhere LMS with Microsoft Entra ID. When you integrate Knowledge Anywhere LMS with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Knowledge Anywhere LMS.
- Enable your users to be automatically signed-in to Knowledge Anywhere LMS with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Knowledge Anywhere LMS single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Knowledge Anywhere LMS supports **SP** initiated SSO.
- Knowledge Anywhere LMS supports **Just In Time** user provisioning.

## Add Knowledge Anywhere LMS from the gallery

To configure the integration of Knowledge Anywhere LMS into Microsoft Entra ID, you need to add Knowledge Anywhere LMS from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Knowledge Anywhere LMS** in the search box.
4. Select **Knowledge Anywhere LMS** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Knowledge Anywhere LMS

Configure and test Microsoft Entra SSO with Knowledge Anywhere LMS using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Knowledge Anywhere LMS.

To configure and test Microsoft Entra SSO with Knowledge Anywhere LMS, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Knowledge Anywhere LMS SSO**- to configure the single sign-on settings on application side.
    1. **Create Knowledge Anywhere LMS test user** - to have a counterpart of B.Simon in Knowledge Anywhere LMS that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Knowledge Anywhere LMS** application integration page, find the **Manage** section and select **Single sign-on**.
3. On the **Select a Single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    1. In the **Identifier** text box, type a URL using the following pattern: `https://<CLIENT_NAME>.knowledgeanywhere.com/`
    2. In the **Reply URL** text box, type a URL using the following pattern: `https://<CLIENT_NAME>.knowledgeanywhere.com/SSO/SAML/Response.aspx?<IDP_NAME>`

    Note

    These values aren't real. Update these values with the actual Identifier and Reply URL which is explained later in the article.
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<CLIENTNAME>.knowledgeanywhere.com/`

    Note

    The Sign-on URL value isn't real. Update this value with the actual Sign-on URL. Contact [Knowledge Anywhere LMS Client support team](https://knowany.zendesk.com/hc/en-us/articles/360000469034-SAML-2-0-Single-Sign-On-SSO-Set-Up-Guide) to get this value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
8. On the **Set up Knowledge Anywhere LMS** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Knowledge Anywhere LMS SSO

1. In a different web browser window, sign in to your Knowledge Anywhere LMS company site as an administrator
2. Select the **Site** tab.

    ![Screenshot shows the Site tab.](media/knowledge-anywhere-lms-tutorial/site.png)
3. Select the **SAML Settings** tab.

    ![Screenshot shows the Knowledge anywhere page with SAML Settings selected.](media/knowledge-anywhere-lms-tutorial/settings.png)
4. Select the **Add New**.

    ![Screenshot shows the Add New button in Service Provider Settings.](media/knowledge-anywhere-lms-tutorial/add-settings.png)
5. On the **Add/Update SAML Settings** page, perform the following steps:

    ![Screenshot shows the Add/Update SAML Settings page where you can make the changes described here.](media/knowledge-anywhere-lms-tutorial/update-settings.png)

    a. Enter the IDP Name as per your organization. For ex:- `Azure`.

    b. In the **IDP Entity ID** textbox, paste **Microsoft Entra Identifier** value ,which you have copied from Azure portal.

    c. In the **IDP URL** textbox, paste **Login URL** value.

    d. Open the downloaded certificate file into notepad, copy the content of the certificate and paste it into **Certificate** textbox.

    e. In the **Logout URL** textbox, paste **Logout URL** value.

    f. Select **Main Site** from the dropdown for the **Domain**.

    g. Copy the **SP Entity ID** value and paste it into **Identifier** text box in the **Basic SAML Configuration** section.

    h. Copy the **SP Response(ACS) URL** value and paste it into **Reply URL** text box in the **Basic SAML Configuration** section.

    i. Select **Save**.

### Create Knowledge Anywhere LMS test user

In this section, a user called B. Simon is created in Knowledge Anywhere LMS. Knowledge Anywhere LMS supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Knowledge Anywhere LMS, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Knowledge Anywhere LMS Sign-on URL where you can initiate the login flow.
- Go to Knowledge Anywhere LMS Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Knowledge Anywhere LMS tile in the My Apps, this option redirects to Knowledge Anywhere LMS Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
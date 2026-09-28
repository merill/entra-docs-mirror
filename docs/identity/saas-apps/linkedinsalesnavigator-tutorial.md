---
layout: Conceptual
title: Configure LinkedIn Sales Navigator for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/linkedinsalesnavigator-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and LinkedIn Sales Navigator.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: f29b5edb-b905-8807-cb63-69cda5991af0
document_version_independent_id: da4951cf-48d6-4e13-b75a-d184a70561d1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/linkedinsalesnavigator-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/linkedinsalesnavigator-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/linkedinsalesnavigator-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/aec7dc3e-0dad-4b82-accf-63218d8767d5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f260444a-7ec6-4768-8e41-ad2438092724
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 8ca5a1cb-fbf9-62bb-a79f-ae5278673963
---

# Configure LinkedIn Sales Navigator for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate LinkedIn Sales Navigator with Microsoft Entra ID. When you integrate LinkedIn Sales Navigator with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to LinkedIn Sales Navigator.
- Enable your users to be automatically signed-in to LinkedIn Sales Navigator with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- LinkedIn Sales Navigator single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- LinkedIn Sales Navigator supports **SP and IDP** initiated SSO.
- LinkedIn Sales Navigator supports **Just In Time** user provisioning.
- LinkedIn Sales Navigator supports **Automated** user provisioning.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add LinkedIn Sales Navigator from the gallery

To configure the integration of LinkedIn Sales Navigator into Microsoft Entra ID, you need to add LinkedIn Sales Navigator from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **LinkedIn Sales Navigator** in the search box.
4. Select **LinkedIn Sales Navigator** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for LinkedIn Sales Navigator

Configure and test Microsoft Entra SSO with LinkedIn Sales Navigator using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in LinkedIn Sales Navigator.

To configure and test Microsoft Entra SSO with LinkedIn Sales Navigator, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure LinkedIn Sales Navigator SSO**- to configure the single sign-on settings on application side.
    1. **Create LinkedIn Sales Navigator test user** - to have a counterpart of B.Simon in LinkedIn Sales Navigator that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **LinkedIn Sales Navigator** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, enter the **Entity ID** value, you copy Entity ID value from the Linkedin Portal explained later in this article.

    b. In the **Reply URL** text box, enter the **Assertion Consumer Access (ACS) Url** value, you copy Assertion Consumer Access (ACS) URL value from the Linkedin Portal explained later in this article.
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`
7. LinkedIn Sales Navigator application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
8. In addition to above, LinkedIn Sales Navigator application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | email | user.mail |
    | department | user.department |
    | firstname | user.givenname |
    | lastname | user.surname |
    | Unique User Identifier | user.mail |
9. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
10. On the **Set up LinkedIn Sales Navigator** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure LinkedIn Sales Navigator SSO

1. In a different web browser window, sign-on to your **LinkedIn Sales Navigator** website as an administrator.
2. In **Account Center**, select **Global Settings** under **Settings**. Also, select **Sales Navigator** from the dropdown list.

    ![Screenshot shows the Application Settings where you can select Sales Navigator.](media/linkedinsalesnavigator-tutorial/settings.png)
3. Select **OR Select Here to load and copy individual fields from the form** and perform the following steps:

    ![Screenshot shows Single Sign-On where you can enter the values described.](media/linkedinsalesnavigator-tutorial/values.png)

    a. Copy **Entity Id** and paste it into the **Identifier** text box in the **Basic SAML Configuration**.

    b. Copy **Assertion Consumer Access (ACS) Url** and paste it into the **Reply URL** text box in the **Basic SAML Configuration**.
4. Go to **LinkedIn Admin Settings** section. Upload the XML file that you have downloaded by selecting the **Upload XML file** option.

    ![Screenshot shows Configure the LinkedIn service provider S S O settings where you can upload an X M L file.](media/linkedinsalesnavigator-tutorial/metadata.png)
5. Select **On** to enable SSO. SSO status changes from **Not Connected** to **Connected**

    ![Screenshot shows Single Sign-On where you can enable Authenticate users with S S O.](media/linkedinsalesnavigator-tutorial/authentication.png)

### Create LinkedIn Sales Navigator test user

Linked Sales Navigator Application supports Just in Time (JIT) user provisioning and after authentication users are created in the application automatically. Activate **Automatically assign licenses** to assign a license to the user.

![Creating a Microsoft Entra test user](media/linkedinsalesnavigator-tutorial/provisioning.png)

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to LinkedIn Sales Navigator Sign on URL where you can initiate the login flow.
- Go to LinkedIn Sales Navigator Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the LinkedIn Sales Navigator for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the LinkedIn Sales Navigator tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the LinkedIn Sales Navigator for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
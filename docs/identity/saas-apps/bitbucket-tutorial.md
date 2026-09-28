---
layout: Conceptual
title: Configure SAML SSO for Bitbucket by resolution GmbH for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/bitbucket-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and SAML SSO for Bitbucket by resolution GmbH.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 4cb58bf6-f2b0-c9b4-c4e1-fbb3e289cb3f
document_version_independent_id: f9ce6748-093e-a315-d019-0e00607ace00
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/bitbucket-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/bitbucket-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/bitbucket-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 1aa4e34c-ed5e-836d-0692-7214bd0a9079
---

# Configure SAML SSO for Bitbucket by resolution GmbH for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate SAML SSO for Bitbucket by resolution GmbH with Microsoft Entra ID. When you integrate SAML SSO for Bitbucket by resolution GmbH with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access toSAML SSO for Bitbucket by resolution GmbH.
- Enable your users to be automatically signed in toSAML SSO for Bitbucket by resolution GmbH with their Microsoft Entra accounts.
- Manage your accounts in one central location: the Azure portal.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- SAML SSO for Bitbucket by resolution GmbH single sign-on enabled subscription

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- SAML SSO for Bitbucket by resolution GmbH supports **SP and IDP** initiated SSO
- SAML SSO for Bitbucket by resolution GmbH supports **Just In Time** user provisioning

## Add SAML SSO for Bitbucket by resolution GmbH from the gallery

To configure the integration of SAML SSO for Bitbucket by resolution GmbH into Microsoft Entra ID, you need to add SAML SSO for Bitbucket by resolution GmbH from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **SAML SSO for Bitbucket by resolution GmbH** in the search box.
4. Select **SAML SSO for Bitbucket by resolution GmbH** from the results, and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for SAML SSO for Bitbucket by resolution GmbH

Configure and test Microsoft Entra SSO with SAML SSO for Bitbucket by resolution GmbH, by using a test user called **B.Simon**. For SSO to work, you need to establish a linked relationship between a Microsoft Entra user and the related user in SAML SSO for Bitbucket by resolution GmbH.

To configure and test Microsoft Entra SSO with SAML SSO for Bitbucket by resolution GmbH, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with Britta Simon.
    2. **Assign the Microsoft Entra test user** - to enable Britta Simon to use Microsoft Entra single sign-on.
2. **Configure SAML SSO for Bitbucket by resolution GmbH SSO**- to configure the Single Sign-On settings on application side.
    1. **Create SAML SSO for Bitbucket by resolution GmbH test user** - to have a counterpart of Britta Simon in SAML SSO for Bitbucket by resolution GmbH that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

In this section, you enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **SAML SSO for Bitbucket by resolution GmbH** application integration page, find the **Manage** section and select **Single Sign-On**.
3. On the **Select a Single Sign-On Method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`

    c. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [SAML SSO for Bitbucket by resolution GmbH Client support team](https://marketplace.atlassian.com/apps/1217045/saml-single-sign-on-sso-bitbucket?hosting=server&amp;tab=support) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure SAML SSO for Bitbucket by resolution GmbH SSO

1. Sign-on to your SAML SSO for Bitbucket by resolution GmbH company site as administrator.
2. On the right side of the main toolbar, select **Settings**.
3. Go to ACCOUNTS section, select **SAML SingleSignOn** on the Menubar.

    ![The Samlsingle](media/bitbucket-tutorial/tutorial_bitbucket_samlsingle.png)
4. On the **SAML SIngleSignOn Plugin Configuration page**, select **Add IdP**.
5. On the **Choose your SAML Identity Provider** Page, enter your IdP Type, Name and Description in the provided fields:

    a. Select **IdP Type** as **Microsoft Entra ID**.

    b. In the **Name** textbox, type the name.

    c. In the **Description** textbox, type the description.

    d. Select **Next**.
6. On the **Identity provider configuration** page, select **Next**.
7. On the **Import SAML IdP Metadata** Page, select **Load File** to upload the **METADATA XML** file which you have downloaded previously.
8. Select **Next**.
9. Select **Save settings**.

    ![The save](media/bitbucket-tutorial/tutorial_bitbucket_save.png)

## Create SAML SSO for Bitbucket by resolution GmbH test user

The objective of this section is to create a user called Britta Simon in SAML SSO for Bitbucket by resolution GmbH. SAML SSO for Bitbucket by resolution GmbH supports just-in-time provisioning and also users can be created manually, contact [SAML SSO for Bitbucket by resolution GmbH Client support team](https://marketplace.atlassian.com/plugins/com.resolution.atlasplugins.samlsso-bitbucket/server/support) as per your requirement.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to SAML SSO for Bitbucket by resolution GmbH Sign on URL where you can initiate the login flow.
- Go to SAML SSO for Bitbucket by resolution GmbH Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the SAML SSO for Bitbucket by resolution GmbH for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the SAML SSO for Bitbucket by resolution GmbH tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the SAML SSO for Bitbucket by resolution GmbH for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
---
layout: Conceptual
title: Configure Miro for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/miro-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Miro.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: d33723bd-5c1d-6d4a-4a70-efae1fd4dbf4
document_version_independent_id: 27a624fa-e38f-5ff5-a380-7354f4c83b4e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/miro-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/miro-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/miro-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f530e01a-888f-395f-28f1-d7bcd37560ab
---

# Configure Miro for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Miro with Microsoft Entra ID. Another version of this article can be found at help.miro.com. When you integrate Miro with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Miro.
- Enable your users to be automatically signed-in to Miro with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Miro single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Miro supports **SP and IDP** initiated SSO and supports **Just In Time** user provisioning.
- Miro supports [**Automated** user provisioning and deprovisioning](miro-provisioning-tutorial) (recommended).

## Add Miro from the gallery

To configure the integration of Miro into Microsoft Entra ID, you need to add Miro from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Miro** in the search box.
4. Select **Miro** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Miro

Configure and test Microsoft Entra SSO with Miro using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Miro.

To configure and test Microsoft Entra SSO with Miro, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Miro SSO**- to configure the single sign-on settings on application side.
    1. **Create Miro test user** - to have a counterpart of B.Simon in Miro that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Miro** application integration page, find the **Manage** section and select **Single sign-on**.
3. On the **Select a Single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following step:

    a. In the **Identifier** text box, type one of the following URL/pattern:

    | **Identifier** |
    | --- |
    | `https://miro.com/` |
    | `https://<SUBDOMAIN>.miro.com/<ORG_ID>/<SAMLSETTINGS_ID>` |
    | `https://miro.com/<ORG_ID>/<SAMLSETTINGS_ID>` |
    | `https://<SUBDOMAIN>.miro.com/<ORG_ID>` |

    b. In the **Reply URL** text box, type one of the following URL/pattern:

    | **Reply URL** |
    | --- |
    | `https://miro.com/sso/saml` |
    | `https://<SUBDOMAIN>.miro.com/sso/saml/<ORG_ID>` |
    | `https://miro.com/sso/saml/<ORG_ID>/<SAMLSETTINGS_ID>` |
    | `https://<SUBDOMAIN>.miro.com/sso/saml/<ORG_ID>/<SAMLSETTINGS_ID>` |
6. Perform the following step, if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type the URL: `https://miro.com/sso/login/`

    Note

    These values aren't real. Update these values with the actual Identifier and Reply URL. Contact [Miro support team](mailto:support@miro.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section in the Microsoft Entra admin center.
7. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer. You need it to configure SSO on the Miro side.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
8. On the **Set up Miro** section, copy the Login URL. You need it to configure SSO on the Miro side.

    ![Screenshot shows to copy Login URL.](media/miro-tutorial/login.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Miro SSO

To configure single sign-on on Miro side, use the certificate you previously downloaded and the Login URL you previously copied. In the Miro account settings go to the **Security** section and toggle on **Enable SSO/SAML**.

1. Paste the Login URL in the **SAML Sign-in URL** field.
2. Open the certificate file with a text editor and copy the certificate sequence. Paste the sequence in the **Key x509 Certificate** field. ![Miro settings](media/miro-tutorial/security.png)
3. In the **Domains** field type in your domain address, select **Add** and follow the verification procedure. Repeat for your other domain addresses if you have any. The Miro SSO feature is working for the end users which domains are on the list. ![Domain](media/miro-tutorial/add-domain.png)
4. Decide if you be using Just in Time provisioning (pulling your users into your subscription during their registration in Miro) and select **Save** to complete the SSO configuration on the Miro side. ![Just in Time Provisioning](media/miro-tutorial/save-configuration.png)

### Create Miro test user

In this section, a user called B.Simon is created in Miro. Miro supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Miro, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options using the test user B.Simon.

#### SP initiated:

- Go to Miro Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, in Azure portal and choose to log in as B.Simon. You should be automatically signed in to the Miro subscription for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Miro tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Miro for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
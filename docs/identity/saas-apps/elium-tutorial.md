---
layout: Conceptual
title: Configure Elium for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/elium-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Elium.
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 5dfe2e75-17a0-d7d6-416e-db1fd40ebf88
document_version_independent_id: d7c788d3-6c8b-871f-fd8d-d370b76ba746
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/elium-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/elium-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/elium-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: fbb110cc-8b11-ec94-f002-700c21b6d348
---

# Configure Elium for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Elium with Microsoft Entra ID. When you integrate Elium with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Elium.
- Enable your users to be automatically signed-in to Elium with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Elium is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Elium single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Elium supports **SP and IDP** initiated SSO.
- Elium supports **Just In Time** user provisioning.
- Elium supports [Automated user provisioning](elium-provisioning-tutorial).

## Add Elium from the gallery

To configure the integration of Elium into Microsoft Entra ID, you need to add Elium from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Elium** in the search box.
4. Select **Elium** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Elium

Configure and test Microsoft Entra SSO with Elium using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Elium.

To configure and test Microsoft Entra SSO with Elium, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Elium SSO**- to configure the single sign-on settings on application side.
    1. **Create Elium test user** - to have a counterpart of B.Simon in Elium that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Elium** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://<platform-domain>.elium.com/login/saml2/metadata`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<platform-domain>.elium.com/login/saml2/acs`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<platform-domain>.elium.com/login/saml2/login`

    Note

    These values aren't real. You get these values from the **SP metadata file** downloadable at `https://<platform-domain>.elium.com/login/saml2/metadata`, which is explained later in this article.
7. Elium application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
8. In addition to above, Elium application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | email | user.mail |
    | first\_name | user.givenname |
    | last\_name | user.surname |
    | job\_title | user.jobtitle |
    | company | user.companyname |

    Note

    These are the default claims. **Only email claim is required**. For JIT provisioning also only email claim is mandatory. Other custom claims can vary from one customer platform to another customer platform.
9. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
10. On the **Set up Elium** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Elium SSO

1. In a different web browser window, sign in to your Elium company site as an administrator
2. Select the **User profile** from right top corner and then select **Settings**.

    ![Configure Single Sign-On User profile.](media/elium-tutorial/profile.png)
3. Select **Security** under **Advanced**.

    ![Configure Single Sign-On Advanced.](media/elium-tutorial/security.png)
4. Scroll down to the **Single sign-on (SSO)** section and perform the following steps:

    ![Configure Single Sign-On.](media/elium-tutorial/configuration.png)

    a. Copy the value of **Verify that SAML2 authentication works for your account** and paste it in the **Sign-on URL** textbox on the **Basic SAML Configuration** section.

    Note

    After configuring SSO, you can always access the default remote login page at the following URL: `https://<platform_domain>/login/regular/login`.

    b. Select **Enable SAML2 federation** checkbox.

    c. Select **JIT Provisioning** checkbox.

    d. Open the **SP Metadata** by selecting the **Download** button.

    e. Search for the **entityID** in the **SP Metadata** file, copy the **entityID** value and paste it in the **Identifier** textbox on the **Basic SAML Configuration** section.

    ![Configure Single Sign-On Configuration.](media/elium-tutorial/metadata.png)

    f. Search for the **AssertionConsumerService** in the **SP Metadata** file, copy the **Location** value and paste it in the **Reply URL** textbox on the **Basic SAML Configuration** section.

    ![Configure Single Sign-On AssertionConsumerService.](media/elium-tutorial/service.png)

    g. Open the downloaded metadata file from Azure portal into notepad, copy the content and paste it into the **IdP Metadata** textbox.

    h. Select **Save**.

### Create Elium test user

In this section, a user called B.Simon is created in Elium. Elium supports **just-in-time provisioning**, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Elium, a new one is created when you attempt to access Elium.

Elium also supports automatic user provisioning, you can find more details [here](elium-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Elium Sign on URL where you can initiate the login flow.
- Go to Elium Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Elium for which you set up the SSO

You can also use Microsoft My Apps to test the application in any mode. When you select the Elium tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Elium for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
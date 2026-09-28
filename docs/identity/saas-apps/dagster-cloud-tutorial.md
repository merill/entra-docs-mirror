---
layout: Conceptual
title: Configure Dagster Cloud for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/dagster-cloud-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Dagster Cloud.
ms.topic: how-to
ms.date: 2024-09-05T00:00:00.0000000Z
locale: en-us
document_id: 5dd98a3c-cbfd-2e2a-b3af-469af1ab738f
document_version_independent_id: a7b16368-eb99-419d-dc6d-e81396c714ce
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/dagster-cloud-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/dagster-cloud-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/dagster-cloud-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 85bcc9b1-19b4-3cd9-e781-efa337f92c0a
---

# Configure Dagster Cloud for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Dagster Cloud with Microsoft Entra ID. When you integrate Dagster Cloud with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Dagster Cloud.
- Enable your users to be automatically signed-in to Dagster Cloud with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Dagster Cloud single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Dagster Cloud supports **SP and IDP** initiated SSO.
- Dagster Cloud supports **Just In Time** user provisioning.
- Dagster Cloud supports [Automated user provisioning](dagster-cloud-provisioning-tutorial).

## Add Dagster Cloud from the gallery

To configure the integration of Dagster Cloud into Microsoft Entra ID, you need to add Dagster Cloud from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Dagster Cloud** in the search box.
4. Select **Dagster Cloud** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Dagster Cloud

Configure and test Microsoft Entra SSO with Dagster Cloud using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Dagster Cloud.

To configure and test Microsoft Entra SSO with Dagster Cloud, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Dagster Cloud SSO**- to configure the single sign-on settings on application side.
    1. **Create Dagster Cloud test user** - to have a counterpart of B.Simon in Dagster Cloud that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Dagster Cloud** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://<ORGANIZATION_NAME>.dagster.cloud/auth/saml/consume`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<ORGANIZATION_NAME>.dagster.cloud/auth/saml/consume`
6. Perform the following step, if you wish to configure the application in **SP** initiated mode:

    In the **Sign on URL** text box, type a URL using the following pattern: `https://<ORGANIZATION_NAME>.dagster.cloud/auth/saml/login`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. You can refer to the patterns shown in the **Basic SAML Configuration** section. [See Dagster Cloud's documentation](https://docs.dagster.io/dagster-plus/account/authentication/setting-up-azure-ad-saml-sso#step-2-configure-sso-in-azure-ad) for more information.
7. Dagster Cloud application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
8. In addition to above, Dagster Cloud application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre-populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | FirstName | user.givenname |
    | LastName | user.surname |
    | Email | user.userprincipalname |
9. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
10. On the **Set up Dagster Cloud** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Dagster Cloud SSO

To configure single sign-on on the **Dagster Cloud** side, you need to upload the **Federation Metadata XML** file to **Dagster Cloud** using [the dagster-cloud CLI](https://docs.dagster.io/dagster-plus/account/authentication/setting-up-azure-ad-saml-sso#step-3-upload-the-saml-metadata-to-dagster).

### Create Dagster Cloud test user

In this section, a user called Britta Simon is created in Dagster Cloud. Dagster Cloud supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Dagster Cloud, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Dagster Cloud Sign on URL where you can initiate the login flow.
- Go to Dagster Cloud Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Dagster Cloud for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Dagster Cloud tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Dagster Cloud for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
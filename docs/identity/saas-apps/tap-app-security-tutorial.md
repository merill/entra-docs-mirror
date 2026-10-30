---
layout: Conceptual
title: Configure TAP App Security for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/tap-app-security-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and TAP App Security.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 67695269-3e6d-c8d3-65db-22ea78ded0f9
document_version_independent_id: dd1a5a50-d8d1-7fa9-143a-5c8b79a833f5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/tap-app-security-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/tap-app-security-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/tap-app-security-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 120fbd2c-0357-341d-64f8-7e17b6c6ea49
---

# Configure TAP App Security for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate TAP App Security with Microsoft Entra ID. When you integrate TAP App Security with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to TAP App Security.
- Enable your users to be automatically signed-in to TAP App Security with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- TAP App Security single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- TAP App Security supports **SP** initiated SSO.
- TAP App Security supports **Just In Time** user provisioning.

## Adding TAP App Security from the gallery

To configure the integration of TAP App Security into Microsoft Entra ID, you need to add TAP App Security from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **TAP App Security** in the search box.
4. Select **TAP App Security** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for TAP App Security

Configure and test Microsoft Entra SSO with TAP App Security using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in TAP App Security.

To configure and test Microsoft Entra SSO with TAP App Security, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure TAP App Security SSO**- to configure the single sign-on settings on application side.
    1. **Create TAP App Security test user** - to have a counterpart of B.Simon in TAP App Security that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **TAP App Security** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    a. In the **Identifier** box, type a URL using the following pattern: `https://app.tapappsecurity.com/<CUSTOMER_DOMAIN_WITHOUT_EXTENSION>/metadata`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://app.tapappsecurity.com/<CUSTOMER_DOMAIN_WITHOUT_EXTENSION>/acs`

    c. In the **Sign-on URL** text box, type the URL: `https://webapp.tapappsecurity.com/`

    Note

    These values aren't real. Update these values with the actual Identifier and Reply URL. Contact [TAP App Security Client support team](mailto:support@tapappsecurity.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. TAP App Security application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
7. In addition to above, TAP App Security application expects few more attributes to be passed back in SAML response, which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | email | user.mail |
    | first | user.givenname |
    | login | user.userprincipalname |
    | last | user.surname |
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
9. On the **Set up TAP App Security** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure TAP App Security SSO

1. Log in to the TAP App Security website as an administrator.
2. Select **Single Sign-On** on the left navigation bar and then select **Active Directory**.

    ![Screenshot for the single sign-on.](media/tap-app-security-tutorial/entra.png)
3. Select the **Integrate Active Directory app** button. Then enter the domain of your organization and select **Save** button.

    ![Screenshot for the active directory.](media/tap-app-security-tutorial/domain.png)
4. Select the gear icon as shown below.

    ![Screenshot for the icon.](media/tap-app-security-tutorial/gear-icon.png)
5. Perform the following steps in the **Active Directory integration** page.

    ![Screenshot for the integration.](media/tap-app-security-tutorial/configuration.png)

    a. Copy **Reply URL (Assertion Consumer Service URL)** value, paste this value into the **Reply URL** text box in the **Basic SAML Configuration** section.

    b. Copy **Identifier (Entity ID)** value, paste this value into the **Identifier** text box in the **Basic SAML Configuration** section.

    c. Select **Choose File** to upload the downloaded **Federation Metadata XML** file.

    d. Select **Save**.

### Create TAP App Security test user

In this section, a user called B.Simon is created in TAP App Security. TAP App Security supports just-in-time provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in TAP App Security, a new one is created when you attempt to access TAP App Security.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to TAP App Security Sign-on URL where you can initiate the login flow.
- Go to TAP App Security Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the TAP App Security tile in the My Apps, this option redirects to TAP App Security Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
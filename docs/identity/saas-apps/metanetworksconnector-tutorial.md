---
layout: Conceptual
title: Configure Meta Networks Connector for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/metanetworksconnector-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Meta Networks Connector.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 8fef64ba-30a4-b8b1-1265-a199cf8527d4
document_version_independent_id: ba102989-5b28-c893-8cbb-36fac0d42b5f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/metanetworksconnector-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/metanetworksconnector-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/metanetworksconnector-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 3abaaf66-e675-bc6e-4909-300cf8b16634
---

# Configure Meta Networks Connector for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Meta Networks Connector with Microsoft Entra ID. When you integrate Meta Networks Connector with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Meta Networks Connector.
- Enable your users to be automatically signed-in to Meta Networks Connector with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Meta Networks Connector single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Meta Networks Connector supports **SP** and **IDP** initiated SSO.
- Meta Networks Connector supports **Just In Time** user provisioning.
- Meta Networks Connector supports [Automated user provisioning](meta-networks-connector-provisioning-tutorial).

## Add Meta Networks Connector from the gallery

To configure the integration of Meta Networks Connector into Microsoft Entra ID, you need to add Meta Networks Connector from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Meta Networks Connector** in the search box.
4. Select **Meta Networks Connector** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Meta Networks Connector

Configure and test Microsoft Entra SSO with Meta Networks Connector using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Meta Networks Connector.

To configure and test Microsoft Entra SSO with Meta Networks Connector, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Meta Networks Connector SSO**- to configure the single sign-on settings on application side.
    1. **Create Meta Networks Connector test user** - to have a counterpart of B.Simon in Meta Networks Connector that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Meta Networks Connector** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, If you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://login.nsof.io/v1/<ORGANIZATION-SHORT-NAME>/saml/metadata`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://login.nsof.io/v1/<ORGANIZATION-SHORT-NAME>/sso/saml`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    a. In the **Sign-on URL** text box, type a URL using the following pattern: `https://<ORGANIZATION-SHORT-NAME>.metanetworks.com/login`

    b. In the **Relay State** textbox, type a URL using the following pattern: `https://<ORGANIZATION-SHORT-NAME>.metanetworks.com/#/`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL, and Sign-On URL are explained later in the article.
7. Meta Networks Connector application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes. Select **Edit** icon to open **User Attributes** dialog.

    ![Screenshot shows User Attributes with the Edit icon selected.](common/edit-attribute.png)
8. In addition to above, Meta Networks Connector application expects few more attributes to be passed back in SAML response. In the **User Claims** section on the **User Attributes** dialog, perform the following steps to add SAML token attribute as shown in the below table:

    | Name | Source attribute | Namespace |
    | --- | --- | --- |
    | firstname | user.givenname |  |
    | lastname | user.surname |  |
    | emailaddress | user.mail | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims` |
    | name | user.userprincipalname | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims` |
    | phone | user.telephonenumber |  |

    a. Select **Add new claim** to open the **Manage user claims** dialog.

    ![Screenshot shows User claims with the option to Add new claim.](common/new-save-attribute.png)

    ![Screenshot shows the Manage user claims dialog box where you can enter the values described.](common/new-attribute-details.png)

    b. In the **Name** textbox, type the attribute name shown for that row.

    c. Leave the **Namespace** blank.

    d. Select Source as **Attribute**.

    e. From the **Source attribute** list, type the attribute value shown for that row.

    f. Select **Ok**

    g. Select **Save**.
9. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
10. On the **Set up Meta Networks Connector** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Meta Networks Connector SSO

1. Open a new tab in your browser and log in to your Meta Networks Connector administrator account.

    Note

    Meta Networks Connector is a secure system. So before accessing their portal you need to get your public IP address added to an allow list on their side. To get your public IP address,follow the below link specified [here](https://whatismyipaddress.com/). Send your IP address to the [Meta Networks Connector Client support team](mailto:support@metanetworks.com) to get your IP address added to an allow list.
2. Go to **Administrator** and select **Settings**.

    ![Screenshot shows Settings selected from the Administration menu.](media/metanetworksconnector-tutorial/menu.png)
3. Make sure **Log Internet Traffic** and **Force VPN MFA** are set to off.

    ![Screenshot shows turning off these settings.](media/metanetworksconnector-tutorial/settings.png)
4. Go to **Administrator** and select **SAML**.

    ![Screenshot shows SAML selected from the Administration menu.](media/metanetworksconnector-tutorial/admin.png)
5. Perform the following steps on the **DETAILS** page:

    ![Screenshot shows the DETAILS page where you can enter the values described.](media/metanetworksconnector-tutorial/details.png)

    a. Copy **SSO URL** value and paste it into the **Sign-In URL** textbox in the **Meta Networks Connector Domain and URLs** section.

    b. Copy **Recipient URL** value and paste it into the **Reply URL** textbox in the **Meta Networks Connector Domain and URLs** section.

    c. Copy **Audience URI (SP Entity ID)** value and paste it into the **Identifier (Entity ID)** textbox in the **Meta Networks Connector Domain and URLs** section.

    d. Enable the SAML.
6. On the **GENERAL** tab and perform the following steps:

    ![Screenshot shows the GENERAL page where you can enter the values described.](media/metanetworksconnector-tutorial/configuration.png)

    a. In the **Identity Provider Single Sign-On URL**, paste the **Login URL** value which you copied previously.

    b. In the **Identity Provider Issuer**, paste the **Microsoft Entra Identifier** value which you copied previously.

    c. Open the downloaded certificate from Azure portal in notepad, paste it into the **X.509 Certificate** textbox.

    d. Enable the **Just-in-Time Provisioning**.

### Create Meta Networks Connector test user

In this section, a user called Britta Simon is created in Meta Networks Connector. Meta Networks Connector supports just-in-time provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Meta Networks Connector, a new one is created when you attempt to access Meta Networks Connector.

Note

If you need to create a user manually, contact [Meta Networks Connector Client support team](mailto:support@metanetworks.com).

Meta Networks also supports automatic user provisioning, you can find more details [here](meta-networks-connector-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Meta Networks Connector Sign on URL where you can initiate the login flow.
- Go to Meta Networks Connector Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Meta Networks Connector for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Meta Networks Connector tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Meta Networks Connector for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
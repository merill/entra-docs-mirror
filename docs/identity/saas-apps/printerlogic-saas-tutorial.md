---
layout: Conceptual
title: Configure PrinterLogic for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/printerlogic-saas-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and PrinterLogic.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: aafec3e0-4e6a-ccc8-4592-e6ac7caaa1fb
document_version_independent_id: d6acc245-965b-01d0-ca66-c0e36b2d0088
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/printerlogic-saas-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/printerlogic-saas-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/printerlogic-saas-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 321624fa-db16-b1d0-9651-f95115213e80
---

# Configure PrinterLogic for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate PrinterLogic with Microsoft Entra ID. When you integrate PrinterLogic with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to PrinterLogic.
- Enable your users to be automatically signed-in to PrinterLogic with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- PrinterLogic single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- PrinterLogic supports **SP and IDP** initiated SSO.
- PrinterLogic supports **Just In Time** user provisioning.
- PrinterLogic supports [Automated user provisioning](printer-logic-saas-provisioning-tutorial).

## Add PrinterLogic from the gallery

To configure the integration of PrinterLogic into Microsoft Entra ID, you need to add PrinterLogic from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **PrinterLogic** in the search box.
4. Select **PrinterLogic** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for PrinterLogic

Configure and test Microsoft Entra SSO with PrinterLogic using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in PrinterLogic.

To configure and test Microsoft Entra SSO with PrinterLogic, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure PrinterLogic SSO**- to configure the single sign-on settings on application side.
    1. **Create PrinterLogic test user** - to have a counterpart of B.Simon in PrinterLogic that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **PrinterLogic** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, enter the values for the following fields:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://gw.app.printercloud.com/<my_instance>/authn/idp/azuread/saml2/metadata`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://gw.app.printercloud.com/<my_instance>/authn/idp/azuread/saml2/acs`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://www.<my_instance>printercloud.com`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [PrinterLogic Client support team](mailto:support@printerlogic.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. PrinterLogic application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/edit-attribute.png)
8. In addition to above, PrinterLogic application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirement.

    | Name | Source Attribute |
    | --- | --- |
    | Role | user.assignedroles |

    Note

    Please select [here](../../identity-platform/howto-add-app-roles-in-apps#app-roles-ui) to know how to configure Role in Microsoft Entra ID.
9. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
10. On the **Set up PrinterLogic** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure PrinterLogic SSO

To configure single sign-on on **PrinterLogic** side, you need to send the downloaded **Certificate (Base64)** and appropriate copied URLs from the application configuration to [PrinterLogic support team](mailto:support@printerlogic.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create PrinterLogic test user

In this section, a user called Britta Simon is created in PrinterLogic. PrinterLogic supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in PrinterLogic, a new one is created after authentication.

PrinterLogic also supports automatic user provisioning, you can find more details [here](printer-logic-saas-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to PrinterLogic Sign on URL where you can initiate the login flow.
- Go to PrinterLogic Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the PrinterLogic for which you set up the SSO.
- You can also use Microsoft My Apps to test the application in any mode. When you select the PrinterLogic tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the PrinterLogic for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
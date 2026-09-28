---
layout: Conceptual
title: Configure EBSCO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/ebsco-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and EBSCO.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 0934fb49-b35b-6c06-e0ce-55fd54d6ec1b
document_version_independent_id: 9ef986f9-da60-5ef0-62d9-f488d8912eab
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/ebsco-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/ebsco-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/ebsco-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d3698370-060b-09a1-e898-fea7e3ceb03a
---

# Configure EBSCO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate EBSCO with Microsoft Entra ID. When you integrate EBSCO with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to EBSCO.
- Enable your users to be automatically signed-in to EBSCO with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- EBSCO single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- EBSCO supports **SP and IDP** initiated SSO.
- EBSCO supports **Just In Time** user provisioning.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add EBSCO from the gallery

To configure the integration of EBSCO into Microsoft Entra ID, you need to add EBSCO from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **EBSCO** in the search box.
4. Select **EBSCO** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for EBSCO

Configure and test Microsoft Entra SSO with EBSCO using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in EBSCO.

To configure and test Microsoft Entra SSO with EBSCO, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure EBSCO SSO**- to configure the single sign-on settings on application side.
    1. **Create EBSCO test user** - to have a counterpart of B.Simon in EBSCO that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **EBSCO** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, then perform the following step:

    In the **Identifier** text box, type the URL: `pingsso.ebscohost.com`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `http://search.ebscohost.com/login.aspx?authtype=sso&custid=<unique EBSCO customer ID>&profile=<profile ID>`

    Note

    The Sign-on URL value isn't real. Update the value with the actual Sign-on URL. Contact [EBSCO Client support team](mailto:support@ebsco.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.

    o **Unique elements:**

    o **Custid** = Enter unique EBSCO customer ID

    o **Profile** = Clients can tailor the link to direct users to a specific profile (depending on what they purchase from EBSCO). They can enter a specific profile ID. The main IDs are eds (EBSCO Discovery Service) and ehost (EBSOCOhost databases). Instructions for the same are given in the EBSCOhost documentation.
7. EBSCO application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)

    Note

    The **name** attribute is mandatory and it's mapped with **Name Identifier value** in EBSCO application. This is added by default so you don't need to add this manually.
8. In addition to above, EBSCO application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | FirstName | user.givenname |
    | LastName | user.surname |
    | Email | user.mail |
9. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
10. On the **Set up EBSCO** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure EBSCO SSO

To configure single sign-on on **EBSCO** side, you need to send the downloaded **Federation Metadata XML** and appropriate copied URLs from the application configuration to [EBSCO support team](mailto:support@ebsco.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create EBSCO test user

In the case of EBSCO, user provisioning is automatic.

**To provision a user account, perform the following steps:**

Microsoft Entra ID passes the required data to EBSCO application. EBSCO’s user provisioning can be automatic OR require a one-time form. It depends on whether the client has a lot of pre-existing EBSCOhost accounts with personal settings saved. The same can be discussed with the [EBSCO support team](mailto:support@ebsco.com) during the implementation. Either way, the client doesn’t have to create any EBSCOhost accounts prior to testing.

Note

You can automate EBSCO host user provisioning/personalization. Contact [EBSCO support team](mailto:support@ebsco.com) about Just-In-Time user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration using My Apps.

1. When you select the EBSCO tile in My Apps, you should get automatically signed-on to your EBSCO application. For more information about My Apps, see [Introduction to My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
2. Once you login to the application, select the **sign in** button in the top right corner.

    ![The EBSCO sign-in in the Applications list](media/ebsco-tutorial/application.png)
3. You receive a one-time prompt to pair the institutional/SAML login with an **Link your existing MyEBSCOhost account to your institution account now** OR **Create a new MyEBSCOhost account and link it to your institution account**. The account is used for personalization on the EBSCOhost application. Select the option **Create a new account** and you see that the form for personalization is pre-completed with the values from the saml response as shown in the screenshot below. Select **‘Continue’** to save this selection.

    ![The EBSCO user in the Applications list](media/ebsco-tutorial/user.png)
4. After completing the above setup, clear cookies/cache and login again. You won’t have to manually sign in again and the personalization settings are remembered.
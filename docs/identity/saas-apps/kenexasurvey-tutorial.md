---
layout: Conceptual
title: Configure IBM Kenexa Survey Enterprise for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/kenexasurvey-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and IBM Kenexa Survey Enterprise.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 2b2a228e-827e-8358-5540-60c9a90d20eb
document_version_independent_id: f8eb6ff3-9c3f-21a3-399d-970f93d4de26
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/kenexasurvey-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/kenexasurvey-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/kenexasurvey-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 4f1db9df-aea5-5d19-8ca8-098b3c1cdbb5
---

# Configure IBM Kenexa Survey Enterprise for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate IBM Kenexa Survey Enterprise with Microsoft Entra ID. When you integrate IBM Kenexa Survey Enterprise with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to IBM Kenexa Survey Enterprise.
- Enable your users to be automatically signed-in to IBM Kenexa Survey Enterprise with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- IBM Kenexa Survey Enterprise single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- IBM Kenexa Survey Enterprise supports **IDP** initiated SSO.

## Add IBM Kenexa Survey Enterprise from the gallery

To configure the integration of IBM Kenexa Survey Enterprise into Microsoft Entra ID, you need to add IBM Kenexa Survey Enterprise from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **IBM Kenexa Survey Enterprise** in the search box.
4. Select **IBM Kenexa Survey Enterprise** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for IBM Kenexa Survey Enterprise

Configure and test Microsoft Entra SSO with IBM Kenexa Survey Enterprise using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in IBM Kenexa Survey Enterprise.

To configure and test Microsoft Entra SSO with IBM Kenexa Survey Enterprise, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure IBM Kenexa Survey Enterprise SSO**- to configure the single sign-on settings on application side.
    1. **Create IBM Kenexa Survey Enterprise test user** - to have a counterpart of B.Simon in IBM Kenexa Survey Enterprise that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **IBM Kenexa Survey Enterprise** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Set up Single Sign-On with SAML** page, perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://surveys.kenexa.com/<companycode>`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`

    Note

    These values aren't real. Update these values with the actual Identifier and Reply URL. Contact [IBM Kenexa Survey Enterprise Client support team](https://www.ibm.com/support/home/?lnk=fcw) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. The IBM Kenexa Survey Enterprise application expects to receive the Security Assertions Markup Language (SAML) assertions in a specific format, which requires you to add custom attribute mappings to the configuration of your SAML token attributes. The value of the user-identifier claim in the response must match the SSO ID that's configured in the Kenexa system. To map the appropriate user identifier in your organization as SSO Internet Datagram Protocol (IDP), work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).

    By default, Microsoft Entra ID sets the user identifier as the user principal name (UPN) value. You can change this value on the **User Attributes** tab, as shown in the following screenshot. The integration works only after you've completed the mapping correctly.

    ![image](common/edit-attribute.png)
7. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
8. On the **Set up IBM Kenexa Survey Enterprise** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure IBM Kenexa Survey Enterprise SSO

To configure single sign-on on **IBM Kenexa Survey Enterprise** side, you need to send the downloaded **Certificate (Base64)** and appropriate copied URLs from the application configuration to [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw). They set this setting to have the SAML SSO connection set properly on both sides.

### Create IBM Kenexa Survey Enterprise test user

In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.

To create users in the IBM Kenexa Survey Enterprise system and map the SSO ID for them, you can work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw). This SSO ID value should also be mapped to the user identifier value from Microsoft Entra ID. You can change this default setting on the **Attribute** tab.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the IBM Kenexa Survey Enterprise for which you set up the SSO.
- You can use Microsoft My Apps. When you select the IBM Kenexa Survey Enterprise tile in the My Apps, you should be automatically signed in to the IBM Kenexa Survey Enterprise for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
---
layout: Conceptual
title: Configure Per Angusta for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/per-angusta-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Per Angusta.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 27c13014-f124-7a31-4df8-a9c0f14bb623
document_version_independent_id: 31eee5c8-d097-193f-0f97-d845e965142c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/per-angusta-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/per-angusta-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/per-angusta-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 78f4b3ca-814d-e75f-ee09-c7b08d23f67d
---

# Configure Per Angusta for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Per Angusta with Microsoft Entra ID. When you integrate Per Angusta with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Per Angusta.
- Enable your users to be automatically signed-in to Per Angusta with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Per Angusta single sign-on (SSO) enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Per Angusta supports **SP** initiated SSO.

## Add Per Angusta from the gallery

To configure the integration of Per Angusta into Microsoft Entra ID, you need to add Per Angusta from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Per Angusta** in the search box.
4. Select **Per Angusta** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Per Angusta

Configure and test Microsoft Entra SSO with Per Angusta using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Per Angusta.

To configure and test Microsoft Entra SSO with Per Angusta, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Per Angusta SSO**- to configure the single sign-on settings on application side.
    1. **Create Per Angusta test user** - to have a counterpart of B.Simon in Per Angusta that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Per Angusta** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** text box, type a value using the following pattern: `<SUBDOMAIN>.per-angusta.com`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.per-angusta.com/saml/consume`

    c. In the **Sign-on URL** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.per-angusta.com/saml/init`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [Per Angusta Client support team](mailto:support@per-angusta.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![The Certificate download link](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Per Angusta SSO

1. Log in to your Per Angusta company site as an administrator.
2. Go to Administration tab.

    ![Screenshot that shows the Admin Account](media/per-angusta-tutorial/users.png)
3. In the left-side menu under **CONFIGURATION**, select **SSO SAML**.

    ![Screenshot that shows the Configuration](media/per-angusta-tutorial/general.png)
4. Perform the following steps in the configuration page:

    ![Screenshot that shows the metadata](media/per-angusta-tutorial/certificate.png)

    ![Screenshot that shows the SSO SAML Certificate](media/per-angusta-tutorial/claims.png)

    1. Copy **Reply URL** value, paste this value into the **Reply URL** text box in the **Basic SAML Configuration** section.
    2. Copy **Entity ID** value, paste this value into the **Identifier** text box in the **Basic SAML Configuration** section.
    3. Copy **SAML initialization URL** value, paste this value into the **Sign on URL** text box in the **Basic SAML Configuration** section.
    4. Enable **Active** SSO checkbox before to test connection.
    5. In the **XML URL** textbox, paste the **App Federation Metadata Url** value which you copied previously.
    6. In the **Claim** textbox, select **Email** from the dropdown.
    7. In the **NameID Format** textbox, please select `urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified` from the dropdown.
    8. Select **Save**.

### Create Per Angusta test user

In this section, you create a user called Britta Simon in Per Angusta. Work with [Per Angusta support team](mailto:support@per-angusta.com) to add the users in the Per Angusta platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Per Angusta Sign-on URL where you can initiate the login flow.
- Go to Per Angusta Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Per Angusta tile in the My Apps, this option redirects to Per Angusta Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
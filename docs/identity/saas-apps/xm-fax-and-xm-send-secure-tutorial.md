---
layout: Conceptual
title: Configure XM Fax and XM SendSecure for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/xm-fax-and-xm-send-secure-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and XM Fax and XM SendSecure.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: afc39e1f-2f92-91c8-a297-50b6cdc2668f
document_version_independent_id: a4529f3c-0b5f-537d-fb4b-fa4765e36f45
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/xm-fax-and-xm-send-secure-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/xm-fax-and-xm-send-secure-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/xm-fax-and-xm-send-secure-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 566759b3-291c-b425-ed37-0534fd75b63a
---

# Configure XM Fax and XM SendSecure for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate XM Fax and XM SendSecure with Microsoft Entra ID. When you integrate XM Fax and XM SendSecure with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to XM Fax and XM SendSecure.
- Enable your users to be automatically signed-in to XM Fax and XM SendSecure with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Microsoft Entra Cloud Application Administrator or Application Administrator role. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).
- XM Fax and XM SendSecure subscription.
- XM Fax and XM SendSecure administrator account.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- XM Fax and XM SendSecure supports **SP-initiated** SSO.
- XM Fax and XM SendSecure supports [Automated user provisioning](xm-fax-and-xm-send-secure-provisioning-tutorial).

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add XM Fax and XM SendSecure from the gallery

To configure the integration of XM Fax and XM SendSecure into Microsoft Entra ID, you need to add XM Fax and XM SendSecure from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **XM Fax and XM SendSecure** in the search box.
4. Select **XM Fax and XM SendSecure** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for XM Fax and XM SendSecure

Configure and test Microsoft Entra SSO with XM Fax and XM SendSecure using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user at XM Fax and XM SendSecure.

To configure and test Microsoft Entra SSO with XM Fax and XM SendSecure, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure XM Fax and XM SendSecure SSO**- to configure the single sign-on settings on application side.
    1. **Create XM Fax and XM SendSecure test user** - to have a counterpart of B.Simon in XM Fax and XM SendSecure that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **XM Fax and XM SendSecure** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type one of the following URLs:

    | **Identifier** |
    | --- |
    | `https://login.xmedius.com/` |
    | `https://login.xmedius.eu/` |
    | `https://login.xmedius.ca/` |

    b. In the **Reply URL** textbox, type one of the following URLs:

    | **Reply URL** |
    | --- |
    | `https://login.xmedius.com/auth/saml/callback` |
    | `https://login.xmedius.eu/auth/saml/callback` |
    | `https://login.xmedius.ca/auth/saml/callback` |

    c. In the **Sign-on URL** text box, type a URL using one of the following patterns:

    | **Sign-on URL** |
    | --- |
    | `https://login.xmedius.com/{account}` |
    | `https://login.xmedius.eu/{account}` |
    | `https://login.xmedius.ca/{account}` |
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
7. On the **Set up XM Fax and XM SendSecure** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows how to copy configuration appropriate URL.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure XM Fax and XM SendSecure SSO

1. Log in to your XM Cloud account using a Web browser.
2. From the main menu of your Web Portal, select **enterprise\_account -&gt; Enterprise Settings**.
3. Go to **Single Sign-On** section and select **SAML 2.0**.
4. Provide the following required information:

    a. In the **Issuer (Identity Provider)** textbox, paste the **Microsoft Entra Identifier** value which you copied previously.

    b. In the **Sign In URL** textbox, paste the **Login URL** value which you copied previously.

    c. Open the downloaded **Certificate (Base64)** into Notepad and paste the content into the **X.509 Signing Certificate** textbox.

    d. select **Save**.

Note

Keep the fail-safe URL (`https://login.[domain]/[account]/no-sso`) provided at the bottom of the SSO configuration section, it will allow you to log in using your XM Cloud account credentials if you lock yourself after SSO activation.

### Create XM Fax and XM SendSecure test user

Create a user called Britta Simon at XM Fax and XM SendSecure. Make sure the email is set to "B.Simon@contoso.com".

Note

Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with the following options.

- Select **Test this application**, this option redirects to XM Fax and XM SendSecure Sign-on URL where you can initiate the login flow.
- Go to XM Fax and XM SendSecure Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the XM Fax and XM SendSecure tile in the My Apps portal, this option redirects to XM Fax and XM SendSecure Sign-on URL. For more information about the My Apps portal, see [Introduction to the My Apps portal](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
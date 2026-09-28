---
layout: Conceptual
title: Configure Predictix Price Reporting for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/predictixpricereporting-tutorial
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
description: In this article,  you learn how to configure single sign-on between Microsoft Entra ID and Predictix Price Reporting.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 28448883-b4e9-a18a-8171-fdb99e2ca6e8
document_version_independent_id: 1f7b04a0-5516-7bd2-9e09-0f6b62a82fe9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/predictixpricereporting-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/predictixpricereporting-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/predictixpricereporting-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d3f65c3b-0c62-f148-fe78-18e430af828d
---

# Configure Predictix Price Reporting for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Predictix Price Reporting with Microsoft Entra ID. When you integrate Predictix Price Reporting with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Predictix Price Reporting.
- Enable your users to be automatically signed-in to Predictix Price Reporting with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Predictix Price Reporting single sign-on (SSO) enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Predictix Price Reporting supports SP-initiated SSO.

## Add Predictix Price Reporting from the gallery

To configure the integration of Predictix Price Reporting into Microsoft Entra ID, you need to add Predictix Price Reporting from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Predictix Price Reporting** in the search box.
4. Select **Predictix Price Reporting** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Predictix Price Reporting

Configure and test Microsoft Entra SSO with Predictix Price Reporting using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Predictix Price Reporting.

To configure and test Microsoft Entra SSO with Predictix Price Reporting, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Predictix Price Reporting SSO**- to configure the single sign-on settings on application side.
    1. **Create a Predictix Price Reporting test user** - to have a counterpart of B.Simon in Predictix Price Reporting that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Predictix Price Reporting** application integration page, find the **Manage** section and select **Single sign-on**.
3. On the **Select a Single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. In the **Basic SAML Configuration** dialog box, perform the following steps:

    a. In the **Identifier (Entity ID)** box, type a URL using one of the following patterns:

    | **Identifier** |
    | --- |
    | `https://<companyname-pricing>.predictix.com` |
    | `https://<companyname-pricing>.dev.predictix.com` |

    b. In the **Sign on URL** box, type a URL using the following pattern: `https://<companyname-pricing>.predictix.com/sso/request`

    Note

    These values are placeholders. Update these values with the actual Identifier and Sign on URL. Contact the [Predictix Price Reporting support team](https://www.infor.com/customer-center) to get the values. You can also refer to the patterns shown in the **Basic SAML Configuration** dialog box.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select the **Download** link next to **Certificate (Base64)**, per your requirements, and save the certificate on your computer:

    ![Certificate download link](common/certificatebase64.png)
7. In the **Set up Predictix Price Reporting** section, copy the appropriate URLs, based on your requirements.

    ![Copy the configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Predictix Price Reporting SSO

To configure single sign-on on the Predictix Price Reporting side, you need to send the certificate that you downloaded and the URLs that you copied to the [Predictix Price Reporting support team](https://www.infor.com/customer-center). This team ensures the SAML SSO connection is set properly on both sides.

### Create a Predictix Price Reporting test user

Next, you need to create a user named Britta Simon in Predictix Price Reporting. Work with the [Predictix Price Reporting support team](https://www.infor.com/customer-center) to add users. Users need to be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Predictix Price Reporting Sign-on URL where you can initiate the login flow.
- Go to Predictix Price Reporting Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Predictix Price Reporting tile in the My Apps, this option redirects to Predictix Price Reporting Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
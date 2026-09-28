---
layout: Conceptual
title: Configure Predictix Ordering for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/predictixordering-tutorial
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
description: In this article,  you learn how to configure single sign-on between Microsoft Entra ID and Predictix Ordering.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 6611bfa6-5f4b-bbb7-a5a2-585c82392ce9
document_version_independent_id: c5600dca-e253-aa95-3315-382d78fae7ae
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/predictixordering-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/predictixordering-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/predictixordering-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ca45d487-3a75-0326-7a04-129a22ee93ab
---

# Configure Predictix Ordering for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Predictix Ordering with Microsoft Entra ID. When you integrate Predictix Ordering with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Predictix Ordering.
- Enable your users to be automatically signed-in to Predictix Ordering with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To configure Microsoft Entra integration with Predictix Ordering, you need to have:

- A Microsoft Entra subscription. If you don't have a Microsoft Entra environment, you can get a [free account](https://azure.microsoft.com/pricing/free-trial/).
- A Predictix Ordering subscription that has single sign-on enabled.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Predictix Ordering supports SP-initiated SSO.

## Add Predictix Ordering from the gallery

To configure the integration of Predictix Ordering into Microsoft Entra ID, you need to add Predictix Ordering from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Predictix Ordering** in the search box.
4. Select **Predictix Ordering** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Predictix Ordering

Configure and test Microsoft Entra SSO with Predictix Ordering using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Predictix Ordering.

To configure and test Microsoft Entra SSO with Predictix Ordering, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Predictix Ordering SSO**- to configure the single sign-on settings on application side.
    1. **Create a Predictix Ordering test user** - to have a counterpart of B.Simon in Predictix Ordering that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Predictix Ordering** application integration page, find the **Manage** section and select **Single sign-on**.
3. On the **Select a Single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. In the **Basic SAML Configuration** dialog box, perform the following steps:

    a. In the **Identifier (Entity ID)** box, type a URL using one of the following patterns:

    | **Identifier** |
    | --- |
    | `https://<companyname-pricing>.dev.ordering.predictix.com` |
    | `https://<companyname-pricing>.ordering.predictix.com` |

    b. In the **Sign on URL** box, type a URL using the following pattern: `https://<companyname-pricing>.ordering.predictix.com/sso/request`

    Note

    These values are placeholders. Update these values with the actual Identifier and Sign on URL. Contact the Predictix Ordering support team to get the values. You can also refer to the patterns shown in the **Basic SAML Configuration** dialog box.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select the **Download** link next to **Certificate (Base64)**, per your requirements, and save the certificate on your computer:

    ![Certificate download link](common/certificatebase64.png)
7. In the **Set up Predictix Ordering** section, copy the appropriate URLs, based on your requirements:

    ![Copy the configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Predictix Ordering SSO

To configure single sign-on on the Predictix Ordering side, you need to send the certificate that you downloaded and the URLs that you copied to the Predictix Ordering support team. This team ensures the SAML SSO connection is set properly on both sides.

### Create a Predictix Ordering test user

Next, you need to create a user named Britta Simon in Predictix Ordering. Work with the Predictix Ordering support team to add users. Users need to be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Predictix Ordering Sign-on URL where you can initiate the login flow.
- Go to Predictix Ordering Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Predictix Ordering tile in the My Apps, this option redirects to Predictix Ordering Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
---
layout: Conceptual
title: Configure Prodog for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/prodog-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Prodog.
services: active-directory
ms.workload: identity
ms.topic: how-to
ms.date: 2024-08-01T00:00:00.0000000Z
locale: en-us
document_id: 4ca603dc-beb7-6d07-2741-f5faf46e574c
document_version_independent_id: 4ca603dc-beb7-6d07-2741-f5faf46e574c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/prodog-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/prodog-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/prodog-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 95c992b7-a033-9eca-5e54-0418be14f26a
---

# Configure Prodog for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Prodog with Microsoft Entra ID. When you integrate Prodog with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Prodog.
- Enable your users to be automatically signed-in to Prodog with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Prodog single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Prodog supports **SP** initiated SSO.

## Add Prodog from the gallery

To configure the integration of Prodog into Microsoft Entra ID, you need to add Prodog from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Prodog** in the search box.
4. Select **Prodog** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Prodog

Configure and test Microsoft Entra SSO with Prodog using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Prodog.

To configure and test Microsoft Entra SSO with Prodog, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Create a Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Prodog SSO**- to configure the single sign-on settings on application side.
    1. **Create Prodog test user** - to have a counterpart of B.Simon in Prodog that's linked to the Microsoft Entra ID representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Prodog** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type one of the following URLs:

    | Identifier |
    | --- |
    | `https://t.leanwo.com` |
    | `https://u.leanwo.com` |

    b. In the **Reply URL** text box, type one of the following URLs:

    | Reply URL |
    | --- |
    | `https://tt.leanwo.com/api/saml/sso/a` |
    | `https://u.leanwo.com/api/saml/sso/a` |

    c. In the **Sign on URL** text box, type ine fo the following URLs:

    | Sign on URL |
    | --- |
    | `https://t.leanwo.com` |
    | `https://u.leanwo.com` |
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows The Certificate download link.](common/certificatebase64.png)
7. On the **Set up Prodog** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows how to copy configuration URLs.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Prodog SSO

To configure single sign-on on **Prodog** side, you need to send the downloaded **Certificate (Base64)** and appropriate copied URLs from Microsoft Entra admin center to [Prodog support team](mailto:15800458450@leanwo.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Prodog test user

In this section, you create a user called B.Simon in Prodog. Work with [Prodog support team](mailto:15800458450@leanwo.com) to add the users in the Prodog platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application** in Microsoft Entra admin center. this option redirects to Prodog Sign-on URL where you can initiate the login flow.
- Go to Prodog Sign-on URL directly and initiate the login flow from there.
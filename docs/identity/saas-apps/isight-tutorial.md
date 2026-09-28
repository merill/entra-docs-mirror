---
layout: Conceptual
title: Configure i-Sight for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/isight-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and i-Sight.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 1b251635-3af7-0c25-9a35-1b4f946eed9f
document_version_independent_id: ee92470c-cf88-b71c-48b3-678d9e9aae77
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/isight-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/isight-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/isight-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 954b22bb-5409-40ab-d56c-910a8b0d22fc
---

# Configure i-Sight for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate i-Sight with Microsoft Entra ID. When you integrate i-Sight with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to i-Sight.
- Enable your users to be automatically signed-in to i-Sight with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- i-Sight single sign-on (SSO) enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- i-Sight supports **IDP** initiated SSO.

## Add i-Sight from the gallery

To configure the integration of i-Sight into Microsoft Entra ID, you need to add i-Sight from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **i-Sight** in the search box.
4. Select **i-Sight** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for i-Sight

Configure and test Microsoft Entra SSO with i-Sight using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in i-Sight.

To configure and test Microsoft Entra SSO with i-Sight, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure i-Sight SSO**- to configure the single sign-on settings on application side.
    1. **Create i-Sight test user** - to have a counterpart of B.Simon in i-Sight that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **i-Sight** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic S A M L Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** text box, type a URL using one of the following patterns:

    | **Identifier** |
    | --- |
    | `https://<CustomerName>.i-sight.com` |
    | `https://<CustomerName>.i-sightuat.com` |

    b. In the **Reply URL** text box, type a URL using one of the following patterns:

    | **Reply URL** |
    | --- |
    | `https://<CustomerName>.i-sight.com/auth/wsfed` |
    | `https://<CustomerName>.i-sightuat.com/auth/wsfed` |

    Note

    These values aren't real. Update these values with the actual Identifier and Reply URL. Contact [i-Sight Client support team](mailto:it@i-sight.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set-up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)
7. On the **Set up i-Sight** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration appropriate U R L.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure i-Sight SSO

To configure single sign-on on **i-Sight** side, you need to send the downloaded **Federation Metadata XML** and appropriate copied URLs from the application configuration to [i-Sight support team](mailto:it@i-sight.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create i-Sight test user

In this section, you create a user called Britta Simon in i-Sight. Work with [i-Sight support team](mailto:it@i-sight.com) to add the users in the i-Sight platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the i-Sight for which you set up the SSO.
- You can use Microsoft My Apps. When you select the i-Sight tile in the My Apps, you should be automatically signed in to the i-Sight for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
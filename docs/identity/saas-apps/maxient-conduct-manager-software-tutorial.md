---
layout: Conceptual
title: Configure Maxient Conduct Manager Software for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/maxient-conduct-manager-software-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Maxient Conduct Manager Software.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 30dea0b4-cf61-7468-064d-2d362c5e71e8
document_version_independent_id: e68ca176-8687-a8bd-b2ac-ded451706854
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/maxient-conduct-manager-software-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/maxient-conduct-manager-software-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/maxient-conduct-manager-software-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 30b4dee4-60d6-3b6d-33f8-154ccea47aa7
---

# Configure Maxient Conduct Manager Software for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Maxient Conduct Manager Software with Microsoft Entra ID. When you integrate Maxient Conduct Manager Software with Microsoft Entra ID, you can:

- Utilize Microsoft Entra ID to authenticate your users for the Maxient Conduct Manager Software.
- Enable your users to be automatically signed-in to Maxient Conduct Manager Software with their Microsoft Entra accounts.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Maxient Conduct Manager Software single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure your Microsoft Entra ID for use with Maxient Conduct Manager Software.

- Maxient Conduct Manager Software supports **SP and IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Maxient Conduct Manager Software from the gallery

To configure the integration of Maxient Conduct Manager Software into Microsoft Entra ID, you need to add Maxient Conduct Manager Software from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Maxient Conduct Manager Software** in the search box.
4. Select **Maxient Conduct Manager Software** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Maxient Conduct Manager Software

Configure and test Microsoft Entra SSO with Maxient Conduct Manager Software. For SSO to work, you need to establish a connection between Microsoft Entra ID and the Maxient Conduct Manager Software.

To configure and test Microsoft Entra SSO with Maxient Conduct Manager Software, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to authenticate for use with the Maxient Conduct Manager Software.
    1. **Set "User Assignment Required?" to No** - to allow everyone at your institution to be able to authenticate.
2. **Test Microsoft Entra Setup With Maxient** - to verify whether the configuration works, and the correct attributes are being released.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Maxient Conduct Manager Software** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section the application is pre-configured in **IDP** initiated mode and the necessary URLs are already pre-populated with Azure. The user needs to save the configuration by selecting the **Save** button.
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://cm.maxient.com/<SCHOOLCODE>`

    Note

    The value isn't real. Update the value with the actual Sign-on URL. Work with your Maxient Implementation/Support representative to get the value.
7. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer. You need to provide your Maxient Implementation/Support representative with this URL.

    ![The Certificate download link](common/copy-metadataurl.png)

### Set "User Assignment Required?" to No

It's important to note that this step is **REQUIRED** for Maxient to function properly. Maxient leverages your Microsoft Entra system to *authenticate* users. The *authorization* of users is performed within the Maxient system for the particular function they’re trying to perform. Maxient doesn't use attributes from your directory to make those decisions.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Maxient Conduct Manager Software**.
3. In the app's overview page, toggle the "User Assignment Required" setting to No.

## Test with Maxient

If a support ticket has not already been opened with a Maxient Implementation/Support representative, send an email to support@maxient.com with the subject "Campus Based Authentication/Azure Setup - &lt;&lt;School Name&gt;&gt;". In the body of the email, provide the **App Federation Metadata Url**. Maxient staff will respond with a test link to verify the proper attributes are being released.
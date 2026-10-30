---
layout: Conceptual
title: Configure Zero Networks for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/zero-networks-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Zero Networks.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: d1d16515-61ee-36f9-0492-7f69c8135493
document_version_independent_id: e8dbe8f2-981d-5428-d3a4-0d0f261765a4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/zero-networks-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/zero-networks-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/zero-networks-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 4fb2a6fc-a7b6-e255-6b95-8fd77e0ea735
---

# Configure Zero Networks for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Zero Networks with Microsoft Entra ID. When you integrate Zero Networks with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Zero Networks.
- Enable your users to be automatically signed-in to Zero Networks with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Zero Networks single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure Microsoft Entra SSO for the Zero Networks Admin Portal and Access Portal.

- Zero Networks supports **SP** and **IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Zero Networks from the gallery

To configure the integration of Zero Networks into Microsoft Entra ID, you need to add Zero Networks from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Zero Networks** in the search box.
4. Select **Zero Networks** from results panel and select **Create** to add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Zero Networks**.
3. select **Single sign-on**.
4. On the **Select a single sign-on method** page, select **SAML**.
5. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
6. On the **Basic SAML Configuration** section, perform the following step.

    a. In the **Identifier (Entity ID)** text box, type the URL: `https://<customerUrl>.zeronetworks.com/api/v1/sso/azure/metadata`

    b. In the **Reply URL (Assertion Consumer Service URL)** text box, type the URL: `https://<customerUrl>.zeronetworks.com/api/v1/sso/azure/acs`

    c. In the **Sign on URL** text box, type the URL: `https://<customerUrl>.zeronetworks.com/#/login`
7. On the **Set up single sign-on with SAML** page, in the **SAML Certificates** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
8. On the **Set up Zero Networks** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

## Configure Zero Networks SSO

1. Log in to the Zero Networks Admin Portal as an administrator.
2. Navigate to **Settings** &gt; **Identity Providers**.
3. Select **Microsoft Azure** and perform the following steps.

    ![Screenshot shows settings of SSO configuration.](media/zero-networks-tutorial/settings.png)

    1. In the **Login URL** textbox, paste the **Login URL** value which you copied previously.
    2. In the **Logout URL** textbox, paste the **Logout URL** value which you copied previously.
    3. Open the downloaded **Certificate (Base64)** into Notepad and paste the content into the **Certificate(Base64)** textbox.
    4. Select **Save**.

## Configure user assignment requirement

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Zero Networks** application integration page, find the **Manage** section and select **Properties**.
3. Change **User assignment required?** to **No**.

![Screenshot for User assignment required.](media/zero-networks-tutorial/user-assignment.png)

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Zero Networks Sign-on URL where you can initiate the login flow.
- Go to Zero Networks Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Zero Networks tile in the My Apps, this option redirects to Zero Networks Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).
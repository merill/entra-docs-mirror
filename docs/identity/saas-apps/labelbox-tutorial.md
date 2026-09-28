---
layout: Conceptual
title: Configure Labelbox for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/labelbox-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra and Labelbox.
services: active-directory
ms.workload: identity
ms.topic: how-to
ms.date: 2024-08-28T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 845495fe-bc8f-92e0-ee2d-3409115ccc5b
document_version_independent_id: 845495fe-bc8f-92e0-ee2d-3409115ccc5b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/labelbox-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/labelbox-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/labelbox-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 7fac1737-8fce-3ff3-0be4-51d9b5d653e4
---

# Configure Labelbox for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Labelbox with Microsoft Entra ID. When you integrate Labelbox with Microsoft Entra ID, you can:

Use Microsoft Entra ID to control who can access Labelbox. Enable your users to be automatically signed in to Labelbox with their Microsoft Entra accounts. Manage your accounts in one central location: the Azure portal.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Labelbox single sign-on (SSO) enabled subscription.

## Add Labelbox from the gallery

To configure the integration of Labelbox into Microsoft Entra ID, you need to add Labelbox from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, enter **Labelbox** in the search box.
4. Select **Labelbox** in the results panel and then add the app. Wait a few seconds while the app is added to your tenant.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Labelbox** &gt; **Single sign-on**.
3. Perform the following steps in the below section:

    a. Select **Go to application**.

    ![Screenshot showing the identity configuration.](common/go-to-application.png)

    b. Copy **Application (client) ID** and use it later in the Labelbox side configuration.

    ![Screenshot of application client values.](common/application-id.png)

    c. Under **Endpoints** tab, copy **OpenID Connect metadata document** link and use it later in the Labelbox side configuration.

    ![Screenshot of showing the endpoints on tab.](common/endpoints.png)
4. Navigate to **Authentication** tab on the left menu and perform the following steps:

    a. Enable the **ID tokens (used for implicit and hybrid flows)** checkbox.

    ![Screenshot showing the Access tokens.](media/labelbox-tutorial/access-token.png)

    b. select **Save**.

    Note

    The **Redirect URIs** value will auto populate, you don't need to perform any manual configuration here.
5. Navigate to **Certificates & secrets** on the left menu and perform the following steps:

    1. Go to **Client secrets** tab and select **+New client secret**.
    2. Enter a valid **Description** in the textbox and select **Expires** days from the drop-down as per your requirement and select **Add**.

        ![Screenshot showing the client secrets value.](common/client-secret.png)
    3. Once you add a client secret, **Value** is generated. Copy the value and use it later in the Labelbox side configuration.

        ![Screenshot showing how to add a client secret.](common/client.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Labelbox SSO

To complete the OAuth/OIDC federation setup on **Labelbox** side, you need to send the copied values like Client ID, Client Secret and OIDC Metadata file from Entra to [Labelbox support team](mailto:support@labelbox.com). They set this setting to have the OIDC connection set properly on both sides.
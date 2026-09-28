---
layout: Conceptual
title: Configure IBM Storage Virtualize for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/ibm-storage-virtualize-oidc-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra and IBM Storage Virtualize.
services: active-directory
ms.workload: identity
ms.topic: how-to
ms.date: 2024-08-02T00:00:00.0000000Z
locale: en-us
document_id: 9d8a2d8f-76ea-16f1-182c-448347d963f4
document_version_independent_id: 9d8a2d8f-76ea-16f1-182c-448347d963f4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/ibm-storage-virtualize-oidc-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/ibm-storage-virtualize-oidc-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/ibm-storage-virtualize-oidc-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 2c34481c-c855-e990-7d2c-f32ffb803344
---

# Configure IBM Storage Virtualize for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate IBM Storage Virtualize with Microsoft Entra ID. When you integrate IBM Storage Virtualize with Microsoft Entra ID, you can:

Use Microsoft Entra ID to control who can access IBM Storage Virtualize. Enable your users to be automatically signed in to IBM Storage Virtualize with their Microsoft Entra accounts. Manage your accounts in one central location: the Azure portal.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- IBM Storage Virtualize single sign-on (SSO) enabled subscription.

## Add IBM Storage Virtualize from the gallery

To configure the integration of IBM Storage Virtualize into Microsoft Entra ID, you need to add IBM Storage Virtualize from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, enter **IBM Storage Virtualize** in the search box.
4. Select **IBM Storage Virtualize** in the results panel and then add the app. Wait a few seconds while the app is added to your tenant.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **IBM Storage Virtualize** &gt; **Single sign-on**.
3. Perform the following steps in the below section:

    1. Select **Go to application**.

        [![Screenshot of showing the identity configuration.](common/go-to-application.png)](common/go-to-application.png#lightbox)
    2. Copy **Application (client) ID** and use it later in the IBM Storage Virtualize side configuration.

        [![Screenshot of application client values.](common/application-id.png)](common/application-id.png#lightbox)
4. Navigate to **Authentication** tab on the left menu and perform the following steps:

    1. In the **Redirect URIs** textbox, paste the **Redirect URI** value, which you have copied from the IBM Storage Virtualize side.

        [![Screenshot of showing the redirect values.](common/redirect.png)](common/redirect.png#lightbox)
    2. Select **Configure** button.
5. Navigate to **Certificates & secrets** on the left menu and perform the following steps:

    1. Go to **Client secrets** tab and select **+New client secret**.
    2. Enter a valid **Description** in the textbox and select **Expires** days from the drop-down as per your requirement and select **Add**.

        [![Screenshot of showing the client secrets value.](common/client-secret.png)](common/client-secret.png#lightbox)
    3. Once you add a client secret, **Value** is generated. Copy the value and use it later in the IBM Storage Virtualize side configuration.

        [![Screenshot of showing how to add a client secret.](common/client.png)](common/client.png#lightbox)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure IBM Storage Virtualize SSO

Below are the configuration steps to complete the OAuth/OIDC federation setup:

1. Sign in to the IBM Storage Virtualize administrator dashboard by using the following URL: `https://tenant.verify.ibm.com/ui/admin`.
2. In the IBM Security Verify interface, select \*\*Applications **Add application**.

    Note

    Each system must be added as a separate application.
3. Navigate to **General tab** and perform the following steps:

    1. In the **Name** field, enter a unique name to identity the system.
    2. In the **Description** field, enter a brief description of the system.
    3. In the **Company name** field, enter name of organization or company.
4. Navigate to **Sign-on** tab and perform the following steps:

    1. Enter your **Application URL** which is used to access the management GUI for your system.
    2. Select **Authorization code** and **JWT bearer** Grant type.
    3. In the **Client ID** field, paste the **Application ID** value, which you have copied from Entra page.
    4. In the **Client Secret** field, paste the value, which you have copied from **Certificates & secrets** section at Entra side.
    5. For User consent, select **don't ask for consent** button.
    6. Copy the **Redirect URIs** and use it later in the Entra configuration.
    7. Select **Username** from the JWT bearer user identification.
    8. Ensure **Cloud Directory** is selected in JWT bearer default identity source.
    9. Ensure **Generate refresh token** option is unchecked.
    10. Ensure **Send all known user attributes in the ID token** option is checked.
    11. Under **Access policies**, Deselect **Use default policy** &gt; select the **Edit** icon &gt; **Select Always require 2FA in all devices** &gt; select **OK**.
    12. Ensure **Restrict custom scopes** option is unchecked.
    13. Select **Save**.
    14. On the confirmation page, select **Confirm** to enable single sign-on for the system.
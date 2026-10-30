---
layout: Conceptual
title: Configure LifeBalance Program for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/lifebalance-program-oidc-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra and LifeBalance Program.
services: active-directory
ms.workload: identity
ms.topic: how-to
ms.date: 2024-08-02T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: b226d162-0b35-aafa-0c40-9c6bb133e39d
document_version_independent_id: b226d162-0b35-aafa-0c40-9c6bb133e39d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/lifebalance-program-oidc-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/lifebalance-program-oidc-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/lifebalance-program-oidc-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 851286ae-2570-8dec-fc24-c5bb5f864404
---

# Configure LifeBalance Program for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate LifeBalance Program with Microsoft Entra ID. When you integrate LifeBalance Program with Microsoft Entra ID, you can:

Use Microsoft Entra ID to control who can access LifeBalance Program. Enable your users to be automatically signed in to LifeBalance Program with their Microsoft Entra accounts. Manage your accounts in one central location: the Azure portal.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a Microsoft Entra subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- LifeBalance Program single sign-on (SSO) enabled subscription with a custom domain. If you don't have a LifeBalance Program subscription you can visit the [LifeBalance sales page](https://sales.lifebalanceprogram.com/).

## Add LifeBalance Program from the gallery

To configure the integration of LifeBalance Program into Microsoft Entra ID, you need to add LifeBalance Program from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, enter **LifeBalance Program** in the search box.
4. Select **LifeBalance Program** in the results panel and then add the app. Wait a few seconds while the app is added to your tenant.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **LifeBalance Program** &gt; **Single sign-on**.
3. Perform the following steps in the below section:

    1. Select **Go to application**.

        [![Screenshot of showing the identity configuration.](common/go-to-application.png)](common/go-to-application.png#lightbox)
    2. Copy **Application (client) ID**, **Directory (tenant) ID** and use it later in the LifeBalance Program side configuration.

        ![Screenshot shows Settings for the configuration.](media/lifebalance-program-oidc-tutorial/directory.png)
4. Navigate to **Authentication** tab on the left menu and perform the following steps:

    1. In the **Redirect URIs** textbox, use the URL associated with your LifeBalance Program subscription in this format. These usually have the following pattern: `https://<LifeBalance Domain>/api/azure_token`

        - If you do not have a custom domain yet, please contact the [LifeBalance Program support team](mailto:info@lifebalanceprogram.com).

        [![Screenshot of showing the redirect values.](common/redirect.png)](common/redirect.png#lightbox)
    2. Select **Configure** button.
5. Navigate to **Certificates & secrets** on the left menu and perform the following steps:

    1. Go to **Client secrets** tab and select **+New client secret**.
    2. Enter a valid **Description** in the textbox and select **Expires** days from the drop-down as per your requirement and select **Add**.

        [![Screenshot of showing the client secrets value.](common/client-secret.png)](common/client-secret.png#lightbox)
    3. Once you add a client secret, **Value** is generated. Copy the value and use it later in the LifeBalance Program side configuration.

        [![Screenshot of showing how to add a client secret.](common/client.png)](common/client.png#lightbox)

### Create a Microsoft Entra test user

In this section, you create a test user called B.Simon.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **New user** &gt; **Create new user**, at the top of the screen.
4. In the **User**properties, follow these steps:
    1. In the **Display name** field, enter `B.Simon`.
    2. In the **User principal name** field, enter the username@companydomain.extension. For example, `B.Simon@contoso.com`.
    3. Select the **Show password** check box, and then write down the value that's displayed in the **Password** box.
    4. Select **Review + create**.
5. Select **Create**.

### Assign the Microsoft Entra test user

In this section, you enable B.Simon to use single sign-on by granting access to LifeBalance Program.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **LifeBalance Program**.
3. In the app's overview page, select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Add Assignment**dialog.
    1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then select the **Select** button at the bottom of the screen.
    2. If you're expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
    3. In the **Add Assignment** dialog, select the **Assign** button.

## Configure LifeBalance Program SSO

To complete the OAuth/OIDC federation setup on **LifeBalance Program** side, you need to send the copied values for Tenant ID, Application ID, and Client Secret from Entra to [LifeBalance Program SSO support team](mailto:sso@lifebalanceprogram.com) via secure email. The LifeBalance SSO team will set these values to have the OIDC connection set properly on both sides.
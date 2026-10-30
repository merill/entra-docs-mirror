---
layout: Conceptual
title: Configure Continuity Software Platform for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/continuity-software-platform-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra and Continuity Software Platform.
services: active-directory
ms.workload: identity
ms.topic: how-to
ms.date: 2024-05-07T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 7a9c48bf-120d-7d97-042d-6f82cf23cbdb
document_version_independent_id: 7a9c48bf-120d-7d97-042d-6f82cf23cbdb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/continuity-software-platform-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/continuity-software-platform-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/continuity-software-platform-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 6d3d6eb6-fd34-2ec9-adc6-a63df24b58e3
---

# Configure Continuity Software Platform for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Continuity Software Platform with Microsoft Entra ID. When you integrate Continuity Software Platform with Microsoft Entra ID, you can:

Use Microsoft Entra ID to control who can access Continuity Software Platform. Enable your users to be automatically signed in to Continuity Software Platform with their Microsoft Entra accounts. Manage your accounts in one central location: the Azure portal.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Continuity Software Platform single sign-on (SSO) enabled subscription.

## Add Continuity Software Platform from the gallery

To configure the integration of Continuity Software Platform into Microsoft Entra ID, you need to add Continuity Software Platform from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, enter **Continuity Software Platform** in the search box.
4. Select **Continuity Software Platform** in the results panel and then add the app. Wait a few seconds while the app is added to your tenant.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Continuity Software Platform** &gt; **Single sign-on**.
3. Perform the following steps in the below section:

    1. Select **Go to application**.

        ![Screenshot of showing the identity configuration.](common/go-to-application.png)
    2. Under **Endpoints**, copy **Application (client) ID** and **Directory (tenant) ID**. Use them later in the Continuity Software Platform side configuration.
4. Navigate to **Authentication** tab on the left menu and perform the following steps:

    1. In the **Redirect URIs** textbox, type a URL using the following pattern: `https://login.microsoftonline.com/<Tenant_ID>/oauth2`

        ![Screenshot of showing the redirect values.](media/continuity-software-platform-tutorial/authentication.png)
    2. Select **Configure**.

    Note

    The Redirect URI value isn't real. Replace &lt;Tenant\_ID&gt; with actual tenant id value in the Redirect URI pattern.
5. Navigate to **Certificates & secrets** on the left menu and perform the following steps:

    1. Go to **Client secrets** tab and select **+New client secret**.
    2. Enter a valid **Description** in the textbox and select **Expires** days from the drop-down as per your requirement and select **Add**.

        ![Screenshot of showing the client secrets value.](common/client-secret.png)
    3. Once you add a client secret, **Value** is generated. Copy the value and use it later in the Continuity Software Platform side configuration.

        ![Screenshot of showing how to add a client secret.](common/client.png)

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

In this section, you enable B.Simon to use single sign-on by granting access to Continuity Software Platform.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Continuity Software Platform**.
3. In the app's overview page, select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Add Assignment**dialog.
    1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then select the **Select** button at the bottom of the screen.
    2. If you're expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
    3. In the **Add Assignment** dialog, select the **Assign** button.

## Configure Continuity Software Platform SSO

Below are the configuration steps to complete the OAuth/OIDC federation setup:

1. Sign into the Continuity Software Platform with admin account.
2. Select **Admin** on the left bar of the **Settings** tab. Then select **Identity Providers** under **Access**.
3. Select **+**.
4. The **Add Identity provider** window is displayed.

    a. In the **Name** field, enter the name for identification.

    b. In the **Description** field, enter a valid description value.

    c. Select **Type** as Azure AD.

    d. In the **Client ID** field, paste the **Application ID** value, which you have copied from Entra page.

    e. In the **Client Secret** field, paste the value, which you have copied from **Certificates & secrets** section at Entra side.

    f. In the **Tenant** field, paste the **Tenant ID** value, which you have copied from Entra page.
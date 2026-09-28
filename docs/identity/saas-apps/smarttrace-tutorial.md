---
layout: Conceptual
title: Configure SmartTrace for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/smarttrace-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra and SmartTrace.
services: active-directory
ms.workload: identity
ms.topic: how-to
ms.date: 2024-09-10T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 9f1dcaa4-0295-7fde-eec5-29833ec82cbd
document_version_independent_id: 9f1dcaa4-0295-7fde-eec5-29833ec82cbd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/smarttrace-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/smarttrace-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/smarttrace-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 85d0dd54-bbfa-15a7-0917-15859dcd6a8c
---

# Configure SmartTrace for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate SmartTrace with Microsoft Entra ID. When you integrate SmartTrace with Microsoft Entra ID, you can:

- Use Microsoft Entra ID to control who can access SmartTrace.
- Enable your users to be automatically signed in to SmartTrace with their Microsoft Entra accounts.
- Manage your accounts in one central location: the Azure portal.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- SmartTrace single sign-on (SSO) enabled subscription.

## Add SmartTrace from the gallery

To configure the integration of SmartTrace into Microsoft Entra ID, you need to add SmartTrace from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, enter **SmartTrace** in the search box.
4. Select **SmartTrace** in the results panel and then add the app. Wait a few seconds while the app is added to your tenant.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **SmartTrace** &gt; **Single sign-on**.
3. Perform the following steps in the below section:

    1. Select **Go to application**.

        ![Screenshot showing the identity configuration.](common/go-to-application.png)
    2. Copy **Application (client) ID** and **Directory (tenant) ID**, use it later in the SmartTrace side configuration.

        ![Screenshot of application client values.](media/smarttrace-tutorial/app.png)
4. Navigate to **Authentication** tab on the left menu and perform the following steps:

    1. In the **Redirect URIs** textbox, type a URL using the following pattern: `https://api.smarttrace.ai/v1/auth/callback/azure/<InstanceName>`
    2. In the **Front-channel logout URL** textbox, type a URL using the following pattern: `https://api.smarttrace.ai/v1/auth/callback/azure-logout/<InstanceName>`![Screenshot showing the redirect values.](common/log.png)
    3. Select **Configure** button.
5. Navigate to **Certificates & secrets** on the left menu and perform the following steps:

    1. Go to **Client secrets** tab and select **+New client secret**.
    2. Enter a valid **Description** in the textbox and select **Expires** days from the drop-down as per your requirement and select **Add**.

        ![Screenshot showing the client secrets value.](common/client-secret.png)
    3. Once you add a client secret, **Value** is generated. Copy the value and use it later in the SmartTrace side configuration.

        ![Screenshot showing how to add a client secret.](common/client.png)

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

In this section, you enable B.Simon to use single sign-on by granting access to SmartTrace.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **SmartTrace**.
3. In the app's overview page, select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Add Assignment**dialog.
    1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then select the **Select** button at the bottom of the screen.
    2. If you're expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
    3. In the **Add Assignment** dialog, select the **Assign** button.

## Configure SmartTrace SSO

Below are the configuration steps to complete the OIDC federation setup:

1. Sign into the SmartTrace site as an administrator.
2. Go to **SmartTrace** header &gt; select **Integrations** and select pencil icon on the **Azure Active Directory** tile.

    ![Screenshot of the SmartTrace header integrations.](media/smarttrace-tutorial/tile.png)
3. Perform the following steps in the **Azure Active Directory** page:

    ![Screenshot of the configuration page in SmartTrace.](media/smarttrace-tutorial/header.png)

    1. In the **APPLICATION ID** textbox, paste the **Application (client) ID**, which you have copied from the Microsoft Entra page.
    2. In the **TENANT ID** textbox, paste the **Directory (tenant) ID**, which you have copied from the Microsoft Entra page.
    3. In the **APPLICATION (CLIENT) SECRET** textbox, paste the value, which you have copied from **Certificates & secrets** section at Microsoft Entra side.
    4. Select **Save**.
---
layout: Conceptual
title: Configure Lexmark Cloud Services (OIDC) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/lexmark-cloud-services-oidc-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra and Lexmark Cloud Services (OIDC).
services: active-directory
ms.workload: identity
ms.topic: how-to
ms.date: 2025-10-03T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 2511c707-93cf-733f-e542-0ba9fc69c1e1
document_version_independent_id: 2511c707-93cf-733f-e542-0ba9fc69c1e1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/lexmark-cloud-services-oidc-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/lexmark-cloud-services-oidc-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/lexmark-cloud-services-oidc-tutorial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/486161dc-fa28-4625-9b1c-1a21d690bc8d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5dd28c86-729c-4723-ab5a-57e26fcec2a8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7aa4baac-024b-42b7-5666-13c5c5aaf095
---

# Configure Lexmark Cloud Services (OIDC) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Lexmark Cloud Services (OIDC) with Microsoft Entra ID. When you integrate Lexmark Cloud Services (OIDC) with Microsoft Entra ID, you can:

Use Microsoft Entra ID to control who can access Lexmark Cloud Services (OIDC). Enable your users to be automatically signed in to Lexmark Cloud Services (OIDC) with their Microsoft Entra accounts. Manage your accounts in one central location: the Azure portal.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Lexmark Cloud Services (OIDC) single sign-on (SSO) enabled subscription.

## Add Lexmark Cloud Services (OIDC) from the gallery

To configure the integration of Lexmark Cloud Services (OIDC) into Microsoft Entra ID, you need to add Lexmark Cloud Services (OIDC) from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Browse Microsoft Entra App Gallery** section, enter **Lexmark Cloud Services (OIDC)** in the search box.
4. Select **Lexmark Cloud Services (OIDC)** in the results panel and then add the app. Wait a few seconds while the app is added to your tenant.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Lexmark Cloud Services (OIDC)** &gt; **Single sign-on**.
3. Perform the following steps:

    1. Select **Go to application**.

        [![Screenshot of showing the identity configuration.](media/lexmark-oidc-tutorial/go-to-application.png)](media/lexmark-oidc-tutorial/go-to-application.png#lightbox)
    2. Copy **Application (client) ID**. You'll use it later in the Lexmark Cloud Services (OIDC) SSO configuration.

        [![Screenshot of application client values.](common/application-id.png)](common/application-id.png#lightbox)
    3. Under **Endpoints** tab, copy **OpenID Connect metadata document** link. You'll use it later in the Lexmark Cloud Services (OIDC) SSO configuration.

        ![Screenshot of showing the endpoints on tab.](common/endpoints.png)
4. Navigate to **Certificates & secrets** on the left menu and perform the following steps:

    1. Go to **Client secrets** tab and select **+New client secret**.
    2. Enter a valid **Description** in the textbox and select **Expires** days from the drop-down as per your requirement and select **Add**.

        [![Screenshot of showing the client secrets value.](media/lexmark-oidc-tutorial/client-secret.png)](media/lexmark-oidc-tutorial/client-secret.png#lightbox)
    3. Once you add a client secret, **Value** is generated. Copy the value. You'll use it later in the Lexmark Cloud Services (OIDC) SSO configuration.

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

In this section, you enable B.Simon to use single sign-on by granting access to Lexmark Cloud Services (OIDC).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Lexmark Cloud Services (OIDC)**.
3. In the app's overview page, select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Add Assignment**dialog.
    1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then select the **Select** button at the bottom of the screen.
    2. In the **Add Assignment** dialog, select the **Assign** button.

## Configure Lexmark Cloud Services (OIDC) SSO

To complete the steps in this section, ensure you have the Organization Administrator role for your organization in Lexmark Cloud Services. Also review the [Lexmark documentation](https://support.lexmark.com/en_us/manuals-guides/online/Lexmark-Cloud-Platform/configuring-azure-ad-federation-for-oidc-overview-.html) on Configuring Microsoft Entra ID with OIDC Federation

## Configure your organization for SSO with OIDC

1. Log in to Lexmark Cloud Services as an Organization Administrator.
2. From the Lexmark Cloud services dashboard or from the navigation menu on the right side of the screen, select **Account Management**. ![Screenshot of selecting Account Management.](media/lexmark-oidc-tutorial/select-account-management.png)
3. If necessary, select your organization, and then select **Next**. ![Screenshot of selecting organization.](media/lexmark-oidc-tutorial/select-organization.png)
4. In the Organization section, select **Authentication Provider**. ![Screenshot of selecting Authentication Provider.](media/lexmark-oidc-tutorial/select-authentication-provider.png)
5. Select **Configure** on **Authentication Provider** pane. ![Screenshot of configure an Authentication Provider.](media/lexmark-oidc-tutorial/select-configure-auth-provider.png)
6. From the **Authentication Provider Type** menu, select **OIDC**.
7. Enter the required information copied from Microsoft Entra ID:

    - Client ID (Application client ID)
    - Client Secret (Client secret value)
    - Well-known URL (OpenID Connect metadata document URL)

Note

The Domains field allows Lexmark Cloud Services to automatically establish a new user account after the user logs in. Listing each organization's domain is not required. If no domain is set, then the new users must be manually added to the organization before they log in.

1. Select **Configure Authentication Provider**. ![Screenshot of Configure Authentication Provider.](media/lexmark-oidc-tutorial/configure-authentication-provider.png)

Note

Once authentication configuration is completed, you will receive an email on configuration status. In case of configuration failure, contact your Lexmark representative.

1. The relying party redirect URIs for US and EU regions. (To be used in the Microsoft Entra Authentication Configuration)
    - US region: `https://lexmarkb2c.b2clogin.com/lexmarkb2c.onmicrosoft.com/oauth2/authresp`
    - EU region: `https://lexmarkb2ceu.b2clogin.com/lexmarkb2ceu.onmicrosoft.com/oauth2/authresp`

Note

Select ID Tokens in Implicit grant and hybrid flows under Entra Authentication Configuration

### Test the SSO configuration

Refer to [Testing a federation] (https://support.lexmark.com/en_us/manuals-guides/online/Lexmark-Cloud-Platform/testing-a-federation-v58742261.html?toc=2.5.4.10) on how to test that your SSO is set up successfully.
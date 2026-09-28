---
layout: Conceptual
title: How to configure an application to expose a web API - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-configure-app-expose-web-apis
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this how-to guide, register a web API with the Microsoft identity platform and configure its scopes, exposing it to clients for permissions-based access to the API's resources.
manager: pmwongera
ms.date: 2025-05-14T00:00:00.0000000Z
ms.reviewer: sureshja
ms.topic: how-to
ms.custom: sfi-image-nochange
locale: en-us
document_id: 23b434db-9091-da08-2c96-839d462bc114
document_version_independent_id: 7bee76e7-acdc-5bc5-50ec-6004c73b9a95
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/quickstart-configure-app-expose-web-apis.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/quickstart-configure-app-expose-web-apis
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/quickstart-configure-app-expose-web-apis.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 00aa8b83-5b74-5fda-5f30-9f63dadd145c
---

# How to configure an application to expose a web API - Microsoft identity platform | Microsoft Learn

In this how-to guide, you'll register a web API with the Microsoft identity platform and expose it to client apps by adding a scope. By registering your web API and exposing it through scopes, assigning an owner and app role, you can provide permissions-based access to its resources to authorized users and client apps that access your API.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- An application registered in the [Microsoft Entra admin center](https://entra.microsoft.com/). If you don't have one, [register an application](quickstart-register-app#register-an-application) now.

## Register the web API

Access to APIs requires configuration of access scopes and roles. If you want to expose your resource application web APIs to client applications, configure access scopes and roles for the API. If you want a client application to access a web API, configure permissions to access the API in the app registration. To provide scoped access to the resources in your web API, you first need to register the API with the Microsoft identity platform.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to the tenant containing the app registration from the **Directories + subscriptions** menu.
3. Perform the steps in [register an application](quickstart-register-app#register-an-application) and skip the **Redirect URI (optional)** section. You don't need to configure a redirect URI for a web API since no user is logged in interactively.

## Assign application owner

1. In your app registration, under **Manage**, select **Owners**, and **Add owners**.
2. In the new window, find and select the owner(s) that you want to assign to the application. Selected owners appear in the right panel. Once done, confirm with **Select**. The app owner(s) will now appear in the owner's list.

Note

Ensure that an owner is assigned to both the API application and the application you want to add permissions to, otherwise the API will not be listed when requesting API permissions.

## Assign app role

1. In your app registration, under **Manage**, select **App roles**, and **Create app role**.
2. Next, specify the app role's attributes in the **Create app role** pane. For this walk-through, you can use the example values or specify your own.

    | Field | Description | Example |
    | --- | --- | --- |
    | **Display name** | The name of your app role | *Employee Records* |
    | **Allowed member types** | Specifies whether the app role can be assigned to users/groups and/or applications | *Applications* |
    | **Value** | The value displayed in the "roles" claim of a token | `Employee.Records` |
    | **Description** | A more detailed description of the app role | *Applications have access to employee records* |
3. Select the checkbox to enable the app role, and then select **Apply**.

## Add a scope

With the web API registered, assigned an app role and owner, you can add scopes to the API's code so it can provide granular permission to consumers.

The code in a client application requests permission to perform operations defined by your web API by passing an access token along with its requests to the protected resource (the web API). Your web API then performs the requested operation only if the access token it receives contains the scopes required for the operation.

### Add a scope requiring admin and user consent

First, follow these steps to create an example scope named `Employees.Read.All`:

1. Select **Expose an API**.
2. At the top of the page, select **Add** next to **Application ID URI**. This defaults to `api://<application-client-id>`. The App ID URI acts as the prefix for the scopes you'll reference in your API's code, and it must be globally unique. Select **Save**.
3. Select **Add a scope**:

    ![An app registration's Expose an API pane in the Azure portal](media/quickstart-configure-app-expose-web-apis/portal-02-expose-api.png)
4. Next, specify the scope's attributes in the **Add a scope** pane. For this walk-through, you can use the example values or specify your own.

    | Field | Description | Example |
    | --- | --- | --- |
    | **Scope name** | The name of your scope. A common scope naming convention is `resource.operation.constraint`. | `Employees.Read.All` |
    | **Who can consent** | Whether this scope can be consented to by users or if admin consent is required. **Admins only** should be used for higher-privileged permissions. | **Admins and users** |
    | **Admin consent display name** | A short description of the scope's purpose that only admins will see. | *Read-only access to Employee records* |
    | **Admin consent description** | A more detailed description of the permission granted by the scope that only admins will see. | *Allow the application to have read-only access to all Employee data.* |
    | **User consent display name** | A short description of the scope's purpose. Shown to users only if you set **Who can consent** to **Admins and users**. | *Read-only access to your Employee records* |
    | **User consent description** | A more detailed description of the permission granted by the scope. Shown to users only if you set **Who can consent** to **Admins and users**. | *Allow the application to have read-only access to your Employee data.* |
    | **State** | Whether the scope is enabled or disabled. | **Enabled** |
5. Select **Add scope**.
6. (Optional) To suppress prompting for consent by users of your app to the scopes you've defined, you can *pre-authorize* the client application to access your web API. Pre-authorize *only* those client applications you trust since your users won't have the opportunity to decline consent.

    1. Under **Authorized client applications**, select **Add a client application**.
    2. Enter the **Application (client) ID** of the client application you want to pre-authorize. For example, that of a web application you've previously registered.
    3. Under **Authorized scopes**, select the scopes for which you want to suppress consent prompting, then select **Add application**.

    If you followed this optional step, the client app is now a pre-authorized client app (PCA), and users won't be prompted for their consent when signing in to it.

### Add a scope requiring admin consent

Next, add another example scope named `Employees.Write.All` that only admins can consent to. Scopes that require admin consent are typically used for providing access to higher-privileged operations, and often by client applications that run as backend services or daemons that don't sign in a user interactively.

To add the `Employees.Write.All` example scope, follow the steps in the Add a scope section and specify these values in the **Add a scope** pane. Select **Add scope** when you're done:

| Field | Example value |
| --- | --- |
| **Scope name** | `Employees.Write.All` |
| **Who can consent** | **Admins only** |
| **Admin consent display name** | *Write access to Employee records* |
| **Admin consent description** | *Allow the application to have write access to all Employee data.* |
| **User consent display name** | *None (leave empty)* |
| **User consent description** | *None (leave empty)* |
| **State** | **Enabled** |

### Verify the exposed scopes

If you have successfully added both example scopes described in the previous sections, they'll appear in the **Expose an API** pane of your web API's app registration, similar to the following image:

![Screenshot of the Expose an API pane showing two exposed scopes.](media/quickstart-configure-app-expose-web-apis/portal-03-scopes-list.png)

The scope's full string is the concatenation of your web API's **Application ID URI** and the scope's **Scope name**. For example, if your web API's application ID URI is `https://contoso.com/api` and the scope name is `Employees.Read.All`, the full scope is:

`https://contoso.com/api/Employees.Read.All`

## Using the exposed scopes

In the next article in this series, you configure a client app's registration with access to your web API and the scopes you defined by following the steps in this article.

Once a client app registration is granted permission to access your web API, the client can be issued an OAuth 2.0 access token by the identity platform. When the client calls the web API, it presents an access token whose scope (`scp`) claim is set to the permissions you've specified in the client's app registration.

You can expose additional scopes later as necessary. Consider that your web API can expose multiple scopes associated with several operations. Your resource can control access to the web API at runtime by evaluating the scope (`scp`) claims in the OAuth 2.0 access token it receives.
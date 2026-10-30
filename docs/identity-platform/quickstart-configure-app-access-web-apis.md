---
layout: Conceptual
title: Web API app registration and API permissions - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-configure-app-access-web-apis
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this quickstart, you learn how to configure app registration and API permissions for a Web API, and how to grant admin consent to these permissions.
manager: pmwongera
ms.custom: 
ms.date: 2025-01-27T00:00:00.0000000Z
ms.reviewer: sureshja
ms.topic: how-to
locale: en-us
document_id: 006699d8-d208-ec2e-9b14-ec6c5d4bd71f
document_version_independent_id: b9ad346f-2140-8d7b-c5aa-b5e4d7bae866
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/quickstart-configure-app-access-web-apis.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/quickstart-configure-app-access-web-apis
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/quickstart-configure-app-access-web-apis.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 632aed2e-ac48-acf3-7af7-a30dee5806ee
---

# Web API app registration and API permissions - Microsoft identity platform | Microsoft Learn

In this how-to guide, you provide a client app registered with the Microsoft identity platform with scoped, permissions-based access to your own web API. You also provide the client app access to Microsoft Graph.

By specifying a web API's scopes in your client app's registration, the client app can obtain an access token containing those scopes from the Microsoft identity platform. Within its code, the web API can then provide permission-based access to its resources based on the scopes found in the access token.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Completion of [Quickstart: Register an application](quickstart-register-app)
- Completion of [Quickstart: Configure an application to expose a web API](quickstart-configure-app-expose-web-apis)

## Add permissions to access your web API

To enable client applications to access web APIs, you need to add permissions to the client application to access the web API. Similarly, in the web API, you need to configure access scopes and roles for the client application.

To grant a client application to access to your own web API, you need to have two app registrations;

- [A client app registration](quickstart-register-app#register-an-application)
- [A web API registration](quickstart-configure-app-expose-web-apis) with exposed scopes

The diagram shows how the two app registrations relate to one another, where the client app has different permission types and the web API has different scopes that the client application can access. In this section, you add permissions to the client app's registration.

![Line diagram showing a web API with exposed scopes on the right and a client app on the left with those scopes selected as permissions](media/quickstart-configure-app-access-web-apis/diagram-01-app-permission-to-api-scopes.svg)

Once you've registered both your client app and web API and you've exposed the API by creating scopes, you can configure the client's permissions to the API by following these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to the tenant containing the app registration from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **App registrations**, and then select your client application (*not* your web API).
4. Select **API permissions**, then **Add a permission** and select **My APIs** in the sidebar.

    ![Screenshot with highlighted buttons of App registrations, API permissions, Add a permission and My APIs to enable the user to request API permissions.](media/quickstart-configure-app-access-web-apis/portal-path-to-my-apis-pane.png)
5. Select the web API you registered as part of the prerequisites, and select **Delegated permissions**.

    - **Delegated permissions** are appropriate for client apps that access a web API as the signed-in user, and whose access should be restricted to the permissions you select in the next step. Leave **Delegated permissions** selected for this example.
    - **Application permissions** are for service- or daemon-type applications that need to access a web API as themselves, without user interaction for sign-in or consent. Unless you've defined application roles for your web API, this option is disabled.
6. Under **Select permissions**, expand the resource whose scopes you defined for your web API, and select the permissions the client app should have on behalf of the signed-in user.

    - If you used the example scope names specified in the [previous quickstart](quickstart-configure-app-expose-web-apis), you should see **Employees.Read.All** and `Employees.Write.All`.
7. Select the permission you created while completing the prerequisites, for example, `Employees.Read.All`.
8. Select **Add permissions** to complete the process.

After adding permissions to your API, you should see the selected permissions under **Configured permissions**. The following image shows the example *Employees.Read.All* delegated permission added to the client app's registration.

![Configured permissions pane in the Azure portal showing the newly added permission](media/quickstart-configure-app-access-web-apis/portal-02-configured-permissions-pane.png)

You might also notice the *User.Read* permission for the Microsoft Graph API. This permission is added automatically when you register an app in the Azure portal.

## Add permissions to access Microsoft Graph

In addition to accessing your own web API on behalf of the signed-in user, your application might also need to access or modify the user's (or other) data stored in Microsoft Graph. Or you might have service or daemon app that needs to access Microsoft Graph as itself, performing operations without any user interaction.

### Delegated permission to Microsoft Graph

Configure delegated permission to Microsoft Graph to enable your client application to perform operations on behalf of the logged-in user, for example reading their email or modifying their profile. By default, users of your client app are asked when they sign in to consent to the delegated permissions you've configured for it.

1. From the **Overview** page of your client application, select **API permissions** &gt; **Add a permission** &gt; **Microsoft Graph**
2. Select **Delegated permissions**. Microsoft Graph exposes many permissions, with the most commonly used shown at the top of the list.
3. Under **Select permissions**, select the following permissions:

    | Permission | Description |
    | --- | --- |
    | `email` | View users' email address |
    | `offline_access` | Maintain access to data you have given it access to |
    | `openid` | Sign users in |
    | `profile` | View users' basic profile |
4. Select **Add permissions** to complete the process.

Whenever you configure permissions, users of your app are asked at sign-in for their consent to allow your app to access the resource API on their behalf.

As an admin, you can also grant consent on behalf of *all* users so they're not prompted to do so. Admin consent is discussed later in the More on API permissions and admin consent section of this article.

### Application permission to Microsoft Graph

Configure application permissions for an application that needs to authenticate as itself without user interaction or consent. Application permissions are typically used by background services or daemon apps that access an API in a "headless" manner, and by web APIs that access another (downstream) API.

In the following steps, you grant permission to Microsoft Graph's *Files.Read.All* permission as an example.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to the tenant containing the app registration from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **App registrations**, and then select your client application.
4. Select **API permissions** &gt; **Add a permission** &gt; **Microsoft Graph** &gt; **Application permissions**.
5. All permissions exposed by Microsoft Graph are shown under **Select permissions**.
6. Select the permission or permissions you want to grant your application. As an example, you might have a daemon app that scans files in your organization, alerting on a specific file type or name. Under **Select permissions**, expand **Files**, and then select the `Files.Read.All` permission.
7. Select **Add permissions**.
8. Some permissions, like Microsoft Graph's *Files.Read.All* permission, require admin consent. You grant admin consent by selecting the **Grant admin consent** button, discussed later in the Admin consent button section.

### Configure client credentials

Apps that use application permissions authenticate as themselves by using their own credentials, without requiring any user interaction. Before your application (or API) can access Microsoft Graph, your own web API, or another API by using application permissions, you must configure that client app's credentials.

For more information about configuring an app's credentials, see the [Add credentials](how-to-add-credentials) section of [Quickstart: Register an application with the Microsoft identity platform](quickstart-register-app).

## More on API permissions and admin consent

The **API permissions** pane of an app registration contains the Configured permissions table and the Admin consent button, which are described in the following sections.

### Configured permissions

The **Configured permissions** table on the **API permissions** pane shows the list of permissions that your application requires for basic operation - the *required resource access (RRA)* list. Users, or their admins, will need to consent to these permissions before using your app. Other, optional permissions can be requested later at runtime (using dynamic consent).

This is the minimum list of permissions people will have to consent to for your app. There could be more, but these will always be required. For security and to help users and admins feel more comfortable using your app, never ask for anything you don’t need.

You can add or remove the permissions that appear in this table by using the steps outlined above. As an admin, you can grant admin consent for the full set of an API's permissions that appear in the table, and revoke consent for individual permissions.

### Admin consent button

The **Grant admin consent for {your tenant}** button allows an admin to grant admin consent to the permissions configured for the application. When you select the button, a dialog is shown requesting that you confirm the consent action.

![Grant admin consent button highlighted in the Configured permissions pane in the Azure portal](media/quickstart-configure-app-access-web-apis/portal-03-grant-admin-consent-button.png)

After granting consent, the permissions that required admin consent are shown as having consent granted:

![Configure permissions table in Azure portal showing admin consent granted for the Files.Read.All permission](media/quickstart-configure-app-access-web-apis/portal-04-admin-consent-granted.png)

The **Grant admin consent** button is *disabled* if you aren't an admin or if no permissions have been configured for the application. If you have permissions that have been granted but not yet configured, the admin consent button prompts you to handle these permissions. You can add them to configured permissions or remove them.

### Remove application permissions

It's important not to give an application too many permissions than is necessary. To revoke admin consent for a permission in your application;

1. Navigate to your application and select **API permissions**.
2. Under **Configured permissions**, select the three dots next to the permission you wish to remove, and select **Revoke admin consent**.
3. In the pop-up that appears, select **Yes, remove** to revoke the admin consent for the permission.
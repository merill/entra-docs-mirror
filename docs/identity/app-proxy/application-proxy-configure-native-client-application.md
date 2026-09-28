---
layout: Conceptual
title: Publish native client apps - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-configure-native-client-application
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Publish native client applications through Microsoft Entra application proxy to provide secure remote access to on-premises APIs and resources.
ms.custom: devx-track-dotnet
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
locale: en-us
document_id: 604591be-b282-efb2-56b0-3bf78c97d00e
document_version_independent_id: d2a5decb-a520-4d01-4f26-e212a61b8269
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-configure-native-client-application.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-configure-native-client-application
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-configure-native-client-application.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 14d1a01b-10b1-b52d-ca74-63b67bbac233
---

# Publish native client apps - Microsoft Entra ID | Microsoft Learn

## Overview

Microsoft Entra application proxy is used to publish web apps. You can also use it to publish native client applications configured with the Microsoft Authentication Library (MSAL). Client applications differ from web apps because they're installed on a device, while web apps are accessed through a browser.

To support native client applications, application proxy accepts Microsoft Entra ID-issued tokens that are sent in the header. The application proxy service does the authentication for the users. This solution doesn't use application tokens for authentication.

![Diagram that shows the relationship between end users, Microsoft Entra ID, and published applications.](media/application-proxy-configure-native-client-application/richclientflow.png)

To publish native applications, use the Microsoft Authentication Library, which takes care of authentication and supports many client environments. Application proxy fits into the [Desktop app that calls a web API on behalf of a signed-in user](../../identity-platform/authentication-flows-app-scenarios#desktop-app-that-calls-a-web-api-on-behalf-of-a-signed-in-user) scenario.

This article walks you through the four steps to publish a native application with application proxy and the Microsoft Authentication Library (MSAL).

## Step 1: Publish your proxy application

Publish your proxy application as you would any other application and assign users to access your application. For more information, see [Publish applications with application proxy](application-proxy-add-on-premises-application).

## Step 2: Register your native application

You now need to register your application in Microsoft Entra ID.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Select your username in the upper-right corner. Verify you're signed in to a directory that uses application proxy. If you need to change directories, select **Switch directory** and choose a directory that uses application proxy.
3. Browse to **Entra ID** &gt; **App registrations**. The list of all app registrations appears.
4. Select **New registration**. The **Register an application** page appears.

    ![Screenshot that shows the app registration creation page in the Microsoft Entra admin center.](media/application-proxy-configure-native-client-application/create.png)
5. In the **Name** heading, specify a user-facing display name for your application.
6. Under the **Supported account types** heading, select an access level using these guidelines.

    - To target only accounts that are internal to your organization, select **Accounts in this organizational directory only**.
    - To target only business or educational customers, select **Accounts in any organizational directory**.
    - To target the widest set of Microsoft identities, select **Accounts in any organizational directory and personal Microsoft accounts**.
7. Under **Redirect URI**, select **Public client (mobile & desktop)**, and then type the redirect URI `https://login.microsoftonline.com/common/oauth2/nativeclient` for your application.
8. Select and read the **Microsoft Platform Policies**, and then select **Register**. An overview page for the new application registration is created and displayed.

For more detailed information about creating a new application registration, see [Integrating applications with Microsoft Entra ID](../../identity-platform/quickstart-register-app).

## Step 3: Grant access to your proxy application

Your native application is registered. Give it access to the proxy application:

1. In the sidebar of the new application registration page, select **API permissions**. The **API permissions** page for the new application registration appears.
2. Select **Add a permission**. The **Request API permissions** page appears.
3. Under the **Select an API** setting, select **APIs my organization uses**. A list appears, containing the applications in your directory that expose APIs.
4. Type in the search box or scroll to find the proxy application that you published in Step 1: Publish your proxy application, and then select the proxy application.
5. In the **What type of permissions does your application require?** heading, select the permission type. If your native application needs to access the proxy application API as the signed-in user, choose **Delegated permissions**.
6. In the **Select permissions** heading, select the desired permission, and select **Add permissions**. The **API permissions** page for your native application now shows the proxy application and permission API that you added.

## Step 4: Add the Microsoft Authentication Library to your code (.NET C# sample)

Edit the native application code in the authentication context of the Microsoft Authentication Library (MSAL) to include the following text:

```
// Acquire access token from Microsoft Entra ID for proxy application
IPublicClientApplication clientApp = PublicClientApplicationBuilder
.Create(<App ID of the Native app>)
.WithDefaultRedirectUri() // will automatically use the default Uri for native app
.WithAuthority("https://login.microsoftonline.com/{<Tenant ID>}")
.Build();

AuthenticationResult authResult = null;
var accounts = await clientApp.GetAccountsAsync();
IAccount account = accounts.FirstOrDefault();

IEnumerable<string> scopes = new string[] {"<Scope>"};

try
 {
    authResult = await clientApp.AcquireTokenSilent(scopes, account).ExecuteAsync();
 }
    catch (MsalUiRequiredException ex)
 {
     authResult = await clientApp.AcquireTokenInteractive(scopes).ExecuteAsync();                
 }

if (authResult != null)
 {
  //Use the Access Token to access the Proxy Application

  HttpClient httpClient = new HttpClient();
  httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
  HttpResponseMessage response = await httpClient.GetAsync("<Proxy App Url>");
 }
```

The required info in the sample code can be found in the Microsoft Entra admin center, as follows:

| Info required | How to find it in the Microsoft Entra admin center |
| --- | --- |
| &lt;Tenant ID&gt; | **Entra ID** &gt; **Overview** &gt; **Properties** |
| &lt;App ID of the Native app&gt; | **Application registration** &gt; *your native application* &gt; **Overview** &gt; **Application ID** |
| &lt;Scope&gt; | **Application registration** &gt; *your native application* &gt; **API permissions** &gt; select the Permission API (user\_impersonation) &gt; A panel with the caption **user\_impersonation** appears on the right-hand side. &gt; The scope is the URL in the edit box. |
| &lt;Proxy App URL&gt; | the External URL and path to the API |

After you edit the MSAL code with these parameters, your users can authenticate to native client applications even when they're outside of the corporate network.
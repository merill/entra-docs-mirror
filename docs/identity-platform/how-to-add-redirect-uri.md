---
layout: Conceptual
title: How to add a redirect URI to your application - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/how-to-add-redirect-uri
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to add a redirect URI to your application in Microsoft Entra to securely handle authentication tokens and enhance app security.
manager: pmwongera
ms.custom: 
ms.date: 2026-05-14T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
locale: en-us
document_id: e5af403f-437a-9db6-fd4c-bb53900fa376
document_version_independent_id: e5af403f-437a-9db6-fd4c-bb53900fa376
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/how-to-add-redirect-uri.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/how-to-add-redirect-uri
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/how-to-add-redirect-uri.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 19303122-df98-884e-5fb4-556ac75a101d
---

# How to add a redirect URI to your application - Microsoft identity platform | Microsoft Learn

To sign in a user, your application must send a login request to the Microsoft Entra authorization endpoint, with a redirect URI specified as a parameter. The redirect URI is a critical security feature that ensures the Microsoft Entra authentication server only sends authorization codes and access tokens to the intended recipient.

## Prerequisites

- [Quickstart: Register an app in Microsoft Entra ID](quickstart-register-app).

## Add a redirect URI

A *redirect URI* is where the Microsoft identity platform sends security tokens after authentication. Redirect URIs are configured on the **Authentication** page in the Microsoft Entra admin center. For **Web** and **Single-page applications**, you specify a redirect URI manually. For **Mobile and desktop** platforms, you select from generated redirect URIs.

Follow these steps to configure settings based on your target platform or device:

1. In the Microsoft Entra admin center, in **App registrations**, select your application.
2. Under **Manage**, select **Authentication**.
3. On the **Redirect URI configuration** tab, select **Add Redirect URI**.
4. On the **Select a platform to add redirect URI** pane, select the tile for your application type (platform) to configure its settings.

    | Platform | Configuration settings | Example |
    | --- | --- | --- |
    | **Web** | Enter the **Redirect URI** for a web app that runs on a server. You can also enter a **Front-channel logout URL**. | `https://contoso.com/auth-response` or `http://localhost:3000/auth-response` if you run your app locally. |
    | **Single-page application** | Enter a **Redirect URI** for client-side apps using JavaScript, Angular, React.js, or Blazor WebAssembly. You can also enter a **Front-channel logout URL**. | `https://contoso.com/auth-response` or `http://localhost:3000/auth-response` if you run your app locally. |
    | **iOS / macOS** | Enter the app **Bundle ID**, which generates a redirect URI for you. Find it in **Build Settings** or in Xcode in *Info.plist*. | `com.microsoft.identityapp.ciam.MSALiOS`. |
    | **Android** | Enter the app **Package name**, which generates a redirect URI for you. Find it in the *AndroidManifest.xml* file. Also generate and enter the **Signature hash**. | Package name: • `com.azuresamples.msalandroidapp` Signature has: • `aB1cD2eF-3gH4iJ5kL6-mN7oP8qR=`. |
    | **Mobile and desktop applications** | Select this platform for desktop apps or mobile apps not using MSAL or a broker. Select a suggested **Redirect URI**, or specify one or more **Custom redirect URIs** | `https://login.microsoftonline.com/common/oauth2/nativeclient` |
5. Select **Configure** to complete the platform configuration.

### Redirect URI restrictions

There are some restrictions on the format of the redirect URIs you add to an app registration. For details about these restrictions, see [Redirect URI (reply URL) restrictions and limitations](reply-url).
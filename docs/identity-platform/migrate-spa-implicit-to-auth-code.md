---
layout: Conceptual
title: Migrate JavaScript single-page app from implicit grant to authorization code flow - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/migrate-spa-implicit-to-auth-code
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: How to update a JavaScript SPA using MSAL.js 2.x and the authorization code flow with PKCE and CORS support.
manager: pmwongera
ms.date: 2025-05-12T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-ropc-nochange
locale: en-us
document_id: d2e35563-a9af-c235-f151-7771cee56326
document_version_independent_id: f196053d-a74e-b19f-bb7d-8470d73942dc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/migrate-spa-implicit-to-auth-code.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/migrate-spa-implicit-to-auth-code
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/migrate-spa-implicit-to-auth-code.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 5da1f2fe-1cfc-89fb-0efd-b127f0abe9a6
---

# Migrate JavaScript single-page app from implicit grant to authorization code flow - Microsoft identity platform | Microsoft Learn

The Microsoft Authentication Library for JavaScript (MSAL.js) v2.0 brings support for the authorization code flow with PKCE and CORS to single-page applications on the Microsoft identity platform. Follow the steps in the sections below to migrate your MSAL.js 1.x application using the implicit grant to MSAL.js 2.0+ (hereafter *2.x*) and the auth code flow.

MSAL.js 2.x improves on MSAL.js 1.x by supporting the authorization code flow in the browser instead of the implicit grant flow. MSAL.js 2.x does **NOT** support the implicit flow.

## Perform migration steps

To update your application to MSAL.js 2.x and the auth code flow, there are three primary steps:

1. Switch your app registration redirect URI(s) from **Web** platform to **Single-page application** platform.
2. Update your code from MSAL.js 1.x to **2.x**.
3. Disable the implicit grant in your app registration when all applications sharing the registration have been updated to MSAL.js 2.x and the auth code flow.

The following sections describe each step in additional detail.

## Switch redirect URIs to SPA platform

If you'd like to continue using your existing app registration for your applications, use the Microsoft Entra admin center to update the registration's redirect URIs to the SPA platform. Doing so enables the authorization code flow with PKCE and CORS support for apps that use the registration (you still need to update your application's code to MSAL.js v2.x).

Follow these steps for app registrations that are currently configured with **Web** platform redirect URIs:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **App registrations**, select your application, and then **Authentication**.
3. In the **Web** platform tile under **Redirect URIs**, select the warning banner indicating that you should migrate your URIs.

    ![Implicit flow warning banner on web app tile in the Entra admin center.](media/migrate-spa-implicit-to-auth-code/portal-01-implicit-warning-banner.png)
4. Select *only* those redirect URIs whose applications will use MSAL.js 2.x, and then select **Configure**.

    ![Select redirect URI pane in SPA pane in the Entra admin center.](media/migrate-spa-implicit-to-auth-code/portal-02-select-redirect-uri.png)

These redirect URIs should now appear in the **Single-page application** platform tile, showing that CORS support with the authorization code flow and PKCE is enabled for these URIs.

![Single-page application tile in app registration in Azure portal](media/migrate-spa-implicit-to-auth-code/portal-03-spa-redirect-uri-tile.png)

## Update your code to MSAL.js 2.x

In MSAL 1.x, you created an application instance by initializing a UserAgentApplication as follows:

```javascript
// MSAL 1.x
import * as msal from "msal";

const msalInstance = new msal.UserAgentApplication(config);
```

In MSAL 2.x, initialize instead a [PublicClientApplication][msal-js-publicclientapplication]:

```javascript
// MSAL 2.x
import * as msal from "@azure/msal-browser";

const msalInstance = new msal.PublicClientApplication(config);
```

For additional changes you might need to make to your code, see the [migration guide](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-browser/docs/v1-migration.md) on GitHub.

## Disable implicit grant settings

Once you've updated all your production applications that use this app registration and its client ID to MSAL 2.x and the authorization code flow, you should uncheck the implicit grant settings under the **Authentication** menu of the app registration.

When you uncheck the implicit grant settings in the app registration, the implicit flow is disabled for all applications using registration and its client ID.

**Do not** disable the implicit grant flow before you've updated all your applications to MSAL.js 2.x and the [PublicClientApplication][msal-js-publicclientapplication].
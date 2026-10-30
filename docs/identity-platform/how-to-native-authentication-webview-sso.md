---
layout: Conceptual
title: Implement Single Sign-On from Native Apps to Embedded Web Views - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/how-to-native-authentication-webview-sso
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to implement SSO between a native mobile app and a web resource in an embedded web view using Microsoft Entra External ID native authentication.
ms.subservice: external
ms.topic: how-to
ms.custom: msecd-doc-authoring-105
ms.date: 2026-04-04T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: b488a0ee-82f2-065e-0cfc-c75c1242ca1e
document_version_independent_id: b488a0ee-82f2-065e-0cfc-c75c1242ca1e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/how-to-native-authentication-webview-sso.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/how-to-native-authentication-webview-sso
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/how-to-native-authentication-webview-sso.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: c5c0878e-b787-fd6c-356e-7e4518c61992
---

# Implement Single Sign-On from Native Apps to Embedded Web Views - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

When your mobile app includes web-based features like a profile update page or rewards dashboard, users expect a seamless single sign-on experience. They shouldn't encounter a second login prompt after already signing in through the native app.

This article shows you how to implement single sign-on (SSO) between a native mobile application and a web resource hosted in an embedded web view (for example, `WKWebView` on iOS or `WebView` on Android). Unlike system browsers, embedded web views allow you to manipulate network requests before they're sent. This capability enables your app to inject the user's authentication state directly into request headers.

The recommended flow works as follows:

1. The user signs in through the mobile app's native UI using the Native Auth SDK or the [native authentication API](reference-native-authentication-api).
2. Before loading the web view, the app retrieves a valid access token from the SDK or API.
3. The app loads the web view with a custom request that includes the access token in the `Authorization: Bearer <access_token>` header.
4. The web resource validates the token and grants access immediately.

The following diagram shows the interaction between the web resource, mobile app, SDK, and the identity service (ESTS):

![Sequence diagram showing the SSO flow where the mobile app signs in via SDK, receives tokens, and loads the web view with the access token in the Authorization header.](media/native-authentication/common/native-application-sign-in-with-web-view-authentication.png)

## Prerequisites

- A mobile app with native authentication configured using the Native Auth SDK or the [native authentication API](reference-native-authentication-api). If you're using the SDK and haven't set up your app yet, see [Prepare your Android app for native authentication](tutorial-native-authentication-prepare-android-app) or [Prepare your iOS/macOS app for native authentication](tutorial-native-authentication-prepare-ios-macos-app).
- A completed sign-in flow in your native app. For guidance, see [Sign in users in an Android mobile app](quickstart-native-authentication-android-sign-in) or [Sign in users in an iOS mobile app](quickstart-native-authentication-ios-sign-in).
- A web resource served over HTTPS (TLS). Don't send tokens over HTTP.
- A shared client identity (application ID) between the mobile app and the web resource. For details, see Limitations and configuration requirements.

## Sign in with native authentication

Complete the standard sign-in flow using the Native Auth SDK or the [native authentication API](reference-native-authentication-api). When sign-in succeeds using the SDK, it caches the access token, ID token, and refresh token securely. If you use the API directly, your app is responsible for securely storing the tokens it receives.

For detailed sign-in implementation steps, see:

- **Android**: [Sign in users in an Android (Kotlin) mobile app](tutorial-native-authentication-android-sign-in-sign-out)
- **iOS/macOS**: [Sign in users in an iOS (Swift) mobile app](tutorial-native-authentication-ios-macos-sign-in-sign-out)

## Retrieve the access token

When the user triggers the action to open the web view, ensure the app has a valid, unexpired access token before loading the web resource.

If you use the Native Auth SDK, request a token silently. The SDK provides a `getAccessToken()` method that retrieves a valid token from the cache or silently refreshes it. For details on acquiring access tokens with specific scopes, see:

- **Android**: [Acquire multiple access tokens](tutorial-native-authentication-android-sign-in-call-api)
- **iOS/macOS**: [Acquire multiple access tokens](tutorial-native-authentication-ios-sign-in-call-api)

If you use the native authentication API directly, your app retrieves tokens through the API's `/oauth/v2.0/token` endpoint. For details, see [Native authentication API reference](reference-native-authentication-api).

Request the token with the exact scopes required by the web resource. For scope requirements, see Limitations and configuration requirements.

## Load the web view with authentication

There are two methods to pass the authentication state to the web view. The recommended approach uses authorization headers. A cookie-based fallback is available for legacy scenarios but is discouraged.

### Option A: Use a bearer token via HTTP header (recommended)

Inject the access token directly into the `Authorization` header of the initial HTTP request used to load the web view. This is the most secure and robust method.

This approach is preferred because it:

- **Is stateless**: It doesn't rely on persistent cookies on the client side.
- **Isolates the token**: It strictly limits the token to this specific request flow.
- **Avoids web-based attack vectors**: It sidesteps common security issues associated with browser-managed sessions.

To load the web view with header-based authentication:

1. Construct the URL for the web resource. Ensure it uses HTTPS.
2. Create a custom network request object.
3. Add the header `Authorization: Bearer <access_token>` to the request.
4. Load the request into the web view component (for example, `WKWebView` on iOS or `WebView` on Android).

### Option B: Use cookies (fallback only)

If the target web resource can't handle header-based authentication (for example, certain legacy single-page applications), you can inject the token as a cookie. This approach is generally discouraged because of security risks.

Injecting cookies into a web view entrusts the authentication state to a browser-managed mechanism. This makes the session "ambient" (automatically attached to requests), which exposes the app to standard web attack classes:

- **XSS (cross-site scripting)**: The session is vulnerable to hijacking if the web content is compromised.
- **CSRF (cross-site request forgery)**: There's a risk of unintended authenticated requests.
- **Session fixation**: An attacker might control the session state.
- **Compliance**: This approach conflicts with security best practices (for example, MASTG-KNOW-0018) regarding persisting sensitive state in web view cookie jars.

Warning

The cookie-based approach is conditionally approved and generally discouraged. Use it only when the target web resource can't support header-based authentication.

If you use the cookie-based approach, these requirements apply:

- Use server-issued session cookies where possible.
- Avoid placing raw access tokens directly into cookies.
- Set cookies with the `HttpOnly`, `Secure`, and appropriate `SameSite` attributes.
- Enforce strict CSRF protection on the server side.

## Validate and persist the token on the backend

When the request reaches the web resource, the backend processes the token to establish the session.

### Validate the token

The web server intercepts incoming requests and verifies the token's signature and claims. For ASP.NET Core backends, use `Microsoft.Identity.Web` (MISE) to handle validation automatically.

Ensure the token's audience (`aud`) claim matches the web API's identifier and the issuer (`iss`) claim matches the expected authority.

### Persist the session

The web view doesn't persist custom headers on subsequent navigation events (for example, when the user selects a link). To maintain the authenticated state after the initial request, the server issues a standard session cookie (`Set-Cookie`) upon successful validation of the initial bearer token.

Configure the session cookie with the following attributes:

- `HttpOnly`
- `Secure`
- An appropriate `SameSite` policy

## Limitations and configuration requirements

To ensure the token issued to the mobile app is accepted by the web resource, keep the following configurations in mind:

- **Shared client identity**: The mobile app and web app should share the same client ID (application ID). If they have different IDs, the backend rejects the mobile app's token as an audience mismatch.
- **Scope alignment**: The mobile app requests the access token with the exact scopes required by the web resource (for example, `Profile.Read`, `Orders.Write`).

Note

This solution is tailored specifically for the web view scenario. A more generic solution that extends SSO capabilities to system browsers and other complex scenarios is planned for a future release.
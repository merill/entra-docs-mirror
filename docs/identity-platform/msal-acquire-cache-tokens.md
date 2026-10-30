---
layout: Conceptual
title: Acquire and cache tokens with Microsoft Authentication Library (MSAL) - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/msal-acquire-cache-tokens
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn about acquiring and caching tokens using MSAL.
manager: pmwongera
ms.date: 2025-05-14T00:00:00.0000000Z
ms.reviewer: 
ms.topic: concept-article
locale: en-us
document_id: 1dc5f32d-7f05-cb8e-fc96-f1a2da4c605f
document_version_independent_id: 79665705-66cc-995f-6b89-7239bbdee2aa
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/msal-acquire-cache-tokens.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/msal-acquire-cache-tokens
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/msal-acquire-cache-tokens.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 9bcd1b4c-9f17-b6ce-bd8e-ca71381b2ba2
---

# Acquire and cache tokens with Microsoft Authentication Library (MSAL) - Microsoft identity platform | Microsoft Learn

[Access tokens](access-tokens) enable clients to securely call web APIs protected by Azure. There are several ways to acquire a token by using the Microsoft Authentication Library (MSAL). Some require user interaction through a web browser, while others don't require user interaction. Usually, the method used for acquiring a token depends on whether the application is a public client application (desktop or mobile), or a confidential client application (web app, web API, or daemon app).

MSAL caches a token after it's been acquired. Your application code should first try to get a token silently from the cache before attempting to acquire a token by other means.

You can also clear the token cache by removing the accounts from the cache. This doesn't remove the session cookie that's in the browser, however.

## Scopes when acquiring tokens

[Scopes](permissions-consent-overview) are the permissions that a web API exposes that client applications can request access to. Client applications request the user's consent for these scopes when making authentication requests to get tokens to access the web APIs. MSAL allows you to get tokens to access Microsoft identity platform APIs. The v2.0 protocol uses scopes instead of resource in the requests. Based on the web API's configuration of the token version it accepts, the v2.0 endpoint returns the access token to MSAL.

Several of MSAL's token acquisition methods require a `scopes` parameter. The `scopes` parameter is a list of strings that declare the desired permissions and the resources requested. Well-known scopes are the [Microsoft Graph permissions](/en-us/graph/permissions-reference).

### Request scopes for a web API

When your application needs to request an access token with specific permissions for a resource API, pass the scopes containing the app ID URI of the API in the format `<app ID URI>/<scope>`.

Some example scope values for different resources:

- Microsoft Graph API: `https://graph.microsoft.com/User.Read`
- Custom web API: `api://aaaabbbb-0000-cccc-1111-dddd2222eeee/api.read`

The format of the scope value varies depending on the resource (the API) receiving the access token and the `aud` claim values it accepts.

For Microsoft Graph only, the `user.read` scope maps to `https://graph.microsoft.com/User.Read`, and both scope formats can be used interchangeably.

Certain web APIs such as the Azure Resource Manager API (`https://management.core.windows.net/`) expect a trailing forward slash (`/`) in the audience claim (`aud`) of the access token. In this case, pass the scope as `https://management.core.windows.net//user_impersonation`, including the double forward slash (`//`).

Other APIs might require that *no scheme or host* is included in the scope value, and expect only the app ID (a GUID) and the scope name, for example:

```json
00001111-aaaa-2222-bbbb-3333cccc4444/api.read
```

Tip

If the downstream resource is not under your control, you might need to try different scope value formats (for example with/without scheme and host) if you receive `401` or other errors when passing the access token to the resource.

### Request dynamic scopes for incremental consent

As the features provided by your application or its requirements change, you can request additional permissions as needed by using the scope parameter. Such *dynamic scopes* allow your users to provide incremental consent to scopes.

For example, you might sign in the user but initially deny them access to any resources. Later, you can give them the ability to view their calendar by requesting the calendar scope in the acquire token method and obtaining the user's consent to do so. For example, by requesting the `https://graph.microsoft.com/User.Read` and `https://graph.microsoft.com/Calendar.Read` scopes.

## Acquiring tokens silently (from the cache)

MSAL maintains a token cache (or two caches for confidential client applications) and caches a token after it's been acquired. In many cases, attempting to silently get a token will acquire another token with more scopes based on a token in the cache. It's also capable of refreshing a token when it's getting close to expiration (as the token cache also contains a refresh token).

### Recommended call pattern for public client applications

Application source code should first try to get a token silently from the cache. If the method call returns a "UI required" error or exception, try acquiring a token by other means.

There are two flows where you **should not** attempt to silently acquire a token:

- [Client credentials flow](msal-authentication-flows#client-credentials), which does not use the user token cache but an application token cache. This method takes care of verifying the application token cache before sending a request to the security token service (STS).
- [Authorization code flow](msal-authentication-flows#authorization-code) in web apps, as it redeems a code that the application obtained by signing in the user and having them consent to more scopes. Since a code and not an account is passed as a parameter, the method can't look in the cache before redeeming the code, which invokes a call to the service.

### Recommended call pattern in web apps using the authorization code flow

For web applications that use the [OpenID Connect authorization code flow](v2-protocols-oidc), the recommended pattern in the controllers is to:

- Instantiate a confidential client application with a token cache with customized serialization.
- Acquire the token using the authorization code flow

## Acquiring tokens

The method of acquiring a token depends on whether it's a public client or confidential client application.

### Public client applications

In public client applications (desktop and mobile), you can:

- Get tokens interactively by having the user sign in through a UI or pop-up window.
- Get a token silently for the signed-in user using [integrated Windows authentication](msal-authentication-flows#integrated-windows-authentication-iwa) (IWA/Kerberos) if the desktop application is running on a Windows computer joined to a domain or to Azure.
- Get a token with a [username and password](msal-authentication-flows#usernamepassword-ropc) in .NET Framework desktop client applications (not recommended). Do not use username/password in confidential client applications.
- Get a token through the [device code flow](msal-authentication-flows#device-code) in applications running on devices that don't have a web browser. The user is provided with a URL and a code, who then goes to a web browser on another device and enters the code and signs in. Microsoft Entra ID then sends a token back to the browser-less device.

### Confidential client applications

For confidential client applications (web app, web API, or a daemon app like a Windows service), you can;

- Acquire tokens **for the application itself** and not for a user, using the [client credentials flow](msal-authentication-flows#client-credentials). This technique can be used for syncing tools, or tools that process users in general and not a specific user.
- Use the [on-behalf-of (OBO) flow](msal-authentication-flows#on-behalf-of-obo) for a web API to call an API on behalf of the user. The application is identified with client credentials in order to acquire a token based on a user assertion (SAML, for example, or a JWT token). This flow is used by applications that need to access resources of a particular user in service-to-service calls. Tokens should be cached on a session basis, not on a user basis.
- Acquire tokens using the [authorization code flow](msal-authentication-flows#authorization-code) in web apps after the user signs in through the authorization request URL. OpenID Connect application typically use this mechanism, which lets the user sign in using OpenID Connect and then access web APIs on behalf of the user. Tokens can be cached on a user or on a session basis. If caching tokens on a user basis, we recommend limiting the session lifetime, so that Microsoft Entra ID can check the state of the Conditional Access policies frequently.

## Authentication results

When your client requests an access token, Microsoft Entra ID also returns an authentication result that includes metadata about the access token. This information includes the expiry time of the access token and the scopes for which it's valid. This data allows your app to do intelligent caching of access tokens without having to parse the access token itself. The authentication result exposes:

- The [access token](access-tokens) for the web API to access resources. This string is usually a Base64-encoded JWT, but the client should **never** look inside the access token. The format isn't guaranteed to remain stable, and it can be encrypted for the resource. People writing code depending on access token content on the client is one of the most common sources of errors and client logic breakage.
- The [ID token](id-tokens) for the user (a JWT).
- The token expiration, which tells the date/time when the token expires.
- The tenant ID contains the tenant in which the user was found. For guest users (Microsoft Entra B2B scenarios), the tenant ID is the guest tenant, not the unique tenant. When the token is delivered in the name of a user, the authentication result also contains information about this user. For confidential client flows where tokens are requested with no user (for the application), this user information is null.
- The scopes for which the token was issued.
- The unique ID for the user.

## (Advanced) Accessing the user's cached tokens in background apps and services

You can use MSAL's token cache implementation to allow background apps, APIs, and services to use the access token cache to continue to act on behalf of users in their absence. Doing so is especially useful if the background apps and services need to continue to work on behalf of the user after the user has exited the front-end web app.

Today, most background processes use [application permissions](/en-us/graph/auth/auth-concepts#microsoft-graph-permissions) when they need to work with a user's data without them being present to authenticate or reauthenticate. Because application permissions often require admin consent, which requires elevation of privilege, unnecessary friction is encountered as the developer didn't intend to obtain permission beyond that which the user originally consented to for their app.

This code sample on GitHub shows how to avoid this unneeded friction by accessing MSAL's token cache from background apps:

[Accessing the logged-in user's token cache from background apps, APIs, and services](https://github.com/Azure-Samples/ms-identity-dotnet-advanced-token-cache)
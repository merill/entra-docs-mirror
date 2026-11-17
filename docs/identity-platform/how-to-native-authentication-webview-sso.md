---
layout: Conceptual
title: Authenticate an embedded webview from a native app - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/how-to-native-authentication-webview-sso
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Use a resource access token to open an authenticated embedded webview and establish a web resource's own session with Microsoft Entra External ID.
ms.topic: how-to
ms.custom: msecd-doc-authoring-1030
ms.date: 2026-11-13T00:00:00.0000000Z
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
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: c5c0878e-b787-fd6c-356e-7e4518c61992
---

# Authenticate an embedded webview from a native app - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

**Authentication approach:** Embedded native authentication.

Use a resource access token to open an authenticated web page inside your native app. This guide connects a user signed in through Microsoft Entra External ID to an HTTPS web resource your team controls, such as your app's rewards page, without a second sign-in prompt.

You need a native app with a working sign-in flow and a web resource that can validate bearer tokens. This resource-token flow provides single sign-on (SSO) to that resource in the embedded webview.

Important

The Native Authentication API V2 is in preview. The [Native Authentication API V1](reference-native-authentication-api-v1) remains generally available. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to preview features.

The resource-token pattern for embedded webviews is generally available. It establishes a session for your web resource, independently of the Native Authentication API's support contract.

## Prerequisites

- An app configured for Embedded native authentication in an external tenant. See [Configure an application](how-to-native-authentication-configure-app).
- A native app with a working sign-in flow. See the [sign-in reference](reference-native-authentication-sign-in).
- An HTTPS web resource with exposed delegated scopes and server-side token validation. See [Expose a web API](quickstart-configure-app-expose-web-apis#add-a-scope).
- Permission for the native app to request those scopes. See [Configure access to your web API](quickstart-configure-app-access-web-apis#add-permissions-to-access-your-web-api).
- An embedded webview that can send an `Authorization` header with its initial request.

## Sign in with native authentication

Request access for the resource you intend to open, rather than reusing a token issued for a different API.

1. Start authorization with the web resource's required scopes in the initial `scope` parameter. Request only the permissions needed for the page's operations.
2. Complete the sign-in actions returned by the service. Follow the returned links and use the latest continuation token for the active transaction.
3. When the service returns `state: continue`, follow `_links.continue` to resume authorization.
4. Exchange the returned authorization code for tokens. Use the response's `access_token` for the web resource, not the `id_token` or a continuation token.

For the authorization and token request contracts, see the [Native Authentication API reference](reference-native-authentication).

For existing V1 integrations, see the [V1 API reference](reference-native-authentication-api-v1) and its [SDK library references](reference-native-authentication-api-v1#sdk-references) for your platform.

The following diagram illustrates the resource-token flow with a V1 SDK:

![Sequence diagram showing an app signing in through an SDK and sending an access token in the embedded webview request.](media/native-authentication/common/native-application-sign-in-with-web-view-authentication.png)

## Retrieve the access token

Before opening the webview, get a valid, unexpired access token for the resource.

1. Check the token response's expiration metadata rather than parsing the access token in the client.
2. If the app doesn't have a usable token for the required resource and scopes, complete authorization to obtain one before loading the page.
3. Keep the token in the native app's protected authentication state until you construct the request. Don't expose it in page scripts, diagnostics, or a URL.

Access tokens are validated by the receiving resource, not by the native client. See [Access tokens](access-tokens).

For V1 SDK token acquisition, use the platform's [SDK library reference](reference-native-authentication-api-v1#sdk-references). Request the scopes described in Limitations and configuration requirements.

## Load the web view with authentication

Send the token in the initial request to the intended web resource. This procedure establishes the web resource's session.

1. Construct the HTTPS URL for your web resource without including the token in its path, query, or fragment.
2. Create the initial webview request with `Authorization: Bearer <access-token>`, replacing `<access-token>` with the access token for the web resource.
3. Load that request in the embedded webview.
4. Restrict bearer-token delivery to the intended resource. Don't forward the header to unrelated origins when handling navigation or redirects.

Use bearer authentication for the initial request and let the server issue the application session cookie after validation. Keep the raw access token in the native app's protected authentication state.

## Validate and persist the token on the backend

The web resource validates the access token and authorizes the requested operation before creating a session.

### Validate the token

Use the resource's token-validation middleware before returning protected content.

1. Validate the token's signature, issuer, and lifetime against the resource's trusted Microsoft Entra configuration.
2. Verify that the `aud` claim identifies the receiving resource.
3. Verify the delegated scopes required for the requested operation and the user's authorization to access the data.
4. Reject the request if validation or authorization fails. Don't create a session from an invalid token.

For the audience and permission checks, see [Validate access-token claims](claims-validation).

### Persist the session

Establish a server-managed session for subsequent webview navigation.

1. After successful token validation, issue the web resource's session cookie through `Set-Cookie`.
2. Set `HttpOnly`, `Secure`, and the `SameSite` policy appropriate for the application's navigation. Apply server-side protection against cross-site request forgery for cookie-authenticated operations.
3. Use the session cookie for subsequent requests to that web resource. Don't store the raw access token in the cookie.

## Verify access and sign-out

Signing out of the native app doesn't terminate the web resource's session or other application and browser sessions. Clear each session through its own sign-out mechanism.

Test both resource authorization and the session that the webview retains.

1. Sign in to the native app and open the web resource. Confirm that the expected user's page opens without another sign-in prompt.
2. Navigate to another protected page in the same web resource. Confirm that its server-issued session cookie maintains the session.
3. Test an expired token, a token issued for a different resource, and a token without the required scope. Confirm that none establishes an authorized session.
4. Sign out and clear authentication state in both the native app and the web resource. Reopen the protected page and confirm that the old web session no longer grants access.
5. Check that application and server diagnostics exclude tokens, cookies, credentials, and personal data.

## Limitations and configuration requirements

The token's audience and permissions identify the web resource and authorized operations. The native client and resource can have separate app registrations.

This integration requires control over the web resource's bearer-token validation and session creation.

The resulting cookie belongs to your web resource. It doesn't create a browser-wide Microsoft Entra session or enable profile or credential-management APIs.
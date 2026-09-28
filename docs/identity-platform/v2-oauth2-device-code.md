---
layout: Conceptual
title: OAuth 2.0 device authorization grant - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/v2-oauth2-device-code
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Sign in users without a browser. Build embedded and browser-less authentication flows using the device authorization grant.
manager: pmwongera
ms.custom: 
ms.date: 2025-01-04T00:00:00.0000000Z
ms.reviewer: jmprieur, ludwignick
ms.topic: reference
locale: en-us
document_id: 58bc32c3-9e21-a56a-f876-3e750576f228
document_version_independent_id: 83231247-55a8-e69b-0712-8c7b1481a02d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/v2-oauth2-device-code.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/v2-oauth2-device-code
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/v2-oauth2-device-code.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: f6e7aa44-03d6-2530-1e03-d5636fbd50b8
---

# OAuth 2.0 device authorization grant - Microsoft identity platform | Microsoft Learn

The Microsoft identity platform supports the [device authorization grant](https://tools.ietf.org/html/rfc8628), which allows users to sign in to input-constrained devices such as a smart TV, IoT device, or a printer. To enable this flow, the device has the user visit a webpage in a browser on another device to sign in. Once the user signs in, the device is able to get access tokens and refresh tokens as needed.

This article describes how to program directly against the protocol in your application. When possible, we recommend you use the supported Microsoft Authentication Libraries (MSAL) instead to [acquire tokens and call secured web APIs](authentication-flows-app-scenarios#scenarios-and-supported-authentication-flows). You can refer to [sample apps that use MSAL](sample-v2-code) for examples.

## Protocol diagram

The entire device code flow is shown in the following diagram. Each step is explained throughout this article.

![Device code flow](media/v2-oauth2-device-code/v2-oauth-device-flow.svg)

## Device authorization request

The client must first check with the authentication server for a device and user code used to initiate authentication. The client collects this request from the `/devicecode` endpoint. In the request, the client should also include the permissions it needs to acquire from the user.

From the moment the request is sent, the user has 15 minutes to sign in. This is the default value for `expires_in`. The request should only be made when the user indicates they're ready to sign in.

```HTTP
// Line breaks are for legibility only.

POST https://login.microsoftonline.com/{tenant}/oauth2/v2.0/devicecode
Content-Type: application/x-www-form-urlencoded

client_id=00001111-aaaa-2222-bbbb-3333cccc4444
&scope=user.read%20openid%20profile

```

| Parameter | Condition | Description |
| --- | --- | --- |
| `tenant` | Required | Can be `/common`, `/consumers`, or `/organizations`. It can also be the directory tenant that you want to request permission from in GUID or friendly name format. |
| `client_id` | Required | The **Application (client) ID** that the [Microsoft Entra admin center – App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) experience assigned to your app. |
| `scope` | Required | A space-separated list of [scopes](permissions-consent-overview) that you want the user to consent to. |

### Device authorization response

A successful response is a JSON object containing the required information to allow the user to sign in.

| Parameter | Format | Description |
| --- | --- | --- |
| `device_code` | String | A long string used to verify the session between the client and the authorization server. The client uses this parameter to request the access token from the authorization server. |
| `user_code` | String | A short string shown to the user used to identify the session on a secondary device. |
| `verification_uri` | URI | The URI the user should go to with the `user_code` in order to sign in. |
| `expires_in` | int | The number of seconds before the `device_code` and `user_code` expire. |
| `interval` | int | The number of seconds the client should wait between polling requests. |
| `message` | String | A human-readable string with instructions for the user. This can be localized by including a **query parameter** in the request of the form `?mkt=xx-XX`, filling in the appropriate language culture code. |

Note

The `verification_uri_complete` response field is not included or supported at this time. We mention this because if you read the [standard](https://tools.ietf.org/html/rfc8628) you see that `verification_uri_complete` is listed as an optional part of the device code flow standard.

## Authenticating the user

After the client receives `user_code` and `verification_uri`, the values are displayed and the user is directed to sign in via their mobile or PC browser.

If the user authenticates with a personal account, using `/common` or `/consumers`, they're asked to sign in again in order to transfer authentication state to the device. This is because the device is unable to access the user's cookies. They're asked to consent to the permissions requested by the client. However, this doesn't apply to work or school accounts used to authenticate.

While the user is authenticating at the `verification_uri`, the client should be polling the `/token` endpoint for the requested token using the `device_code`.

```HTTP
POST https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
Content-Type: application/x-www-form-urlencoded

grant_type=urn:ietf:params:oauth:grant-type:device_code&client_id=00001111-aaaa-2222-bbbb-3333cccc4444&device_code=GMMhmHCXhWEzkobqIHGG_EnNYYsAkukHspeYUk9E8...
```

| Parameter | Required | Description |
| --- | --- | --- |
| `tenant` | Required | The same tenant or tenant alias used in the initial request. |
| `grant_type` | Required | Must be `urn:ietf:params:oauth:grant-type:device_code` |
| `client_id` | Required | Must match the `client_id` used in the initial request. |
| `device_code` | Required | The `device_code` returned in the device authorization request. |

### Expected errors

The device code flow is a polling protocol so errors served to the client must be expected prior to completion of user authentication.

| Error | Description | Client Action |
| --- | --- | --- |
| `authorization_pending` | The user hasn't finished authenticating, but hasn't canceled the flow. | Repeat the request after at least `interval` seconds. |
| `authorization_declined` | The end user denied the authorization request. | Stop polling and revert to an unauthenticated state. |
| `bad_verification_code` | The `device_code` sent to the `/token` endpoint wasn't recognized. | Verify that the client is sending the correct `device_code` in the request. |
| `expired_token` | Value of `expires_in` has been exceeded and authentication is no longer possible with `device_code`. | Stop polling and revert to an unauthenticated state. |

### Successful authentication response

A successful token response looks like:

```json
{
    "token_type": "Bearer",
    "scope": "User.Read profile openid email",
    "expires_in": 3599,
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD..."
}
```

| Parameter | Format | Description |
| --- | --- | --- |
| `token_type` | String | Always `Bearer`. |
| `scope` | Space separated strings | If an access token was returned, this lists the scopes in which the access token is valid for. |
| `expires_in` | int | Number of seconds the included access token is valid for. |
| `access_token` | Opaque string | Issued for the [scopes](permissions-consent-overview) that were requested. |
| `id_token` | JWT | Issued if the original `scope` parameter included the `openid` scope. |
| `refresh_token` | Opaque string | Issued if the original `scope` parameter included `offline_access`. |

You can use the refresh token to acquire new access tokens and refresh tokens using the same flow documented in the [OAuth Code flow documentation](v2-oauth2-auth-code-flow#refresh-the-access-token).

Warning

Don't attempt to validate or read tokens for any API you don't own, including the tokens in this example, in your code. Tokens for Microsoft services can use a special format that will not validate as a JWT, and may also be encrypted for consumer (Microsoft account) users. While reading tokens is a useful debugging and learning tool, do not take dependencies on this in your code or assume specifics about tokens that aren't for an API you control.
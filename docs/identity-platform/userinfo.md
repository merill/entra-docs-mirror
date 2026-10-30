---
layout: Conceptual
title: Microsoft identity platform UserInfo endpoint - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/userinfo
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn about the UserInfo endpoint on the Microsoft identity platform.
manager: dougeby
ms.custom: 
ms.date: 2023-12-19T00:00:00.0000000Z
ms.reviewer: ludwignick
ms.topic: reference
locale: en-us
document_id: 0b8f22d9-e4a8-5a4a-6fcc-4616a77d073f
document_version_independent_id: 6970fe1c-5661-e3e0-c6ec-460a9d390c1f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/userinfo.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/userinfo
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/userinfo.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 112c1354-8ad1-6280-77ca-ef4231336121
---

# Microsoft identity platform UserInfo endpoint - Microsoft identity platform | Microsoft Learn

As part of the OpenID Connect (OIDC) standard, the [UserInfo endpoint](https://openid.net/specs/openid-connect-core-1_0.html#UserInfo) returns information about an authenticated user.

## Find the .well-known configuration endpoint

You can find the UserInfo endpoint programmatically by reading the `userinfo_endpoint` field of the OpenID configuration document at `https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration`. We don't recommend hard-coding the UserInfo endpoint in your applications. Instead, use the OIDC configuration document to find the endpoint at runtime.

The UserInfo endpoint is typically called automatically by [OIDC-compliant libraries](https://openid.net/developers/certified/) to get information about the user. From the [list of claims identified in the OIDC standard](https://openid.net/specs/openid-connect-core-1_0.html#StandardClaims), the Microsoft identity platform produces the name claims, subject claim, and email when available and consented to.

## Consider using an ID token instead

The information in an ID token is a superset of the information available on UserInfo endpoint. Because you can get an ID token at the same time you get a token to call the UserInfo endpoint, we suggest getting the user's information from the token instead of calling the UserInfo endpoint. Using the ID token instead of calling the UserInfo endpoint eliminates up to two network requests, reducing latency in your application.

If you require more details about the user like manager or job title, call the [Microsoft Graph `/user` API](/en-us/graph/api/user-get). You can also use [optional claims](optional-claims) to include additional user information in your ID and access tokens.

## Calling the UserInfo endpoint

UserInfo is a standard OAuth bearer token API hosted by Microsoft Graph. Call the UserInfo endpoint as you would call any Microsoft Graph API by using the access token your application received when it requested access to Microsoft Graph. The UserInfo endpoint returns a JSON response containing claims about the user.

### Permissions

Use the following [OIDC permissions](scopes-oidc#openid-connect-scopes) to call the UserInfo API. The `openid` claim is required, and the `profile` and `email` scopes ensure that additional information is provided in the response.

| Permission type | Permissions |
| --- | --- |
| Delegated (work or school account) | `openid` (required), `profile`, `email` |
| Delegated (personal Microsoft account) | `openid` (required), `profile`, `email` |
| Application | Not applicable |

Tip

Copy this URL in your browser to get an access token for the UserInfo endpoint and an [ID token](id-tokens). Replace the client ID and redirect URI with values from an app registration.

`https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=<yourClientID>&response_type=token+id_token&redirect_uri=<YourRedirectUri>&scope=user.read+openid+profile+email&response_mode=fragment&state=12345&nonce=678910`

You can use the access token that's returned in the query in the next section.

Microsoft Graph uses a special token issuance pattern that may impact your app's ability to read or validate it. As with any other Microsoft Graph token, the token you receive here may not be a JWT and your app should consider it opaque. If you signed in a Microsoft account user, it will be an encrypted token format. None of these factors, however, impact your app's ability to use the access token in a request to the UserInfo endpoint.

### Calling the API

The UserInfo API supports both GET and POST requests.

```http
GET or POST /oidc/userinfo HTTP/1.1
Host: graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJub25jZSI6Il…
```

### UserInfo response

```jsonc
{
    "sub": "OLu859SGc2Sr9ZsqbkG-QbeLgJlb41KcdiPoLYNpSFA",
    "name": "Mikah Ollenburg", // all names require the “profile” scope.
    "family_name": " Ollenburg",
    "given_name": "Mikah",
    "picture": "https://graph.microsoft.com/v1.0/me/photo/$value",
    "email": "mikoll@contoso.com" // requires the “email” scope.
}
```

The claims shown in the response are all those that the UserInfo endpoint can return. These values are the same values included in an [ID token](id-tokens).

## Notes and caveats on the UserInfo endpoint

You can't add to or customize the information returned by the UserInfo endpoint.

To customize the information returned by the identity platform during authentication and authorization, use [claims mapping](saml-claims-customization) and [optional claims](optional-claims) to modify security token configuration.
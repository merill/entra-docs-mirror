---
layout: Conceptual
title: Call a web API from a mobile app - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/scenario-mobile-call-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to build a mobile app that calls web APIs. (Call a web API.)
manager: pmwongera
ms.custom: 
ms.date: 2020-05-18T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.subservice: workforce
ms.topic: how-to
locale: en-us
document_id: a660db43-e1d2-0d2b-ece2-93907d6a3f4c
document_version_independent_id: 26b26c5e-6063-7ef4-e43a-e478a1f7e32d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/scenario-mobile-call-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/scenario-mobile-call-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/scenario-mobile-call-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
platformId: 8331713a-2608-21b1-88e7-59d9833d9393
---

# Call a web API from a mobile app - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

After your app signs in a user and receives tokens, the Microsoft Authentication Library (MSAL) exposes information about the user, the user's environment, and the issued tokens. Your app can use these values to call a web API or display a welcome message to the user.

In this article, we'll first look at the MSAL result. Then we'll look at how to use an access token from `AuthenticationResult` or `result` to call a protected web API.

## MSAL result

MSAL provides the following values:

- `AccessToken` calls protected web APIs in an HTTP bearer request.
- `IdToken` contains useful information about the signed-in user. This information includes the user's name, the home tenant, and a unique identifier for storage.
- `ExpiresOn` is the expiration time of the token. MSAL handles an app's automatic refresh.
- `TenantId` is the identifier of the tenant where the user signed in. For guest users in Microsoft Entra B2B, this value identifies the tenant where the user signed in. The value doesn't identify the user's home tenant.
- `Scopes` indicates the scopes that were granted with your token. The granted scopes might be a subset of the scopes that you requested.

MSAL also provides an abstraction for an `Account` value. An `Account` value represents the current user's signed-in account:

- `HomeAccountIdentifier` identifies the user's home tenant.
- `UserName` is the user's preferred username. This value might be empty for Azure AD B2C users.
- `AccountIdentifier` identifies the signed-in user. In most cases, this value is the same as the `HomeAccountIdentifier` value unless the user is a guest in another tenant.

## Call an API

After you have the access token, you can call a web API. Your app will use the token to build an HTTP request and then run the request.

### Android

```Java
        RequestQueue queue = Volley.newRequestQueue(this);
        JSONObject parameters = new JSONObject();

        try {
            parameters.put("key", "value");
        } catch (Exception e) {
            // Error when constructing.
        }
        JsonObjectRequest request = new JsonObjectRequest(Request.Method.GET, MSGRAPH_URL,
                parameters,new Response.Listener<JSONObject>() {
            @Override
            public void onResponse(JSONObject response) {
                // Successfully called Graph. Process data and send to UI.
            }
        }, new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {
                // Error.
            }
        }) {
            @Override
            public Map<String, String> getHeaders() throws AuthFailureError {
                Map<String, String> headers = new HashMap<>();

                // Put access token in HTTP request.
                headers.put("Authorization", "Bearer " + authResult.getAccessToken());
                return headers;
            }
        };

        request.setRetryPolicy(new DefaultRetryPolicy(
                3000,
                DefaultRetryPolicy.DEFAULT_MAX_RETRIES,
                DefaultRetryPolicy.DEFAULT_BACKOFF_MULT));
        queue.add(request);
```

### MSAL for iOS and macOS

The methods to acquire tokens return an `MSALResult` object. `MSALResult` exposes an `accessToken` property. You can use `accessToken` to call a web API. Add this property to the HTTP authorization header before you call to access the protected web API.

```objc
NSMutableURLRequest *urlRequest = [NSMutableURLRequest new];
urlRequest.URL = [NSURL URLWithString:"https://contoso.api.com"];
urlRequest.HTTPMethod = @"GET";
urlRequest.allHTTPHeaderFields = @{ @"Authorization" : [NSString stringWithFormat:@"Bearer %@", accessToken] };

NSURLSessionDataTask *task =
[[NSURLSession sharedSession] dataTaskWithRequest:urlRequest
     completionHandler:^(NSData * _Nullable data, NSURLResponse * _Nullable response, NSError * _Nullable error) {}];
[task resume];
```

```swift
let urlRequest = NSMutableURLRequest()
urlRequest.url = URL(string: "https://contoso.api.com")!
urlRequest.httpMethod = "GET"
urlRequest.allHTTPHeaderFields = [ "Authorization" : "Bearer \(accessToken)" ]

let task = URLSession.shared.dataTask(with: urlRequest as URLRequest) { (data: Data?, response: URLResponse?, error: Error?) in }
task.resume()
```

## Make several API requests

To call the same API several times, or call multiple APIs, then consider the following subjects when you build your app:

- **Incremental consent**: The Microsoft identity platform allows apps to get user consent when permissions are required rather than all at the start. Each time your app is ready to call an API, it should request only the scopes that it needs.
- **Conditional Access**: When you make several API requests, in certain scenarios you might have to meet additional conditional-access requirements. Requirements can increase in this way if the first request has no conditional-access policies and your app attempts to silently access a new API that requires Conditional Access. To handle this problem, be sure to catch errors from silent requests, and be prepared to make an interactive request. For more information, see [Guidance for Conditional Access](v2-conditional-access-dev-guide).

## Call several APIs by using incremental consent and Conditional Access

To call several APIs for the same user, after you acquire a token for the user, you can avoid repeatedly asking the user for credentials by subsequently calling `AcquireTokenSilent` to get a token:

```csharp
var result = await app.AcquireTokenXX("scopeApi1")
                      .ExecuteAsync();

result = await app.AcquireTokenSilent("scopeApi2")
                  .ExecuteAsync();
```

Interaction is required when:

- The user consented for the first API but now needs to consent for more scopes. In this case, you use incremental consent.
- The first API doesn't require [multifactor authentication](../identity/authentication/concept-mfa-howitworks), but the next API does.

```csharp
var result = await app.AcquireTokenXX("scopeApi1")
                      .ExecuteAsync();

try
{
 result = await app.AcquireTokenSilent("scopeApi2")
                  .ExecuteAsync();
}
catch(MsalUiRequiredException ex)
{
 result = await app.AcquireTokenInteractive("scopeApi2")
                  .WithClaims(ex.Claims)
                  .ExecuteAsync();
}
```
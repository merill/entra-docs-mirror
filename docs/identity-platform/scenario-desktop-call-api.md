---
layout: Conceptual
title: Call web APIs from a desktop app - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/scenario-desktop-call-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to build a desktop app that calls web APIs
manager: pmwongera
ms.custom: 
ms.date: 2019-10-30T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.subservice: workforce
ms.topic: how-to
locale: en-us
document_id: df2bcf06-417e-bf01-6d1c-834667b8f71f
document_version_independent_id: 81b891a7-5d7c-e25d-0644-b472dc6114c8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/scenario-desktop-call-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/scenario-desktop-call-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/scenario-desktop-call-api.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/7696cda6-0510-47f6-8302-71bb5d2e28cf
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/69c76c32-967e-4c65-b89a-74cc527db725
platformId: c952e257-89f7-5d37-bcf2-b5e21d71336b
---

# Call web APIs from a desktop app - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Now that you have a token, you can call a protected web API.

## Call a web API

# [.NET](#tab/dotnet)
### AuthenticationResult properties in MSAL.NET

The methods to acquire tokens return `AuthenticationResult`. For async methods, `Task<AuthenticationResult>` returns.

In MSAL.NET, `AuthenticationResult` exposes:

- `AccessToken` for the web API to access resources. This parameter is a string, usually a Base-64-encoded JWT. The client should never look inside the access token. The format isn't guaranteed to remain stable, and it can be encrypted for the resource. Writing code that depends on access token content on the client is one of the biggest sources of errors and client logic breaks. For more information, see [Access tokens](access-tokens).
- `IdToken` for the user. This parameter is an encoded JWT. For more information, see [ID tokens](id-tokens).
- `ExpiresOn` tells the date and time when the token expires.
- `TenantId` contains the tenant in which the user was found. For guest users in Microsoft Entra B2B scenarios, the tenant ID is the guest tenant, not the unique tenant. When the token is delivered for a user, `AuthenticationResult` also contains information about this user. For confidential client flows where tokens are requested with no user for the application, this user information is null.
- The `Scopes` for which the token was issued.
- The unique ID for the user.

### IAccount

MSAL.NET defines the notion of an account through the `IAccount` interface. This breaking change provides the right semantics. The same user can have several accounts, in different Microsoft Entra directories. Also, MSAL.NET provides better information in the case of guest scenarios because home account information is provided. The following diagram shows the structure of the `IAccount` interface.

![IAccount interface structure](https://user-images.githubusercontent.com/13203188/44657759-4f2df780-a9fe-11e8-97d1-1abbffade340.png)

The `AccountId` class identifies an account in a specific tenant with the properties shown in the following table.

| Property | Description |
| --- | --- |
| `TenantId` | A string representation for a GUID, which is the ID of the tenant where the account resides. |
| `ObjectId` | A string representation for a GUID, which is the ID of the user who owns the account in the tenant. |
| `Identifier` | Unique identifier for the account. `Identifier` is the concatenation of `ObjectId` and `TenantId` separated by a comma. They're not Base 64 encoded. |

The `IAccount` interface represents information about a single account. The same user can be present in different tenants, which means that a user can have multiple accounts. Its members are shown in the following table.

| Property | Description |
| --- | --- |
| `Username` | A string that contains the displayable value in UserPrincipalName (UPN) format, for example, john.doe@contoso.com. This string can be null, unlike HomeAccountId and HomeAccountId.Identifier, which won't be null. This property replaces the `DisplayableId` property of `IUser` in previous versions of MSAL.NET. |
| `Environment` | A string that contains the identity provider for this account, for example, `login.microsoftonline.com`. This property replaces the `IdentityProvider` property of `IUser`, except that `IdentityProvider` also had information about the tenant, in addition to the cloud environment. Here, the value is only the host. |
| `HomeAccountId` | The account ID of the home account for the user. This property uniquely identifies the user across Microsoft Entra tenants. |

### Use the token to call a protected API

After `AuthenticationResult` is returned by MSAL in `result`, add it to the HTTP authorization header before you make the call to access the protected web API.

```csharp
httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

// Call the web API.
HttpResponseMessage response = await _httpClient.GetAsync(apiUri);
...

```

# [Java](#tab/java)
```Java
HttpURLConnection conn = (HttpURLConnection) url.openConnection();

PublicClientApplication pca = PublicClientApplication.builder(clientId)
        .authority(authority)
        .build();

// Acquire a token, acquireTokenHelper would call publicClientApplication's acquireTokenSilently then acquireToken
// see https://github.com/Azure-Samples/ms-identity-java-desktop for a full example
IAuthenticationResult authenticationResult = acquireTokenHelper(pca);

// Set the appropriate header fields in the request header.
conn.setRequestProperty("Authorization", "Bearer " + authenticationResult.accessToken);
conn.setRequestProperty("Accept", "application/json");

String response = HttpClientHelper.getResponseStringFromConn(conn);

int responseCode = conn.getResponseCode();
if(responseCode != HttpURLConnection.HTTP_OK) {
    throw new IOException(response);
}

JSONObject responseObject = HttpClientHelper.processResponse(responseCode, response);
```

# [MacOS](#tab/macOS)
## Call a web API in MSAL for iOS and macOS

The methods to acquire tokens return an `MSALResult` object. `MSALResult` exposes an `accessToken` property that can be used to call a web API. Add an access token to the HTTP authorization header before you make the call to access the protected web API.

Objective-C:

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

Swift:

```swift
let urlRequest = NSMutableURLRequest()
urlRequest.url = URL(string: "https://contoso.api.com")!
urlRequest.httpMethod = "GET"
urlRequest.allHTTPHeaderFields = [ "Authorization" : "Bearer \(accessToken)" ]

let task = URLSession.shared.dataTask(with: urlRequest as URLRequest) { (data: Data?, response: URLResponse?, error: Error?) in }
task.resume()
```

## Call several APIs: Incremental consent and Conditional Access

To call several APIs for the same user, after you get a token for the first API, call `AcquireTokenSilent`. You'll get a token for the other APIs silently most of the time.

```csharp
var result = await app.AcquireTokenXX("scopeApi1")
                      .ExecuteAsync();

result = await app.AcquireTokenSilent("scopeApi2")
                  .ExecuteAsync();
```

Interaction is required when:

- The user consented for the first API but now needs to consent for more scopes. This kind of consent is known as incremental consent.
- The first API didn't require multifactor authentication, but the next one does.

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

# [Node.js](#tab/nodejs)
Using an HTTP client like [Axios](https://www.npmjs.com/package/axios), call the API endpoint URI with an access token as *authorization bearer*.

```javascript
const axios = require('axios');

async function callEndpointWithToken(endpoint, accessToken) {
    const options = {
        headers: {
            Authorization: `Bearer ${accessToken}`
        }
    };

    console.log('Request made at: ' + new Date().toString());

    const response = await axios.default.get(endpoint, options);

    return response.data;
}

```

# [Python](#tab/python)
```Python
endpoint = "url to the API"
http_headers = {'Authorization': 'Bearer ' + result['access_token'],
                'Accept': 'application/json',
                'Content-Type': 'application/json'}
data = requests.get(endpoint, headers=http_headers, stream=False).json()
```

---
---
layout: Conceptual
title: How to call a downstream web API from a daemon app - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/scenario-daemon-call-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to build a daemon app that calls a web API.
manager: dougeby
ms.date: 2025-03-25T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.subservice: workforce
ms.topic: how-to
locale: en-us
document_id: 3c18f989-2447-a35c-3870-e8de9d0da2a3
document_version_independent_id: 029e13c0-ff45-9321-3dfc-c9978b7fa95c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/scenario-daemon-call-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/scenario-daemon-call-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/scenario-daemon-call-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7696cda6-0510-47f6-8302-71bb5d2e28cf
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/69c76c32-967e-4c65-b89a-74cc527db725
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: d2134164-a849-4d14-1a00-fda1d30dd5b9
---

# How to call a downstream web API from a daemon app - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

.NET daemon apps can call a web API. .NET daemon apps can also call several preapproved web APIs.

## Calling a web API from a daemon application

Here's how to use the token to call an API:

# [.NET](#tab/idweb)
Microsoft.Identity.Web abstracts away the complexity of MSAL.NET. It provides you with higher-level APIs that handle the internals of MSAL.NET for you, such as processing Conditional Access errors, caching.

Here's the Program.cs of the daemon app calling a downstream API:

```csharp
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Identity.Abstractions;
using Microsoft.Identity.Web;

// In the Program.cs, acquire a token for your downstream API

var tokenAcquirerFactory = TokenAcquirerFactory.GetDefaultInstance();
tokenAcquirerFactory.Services.AddDownstreamApi("MyApi",
    tokenAcquirerFactory.Configuration.GetSection("MyWebApi"));
var sp = tokenAcquirerFactory.Build();

var api = sp.GetRequiredService<IDownstreamApi>();
var result = await api.GetForAppAsync<IEnumerable<TodoItem>>("MyApi");
Console.WriteLine($"result = {result?.Count()}");
```

Here's the Program.cs of a daemon app that calls Microsoft Graph:

```csharp
var tokenAcquirerFactory = TokenAcquirerFactory.GetDefaultInstance();
tokenAcquirerFactory.Services.AddMicrosoftGraph();
var serviceProvider = tokenAcquirerFactory.Build();
try
{
    GraphServiceClient graphServiceClient = serviceProvider.GetRequiredService<GraphServiceClient>();
    var users = await graphServiceClient.Users
        .GetAsync(r => r.Options.WithAppOnly());
    Console.WriteLine($"{users.Count} users");
    Console.ReadKey();
}
catch (Exception ex) { Console.WriteLine("We could not retrieve the user's list: " + $"{ex}"); }
```

# [Java](#tab/java)
```Java
HttpURLConnection conn = (HttpURLConnection) url.openConnection();

// Set the appropriate header fields in the request header.
conn.setRequestProperty("Authorization", "Bearer " + accessToken);
conn.setRequestProperty("Accept", "application/json");

String response = HttpClientHelper.getResponseStringFromConn(conn);

int responseCode = conn.getResponseCode();
if(responseCode != HttpURLConnection.HTTP_OK) {
    throw new IOException(response);
}

JSONObject responseObject = HttpClientHelper.processResponse(responseCode, response);
```

# [Node.js](#tab/nodejs)
Using an HTTP client like [Axios](https://www.npmjs.com/package/axios), call the API endpoint URI with an access token as the *authorization bearer*.

```JavaScript
const axios = require('axios');

async function callApi(endpoint, accessToken) {

    const options = {
        headers: {
            Authorization: `Bearer ${accessToken}`
        }
    };

    console.log('request made to web API at: ' + new Date().toString());

    try {
        const response = await axios.default.get(endpoint, options);
        return response.data;
    } catch (error) {
        console.log(error)
        return error;
    }
};
```

# [Python](#tab/python)
```Python
endpoint = "url to the API"
http_headers = {'Authorization': 'Bearer ' + result['access_token'],
                'Accept': 'application/json',
                'Content-Type': 'application/json'}
data = requests.get(endpoint, headers=http_headers, stream=False).json()
```

# [.NET low level](#tab/dotnet)
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

---

## Calling several APIs

For daemon apps, the web APIs that you call need to be preapproved. There's no incremental consent with daemon apps. (There's no user interaction.) The tenant admin needs to provide consent in advance for the application and all the API permissions. If you want to call several APIs, acquire a token for each resource, each time calling `AcquireTokenForClient`. MSAL uses the application token cache to avoid unnecessary service calls.
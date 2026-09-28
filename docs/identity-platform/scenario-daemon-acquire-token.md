---
layout: Conceptual
title: Acquire tokens to call a web API using a daemon application - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/scenario-daemon-acquire-token
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: dmwendia
ms.service: identity-platform
description: Learn how to build a daemon app that calls web APIs (acquiring tokens)
manager: dougeby
ms.date: 2026-06-15T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.subservice: workforce
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 5b2f8fc6-8048-42e9-803f-6b5f307664c9
document_version_independent_id: 0744fa48-8797-e4fb-5ed9-6395adfc7656
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/scenario-daemon-acquire-token.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/scenario-daemon-acquire-token
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/scenario-daemon-acquire-token.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7696cda6-0510-47f6-8302-71bb5d2e28cf
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/69c76c32-967e-4c65-b89a-74cc527db725
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: b4c6478b-e630-42d8-eab5-6a769d6c0f51
---

# Acquire tokens to call a web API using a daemon application - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

## Acquire a token for a confidential client application

Daemon applications and other confidential client apps that run without user interaction use the OAuth 2.0 client credentials flow to acquire app-only access tokens. This article explains how to configure the required scopes, call the `AcquireTokenForClient` API (or its platform equivalent) to acquire a token, and troubleshoot common errors. Before you proceed, make sure you've already created a confidential client application.

## Scopes to request

The scope to request for a client credential flow is the name of the resource followed by `/.default`. The `/.default` notation tells Microsoft Entra ID to use the *application-level permissions* declared statically during application registration. Also, these API permissions must be granted by a tenant administrator.

# [.NET](#tab/idweb)
Here's an example of defining the scopes for the web API as part of the configuration in an [*appsettings.json*](https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2/blob/master/2-Call-OwnApi/daemon-console/appsettings.json) file. This example is taken from the [.NET console daemon](https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2) code sample on GitHub.

```json
{
    "AzureAd": {
        // Same AzureAd section as before.
    },

    "MyWebApi": {
        "BaseUrl": "https://localhost:44372/",
        "RelativePath": "api/TodoList",
        "RequestAppToken": true,
        "Scopes": [ "[Enter here the scopes for your web API]" ]
    }
}
```

# [Java](#tab/java)
In Java, define the default Microsoft Graph scope as a constant:

```Java
final static String GRAPH_DEFAULT_SCOPE = "https://graph.microsoft.com/.default";
```

# [Node.js](#tab/nodejs)
In Node.js, specify the scope in the token request object:

```JavaScript
const tokenRequest = {
    scopes: [process.env.GRAPH_ENDPOINT + '.default'], // e.g. 'https://graph.microsoft.com/.default'
};
```

# [Python](#tab/python)
In MSAL Python, the configuration file looks like this code snippet:

```Json
{
    "scope": ["https://graph.microsoft.com/.default"],
}
```

# [.NET (low level)](#tab/dotnet)
In low-level .NET code, build the scope by appending `/.default` to the resource ID:

```csharp
ResourceId = "someAppIDURI";
var scopes = new [] {  ResourceId+"/.default"};
```

---

### Azure AD (v1.0) resources

The scope used for client credentials should always be the resource ID followed by `/.default`.

Important

When MSAL requests an access token for a resource that accepts a version 1.0 access token, Microsoft Entra ID parses the desired audience from the requested scope by taking everything before the last slash and using it as the resource identifier. So if, like Azure SQL Database (`https://database.windows.net`), the resource expects an audience that ends with a slash (for Azure SQL Database, `https://database.windows.net/`), you need to request a scope of `https://database.windows.net//.default`. (Note the double slash.) See also MSAL.NET issue [#747: `Resource url's trailing slash is omitted, which caused sql auth failure`](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet/issues/747).

## AcquireTokenForClient API

To acquire a token for the app, use `AcquireTokenForClient` or its equivalent, depending on the platform.

# [.NET](#tab/idweb)
With Microsoft.Identity.Web, you don't need to acquire a token directly. You can use higher level APIs, as you see in [Calling a web API from a daemon application](scenario-daemon-call-api). If however you're using an SDK that requires a token, you can obtain an app token through the `ITokenAcquirer` abstraction as shown in the following example:

```csharp
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Identity.Abstractions;
using Microsoft.Identity.Web;

// In the Program.cs, acquire a token for your downstream API

var tokenAcquirerFactory = TokenAcquirerFactory.GetDefaultInstance();
ITokenAcquirer acquirer = tokenAcquirerFactory.GetTokenAcquirer();
AcquireTokenResult tokenResult = await acquirer.GetTokenForUserAsync(new[] { "https://graph.microsoft.com/.default" });
string accessToken = tokenResult.AccessToken;
```

# [Java](#tab/java)
The following Java token-acquisition example is extracted from the [MSAL Java dev samples](https://github.com/AzureAD/microsoft-authentication-library-for-java/tree/dev/msal4j-sdk/src/samples/confidential-client/).

```Java
private static IAuthenticationResult acquireToken() throws Exception {

     // Load token cache from file and initialize token cache aspect. The token cache will have
     // dummy data, so the acquireTokenSilently call will fail.
     TokenCacheAspect tokenCacheAspect = new TokenCacheAspect("sample_cache.json");

     IClientCredential credential = ClientCredentialFactory.createFromSecret(CLIENT_SECRET);
     ConfidentialClientApplication cca =
             ConfidentialClientApplication
                     .builder(CLIENT_ID, credential)
                     .authority(AUTHORITY)
                     .setTokenCacheAccessAspect(tokenCacheAspect)
                     .build();

     IAuthenticationResult result;
     try {
         SilentParameters silentParameters =
                 SilentParameters
                         .builder(SCOPE)
                         .build();

         // try to acquire token silently. This call will fail since the token cache does not
         // have a token for the application you are requesting an access token for
         result = cca.acquireTokenSilently(silentParameters).join();
     } catch (Exception ex) {
         if (ex.getCause() instanceof MsalException) {

             ClientCredentialParameters parameters =
                     ClientCredentialParameters
                             .builder(SCOPE)
                             .build();

             // Try to acquire a token. If successful, you should see
             // the token information printed out to console
             result = cca.acquireToken(parameters).join();
         } else {
             // Handle other exceptions accordingly
             throw ex;
         }
     }
     return result;
 }
```

# [Node.js](#tab/nodejs)
The following code snippet illustrates token acquisition in an MSAL Node confidential client application:

```JavaScript
try {
    const authResponse = await cca.acquireTokenByClientCredential(tokenRequest);
    console.log(authResponse.accessToken) // display access token
} catch (error) {
    console.log(error);
}
```

# [Python](#tab/python)
The following example shows the MSAL Python pattern for acquiring an app-only access token with client credentials:

```Python
result = None

# First, the code looks up a token from the cache.
# Because we're looking for a token for the current app, not for a user,
# use None for the account parameter.
result = app.acquire_token_silent(config["scope"], account=None)

if not result:
    logging.info("No suitable token exists in cache. Let's get a new one from Azure AD.")
    result = app.acquire_token_for_client(scopes=config["scope"])

if "access_token" in result:
    # Call a protected API with the access token.
    print(result["token_type"])
else:
    print(result.get("error"))
    print(result.get("error_description"))
    print(result.get("correlation_id"))  # You might need this when reporting a bug.
```

# [.NET (low level)](#tab/dotnet)
```csharp
using Microsoft.Identity.Client;

// With client credentials flows, the scope is always of the shape "resource/.default" because the
// application permissions need to be set statically (in the portal or by PowerShell), and then granted by
// a tenant administrator.
string[] scopes = new string[] { "https://graph.microsoft.com/.default" };

AuthenticationResult result = null;
try
{
 result = await app.AcquireTokenForClient(scopes)
                  .ExecuteAsync();
}
catch (MsalUiRequiredException ex)
{
    // The application doesn't have sufficient permissions.
    // - Did you declare enough app permissions during app creation?
    // - Did the tenant admin grant permissions to the application?
}
catch (MsalServiceException ex) when (ex.Message.Contains("AADSTS70011"))
{
    // Invalid scope. The scope has to be in the form "https://resourceurl/.default"
    // Mitigation: Change the scope to be as expected.
}
```

### AcquireTokenForClient uses the application token cache

In MSAL.NET, `AcquireTokenForClient` uses the application token cache. (All the other AcquireToken*XX* methods use the user token cache.) Don't call `AcquireTokenSilent` before you call `AcquireTokenForClient`, because `AcquireTokenSilent` uses the *user* token cache. `AcquireTokenForClient` checks the *application* token cache itself and updates it.

---

### Protocol

If you don't yet have a library for your chosen language, you might want to use the protocol directly:

#### First case: Access the token request by using a shared secret

```HTTP
POST /{tenant}/oauth2/v2.0/token HTTP/1.1           //Line breaks for clarity.
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=00001111-aaaa-2222-bbbb-3333cccc4444
&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default
&client_secret=A1b-C2d_E3f.H4i,J5k?L6m!N7o-P8q_R9s.T0u
&grant_type=client_credentials
```

#### Second case: Access the token request by using a certificate

```HTTP
POST /{tenant}/oauth2/v2.0/token HTTP/1.1               // Line breaks for clarity.
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

scope=https%3A%2F%2Fgraph.microsoft.com%2F.default
&client_id=11112222-bbbb-3333-cccc-4444dddd5555
&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer
&client_assertion=aaaaaaaa-0b0b-...
&grant_type=client_credentials
```

For more information, see the protocol documentation: [Microsoft identity platform and the OAuth 2.0 client credentials flow](v2-oauth2-client-creds-grant-flow).

## Troubleshooting

### Did you use the resource/.default scope?

If you get an error message telling you that you used an invalid scope, you probably didn't use the `resource/.default` scope.

### Did you forget to provide admin consent? Daemon apps need it!

If you get an **Insufficient privileges to complete the operation** error when you call the API, the tenant administrator needs to grant permissions to the application.

If you don't grant admin consent to your application, the API returns an error response similar to the following example:

```json
Failed to call the web API: Forbidden
Content: {
  "error": {
    "code": "Authorization_RequestDenied",
    "message": "Insufficient privileges to complete the operation.",
    "innerError": {
      "request-id": "<guid>",
      "date": "<date>"
    }
  }
}
```

Select one of the following options, depending on the role.

##### Cloud Application Administrator

For a Cloud Application Administrator, go to **Enterprise applications** in the Microsoft Entra admin center. Select the app registration, and select **Permissions** from the **Security** section of the left pane. Then select the large button labeled **Grant admin consent for {Tenant Name}** (where **{Tenant Name}** is the name of the directory).

##### Standard user

For a standard user of your tenant, ask a Cloud Application Administrator to grant admin consent to the application. To request consent, direct the administrator to the following admin consent endpoint URL:

```url
https://login.microsoftonline.com/Enter_the_Tenant_Id_Here/adminconsent?client_id=Enter_the_Application_Id_Here
```

In the URL:

- Replace `Enter_the_Tenant_Id_Here` with the tenant ID or tenant name (for example, `contoso.microsoft.com`).
- `Enter_the_Application_Id_Here` is the application (client) ID for the registered application.

The error `AADSTS50011: No reply address is registered for the application` may be displayed after you grant consent to the app by using the preceding URL. The `AADSTS50011` error occurs because the application and the URL don't have a redirect URI. You can safely ignore this error.

### Are you calling your own API?

If your daemon app calls your own web API and you weren't able to add an app permission to the daemon's app registration, you need to [Add app roles to the web API's app registration](howto-add-app-roles-in-apps).
---
layout: Conceptual
title: Acquire a token to call a web API (desktop app) - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/scenario-desktop-acquire-token
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to build a desktop app that calls web APIs to acquire a token for the app
manager: pmwongera
ms.date: 2023-03-27T00:00:00.0000000Z
ms.subservice: workforce
ms.topic: how-to
locale: en-us
document_id: a7a27a93-a596-114e-6bc2-7a8ab5b20ef2
document_version_independent_id: 54077d4d-6f1c-5a92-9d61-0533f85628fe
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/scenario-desktop-acquire-token.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/scenario-desktop-acquire-token
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/scenario-desktop-acquire-token.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 63497ab9-2a7b-41f1-403a-6c4610a7b35d
---

# Acquire a token to call a web API (desktop app) - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

After you've built an instance of the public client application, you'll use it to acquire a token that you'll then use to call a web API.

## Recommended pattern

The web API is defined by its *scopes*. Whatever the experience you provide in your application, the pattern to use is:

- Systematically attempt to get a token from the token cache by calling `AcquireTokenSilent`.
- If this call fails, use the `AcquireToken` flow that you want to use, which is represented here by `AcquireTokenXX`.

# [.NET](#tab/dotnet)
### In MSAL.NET

```csharp
AuthenticationResult result;
var accounts = await app.GetAccountsAsync();
IAccount account = ChooseAccount(accounts); // for instance accounts.FirstOrDefault
                                            // if the app manages is at most one account
try
{
 result = await app.AcquireTokenSilent(scopes, account)
                   .ExecuteAsync();
}
catch(MsalUiRequiredException ex)
{
  result = await app.AcquireTokenXX(scopes, account)
                    .WithOptionalParameterXXX(parameter)
                    .ExecuteAsync();
}
```

# [Java](#tab/java)
```java
Set<IAccount> accountsInCache = pca.getAccounts().join();
// Take first account in the cache. In a production application, you would filter
// accountsInCache to get the right account for the user authenticating.
IAccount account = accountsInCache.iterator().next();

IAuthenticationResult result;
try {
    SilentParameters silentParameters =
            SilentParameters
                    .builder(SCOPE, account)
                    .build();

    // try to acquire token silently. This call will fail since the token cache
    // does not have any data for the user you are trying to acquire a token for
    result = pca.acquireTokenSilently(silentParameters).join();
} catch (Exception ex) {
    if (ex.getCause() instanceof MsalException) {

        InteractiveRequestParameters parameters = InteractiveRequestParameters
                .builder(new URI("http://localhost"))
                .scopes(SCOPE)
                .build();

        // Try to acquire a token interactively with system browser. If successful, you should see
        // the token and account information printed out to console
        result = pca.acquireToken(parameters).join();
    } else {
        // Handle other exceptions accordingly
        throw ex;
    }
}
return result;
```

# [macOS](#tab/macOS)
### In MSAL for iOS and macOS

Objective-C:

```objc
MSALAccount *account = [application accountForIdentifier:accountIdentifier error:nil];

MSALSilentTokenParameters *silentParams = [[MSALSilentTokenParameters alloc] initWithScopes:scopes account:account];
[application acquireTokenSilentWithParameters:silentParams completionBlock:^(MSALResult *result, NSError *error) {

    // Check the error
    if (error && [error.domain isEqual:MSALErrorDomain] && error.code == MSALErrorInteractionRequired)
    {
        // Interactive auth will be required, call acquireTokenWithParameters:error:
    }
}];
```

Swift:

```swift
guard let account = try? application.account(forIdentifier: accountIdentifier) else { return }
let silentParameters = MSALSilentTokenParameters(scopes: scopes, account: account)
application.acquireTokenSilent(with: silentParameters) { (result, error) in

    guard let authResult = result, error == nil else {

    let nsError = error! as NSError

        if (nsError.domain == MSALErrorDomain &&
            nsError.code == MSALError.interactionRequired.rawValue) {

            // Interactive auth will be required, call acquireToken()
            return
        }
        return
    }
}
```

# [Node.js](#tab/nodejs)
In MSAL Node, you acquire tokens via authorization code flow with Proof Key for Code Exchange (PKCE). MSAL Node uses an in-memory token cache to see if there are any user accounts in the cache. If there is, the account object can be passed to the `acquireTokenSilent()` method to retrieve a cached access token.

```javascript

const msal = require("@azure/msal-node");

const msalConfig = {
    auth: {
        clientId: "your_client_id_here",
        authority: "your_authority_here",
    }
};

const pca = new msal.PublicClientApplication(msalConfig);
const msalTokenCache = pca.getTokenCache();

let accounts = await msalTokenCache.getAllAccounts();

    if (accounts.length > 0) {

        const silentRequest = {
            account: accounts[0], // Index must match the account that is trying to acquire token silently
            scopes: ["user.read"],
        };

        pca.acquireTokenSilent(silentRequest).then((response) => {
            console.log("\nSuccessful silent token acquisition");
            console.log("\nResponse: \n:", response);
            res.sendStatus(200);
        }).catch((error) => console.log(error));
    } else {
        const {verifier, challenge} = await msal.cryptoProvider.generatePkceCodes();

        const authCodeUrlParameters = {
            scopes: ["User.Read"],
            redirectUri: "your_redirect_uri",
            codeChallenge: challenge, // PKCE Code Challenge
            codeChallengeMethod: "S256" // PKCE Code Challenge Method 
        };

        // get url to sign user in and consent to scopes needed for application
        pca.getAuthCodeUrl(authCodeUrlParameters).then((response) => {
            console.log(response);

            const tokenRequest = {
                code: response["authorization_code"],
                codeVerifier: verifier, // PKCE Code Verifier 
                redirectUri: "your_redirect_uri",
                scopes: ["User.Read"],
            };

            // acquire a token by exchanging the code
            pca.acquireTokenByCode(tokenRequest).then((response) => {
                console.log("\nResponse: \n:", response);
            }).catch((error) => {
                console.log(error);
            });
        }).catch((error) => console.log(JSON.stringify(error)));
    }
```

# [Python](#tab/python)
```python
result = None

# Firstly, check the cache to see if this end user has signed in before
accounts = app.get_accounts(username=config["username"])
if accounts:
    result = app.acquire_token_silent(config["scope"], account=accounts[0])

if not result:
    result = app.acquire_token_by_xxx(scopes=config["scope"])
```

---

There are various ways you can acquire tokens in a desktop application.

- [Interactively](scenario-desktop-acquire-token-interactive)
- [Integrated Windows authentication](scenario-desktop-acquire-token-integrated-windows-authentication)
- [WAM](scenario-desktop-acquire-token-wam)
- [Username Password](scenario-desktop-acquire-token-username-password)
- [Device code flow](scenario-desktop-acquire-token-device-code-flow)

Important

If users need to use multi-factor authentication (MFA) to log in to the application, they will be blocked instead.
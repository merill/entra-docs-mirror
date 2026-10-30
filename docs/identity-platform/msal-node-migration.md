---
layout: Conceptual
title: Migrate your Node.js application from ADAL to MSAL - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/msal-node-migration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: How to update your existing Node.js application to use the Microsoft Authentication Library (MSAL) for authentication and authorization instead of the Active Directory Authentication Library (ADAL).
manager: pmwongera
ms.date: 2021-04-26T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-ropc-nochange
locale: en-us
document_id: 85ddb2f7-4a84-5174-a8fd-d5fd73ddaef6
document_version_independent_id: 285b621a-9a32-744d-b3ae-a93bd6c07aec
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/msal-node-migration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/msal-node-migration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/msal-node-migration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: ccc7a79e-41e0-aea8-bee8-2231c5392465
---

# Migrate your Node.js application from ADAL to MSAL - Microsoft identity platform | Microsoft Learn

[Microsoft Authentication Library for Node](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-node) (MSAL Node) is now the recommended SDK for enabling authentication and authorization for your applications registered on the Microsoft identity platform. This article covers the important steps you need to go through in order to migrate your apps from Active Directory Authentication Library for Node (ADAL Node) to MSAL Node.

## Prerequisites

- Node version 10, 12, 14, 16 or 18. See the [note on version support](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-node#node-version-support)

## Update app registration settings

When working with ADAL Node, you were likely using the **Azure AD v1.0 endpoint**. Apps migrating from ADAL to MSAL should switch to **Azure AD v2.0 endpoint**.

## Install and import MSAL

1. install MSAL Node package via npm:

```console
  npm install @azure/msal-node
```

1. After that, import MSAL Node in your code:

```javascript
  const msal = require('@azure/msal-node');
```

1. Finally, uninstall the ADAL Node package and remove any references in your code:

```console
  npm uninstall adal-node
```

## Initialize MSAL

In ADAL Node, you initialize an `AuthenticationContext` object, which then exposes the methods you can use in different authentication flows (for example, `acquireTokenWithAuthorizationCode` for web apps). When initializing, the only mandatory parameter is the **authority URI**:

```javascript
var adal = require('adal-node');

var authorityURI = "https://login.microsoftonline.com/common";
var authenticationContext = new adal.AuthenticationContext(authorityURI);
```

In MSAL Node, you have two alternatives instead: If you're building a mobile app or a desktop app, you instantiate a `PublicClientApplication` object. The constructor expects a configuration object that contains the `clientId` parameter at the very least. MSAL defaults the authority URI to `https://login.microsoftonline.com/common` if you don't specify it.

```javascript
const msal = require('@azure/msal-node');

const pca = new msal.PublicClientApplication({
        auth: {
            clientId: "YOUR_CLIENT_ID"
        }
    });
```

Note

If you use the `https://login.microsoftonline.com/common` authority in v2.0, you will allow users to sign in with any Microsoft Entra organization or a personal Microsoft account (MSA). In MSAL Node, if you want to restrict login to any Microsoft Entra account (same behavior as with ADAL Node), use `https://login.microsoftonline.com/organizations` instead.

On the other hand, if you're building a web app or a daemon app, you instantiate a `ConfidentialClientApplication` object. With such apps you also need to supply a *client credential*, such as a client secret or a certificate:

```javascript
const msal = require('@azure/msal-node');

const cca = new msal.ConfidentialClientApplication({
        auth: {
            clientId: "YOUR_CLIENT_ID",
            clientSecret: "YOUR_CLIENT_SECRET"
        }
    });
```

Both `PublicClientApplication` and `ConfidentialClientApplication`, unlike ADAL's `AuthenticationContext`, is bound to a client ID. This means that if you have different client IDs that you like to use in your application, you need to instantiate a new MSAL instance for each. See for more: [Initialization of MSAL Node](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/initialize-confidential-client-application.md)

## Configure MSAL

When building apps on Microsoft identity platform, your app will contain many parameters related to authentication. In ADAL Node, the `AuthenticationContext` object has a limited number of configuration parameters that you can instantiate it with, while the remaining parameters hang freely in your code (for example, *clientSecret*):

```javascript
var adal = require('adal-node');

var authority = "https://login.microsoftonline.com/YOUR_TENANT_ID"
var validateAuthority = true,
var cache = null;

var authenticationContext = new adal.AuthenticationContext(authority, validateAuthority, cache);
```

- `authority`: URL that identifies a token authority
- `validateAuthority`: a feature that prevents your code from requesting tokens from a potentially malicious authority
- `cache`: sets the token cache used by this AuthenticationContext instance. If this parameter isn't set, then a default, in memory cache is used

MSAL Node on the other hand uses a configuration object of type [Configuration](https://azuread.github.io/microsoft-authentication-library-for-js/ref/modules/_azure_msal_node.html#configuration). It contains the following properties:

```javascript
const msal = require('@azure/msal-node');

const msalConfig = {
    auth: {
        clientId: "YOUR_CLIENT_ID",
        authority: "https://login.microsoftonline.com/YOUR_TENANT_ID",
        clientSecret: "YOUR_CLIENT_SECRET",
        knownAuthorities: [],
    },
    cache: {
        // your implementation of caching
    },
    system: {
        loggerOptions: { /** logging related options */ }
    }
}

const cca = new msal.ConfidentialClientApplication(msalConfig);
```

As a notable difference, MSAL doesn't have a flag to disable authority validation and authorities are always validated by default. MSAL compares your requested authority against a list of authorities known to Microsoft or a list of authorities you've specified in your configuration. See for more: [Configuration Options](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/configuration.md)

## Switch to MSAL API

Most of the public methods in ADAL Node have equivalents in MSAL Node:

| ADAL | MSAL | Notes |
| --- | --- | --- |
| `acquireToken` | `acquireTokenSilent` | Renamed and now expects an [account](https://azuread.github.io/microsoft-authentication-library-for-js/ref/modules/_azure_msal_common.html#accountinfo) object |
| `acquireTokenWithAuthorizationCode` | `acquireTokenByCode` |  |
| `acquireTokenWithClientCredentials` | `acquireTokenByClientCredential` |  |
| `acquireTokenWithRefreshToken` | `acquireTokenByRefreshToken` | Useful for migrating valid refresh tokens |
| `acquireTokenWithDeviceCode` | `acquireTokenByDeviceCode` | Now abstracts user code acquisition (see below) |
| `acquireTokenWithUsernamePassword` | `acquireTokenByUsernamePassword` |  |

However, some methods in ADAL Node are deprecated, while MSAL Node offers new methods:

| ADAL | MSAL | Notes |
| --- | --- | --- |
| `acquireUserCode` | N/A | Merged with `acquireTokeByDeviceCode` (see above) |
| N/A | `acquireTokenOnBehalfOf` | A new method that abstracts [OBO flow](v2-oauth2-on-behalf-of-flow) |
| `acquireTokenWithClientCertificate` | N/A | No longer needed as certificates are assigned during initialization now (see configuration options) |
| N/A | `getAuthCodeUrl` | A new method that abstracts [authorize endpoint](v2-protocols#endpoints) URL construction |

## Use scopes instead of resources

An important difference between v1.0 vs. v2.0 endpoints is about how the resources are accessed. In ADAL Node, you would first register a permission on app registration portal, and then request an access token for a resource (such as Microsoft Graph) as shown below:

```javascript
authenticationContext.acquireTokenWithAuthorizationCode(
    req.query.code,
    redirectUri,
    resource, // e.g. 'https://graph.microsoft.com'
    clientId,
    clientSecret,
    function (err, response) {
        // do something with the authentication response
    }
);
```

MSAL Node supports only the **v2.0** endpoint. The v2.0 endpoint employs a *scope-centric* model to access resources. Thus, when you request an access token for a resource, you also need to specify the scope for that resource:

```javascript
const tokenRequest = {
    code: req.query.code,
    scopes: ["https://graph.microsoft.com/User.Read"],
    redirectUri: REDIRECT_URI,
};

pca.acquireTokenByCode(tokenRequest).then((response) => {
    // do something with the authentication response
}).catch((error) => {
    console.log(error);
});
```

One advantage of the scope-centric model is the ability to use *dynamic scopes*. When building applications using v1.0, you needed to register the full set of permissions (called *static scopes*) required by the application for the user to consent to at the time of login. In v2.0, you can use the scope parameter to request the permissions at the time you want them (hence, *dynamic scopes*). This allows the user to provide **incremental consent** to scopes. So if at the beginning you just want the user to sign in to your application and you don’t need any kind of access, you can do so. If later you need the ability to read the calendar of the user, you can then request the calendar scope in the acquireToken methods and get the user's consent. See for more: [Resources and scopes](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-browser/docs/resources-and-scopes.md)

## Use promises instead of callbacks

In ADAL Node, callbacks are used for any operation after the authentication succeeds and a response is obtained:

```javascript
var context = new AuthenticationContext(authorityUrl, validateAuthority);

context.acquireTokenWithClientCredentials(resource, clientId, clientSecret, function(err, response) {
    if (err) {
        console.log(err);
    } else {
        // do something with the authentication response
    }
});
```

In MSAL Node, promises are used instead:

```javascript
    const cca = new msal.ConfidentialClientApplication(msalConfig);

    cca.acquireTokenByClientCredential(tokenRequest).then((response) => {
        // do something with the authentication response
    }).catch((error) => {
        console.log(error);
    });
```

You can also use the **async/await** syntax that comes with ES8:

```javascript
    try {
        const authResponse = await cca.acquireTokenByCode(tokenRequest);
    } catch (error) {
        console.log(error);
    }
```

## Enable logging

In ADAL Node, you configure logging separately at any place in your code:

```javascript
var adal = require('adal-node');

//PII or OII logging disabled. Default Logger does not capture any PII or OII.
adal.logging.setLoggingOptions({
  log: function (level, message, error) {
    console.log(message);

    if (error) {
        console.log(error);
    }
  },
  level: logging.LOGGING_LEVEL.VERBOSE, // provide the logging level
  loggingWithPII: false  // Determine if you want to log personal identification information. The default value is false.
});
```

In MSAL Node, logging is part of the configuration options and is created with the initialization of the MSAL Node instance:

```javascript
const msal = require('@azure/msal-node');

const msalConfig = {
    auth: {
        // authentication related parameters
    },
    cache: {
        // cache related parameters
    },
    system: {
        loggerOptions: {
            loggerCallback(loglevel, message, containsPii) {
                console.log(message);
            },
            piiLoggingEnabled: false,
            logLevel: msal.LogLevel.Verbose,
        }
    }
}

const cca = new msal.ConfidentialClientApplication(msalConfig);
```

## Enable token caching

In ADAL Node, you had the option of importing an in-memory token cache. The token cache is used as a parameter when initializing an `AuthenticationContext` object:

```javascript
var MemoryCache = require('adal-node/lib/memory-cache');

var cache = new MemoryCache();
var authorityURI = "https://login.microsoftonline.com/common";

var context = new AuthenticationContext(authorityURI, true, cache);
```

MSAL Node uses an in-memory token cache by default. You don't need to explicitly import it; in-memory token cache is exposed as part of the `ConfidentialClientApplication` and `PublicClientApplication` classes.

```javascript
const msalTokenCache = publicClientApplication.getTokenCache();
```

Importantly, your previous token cache with ADAL Node won't be transferable to MSAL Node, since cache schemas are incompatible. However, you may use the valid refresh tokens your app obtained previously with ADAL Node in MSAL Node. See the section on refresh tokens for more.

You can also write your cache to disk by providing your own **cache plugin**. The cache plugin must implement the interface `ICachePlugin`. Like logging, caching is part of the configuration options and is created with the initialization of the MSAL Node instance:

```javascript
const msal = require('@azure/msal-node');

const msalConfig = {
    auth: {
        // authentication related parameters
    },
    cache: {
        cachePlugin // your implementation of cache plugin
    },
    system: {
        // logging related options
    }
}

const msalInstance = new ConfidentialClientApplication(msalConfig);
```

An example cache plugin can be implemented as below:

```javascript
const fs = require('fs');

// Call back APIs which automatically write and read into a .json file - example implementation
const beforeCacheAccess = async (cacheContext) => {
    cacheContext.tokenCache.deserialize(await fs.readFile(cachePath, "utf-8"));
};

const afterCacheAccess = async (cacheContext) => {
    if(cacheContext.cacheHasChanged) {
        await fs.writeFile(cachePath, cacheContext.tokenCache.serialize());
    }
};

// Cache Plugin
const cachePlugin = {
    beforeCacheAccess,
    afterCacheAccess
};
```

If you're developing [public client applications](msal-client-applications) like desktop apps, the [Microsoft Authentication Extensions for Node](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/extensions/msal-node-extensions) offers secure mechanisms for client applications to perform cross-platform token cache serialization and persistence. Supported platforms are Windows, Mac and Linux.

Note

[Microsoft Authentication Extensions for Node](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/extensions/msal-node-extensions) is **not** recommended for web applications, as it may lead to scale and performance issues. Instead, web apps are recommended to persist the cache in session.

## Remove logic around refresh tokens

In ADAL Node, the refresh tokens (RT) were exposed allowing you to develop solutions around the use of these tokens by caching them and using the `acquireTokenWithRefreshToken` method. Typical scenarios where RTs are especially relevant:

- Long running services that do actions including refreshing dashboards on behalf of the users where the users are no longer connected.
- WebFarm scenarios for enabling the client to bring the RT to the web service (caching is done client side, encrypted cookie, and not server side).

MSAL Node, along with other MSALs, doesn't expose refresh tokens for security reasons. Instead, MSAL handles refreshing tokens for you. As such, you no longer need to build logic for this. However, you **can** make use of your previously acquired (and still valid) refresh tokens from ADAL Node's cache to get a new set of tokens with MSAL Node. To do this, MSAL Node offers `acquireTokenByRefreshToken`, which is equivalent to ADAL Node's `acquireTokenWithRefreshToken` method:

```javascript
var msal = require('@azure/msal-node');

const config = {
    auth: {
        clientId: "ENTER_CLIENT_ID",
        authority: "https://login.microsoftonline.com/ENTER_TENANT_ID",
        clientSecret: "ENTER_CLIENT_SECRET"
    }
};

const cca = new msal.ConfidentialClientApplication(config);

const refreshTokenRequest = {
    refreshToken: "", // your previous refresh token here
    scopes: ["https://graph.microsoft.com/.default"],
    forceCache: true,
};

cca.acquireTokenByRefreshToken(refreshTokenRequest).then((response) => {
    console.log(response);
}).catch((error) => {
    console.log(error);
});
```

For more information, please refer to the [MSAL Node samples](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/samples/msal-node-samples).

Note

We recommend you to destroy the older ADAL Node token cache once you utilize the still valid refresh tokens to get a new set of tokens using the MSAL Node's `acquireTokenByRefreshToken` method as shown above.

## Handle errors and exceptions

When using MSAL Node, the most common type of error you might face is the `interaction_required` error. This error is often resolved by initiating an interactive token acquisition prompt. For instance, when using `acquireTokenSilent`, if there are no cached refresh tokens, MSAL Node won't be able to acquire an access token silently. Similarly, the web API you're trying to access might have a [Conditional Access](../identity/conditional-access/overview) policy in place, requiring the user to perform [multi-factor authentication (MFA)](../identity/authentication/concept-mfa-howitworks). In such cases, handling `interaction_required` error by triggering `acquireTokenByCode` will prompt the user for MFA, allowing them to fullfil it.

Yet another common error you might face is `consent_required`, which occurs when permissions required for obtaining an access token for a protected resource aren't consented by the user. As in `interaction_required`, the solution for `consent_required` error is often initiating an interactive token acquisition prompt, using the `acquireTokenByCode` method.

## Run the app

Once your changes are done, run the app and test your authentication scenario:

```console
npm start
```

## Example: Acquiring tokens with ADAL Node vs. MSAL Node

The snippet below demonstrates a confidential client web app in the Express.js framework. It performs a sign-in when a user hits the authentication route `/auth`, acquires an access token for Microsoft Graph via the `/redirect` route and then displays the content of the said token.

| Using ADAL Node | Using MSAL Node |
| --- | --- |
| ```javascript<br>// Import dependencies<br>var express = require('express');<br>var crypto = require('crypto');<br>var adal = require('adal-node');<br><br>// Authentication parameters<br>var clientId = 'Enter_the_Application_Id_Here';<br>var clientSecret = 'Enter_the_Client_Secret_Here';<br>var tenant = 'Enter_the_Tenant_Info_Here';<br>var authorityUrl = 'https://login.microsoftonline.com/' + tenant;<br>var redirectUri = 'http://localhost:3000/redirect';<br>var resource = 'https://graph.microsoft.com';<br><br>// Configure logging<br>adal.Logging.setLoggingOptions({<br>    log: function (level, message, error) {<br>        console.log(message);<br>    },<br>    level: adal.Logging.LOGGING_LEVEL.VERBOSE,<br>    loggingWithPII: false<br>});<br><br>// Auth code request URL template<br>var templateAuthzUrl = 'https://login.microsoftonline.com/'<br>    + tenant + '/oauth2/authorize?response_type=code&client_id='<br>    + clientId + '&redirect_uri=' + redirectUri<br>    + '&state=<state>&resource=' + resource;<br><br>// Initialize express<br>var app = express();<br><br>// State variable persists throughout the app lifetime<br>app.locals.state = "";<br><br>app.get('/auth', function(req, res) {<br><br>    // Create a random string to use against XSRF<br>    crypto.randomBytes(48, function(ex, buf) {<br>        app.locals.state = buf.toString('base64')<br>            .replace(/\//g, '_')<br>            .replace(/\+/g, '-');<br><br>        // Construct auth code request URL<br>        var authorizationUrl = templateAuthzUrl<br>            .replace('<state>', app.locals.state);<br><br>        res.redirect(authorizationUrl);<br>    });<br>});<br><br>app.get('/redirect', function(req, res) {<br>    // Compare state parameter against XSRF<br>    if (app.locals.state !== req.query.state) {<br>        res.send('error: state does not match');<br>    }<br><br>    // Initialize an AuthenticationContext object<br>    var authenticationContext =<br>        new adal.AuthenticationContext(authorityUrl);<br><br>    // Exchange auth code for tokens<br>    authenticationContext.acquireTokenWithAuthorizationCode(<br>        req.query.code,<br>        redirectUri,<br>        resource,<br>        clientId,<br>        clientSecret,<br>        function(err, response) {<br>            res.send(response);<br>        }<br>    );<br>});<br><br>app.listen(3000, function() {<br>    console.log(`listening on port 3000!`);<br>});<br>``` | ```javascript<br>// Import dependencies<br>const express = require("express");<br>const msal = require('@azure/msal-node');<br><br>// Authentication parameters<br>const config = {<br>    auth: {<br>        clientId: "Enter_the_Application_Id_Here",<br>        authority: "https://login.microsoftonline.com/Enter_the_Tenant_Info_Here",<br>        clientSecret: "Enter_the_Client_Secret_Here"<br>    },<br>    system: {<br>        loggerOptions: {<br>            loggerCallback(loglevel, message, containsPii) {<br>                console.log(message);<br>            },<br>            piiLoggingEnabled: false,<br>            logLevel: msal.LogLevel.Verbose,<br>        }<br>    }<br>};<br><br>const REDIRECT_URI = "http://localhost:3000/redirect";<br><br>// Initialize MSAL Node object using authentication parameters<br>const cca = new msal.ConfidentialClientApplication(config);<br><br>// Initialize express<br>const app = express();<br><br>app.get('/auth', (req, res) => {<br><br>    // Construct a request object for auth code<br>    const authCodeUrlParameters = {<br>        scopes: ["user.read"],<br>        redirectUri: REDIRECT_URI,<br>    };<br><br>    // Request auth code, then redirect<br>    cca.getAuthCodeUrl(authCodeUrlParameters)<br>        .then((response) => {<br>            res.redirect(response);<br>        }).catch((error) => res.send(error));<br>});<br><br>app.get('/redirect', (req, res) => {<br><br>    // Use the auth code in redirect request to construct<br>    // a token request object<br>    const tokenRequest = {<br>        code: req.query.code,<br>        scopes: ["user.read"],<br>        redirectUri: REDIRECT_URI,<br>    };<br><br>    // Exchange the auth code for tokens<br>    cca.acquireTokenByCode(tokenRequest)<br>        .then((response) => {<br>            res.send(response);<br>        }).catch((error) => res.status(500).send(error));<br>});<br><br>app.listen(3000, () =><br>    console.log(`listening on port 3000!`));<br>``` |
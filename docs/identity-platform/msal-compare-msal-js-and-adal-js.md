---
layout: Conceptual
title: Migrate your JavaScript application from ADAL.js to MSAL.js - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/msal-compare-msal-js-and-adal-js
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: How to update your existing JavaScript application to use the Microsoft Authentication Library (MSAL) for authentication and authorization instead of the Active Directory Authentication Library (ADAL).
manager: pmwongera
ms.date: 2021-07-06T00:00:00.0000000Z
ms.topic: how-to
ms.custom: has-adal-ref, sfi-ropc-nochange
locale: en-us
document_id: 5ea18eae-23e6-ce30-4287-75a374c51315
document_version_independent_id: c9ee7f09-73dd-ffee-4b4f-cb3b22d1b959
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/msal-compare-msal-js-and-adal-js.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/msal-compare-msal-js-and-adal-js
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/msal-compare-msal-js-and-adal-js.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: cda4f892-136c-3190-a14d-fc08eb69f315
---

# Migrate your JavaScript application from ADAL.js to MSAL.js - Microsoft identity platform | Microsoft Learn

[Microsoft Authentication Library for JavaScript](https://github.com/AzureAD/microsoft-authentication-library-for-js) (MSAL.js, also known as `msal-browser`) 2.x is the authentication library we recommend using with JavaScript applications on the Microsoft identity platform. This article highlights the changes you need to make to migrate an app that uses the ADAL.js to use MSAL.js 2.x

Note

We strongly recommend MSAL.js 2.x over MSAL.js 1.x. The auth code grant flow is more secure and allows single-page applications to maintain a good user experience despite the privacy measures browsers like Safari have implemented to block 3rd party cookies, among other benefits.

## Prerequisites

- You must set the **Platform** / **Reply URL Type** to **Single-page application** on App Registration portal (if you have other platforms added in your app registration, such as **Web**, you need to make sure the redirect URIs don't overlap. See: [Redirect URI restrictions](reply-url))
- You must provide [polyfills](msal-js-use-ie-browser) for ES6 features that MSAL.js relies on (for example, promises) in order to run your apps on **Internet Explorer**
- Migrate your Microsoft Entra apps to [v2 endpoint](v2-overview) if you haven't already

## Install and import MSAL

There are two ways to install the MSAL.js 2.x library:

### Via npm:

```console
npm install @azure/msal-browser
```

Then, depending on your module system, import it as shown below:

```javascript
import * as msal from "@azure/msal-browser"; // ESM

const msal = require('@azure/msal-browser'); // CommonJS
```

### Via CDN:

Load the script in the header section of your HTML document:

```html
<!DOCTYPE html>
<html>
  <head>
    <script type="text/javascript" src="https://alcdn.msauth.net/browser/2.14.2/js/msal-browser.min.js"></script>
  </head>
</html>
```

For alternative CDN links and best practices when using CDN, see: [CDN Usage](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-browser/docs/cdn-usage.md)

## Initialize MSAL

In ADAL.js, you instantiate the [AuthenticationContext](https://github.com/AzureAD/azure-activedirectory-library-for-js/wiki/Config-authentication-context#authenticationcontext) class, which then exposes the methods you can use to achieve authentication (`login`, `acquireTokenPopup` , and so on). This object serves as the representation of your application's connection to the authorization server or identity provider. When initializing, the only mandatory parameter is the **clientId**:

```javascript
window.config = {
  clientId: "YOUR_CLIENT_ID"
};

var authContext = new AuthenticationContext(config);
```

In MSAL.js, you instantiate the [PublicClientApplication](https://azuread.github.io/microsoft-authentication-library-for-js/ref/classes/_azure_msal_node.PublicClientApplication.html) class instead. Like ADAL.js, the constructor expects a configuration object that contains the `clientId` parameter at minimum. See for more: [Initialize MSAL.js](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-browser/docs/initialization.md)

```javascript
const msalConfig = {
  auth: {
      clientId: 'YOUR_CLIENT_ID'
  }
};

const msalInstance = new msal.PublicClientApplication(msalConfig);
```

In both ADAL.js and MSAL.js, the authority URI defaults to `https://login.microsoftonline.com/common` if you don't specify it.

Note

If you use the `https://login.microsoftonline.com/common` authority in v2.0, you will allow users to sign in with any Microsoft Entra organization or a personal Microsoft account (MSA). In MSAL.js, if you want to restrict login to any Microsoft Entra account (same behavior as with ADAL.js), use `https://login.microsoftonline.com/organizations` instead.

## Configure MSAL

Some of the [configuration options in ADAL.js](https://github.com/AzureAD/azure-activedirectory-library-for-js/wiki/Config-authentication-context) that are used when initializing [AuthenticationContext](https://github.com/AzureAD/azure-activedirectory-library-for-js/wiki/Config-authentication-context#authenticationcontext) are deprecated in MSAL.js, while some new ones are introduced. See the [full list of available options](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-browser/docs/configuration.md). Importantly, many of these options, except for `clientId`, can be overridden during token acquisition, allowing you to set them on a *per-request* basis. For instance, you can use a different **authority URI** or **redirect URI** than the one you set during initialization when acquiring tokens.

Additionally, you no longer need to specify the login experience (that is, whether using pop-up windows or redirecting the page) via the configuration options. Instead, `MSAL.js` exposes `loginPopup` and `loginRedirect` methods through the `PublicClientApplication` instance.

## Enable logging

In ADAL.js, you configure logging separately at any place in your code:

```javascript
window.config = {
  clientId: "YOUR_CLIENT_ID"
};

var authContext = new AuthenticationContext(config);

var Logging = {
  level: 3,
  log: function (message) {
      console.log(message);
  },
  piiLoggingEnabled: false
};

authContext.log(Logging)
```

In MSAL.js, logging is part of the configuration options and is created during the initialization of `PublicClientApplication`:

```javascript
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

const msalInstance = new msal.PublicClientApplication(msalConfig);
```

## Switch to MSAL API

Some of the public methods in ADAL.js have equivalents in MSAL.js:

| ADAL | MSAL | Notes |
| --- | --- | --- |
| `acquireToken` | `acquireTokenSilent` | Renamed and now expects an [account](https://azuread.github.io/microsoft-authentication-library-for-js/ref/modules/_azure_msal_common.html#accountinfo) object |
| `acquireTokenPopup` | `acquireTokenPopup` | Now async and returns a promise |
| `acquireTokenRedirect` | `acquireTokenRedirect` | Now async and returns a promise |
| `handleWindowCallback` | `handleRedirectPromise` | Needed if using redirect experience |
| `getCachedUser` | `getAllAccounts` | Renamed and now returns an array of accounts. |

Others were deprecated, while MSAL.js offers new methods:

| ADAL | MSAL | Notes |
| --- | --- | --- |
| `login` | N/A | Deprecated. Use `loginPopup` or `loginRedirect` |
| `logOut` | N/A | Deprecated. Use `logoutPopup` or `logoutRedirect` |
| N/A | `loginPopup` |  |
| N/A | `loginRedirect` |  |
| N/A | `logoutPopup` |  |
| N/A | `logoutRedirect` |  |
| N/A | `getAccountByHomeId` | Filters accounts by home ID (oid + tenant ID) |
| N/A | `getAccountLocalId` | Filters accounts by local ID (useful for ADFS) |
| N/A | `getAccountUsername` | Filters accounts by username (if exists) |

In addition, as MSAL.js is implemented in TypeScript unlike ADAL.js, it exposes various types and interfaces that you can make use of in your projects. See the [MSAL.js API reference](https://azuread.github.io/microsoft-authentication-library-for-js/ref/) for more.

## Use scopes instead of resources

An important difference between the Azure Active Directory v1.0 versus 2.0 endpoints is about how the resources are accessed. When using ADAL.js with the **v1.0** endpoint, you would first register a permission on app registration portal, and then request an access token for a resource (such as Microsoft Graph) as shown below:

```javascript
authContext.acquireTokenRedirect("https://graph.microsoft.com", function (error, token) {
  // do something with the access token
});
```

MSAL.js supports only the **v2.0** endpoint. The **v2.0** endpoint employs a *scope-centric* model to access resources. Thus, when you request an access token for a resource, you also need to specify the scope for that resource:

```javascript
msalInstance.acquireTokenRedirect({
  scopes: ["https://graph.microsoft.com/User.Read"]
});
```

One advantage of the scope-centric model is the ability to use *dynamic scopes*. When building applications using the v1.0 endpoint, you needed to register the full set of permissions (called *static scopes*) required by the application for the user to consent to at the time of login. In v2.0, you can use the scope parameter to request the permissions at the time you want them (hence, *dynamic scopes*). This allows the user to provide **incremental consent** to scopes. So if at the beginning you just want the user to sign in to your application and you don’t need any kind of access, you can do so. If later you need the ability to read the calendar of the user, you can then request the calendar scope in the acquireToken methods and get the user's consent. See for more: [Resources and scopes](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-browser/docs/resources-and-scopes.md)

## Use promises instead of callbacks

In ADAL.js, callbacks are used for any operation after the authentication succeeds and a response is obtained:

```javascript
authContext.acquireTokenPopup(resource, extraQueryParameter, claims, function (error, token) {
  // do something with the access token
});
```

In MSAL.js, promises are used instead:

```javascript
msalInstance.acquireTokenPopup({
      scopes: ["User.Read"] // shorthand for https://graph.microsoft.com/User.Read
  }).then((response) => {
      // do something with the auth response
  }).catch((error) => {
      // handle errors
  });
```

You can also use the **async/await** syntax that comes with ES8:

```javascript
const getAccessToken = async() => {
  try {
      const authResponse = await msalInstance.acquireTokenPopup({
          scopes: ["User.Read"]
      });
  } catch (error) {
      // handle errors
  }
}
```

## Cache and retrieve tokens

Like ADAL.js, MSAL.js caches tokens and other authentication artifacts in browser storage, using the [Web Storage API](https://developer.mozilla.org/docs/Web/API/Web_Storage_API). You're recommended to use `sessionStorage` option (see: configuration) because it's more secure in storing tokens that are acquired by your users, but `localStorage` will give you [Single Sign On](msal-js-sso) across tabs and user sessions.

Importantly, you aren't supposed to access the cache directly. Instead, you should use an appropriate MSAL.js API for retrieving authentication artifacts like access tokens or user accounts.

## Renew tokens with refresh tokens

ADAL.js uses the [OAuth 2.0 implicit flow](v2-oauth2-implicit-grant-flow), which doesn't return refresh tokens for security reasons (refresh tokens have longer lifetime than access tokens and are therefore more dangerous in the hands of malicious actors). Hence, ADAL.js performs token renewal using a hidden IFrame so that the user isn't repeatedly prompted to authenticate.

With the auth code flow with PKCE support, apps using MSAL.js 2.x obtain refresh tokens along with ID and access tokens, which can be used to renew them. The usage of refresh tokens is abstracted away, and the developers aren't supposed to build logic around them. Instead, MSAL manages token renewal using refresh tokens by itself. Your previous token cache with ADAL.js won't be transferable to MSAL.js, as the token cache schema has changed and incompatible with the schema used in ADAL.js.

## Handle errors and exceptions

When using MSAL.js, the most common type of error you might face is the `interaction_in_progress` error. This error is thrown when an interactive API (`loginPopup`, `loginRedirect`, `acquireTokenPopup`, `acquireTokenRedirect`) is invoked while another interactive API is still in progress. The `login*` and `acquireToken*` APIs are *async* so you'll need to ensure that the resulting promises have resolved before invoking another one.

Another common error is `interaction_required`. This error is often resolved by initiating an interactive token acquisition prompt. For instance, the web API you're trying to access might have a [Conditional Access](../identity/conditional-access/overview) policy in place, requiring the user to perform [multifactor authentication (MFA)](../identity/authentication/concept-mfa-howitworks). In that case, handling `interaction_required` error by triggering `acquireTokenPopup` or `acquireTokenRedirect` will prompt the user for MFA, allowing them to fullfil it.

Yet another common error you might face is `consent_required`, which occurs when permissions required for obtaining an access token for a protected resource aren't consented by the user. As in `interaction_required`, the solution for `consent_required` error is often initiating an interactive token acquisition prompt, using either `acquireTokenPopup` or `acquireTokenRedirect`.

See for more: [Common MSAL.js errors and how to handle them](msal-error-handling-js)

## Use the Events API

MSAL.js (&gt;=v2.4) introduces an events API that you can make use of in your apps. These events are related to the authentication process and what MSAL is doing at any moment, and can be used to update UI, show error messages, check if any interaction is in progress and so on. For instance, below is an event callback that will be called when login process fails for any reason:

```javascript
const callbackId = msalInstance.addEventCallback((message) => {
  // Update UI or interact with EventMessage here
  if (message.eventType === EventType.LOGIN_FAILURE) {
      if (message.error instanceof AuthError) {
          // Do something with the error
      }
    }
});
```

For performance, it's important to unregister event callbacks when they're no longer needed. See for more: [MSAL.js Events API](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-browser/docs/events.md)

## Handle multiple accounts

ADAL.js has the concept of a *user* to represent the currently authenticated entity. MSAL.js replaces *users* with *accounts*, given the fact that a user can have more than one account associated with them. This also means that you now need to control for multiple accounts and choose the appropriate one to work with. The snippet below illustrates this process:

```javascript
let homeAccountId = null; // Initialize global accountId (can also be localAccountId or username) used for account lookup later, ideally stored in app state

// This callback is passed into `acquireTokenPopup` and `acquireTokenRedirect` to handle the interactive auth response
function handleResponse(resp) {
  if (resp !== null) {
      homeAccountId = resp.account.homeAccountId; // alternatively: resp.account.homeAccountId or resp.account.username
  } else {
      const currentAccounts = myMSALObj.getAllAccounts();
      if (currentAccounts.length < 1) { // No cached accounts
          return;
      } else if (currentAccounts.length > 1) { // Multiple account scenario
          // Add account selection logic here
      } else if (currentAccounts.length === 1) {
          homeAccountId = currentAccounts[0].homeAccountId; // Single account scenario
      }
  }
}
```

For more information, see: [Accounts in MSAL.js](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-browser/docs/accounts.md)

## Use the wrappers libraries

If you're developing for Angular and React frameworks, you can use [MSAL Angular v2](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-angular) and [MSAL React](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-react), respectively. These wrappers expose the same public API as MSAL.js while offering framework-specific methods and components that can streamline the authentication and token acquisition processes.

## Run the app

Once your changes are done, run the app and test your authentication scenario:

```console
npm start
```

## Example: Securing a SPA with ADAL.js vs. MSAL.js

The snippets below demonstrates the minimal code required for a single-page application authenticating users with the Microsoft identity platform and getting an access token for Microsoft Graph using first ADAL.js and then MSAL.js:

| Using ADAL.js | Using MSAL.js |
| --- | --- |
| ```html<br><br><head><br>    <meta charset="UTF-8"><br>    <meta http-equiv="X-UA-Compatible" content="IE=edge"><br>    <meta name="viewport" content="width=device-width, initial-scale=1.0"><br>    <script type="text/javascript" src="https://alcdn.msauth.net/lib/1.0.18/js/adal.min.js"></script><br></head><br><br><body><br>    <div><br>        <p id="welcomeMessage" style="visibility: hidden;"></p><br>        <button id="loginButton">Login</button><br>        <button id="logoutButton" style="visibility: hidden;">Logout</button><br>        <button id="tokenButton" style="visibility: hidden;">Get Token</button><br>    </div><br>    <script><br>        // DOM elements to work with<br>        var welcomeMessage = document.getElementById("welcomeMessage");<br>        var loginButton = document.getElementById("loginButton");<br>        var logoutButton = document.getElementById("logoutButton");<br>        var tokenButton = document.getElementById("tokenButton");<br><br>        // if user is logged in, update the UI<br>        function updateUI(user) {<br>            if (!user) {<br>                return;<br>            }<br><br>            welcomeMessage.innerHTML = 'Hello ' + user.profile.upn + '!';<br>            welcomeMessage.style.visibility = "visible";<br>            logoutButton.style.visibility = "visible";<br>            tokenButton.style.visibility = "visible";<br>            loginButton.style.visibility = "hidden";<br>        };<br><br>        // attach logger configuration to window<br>        window.Logging = {<br>            piiLoggingEnabled: false,<br>            level: 3,<br>            log: function (message) {<br>                console.log(message);<br>            }<br>        };<br><br>        // ADAL configuration<br>        var adalConfig = {<br>            instance: 'https://login.microsoftonline.com/',<br>            clientId: "ENTER_CLIENT_ID_HERE",<br>            tenant: "ENTER_TENANT_ID_HERE",<br>            redirectUri: "ENTER_REDIRECT_URI_HERE",<br>            cacheLocation: "sessionStorage",<br>            popUp: true,<br>            callback: function (errorDesc, token, error, tokenType) {<br>                if (error) {<br>                    console.log(error, errorDesc);<br>                } else {<br>                    updateUI(authContext.getCachedUser());<br>                }<br>            }<br>        };<br><br>        // instantiate ADAL client object<br>        var authContext = new AuthenticationContext(adalConfig);<br><br>        // handle redirect response or check for cached user<br>        if (authContext.isCallback(window.location.hash)) {<br>            authContext.handleWindowCallback();<br>        } else {<br>            updateUI(authContext.getCachedUser());<br>        }<br><br>        // attach event handlers to button clicks<br>        loginButton.addEventListener('click', function () {<br>            authContext.login();<br>        });<br><br>        logoutButton.addEventListener('click', function () {<br>            authContext.logOut();<br>        });<br><br>        tokenButton.addEventListener('click', () => {<br>            authContext.acquireToken(<br>                "https://graph.microsoft.com",<br>                function (errorDesc, token, error) {<br>                    if (error) {<br>                        console.log(error, errorDesc);<br><br>                        authContext.acquireTokenPopup(<br>                            "https://graph.microsoft.com",<br>                            null, // extraQueryParameters<br>                            null, // claims<br>                            function (errorDesc, token, error) {<br>                                if (error) {<br>                                    console.log(error, errorDesc);<br>                                } else {<br>                                    console.log(token);<br>                                }<br>                            }<br>                        );<br>                    } else {<br>                        console.log(token);<br>                    }<br>                }<br>            );<br>        });<br>    </script><br></body><br><br></html><br><br>``` | ```html<br><br><head><br>    <meta charset="UTF-8"><br>    <meta http-equiv="X-UA-Compatible" content="IE=edge"><br>    <meta name="viewport" content="width=device-width, initial-scale=1.0"><br>    <script type="text/javascript" src="https://alcdn.msauth.net/browser/2.34.0/js/msal-browser.min.js"></script><br></head><br><br><body><br>    <div><br>        <p id="welcomeMessage" style="visibility: hidden;"></p><br>        <button id="loginButton">Login</button><br>        <button id="logoutButton" style="visibility: hidden;">Logout</button><br>        <button id="tokenButton" style="visibility: hidden;">Get Token</button><br>    </div><br>    <script><br>        // DOM elements to work with<br>        const welcomeMessage = document.getElementById("welcomeMessage");<br>        const loginButton = document.getElementById("loginButton");<br>        const logoutButton = document.getElementById("logoutButton");<br>        const tokenButton = document.getElementById("tokenButton");<br><br>        // if user is logged in, update the UI<br>        const updateUI = (account) => {<br>            if (!account) {<br>                return;<br>            }<br><br>            welcomeMessage.innerHTML = `Hello ${account.username}!`;<br>            welcomeMessage.style.visibility = "visible";<br>            logoutButton.style.visibility = "visible";<br>            tokenButton.style.visibility = "visible";<br>            loginButton.style.visibility = "hidden";<br>        };<br><br>        // MSAL configuration<br>        const msalConfig = {<br>            auth: {<br>                clientId: "ENTER_CLIENT_ID_HERE",<br>                authority: "https://login.microsoftonline.com/ENTER_TENANT_ID_HERE",<br>                redirectUri: "ENTER_REDIRECT_URI_HERE",<br>            },<br>            cache: {<br>                cacheLocation: "sessionStorage"<br>            },<br>            system: {<br>                loggerOptions: {<br>                    loggerCallback(loglevel, message, containsPii) {<br>                        console.log(message);<br>                    },<br>                    piiLoggingEnabled: false,<br>                    logLevel: msal.LogLevel.Verbose,<br>                }<br>            }<br>        };<br><br>        // instantiate MSAL client object<br>        const pca = new msal.PublicClientApplication(msalConfig);<br><br>        // handle redirect response or check for cached user<br>        pca.handleRedirectPromise().then((response) => {<br>            if (response) {<br>                pca.setActiveAccount(response.account);<br>                updateUI(response.account);<br>            } else {<br>                const account = pca.getAllAccounts()[0];<br>                updateUI(account);<br>            }<br>        }).catch((error) => {<br>            console.log(error);<br>        });<br><br>        // attach event handlers to button clicks<br>        loginButton.addEventListener('click', () => {<br>            pca.loginPopup().then((response) => {<br>                pca.setActiveAccount(response.account);<br>                updateUI(response.account);<br>            })<br>        });<br><br>        logoutButton.addEventListener('click', () => {<br>            pca.logoutPopup().then((response) => {<br>                window.location.reload();<br>            });<br>        });<br><br>        tokenButton.addEventListener('click', () => {<br>            const account = pca.getActiveAccount();<br><br>            pca.acquireTokenSilent({<br>                account: account,<br>                scopes: ["User.Read"]<br>            }).then((response) => {<br>                console.log(response);<br>            }).catch((error) => {<br>                if (error instanceof msal.InteractionRequiredAuthError) {<br>                    pca.acquireTokenPopup({<br>                        scopes: ["User.Read"]<br>                    }).then((response) => {<br>                        console.log(response);<br>                    });<br>                }<br><br>                console.log(error);<br>            });<br>        });<br>    </script><br></body><br><br></html><br><br>``` |
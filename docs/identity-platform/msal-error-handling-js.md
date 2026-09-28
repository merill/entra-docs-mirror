---
layout: Conceptual
title: Handle errors and exceptions in MSAL.js - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/msal-error-handling-js
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to handle errors and exceptions, Conditional Access claims challenges, and retries in MSAL.js applications.
manager: dougeby
ms.custom: 
ms.date: 2023-12-19T00:00:00.0000000Z
ms.reviewer: 
ms.topic: how-to
locale: en-us
document_id: 4e97ee60-1cb2-9517-04b5-f7c80f7bcd7b
document_version_independent_id: 08b8c5f2-333a-8576-c5d2-64afa758892c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/msal-error-handling-js.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/msal-error-handling-js
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/msal-error-handling-js.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 9aacec84-ea1f-a9e0-04ba-5781a326ea5a
---

# Handle errors and exceptions in MSAL.js - Microsoft identity platform | Microsoft Learn

This article gives an overview of the different types of errors and recommendations for handling common sign-in errors.

## MSAL error handling basics

Exceptions in Microsoft Authentication Library (MSAL) are intended for app developers to troubleshoot, not for displaying to end users. Exception messages are not localized.

When processing exceptions and errors, you can use the exception type itself and the error code to distinguish between exceptions. For a list of error codes, see [Microsoft Entra authentication and authorization error codes](reference-error-codes).

During the sign-in experience, you may encounter errors about consents, Conditional Access (MFA, Device Management, Location-based restrictions), token issuance and redemption, and user properties.

The following section provides more details about error handling for your app.

## Error handling in MSAL.js

MSAL.js provides error objects that abstract and classify the different types of common errors. It also provides an interface to access specific details of the errors such as error messages to handle them appropriately.

### Error object

```javascript
export class AuthError extends Error {
    // This is a short code describing the error
    errorCode: string;
    // This is a descriptive string of the error,
    // and may also contain the mitigation strategy
    errorMessage: string;
    // Name of the error class
    this.name = "AuthError";
}
```

By extending the error class, you have access to the following properties:

- `AuthError.message`: Same as the `errorMessage`.
- `AuthError.stack`: Stack trace for thrown errors.

### Error types

The following error types are available:

- `AuthError`: Base error class for the MSAL.js library, also used for unexpected errors.
- `ClientAuthError`: Error class that denotes an issue with Client authentication. Most errors that come from the library are ClientAuthErrors. These errors result from things like calling a login method when login is already in progress, the user cancels the login, and so on.
- `ClientConfigurationError`: Error class that extends `ClientAuthError`. It's thrown before requests are made when the given user config parameters are malformed or missing.
- `ServerError`: Error class, represents the error strings sent by the authentication server. These errors may be invalid request formats or parameters, or any other errors that prevent the server from authenticating or authorizing the user.
- `InteractionRequiredAuthError`: Error class, extends `ServerError` to represent server errors, which require an interactive call. This error is thrown by `acquireTokenSilent` if the user is required to interact with the server to provide credentials or consent for authentication/authorization. Error codes include `"interaction_required"`, `"login_required"`, and `"consent_required"`.

For error handling in authentication flows with redirect methods (`loginRedirect`, `acquireTokenRedirect`), you'll need to handle the redirect promise, which is called with success or failure after the redirect using the `handleRedirectPromise()` method as follows:

```javascript
const msal = require('@azure/msal-browser');
const myMSALObj = new msal.PublicClientApplication(msalConfig);

// Register Callbacks for redirect flow
myMSALObj.handleRedirectPromise()
    .then(function (response) {
        //success response
    })
    .catch((error) => {
        console.log(error);
    })
myMSALObj.acquireTokenRedirect(request);
```

The methods for pop-up experience (`loginPopup`, `acquireTokenPopup`) return promises, so you can use the promise pattern (`.then` and `.catch`) to handle them as shown:

```javascript
myMSALObj.acquireTokenPopup(request).then(
    function (response) {
        // success response
    }).catch(function (error) {
        console.log(error);
    });
```

### Errors that require interaction

An error is returned when you attempt to use a non-interactive method of acquiring a token such as `acquireTokenSilent`, but MSAL couldn't do it silently.

Possible reasons are:

- you need to sign in
- you need to consent
- you need to go through a multi-factor authentication experience.

The remediation is to call an interactive method such as `acquireTokenPopup` or `acquireTokenRedirect`:

```javascript
// Request for Access Token
myMSALObj.acquireTokenSilent(request).then(function (response) {
    // call API
}).catch( function (error) {
    // call acquireTokenPopup in case of acquireTokenSilent failure
    // due to interaction required
    if (error instanceof InteractionRequiredAuthError) {
        myMSALObj.acquireTokenPopup(request).then(
            function (response) {
                // call API
            }).catch(function (error) {
                console.log(error);
            });
    }
});
```

## Conditional Access and claims challenges

When getting tokens silently, your application may receive errors when a [Conditional Access claims challenge](v2-conditional-access-dev-guide) such as MFA policy is required by an API you're trying to access.

The pattern for handling this error is to interactively acquire a token using MSAL. This prompts the user and gives them the opportunity to satisfy the required Conditional Access policy.

In certain cases when calling an API requiring Conditional Access, you can receive a claims challenge in the error from the API. For instance if the Conditional Access policy is to have a managed device (Intune) the error will be something like [AADSTS53000: Your device is required to be managed to access this resource](reference-error-codes) or something similar. In this case, you can pass the claims in the acquire token call so that the user is prompted to satisfy the appropriate policy.

When getting tokens silently (using `acquireTokenSilent`) using MSAL.js, your application may receive errors when the API you're trying to access requires a [Conditional Access claims challenge](v2-conditional-access-dev-guide) such as MFA policy.

The pattern to handle this error is to make an interactive call to acquire token in MSAL.js such as `acquireTokenPopup` or `acquireTokenRedirect` as in the following example:

```javascript
myMSALObj.acquireTokenSilent(accessTokenRequest).then(function(accessTokenResponse) {
    // call API
}).catch(function(error) {
    if (error instanceof InteractionRequiredAuthError) {
    
        // extract, if exists, claims from the error object
        if (error.claims) {
            accessTokenRequest.claims = error.claims,
        
        // call acquireTokenPopup in case of InteractionRequiredAuthError failure
        myMSALObj.acquireTokenPopup(accessTokenRequest).then(function(accessTokenResponse) {
            // call API
        }).catch(function(error) {
            console.log(error);
        });
    }
});
```

Interactively acquiring the token prompts the user and gives them the opportunity to satisfy the required Conditional Access policy.

When calling an API requiring Conditional Access, you can receive a claims challenge in the error from the API. In this case, you can pass the claims returned in the error to the `claims` parameter in the [access token request object](msal-js-pass-custom-state-authentication-request) to satisfy the appropriate policy.

See [How to use Continuous Access Evaluation enabled APIs in your applications](app-resilience-continuous-access-evaluation) for more detail.

### Using other frameworks

Using toolkits like Tauri for registered single page applications (SPAs) with the identity platform is not recognized for production apps. SPAs only support URLs that start with `https` for production apps and `http://localhost` for local development. Prefixes like `tauri://localhost` can't be used for browser apps. This format can only be supported for mobile or web apps as they have a confidential component unlike browser apps.

## Retrying after errors and exceptions

You're expected to implement your own retry policies when calling MSAL. MSAL makes HTTP calls to the Microsoft Entra service, and occasionally failures can occur. For example the network can go down or the server is overloaded.

### HTTP 429

When the Service Token Server (STS) is overloaded with too many requests, it returns HTTP error 429 with a hint about how long until you can try again in the `Retry-After` response field.
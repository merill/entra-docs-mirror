---
layout: Conceptual
title: Initialize MSAL.js client apps - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/msal-js-initializing-client-applications
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn about initializing client applications using the Microsoft Authentication Library for JavaScript (MSAL.js).
manager: pmwongera
ms.custom: 
ms.date: 2025-05-12T00:00:00.0000000Z
ms.reviewer: 
ms.topic: how-to
locale: en-us
document_id: 69b44d91-f31e-b934-dbb0-fc7e69954b44
document_version_independent_id: 76a2ef76-270a-e6f9-d13a-88b04be315d7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/msal-js-initializing-client-applications.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/msal-js-initializing-client-applications
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/msal-js-initializing-client-applications.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/fe39cd45-39de-4047-953d-db268d7c71d9
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/ca56ff04-5597-4109-9f5d-17812bae2fac
platformId: d1993ea4-d24d-c47f-fe06-c6aea985c1bb
---

# Initialize MSAL.js client apps - Microsoft identity platform | Microsoft Learn

This article describes initializing the Microsoft Authentication Library for JavaScript (MSAL.js) with an instance of a user-agent application.

The user-agent application is a form of public client application in which the client code is executed in a user-agent such as a web browser. Clients such as these don't store secrets because the browser context is openly accessible.

To learn more about the client application types and application configuration options, see [Public and confidential client apps in MSAL](msal-client-applications).

## Prerequisites

Before initializing an application, you first need to [register it in the Microsoft Entra admin center](scenario-spa-app-configuration), establishing a trust relationship between your application and the Microsoft identity platform.

After registering your app, you'll need some or all of the following values that can be found in the Microsoft Entra admin center.

| Value | Required | Description |
| --- | --- | --- |
| Application (client) ID | Required | A GUID that uniquely identifies your application within the Microsoft identity platform. |
| Authority | Optional | The identity provider URL (the *instance*) and the *sign-in audience* for your application. The instance and sign-in audience, when concatenated, make up the *authority*. |
| Directory (tenant) ID | Optional | Specify Directory (tenant) ID if you're building a line-of-business application solely for your organization, often referred to as a *single-tenant application*. |
| Redirect URI | Optional | If you're building a web app, the `redirectUri` specifies where the identity provider (the Microsoft identity platform) should return the security tokens it has issued. |

## Initialize MSAL.js 2.x apps

Initialize the MSAL.js authentication context by instantiating a [PublicClientApplication][msal-js-publicclientapplication] with a [Configuration][msal-js-configuration] object. The minimum required configuration property is the `clientID` of the application, shown as **Application (client) ID** on the **Overview** page of the app registration in the Microsoft Entra admin center.

Here's an example configuration object and instantiation of a `PublicClientApplication`:

```javascript
const msalConfig = {
  auth: {
    clientId: "Enter_the_Application_Id_Here",
    authority: "https://login.microsoftonline.com/Enter_the_Tenant_Info_Here",
    knownAuthorities: [],
    redirectUri: "https://localhost:{port}/redirect",
    postLogoutRedirectUri: "https://localhost:{port}/redirect",
    navigateToLoginRequestUrl: true,
  },
  cache: {
    cacheLocation: "sessionStorage",
    storeAuthStateInCookie: false,
  },
  system: {
    loggerOptions: {
      loggerCallback: (
        level: LogLevel,
        message: string,
        containsPii: boolean
      ): void => {
        if (containsPii) {
          return;
        }
        switch (level) {
          case LogLevel.Error:
            console.error(message);
            return;
          case LogLevel.Info:
            console.info(message);
            return;
          case LogLevel.Verbose:
            console.debug(message);
            return;
          case LogLevel.Warning:
            console.warn(message);
            return;
        }
      },
      piiLoggingEnabled: false,
    },
    windowHashTimeout: 60000,
    iframeHashTimeout: 6000,
    loadFrameTimeout: 0,
  },
};

// Create an instance of PublicClientApplication
const msalInstance = new PublicClientApplication(msalConfig);

// Handle the redirect flows
msalInstance
  .handleRedirectPromise()
  .then((tokenResponse) => {
    // Handle redirect response
  })
  .catch((error) => {
    // Handle redirect error
  });
```

### `handleRedirectPromise`

Invoke [handleRedirectPromise][msal-js-handleredirectpromise] when the application uses redirect flows. When using redirect flows, `handleRedirectPromise` should be run on every page load.

Three outcomes are possible from the promise:

- `.then` is invoked and `tokenResponse` is truthy: The application is returning from a redirect operation that was successful.
- `.then` is invoked and `tokenResponse` is falsy (`null`): The application isn't returning from a redirect operation.
- `.catch` is invoked: The application is returning from a redirect operation and there was an error.

## Initialize MSAL.js 1.x apps

Initialize the MSAL 1.x authentication context by instantiating a UserAgentApplication with a configuration object. The minimum required configuration property is the `clientID` of your application, shown as **Application (client) ID** on the **Overview** page of the app registration in the Microsoft Entra admin center.

For authentication methods with redirect flows (loginRedirect and acquireTokenRedirect) in MSAL.js 1.2.x or earlier, you must explicitly register a callback for success or error through the `handleRedirectCallback()` method. Explicitly registering the callback is required in MSAL.js 1.2.x and earlier because redirect flows don't return promises like the methods with a pop-up experience do. Registering the callback is *optional* in MSAL.js version 1.3.x and later.

```javascript
// Configuration object constructed
const msalConfig = {
  auth: {
    clientId: "Enter_the_Application_Id_Here",
  },
};

// Create UserAgentApplication instance
const msalInstance = new UserAgentApplication(msalConfig);

function authCallback(error, response) {
  // Handle redirect response
}

// Register a redirect callback for Success or Error (when using redirect methods)
// **REQUIRED** in MSAL.js 1.2.x and earlier
// **OPTIONAL** in MSAL.js 1.3.x and later
msalInstance.handleRedirectCallback(authCallback);
```

## Single instance and configuration

Both MSAL.js 1.x and 2.x are designed to have a single instance and configuration of the `UserAgentApplication` or `PublicClientApplication`, respectively, to represent a single authentication context.

Multiple instances of `UserAgentApplication` or `PublicClientApplication` aren't recommended as they can cause conflicting cache entries and behavior in the browser.
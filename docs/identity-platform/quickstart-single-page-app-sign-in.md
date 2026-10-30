---
layout: Conceptual
title: Quickstart - Sign in users in a single-page app (SPA) and call the Microsoft Graph API - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-single-page-app-sign-in
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Quickstart that shows how to configure a sample SPA that signs in employees or customers by using the Microsoft identity platform
manager: pmwongera
ms.custom: 
ms.date: 2025-01-27T00:00:00.0000000Z
ms.reviewer: 
zone_pivot_groups: entra-tenants
ms.topic: quickstart
locale: en-us
document_id: b22a5c16-97fb-0509-f4d2-70a44c0c0385
document_version_independent_id: b22a5c16-97fb-0509-f4d2-70a44c0c0385
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/quickstart-single-page-app-sign-in.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/quickstart-single-page-app-sign-in
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/quickstart-single-page-app-sign-in.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: cf317eac-6195-3ddc-326b-904eddd07ccc
---

# Quickstart - Sign in users in a single-page app (SPA) and call the Microsoft Graph API - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this quickstart, you use a sample single-page app (SPA) to show you how to sign in users by using the [authorization code flow](v2-oauth2-auth-code-flow) with Proof Key for Code Exchange (PKCE) and call the Microsoft Graph API. The sample uses the [Microsoft Authentication Library](msal-overview) to handle authentication.

::: zone pivot="workforce"

## Prerequisites

- An Azure account with an active subscription. If you don't already have one, [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- This Azure account must have permissions to manage applications. Any of the following Microsoft Entra roles include the required permissions:
    - Application Administrator
    - Application Developer
- A workforce tenant. You can use your Default Directory or [set up a new tenant](quickstart-create-new-tenant).
- [Visual Studio Code](https://code.visualstudio.com/download) or another code editor.

# [JavaScript](#tab/javascript-workforce)
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- Add the following redirect URIs using the **Single-page application** platform configuration. Refer to [How to add a redirect URI in your application](how-to-add-redirect-uri)for more details.
    - **Redirect URI**: `http://localhost:3000/`
- [Node.js](https://nodejs.org/en/download/)

# [React](#tab/react-workforce)
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- Add the following redirect URIs using the **Single-page application** platform configuration. Refer to [How to add a redirect URI in your application](how-to-add-redirect-uri)for more details.
    - **Redirect URI**: `http://localhost:3000/`
- [Node.js](https://nodejs.org/en/download/)

# [Angular](#tab/angular-workforce)
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- Add the following redirect URI using the **Single-page application** platform configuration. Refer to [How to add a redirect URI in your application](how-to-add-redirect-uri)for more details.
    - **Redirect URI**: `http://localhost:4200/`
- [Node.js](https://nodejs.org/en/download/)

# [Blazor](#tab/blazor-workforce)
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- Add the following redirect URIs using the **Single-page application** platform configuration. Refer to [How to add a redirect URI in your application](how-to-add-redirect-uri)for more details.
    - **Redirect URI**: `http://localhost:5000/authentication/login-callback.`
- [.NET SDK](https://dotnet.microsoft.com/download/dotnet)

---

## Clone or download the sample application

To obtain the sample application, you can either clone it from GitHub or download it as a .zip file.

# [JavaScript](#tab/javascript-workforce)
- To clone the sample, open a command prompt and navigate to where you wish to create the project, and enter the following command:

    ```console
    git clone https://github.com/Azure-Samples/ms-identity-docs-code-javascript.git
    ```
- [Download the .zip file](https://github.com/Azure-Samples/ms-identity-docs-code-javascript/archive/refs/heads/main.zip). Extract it to a file path where the length of the name is fewer than 260 characters.

# [React](#tab/react-workforce)
- To clone the sample, open a command prompt and navigate to where you wish to create the project, and enter the following command:

    ```console
    git clone https://github.com/Azure-Samples/ms-identity-docs-code-javascript.git
    ```
- [Download the .zip file](https://github.com/Azure-Samples/ms-identity-docs-code-javascript/tree/main). Extract it to a file path where the length of the name is fewer than 260 characters.

# [Angular](#tab/angular-workforce)
- To clone the sample, open a command prompt and navigate to where you wish to create the project, and enter the following command:

    ```console
    git clone https://github.com/Azure-Samples/ms-identity-docs-code-javascript.git
    ```
- [Download the .zip file](https://github.com/Azure-Samples/ms-identity-docs-code-javascript/archive/refs/heads/main.zip). Extract it to a file path where the length of the name is fewer than 260 characters.

# [Blazor](#tab/blazor-workforce)
- To clone the sample, open a command prompt and navigate to where you wish to create the project, and enter the following command:

    ```console
    git clone https://github.com/Azure-Samples/ms-identity-docs-code-dotnet.git
    ```
- [Download the .zip file](https://github.com/Azure-Samples/ms-identity-docs-code-dotnet/archive/refs/heads/main.zip). Extract it to a file path where the length of the name is fewer than 260 characters.

---

## Configure the project

# [JavaScript](#tab/javascript-workforce)
1. In your IDE, open the project folder, *ms-identity-docs-code-javascript*, containing the sample.
2. Open *vanillajs-spa/App/public/authConfig.js* and update the following values with the information recorded in the admin center.

    ```JavaScript
    /**
     * Configuration object to be passed to MSAL instance on creation. 
     * For a full list of MSAL.js configuration parameters, visit:
     * https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-browser/docs/configuration.md 
     */
    const msalConfig = {
        auth: {
             clientId: "Enter_the_Application_Id_Here",
             // WORKFORCE TENANT
             authority: "https://login.microsoftonline.com/Enter_the_Tenant_Info_Here", //  Replace the placeholder with your tenant info
             // EXTERNAL TENANT
             // authority: "https://Enter_the_Tenant_Subdomain_Here.ciamlogin.com/", // Replace the placeholder with your tenant subdomain
            redirectUri: '/', // You must register this URI on App Registration. Defaults to window.location.href e.g. http://localhost:3000/
            navigateToLoginRequestUrl: true, // If "true", will navigate back to the original request location before processing the auth code response.
        },
        cache: {
            cacheLocation: 'sessionStorage', // Configures cache location. "sessionStorage" is more secure, but "localStorage" gives you SSO.
            storeAuthStateInCookie: false, // set this to true if you have to support IE
        },
        system: {
            loggerOptions: {
                loggerCallback: (level, message, containsPii) => {
                    if (containsPii) {
                        return;
                    }
                    switch (level) {
                        case msal.LogLevel.Error:
                            console.error(message);
                            return;
                        case msal.LogLevel.Info:
                            console.info(message);
                            return;
                        case msal.LogLevel.Verbose:
                            console.debug(message);
                            return;
                        case msal.LogLevel.Warning:
                            console.warn(message);
                            return;
                    }
                },
            },
        },
    };
    
    /**
     * Scopes you add here will be prompted for user consent during sign-in.
     * By default, MSAL.js will add OIDC scopes (openid, profile, email) to any login request.
     * For more information about OIDC scopes, visit: 
     * https://learn.microsoft.com/en-us/entra/identity-platform/permissions-consent-overview#openid-connect-scopes
     */
    const loginRequest = {
        scopes: ["User.Read"],
    };
    
    /**
     * An optional silentRequest object can be used to achieve silent SSO
     * between applications by providing a "login_hint" property.
     */
    
    // const silentRequest = {
    //   scopes: ["openid", "profile"],
    //   loginHint: "example@domain.net"
    // };
    
    // exporting config object for jest
    if (typeof exports !== 'undefined') {
        module.exports = {
            msalConfig: msalConfig,
            loginRequest: loginRequest,
        };
    }
    ```

    - `clientId` - The identifier of the application, also referred to as the client. Replace the text in quotes with the **Application (client) ID** value that was recorded earlier.
    - `authority` - The authority is a URL that indicates a directory that MSAL can request tokens from. Replace *Enter\_the\_Tenant\_Info\_Here* with the **Directory (tenant) ID** value that was recorded earlier.
    - `redirectUri` - The **Redirect URI** of the application. If necessary, replace the text in quotes with the redirect URI that was recorded earlier.

# [React](#tab/react-workforce)
1. In your IDE, open the project folder, *ms-identity-docs-code-javascript/react-spa*, containing the sample.
2. Open *react-spa/src/authConfig.js* and update the following values with the information recorded in the admin center.

    ```JavaScript
    /*
     * Copyright (c) Microsoft Corporation. All rights reserved.
     * Licensed under the MIT License.
     */
    
    import { LogLevel } from "@azure/msal-browser";
    
    /**
     * Configuration object to be passed to MSAL instance on creation. 
     * For a full list of MSAL.js configuration parameters, visit:
     * https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-browser/docs/configuration.md 
     */
    
    export const msalConfig = {
        auth: {
            clientId: "Enter_the_Application_Id_Here",
            authority: "https://login.microsoftonline.com/Enter_the_Tenant_Info_Here",
            redirectUri: "http://localhost:3000",
        },
        cache: {
            cacheLocation: "sessionStorage", // This configures where your cache will be stored
            storeAuthStateInCookie: false, // Set this to "true" if you are having issues on IE11 or Edge
        },
        system: {	
            loggerOptions: {	
                loggerCallback: (level, message, containsPii) => {	
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
                        default:
                            return;
                    }	
                }	
            }	
        }
    };
    
    /**
     * Scopes you add here will be prompted for user consent during sign-in.
     * By default, MSAL.js will add OIDC scopes (openid, profile, email) to any login request.
     * For more information about OIDC scopes, visit: 
     * https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-permissions-and-consent#openid-connect-scopes
     */
    export const loginRequest = {
        scopes: ["User.Read"]
    };
    
    /**
     * Add here the scopes to request when obtaining an access token for MS Graph API. For more information, see:
     * https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-browser/docs/resources-and-scopes.md
     */
    export const graphConfig = {
        graphMeEndpoint: "https://graph.microsoft.com/v1.0/me",
    };
    ```

    - `clientId` - The identifier of the application, also referred to as the client. Replace the text in quotes with the **Application (client) ID** value that was recorded earlier.
    - `authority` - The authority is a URL that indicates a directory that MSAL can request tokens from. Replace *Enter\_the\_Tenant\_Info\_Here* with the **Directory (tenant) ID** value that was recorded earlier.
    - `redirectUri` - The **Redirect URI** of the application. If necessary, replace the text in quotes with the redirect URI that was recorded earlier.

# [Angular](#tab/angular-workforce)
1. In your IDE, open the project folder, *ms-identity-docs-code-javascript/angular-spa*, containing the sample.
2. Open *angular-spa/src/app/app.module.ts* and update the following values with the information recorded in the admin center.

    ```JavaScript
    // Required for Angular multi-browser support
    import { BrowserModule } from '@angular/platform-browser';
    
    // Required for Angular
    import { NgModule } from '@angular/core';
    
    // Required modules and components for this application
    import { AppRoutingModule } from './app-routing.module';
    import { AppComponent } from './app.component';
    import { ProfileComponent } from './profile/profile.component';
    import { HomeComponent } from './home/home.component';
    
    // HTTP modules required by MSAL
    import { HTTP_INTERCEPTORS, HttpClientModule } from '@angular/common/http';
    
    // Required for MSAL
    import { IPublicClientApplication, PublicClientApplication, InteractionType, BrowserCacheLocation, LogLevel } from '@azure/msal-browser';
    import { MsalGuard, MsalInterceptor, MsalBroadcastService, MsalInterceptorConfiguration, MsalModule, MsalService, MSAL_GUARD_CONFIG, MSAL_INSTANCE, MSAL_INTERCEPTOR_CONFIG, MsalGuardConfiguration, MsalRedirectComponent } from '@azure/msal-angular';
    
    const isIE = window.navigator.userAgent.indexOf('MSIE ') > -1 || window.navigator.userAgent.indexOf('Trident/') > -1;
    
    export function MSALInstanceFactory(): IPublicClientApplication {
      return new PublicClientApplication({
        auth: {
          // 'Application (client) ID' of app registration in the Microsoft Entra admin center - this value is a GUID
          clientId: "Enter_the_Application_Id_Here",
          // Full directory URL, in the form of https://login.microsoftonline.com/<tenant>
          authority: "https://login.microsoftonline.com/Enter_the_Tenant_Info_Here",
          // Must be the same redirectUri as what was provided in your app registration.
          redirectUri: "http://localhost:4200",
        },
        cache: {
          cacheLocation: BrowserCacheLocation.LocalStorage,
          storeAuthStateInCookie: isIE
        }
      });
    }
    
    // MSAL Interceptor is required to request access tokens in order to access the protected resource (Graph)
    export function MSALInterceptorConfigFactory(): MsalInterceptorConfiguration {
      const protectedResourceMap = new Map<string, Array<string>>();
      protectedResourceMap.set('https://graph.microsoft.com/v1.0/me', ['user.read']);
    
      return {
        interactionType: InteractionType.Redirect,
        protectedResourceMap
      };
    }
    
    // MSAL Guard is required to protect routes and require authentication before accessing protected routes
    export function MSALGuardConfigFactory(): MsalGuardConfiguration {
      return { 
        interactionType: InteractionType.Redirect,
        authRequest: {
          scopes: ['user.read']
        }
      };
    }
    
    // Create an NgModule that contains the routes and MSAL configurations
    @NgModule({
      declarations: [
        AppComponent,
        HomeComponent,
        ProfileComponent
      ],
      imports: [
        BrowserModule,
        AppRoutingModule,
        HttpClientModule,
        MsalModule
      ],
      providers: [
        {
          provide: HTTP_INTERCEPTORS,
          useClass: MsalInterceptor,
          multi: true
        },
        {
          provide: MSAL_INSTANCE,
          useFactory: MSALInstanceFactory
        },
        {
          provide: MSAL_GUARD_CONFIG,
          useFactory: MSALGuardConfigFactory
        },
        {
          provide: MSAL_INTERCEPTOR_CONFIG,
          useFactory: MSALInterceptorConfigFactory
        },
        MsalService,
        MsalGuard,
        MsalBroadcastService
      ],
      bootstrap: [AppComponent, MsalRedirectComponent]
    })
    export class AppModule { }
    ```

    - `clientId` - The identifier of the application, also referred to as the client. Replace the text in quotes with the **Application (client) ID** value that was recorded earlier.
    - `authority` - The authority is a URL that indicates a directory that MSAL can request tokens from. Replace *Enter\_the\_Tenant\_Info\_Here* with the **Directory (tenant) ID** value that was recorded earlier.
    - `redirectUri` - The **Redirect URI** of the application. If necessary, replace the text in quotes with the redirect URI that was recorded earlier.

# [Blazor](#tab/blazor-workforce)
1. In your IDE, open the project folder, *ms-identity-docs-code-dotnet/spa-blazor-wasm*, containing the sample.
2. Open *spa-blazor-wasm/wwwroot/appsettings.json* and update the following values with the information recorded earlier in the admin center.

    ```JavaScript
    {
      "AzureAd": {
        "Authority": "https://login.microsoftonline.com/<Enter the tenant ID obtained from the Microsoft Entra admin center>",
        "ClientId": "Enter the client ID obtained from the Microsoft Entra admin center",
        "ValidateAuthority": true
      }
    }
    ```

    - `Authority` - The authority is a URL that indicates a directory that MSAL can request tokens from. Replace *Enter\_the\_Tenant\_Info\_Here* with the **Directory (tenant) ID** value that was recorded earlier.
    - `ClientId` - The identifier of the application, also referred to as the client. Replace the text in quotes with the **Application (client) ID** value that was recorded earlier.

---

## Run the application and sign in and sign out

# [JavaScript](#tab/javascript-workforce)
Run the project with a web server by using Node.js:

1. To start the server, run the following commands from within the project directory:

    ```console
    cd vanillajs-spa/App
    npm install
    npm start
    ```
2. Copy the `https` URL that appears in the terminal, for example, `https://localhost:3000`, and paste it into a browser. We recommend using a private or incognito browser session.
3. Follow the steps and enter the necessary details to sign in with your Microsoft account. You'll be requested an email address so a one time passcode can be sent to you. Enter the code when prompted.
4. The application will request permission to maintain access to data you have given it access to, and to sign you in and read your profile. Select **Accept**. The following screenshot appears, indicating that you have signed in to the application and have accessed your profile details from the Microsoft Graph API.

    [![Screenshot of JavaScript App depicting the results of the API call.](media/quickstarts/js-spa/quickstart-js-spa-sign-in.png)](media/quickstarts/js-spa/quickstart-js-spa-sign-in.png#lightbox)

# [React](#tab/react-workforce)
Run the project with a web server by using Node.js:

1. To start the server, run the following commands from within the project directory:

    ```console
    cd react-spa
    npm install
    npm start
    ```
2. Copy the `https` URL that appears in the terminal, for example, `https://localhost:3000`, and paste it into a browser. We recommend using a private or incognito browser session.
3. Follow the steps and enter the necessary details to sign in with your Microsoft account. You're requested an email address so a one time passcode can be sent to you. Enter the code when prompted.
4. The application requests permission to maintain access to data you have given it access to, and to sign you in and read your profile. Select **Accept**. The following screenshot appears, indicating that you have signed in to the application and have accessed your profile details from the Microsoft Graph API.

    [![Screenshot of JavaScript App depicting the results of the API call.](media/common-spa/react-spa/display-api-call-results-react-spa.png)](media/common-spa/react-spa/display-api-call-results-react-spa.png#lightbox)

# [Angular](#tab/angular-workforce)
Run the project with a web server by using Node.js:

1. To start the server, run the following commands from within the project directory:

    ```console
    cd angular-spa
    npm install
    npm start
    ```
2. Copy the `https` URL that appears in the terminal, for example, `https://localhost:4200`, and paste it into a browser address bar. We recommend using a private or incognito browser session.
3. Follow the steps and enter the necessary details to sign in with your Microsoft account. You'll be requested an email address so a one time passcode can be sent to you. Enter the code when prompted.
4. The application will request permission to maintain access to data you have given it access to, and to sign you in and read your profile. Select **Accept**. The following screenshot appears, indicating that you have signed in to the application and have accessed your profile details from the Microsoft Graph API.

    [![Screenshot of JavaScript App depicting the results of the API call.](media/quickstarts/angular-spa/quickstart-angular-spa-sign-in.png)](media/quickstarts/angular-spa/quickstart-angular-spa-sign-in.png#lightbox)

# [Blazor](#tab/blazor-workforce)
Run the project with a web server by using dotnet:

1. To start the server, run the following commands from within the project directory:

    ```console
    cd spa-blazor-wasm
    dotnet workload install wasm-tools
    dotnet run
    ```
2. Copy the `http` URL that appears in the terminal, for example, `http://localhost:5000`, and paste it into a browser. We recommend using a private or incognito browser session.
3. Follow the steps and enter the necessary details to sign in with your Microsoft account. You'll be requested an email address so a one time passcode can be sent to you. Enter the code when prompted.
4. The application will request permission to maintain access to data you have given it access to, and to sign you in and read your profile. Select **Accept**. The following screenshot appears, indicating that you have signed in to the application and have accessed your profile details from the Microsoft Graph API.

    [![Screenshot of Blazor WASM SPA App depicting the results of the API call.](media/common-spa/blazor-spa/display-api-call-results-blazor-spa.png)](media/common-spa/blazor-spa/display-api-call-results-blazor-spa.png#lightbox)

---

::: zone-end

::: zone pivot="external"

## Prerequisites

- An Azure account with an active subscription. If you don't already have one, [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- This Azure account must have permissions to manage applications. Any of the following Microsoft Entra roles include the required permissions:
    - Application Administrator
    - Application Developer
- An external tenant. To create one, choose from the following methods:
    - Use the [Microsoft Entra External ID extension](https://aka.ms/ciamvscode/samples/marketplace) to set up an external tenant directly in Visual Studio Code. *(Recommended)*
    - [Create a new external tenant](../external-id/customers/how-to-create-external-tenant-portal) in the Microsoft Entra admin center.
- A user flow. For more information, refer to [create self-service sign-up user flows for apps in external tenants](../external-id/customers/how-to-user-flow-sign-up-sign-in-customers). This user flow can be used for multiple applications.
- [Visual Studio Code](https://code.visualstudio.com/download) or another code editor.

# [JavaScript](#tab/javascript-external)
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- Add the following redirect URIs using the **Single-page application** platform configuration. Refer to [How to add a redirect URI in your application](how-to-add-redirect-uri)for more details.
    - **Redirect URI**: `http://localhost:3000/`
- [Add your application to the user flow](/en-us/entra/external-id/customers/how-to-user-flow-add-application)
- [Node.js](https://nodejs.org/en/download/)

# [React](#tab/react-external)
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- Add the following redirect URIs using the **Single-page application** platform configuration. Refer to [How to add a redirect URI in your application](how-to-add-redirect-uri)for more details.
    - **Redirect URI**: `http://localhost:3000/`
- [Add your application to the user flow](/en-us/entra/external-id/customers/how-to-user-flow-add-application)
- [Node.js](https://nodejs.org/en/download/)

# [Angular](#tab/angular-external)
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- Add the following redirect URIs using the **Single-page application** platform configuration. Refer to [How to add a redirect URI in your application](how-to-add-redirect-uri)for more details.
    - **Redirect URI**: `http://localhost:4200/`
- [Add your application to the user flow](/en-us/entra/external-id/customers/how-to-user-flow-add-application)
- [Node.js](https://nodejs.org/en/download/)

---

## Clone or download sample SPA

To obtain the sample application, you can either clone it from GitHub or download it as a .zip file.

# [JavaScript](#tab/javascript-external)
- To clone the sample, open a command prompt and navigate to where you wish to create the project, and enter the following command:

    ```console
    git clone https://github.com/Azure-Samples/ms-identity-ciam-javascript-tutorial.git
    ```
- [Download the sample](https://github.com/Azure-Samples/ms-identity-ciam-javascript-tutorial/archive/refs/heads/main.zip). Extract it to a file path where the length of the name is fewer than 260 characters.

# [React](#tab/react-external)
- To clone the sample, open a command prompt and navigate to where you wish to create the project, and enter the following command:

    ```console
    git clone https://github.com/Azure-Samples/ms-identity-ciam-javascript-tutorial.git
    ```
- [Download the sample](https://github.com/Azure-Samples/ms-identity-ciam-javascript-tutorial/archive/refs/heads/main.zip). Extract it to a file path where the length of the name is fewer than 260 characters.

# [Angular](#tab/angular-external)
- To clone the sample, open a command prompt and navigate to where you wish to create the project, and enter the following command:

    ```console
    git clone https://github.com/Azure-Samples/ms-identity-ciam-javascript-tutorial.git
    ```
- [Download the sample](https://github.com/Azure-Samples/ms-identity-ciam-javascript-tutorial/archive/refs/heads/main.zip). Extract it to a file path where the length of the name is fewer than 260 characters.

---

## Configure the sample SPA

# [JavaScript](#tab/javascript-external)
1. Open `App/public/authConfig.js` and replace the following with the values obtained from the Microsoft Entra admin center:

    - `Enter_the_Application_Id_Here` and replace it with the Application (client) ID of the app you registered earlier.
    - `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant name, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).
2. Save the file.

# [React](#tab/react-external)
1. Open `SPA\src\authConfig.js` and replace the following with the values obtained from the Microsoft Entra admin center:

    - `Enter_the_Application_Id_Here` and replace it with the Application (client) ID of the app you registered earlier.
    - `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant name, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).
2. Save the file.

# [Angular](#tab/angular-external)
1. Open `SPA/src/app/auth-config.ts` and replace the following with the values obtained from the Microsoft Entra admin center:

    - `Enter_the_Application_Id_Here` and replace it with the Application (client) ID of the app you registered earlier.
    - `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant name, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).
2. Save the file.

---

## Run your project and sign in

# [JavaScript](#tab/javascript-external)
1. To start the server, run the following commands from within the project directory:

    ```console
    cd 1-Authentication\0-sign-in-vanillajs\App
    npm install
    npm start
    ```
2. Copy the `https` URL that appears in the terminal, for example, `https://localhost:3000`, and paste it into a browser. We recommend using a private or incognito browser session.
3. Sign-in with an account registered to the tenant.
4. The following screenshot appears, indicating that you have signed in to the application and have accessed your profile details from the Microsoft Graph API.

    [![Screenshot of JavaScript App depicting the results of the API call.](media/common-spa/react-spa/display-api-call-results-react-spa.png)](media/common-spa/react-spa/display-api-call-results-react-spa.png#lightbox)

# [React](#tab/react-external)
1. To start the server, run the following commands from within the project directory:

    ```console
    cd 1-Authentication\1-sign-in-react\SPA
    npm install
    npm start
    ```
2. Copy the `https` URL that appears in the terminal, for example, `https://localhost:3000`, and paste it into a browser. We recommend using a private or incognito browser session.
3. Sign-in with an account registered to the external tenant.
4. The following screenshot appears, indicating that you have signed in to the application and have accessed your profile details from the Microsoft Graph API.

# [Angular](#tab/angular-external)
1. To start the server, run the following commands from within the project directory:

    ```console
    cd 1-Authentication\2-sign-in-angular\SPA
    npm install
    npm start
    ```
2. Copy the `https` URL that appears in the terminal, for example, `https://localhost:4200`, and paste it into a browser. We recommend using a private or incognito browser session.
3. Sign-in with an account registered to the external tenant.
4. The following screenshot appears, indicating that you have signed in to the application and have accessed your profile details from the Microsoft Graph API.

    [![Screenshot of JavaScript App depicting the results of the API call.](media/common-spa/angular-spa/customer-display-api-call-results-angular-spa.png)](media/common-spa/angular-spa/customer-display-api-call-results-angular-spa.png#lightbox)

---

::: zone-end

## Sign out from the application

1. Find the **Sign out** button on the page, and select it.
2. You'll be prompted to pick an account to sign out from. Select the account you used to sign in.

A message appears indicating that you have signed out. You can now close the browser window.
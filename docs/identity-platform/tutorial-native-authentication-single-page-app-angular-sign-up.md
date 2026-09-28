---
layout: Conceptual
title: Sign up users into an Angular SPA by using native authentication SDK - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-single-page-app-angular-sign-up
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to build an Angular single-page application that uses native authentication JavaScript SDK to sign up users.
manager: dougeby
ms.subservice: external
ms.topic: tutorial
ms.date: 2025-11-18T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 0b960147-7035-dfc0-b62a-ea3f7611b393
document_version_independent_id: 0b960147-7035-dfc0-b62a-ea3f7611b393
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-single-page-app-angular-sign-up.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-single-page-app-angular-sign-up
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-single-page-app-angular-sign-up.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: 51ccd9ad-d9cc-3282-e329-2e318a980bcc
---

# Sign up users into an Angular SPA by using native authentication SDK - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this tutorial, you learn how to build an Angular single-page app that signs up users by using native authentication's JavaScript SDK.

In this tutorial, you:

- Create an Angular Next.js project.
- Add MSAL JS SDK to it.
- Add UI components of the app.
- Setup the project to sign up users.

## Prerequisites

- Complete the steps in [Quickstart: Sign in users in an Angular single-page app by using native authentication JavaScript SDK](quickstart-native-authentication-single-page-app-sdk-sign-in?tabs=angular). This quickstart shows you run a sample Angular code sample.
- Complete the steps in [Set up CORS proxy server to manage CORS headers for native authentication](how-to-native-authentication-single-page-app-javascript-sdk-set-up-local-cors).
- [Visual Studio Code](https://visualstudio.microsoft.com/downloads/) or another code editor.
- [Node.js](https://nodejs.org/en/download/).
- [Angular CLI](https://angular.dev/tools/cli).
- If you want to let users sign up with a username (alias), enable the **Username** built-in user attribute in your sign-up user flow. For the steps, see [Enable username in the sign-in identifier policy](../external-id/customers/how-to-sign-in-alias#enable-username-in-sign-in-identifier-policy).

## Create a React project and install dependencies

In a location of choice in your computer, run the following commands to create a new Angular project with the name *reactspa*, navigate into the project folder, then install packages:

```console
ng new angularspa
cd angularspa
```

After you successfully run the commands, you should have an app with the following structure:

```console
angularspa/
└──node_modules/
   └──...
└──public/
   └──...
└──src/
   └──app/
      └──app.component.html
      └──app.component.scss
      └──app.component.ts
      └──app.modules.ts
      └──app.config.ts
      └──app.routes.ts
   └──index.html
   └──main.ts
   └──style.scss
└──angular.json
└──package-lock.json
└──package.json
└──README.md
└──tsconfig.app.json
└──tsconfig.json
└──tsconfig.spec.json
```

## Add JavaScript SDK to your project

To use the native authentication JavaScript SDK in your app, use your terminal to install it by using the following command:

```console
npm install @azure/msal-browser
```

The native authentication capabilities are part of the `azure-msal-browser` library. To use native authentication features, you import from `@azure/msal-browser/custom-auth`. For example:

```typescript
  import CustomAuthPublicClientApplication from "@azure/msal-browser/custom-auth";
```

## Add client configuration

In this section, you define a configuration for native authentication public client application to enable it to interact with the interface of the SDK. To do so,

1. Create a file called *src/app/config/auth-config.ts*, then add the following code:

    ```typescript
    export const customAuthConfig: CustomAuthConfiguration = {
        customAuth: {
            challengeTypes: ["password", "oob", "redirect"],
            authApiProxyUrl: "http://localhost:3001/api",
        },
        auth: {
            clientId: "Enter_the_Application_Id_Here",
            authority: "https://Enter_the_Tenant_Subdomain_Here.ciamlogin.com",
            redirectUri: "/",
            postLogoutRedirectUri: "/",
            navigateToLoginRequestUrl: false,
        },
        cache: {
            cacheLocation: "sessionStorage",
        },
        system: {
            loggerOptions: {
                loggerCallback: (level: LogLevel, message: string, containsPii: boolean) => {
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
            },
        },
    };
    ```

    In the code, find the placeholder:

    - `Enter_the_Application_Id_Here` then replace it with the Application (client) ID of the app you registered earlier.
    - `Enter_the_Tenant_Subdomain_Here` then replace it with the tenant subdomain in your Microsoft Entra admin center. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant name, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).
2. Create a file called *src/app/services/auth.service.ts*, then add the following code:

    ```typescript
    import { Injectable } from '@angular/core';
    import { CustomAuthPublicClientApplication, ICustomAuthPublicClientApplication } from '@azure/msal-browser/custom-auth';
    import { customAuthConfig } from '../config/auth-config';
    
    @Injectable({ providedIn: 'root' })
    export class AuthService {
      private authClientPromise: Promise<ICustomAuthPublicClientApplication>;
      private authClient: ICustomAuthPublicClientApplication | null = null;
    
      constructor() {
        this.authClientPromise = this.init();
      }
    
      private async init(): Promise<ICustomAuthPublicClientApplication> {
        this.authClient = await CustomAuthPublicClientApplication.create(customAuthConfig);
        return this.authClient;
      }
    
      getClient(): Promise<ICustomAuthPublicClientApplication> {
        return this.authClientPromise;
      }
    }
    ```

## Create a sign-up component

1. Create a directory called */app/components*.
2. Use Angular CLI to generate a new component for the sign-up page inside the *components* folder by running the following command:

    ```console
    cd components
    ng generate component sign-up
    ```
3. Open *sign-up/sign-up.component.ts* file, then replace its contents with the contents in [sign-up.component](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/angular-sample/src/app/components/sign-up/sign-up.component.ts)
4. Open *sign-up/sign-up.component.html* file and add the code in [html file](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/angular-sample/src/app/components/sign-up/sign-up.component.html).

    - The following logic in the *sign-up.component.ts* file determines what the user needs to do next after starting the sign-up process. Depending on the result, it shows either the password form or the verification code form in *sign-up.component.html* so the user can continue with the sign-up flow:

        ```typescript
           const attributes: UserAccountAttributes = {
                       givenName: this.firstName,
                       surname: this.lastName,
                       jobTitle: this.jobTitle,
                       city: this.city,
                       country: this.country,
                   };
           const result = await client.signUp({
                       username: this.email,
                       attributes,
                   });
        
           if (result.isPasswordRequired()) {
               this.showPassword = true;
               this.showCode = false;
           } else if (result.isCodeRequired()) {
               this.showPassword = false;
               this.showCode = true;
           }
        ```

        The SDK's instance method, `signUp()` starts the sign-up flow.
    - If you want the user to start sign-in flow immediately after sign-up is completed, use this snippet:

        ```html
        <div *ngIf="isSignedUp">
            <p>The user has been signed up, please click <a href="/sign-in">here</a> to sign in.</p>
        </div>
        ```
5. Open the *src/app/app.component.scss* file, then add the following [styles file](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/angular-sample/src/app/app.component.scss).

## Collect a username (alias) during sign-up

You can let users sign up with a username (alias) in addition to their email. The username (alias) is an alternate sign-in identifier, such as a customer ID, account number, or another value that you choose.

During sign-up, the username (email) is always required as the primary identifier, and the username (alias) doesn't replace it. By default, the username (alias) is optional, though an administrator can configure it as required. Your app always collects the username (email) and collects the alias as an attribute alongside the email. At sign-in, the user can then sign in with either their username (email) or their username (alias). To learn how the **Username** attribute is configured as optional or required, see [Configure the user input types and page layout](../external-id/customers/how-to-define-custom-attributes#configure-the-user-input-types-and-page-layout).

To collect a username (alias) during sign-up:

1. Make sure the **Username** built-in user attribute is enabled in your sign-up user flow. For the steps, see [Enable username in the sign-in identifier policy](../external-id/customers/how-to-sign-in-alias#enable-username-in-sign-in-identifier-policy).
2. Add a `flatUsername` field to the sign-up component, then include the `flatusername` attribute in the `UserAccountAttributes` you pass to `signUp()`:

    ```typescript
    flatUsername = "";
    
    const attributes: UserAccountAttributes = {
        givenName: this.firstName,
         //...
        flatusername: this.flatUsername,
    };
    ```
3. Add an alias input to *sign-up.component.html* alongside the existing fields:

    ```html
    <input type="text" [(ngModel)]="flatUsername" name="flatUsername" placeholder="Username (alias)" />
    ```
4. Handle errors related to the username (alias):

    - `result.error?.isUserAlreadyExists()` covers a duplicate email *or* a duplicate username (alias). Update the message accordingly, for example, *An account with this email or username already exists*.
    - An invalid username (alias) is surfaced through `result.error?.isAttributesValidationFailed()` rather than `result.error?.isInvalidUsername()`. Branch on this method to show a username-specific message.

## Automatically sign-in after sign-up (optional)

You can automatically sign in your users after a successful sign-up without starting a fresh sign-in flow. To do so, use the following code snippet. See a complete example at [sign-up/sign-up.component.ts](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/angular-sample/src/app/components/sign-up/sign-up.component.ts):

```typescript
    if (this.signUpState instanceof SignUpCompletedState) {
        const result = await this.signUpState.signIn();
    
        if (result.isFailed()) {
            this.error = result.error?.errorData?.errorDescription || "An error occurred during auto sign-in";
        }
    
        if (result.isCompleted()) {
            this.userData = result.data;
            this.signUpState = result.state;
            this.isSignedUp = true;
            this.showCode = false;
            this.showPassword = false;
        }
    }
```

When you autosign in a user, use the following snippet in your [sign-up/sign-up.component.html](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/angular-sample/src/app/components/sign-up/sign-up.component.html) html file.

```html
    <div *ngIf="userData && !isSignedIn">
        <p>Signed up complete, and signed in as {{ userData?.getAccount()?.username }}</p>
    </div>
    <div *ngIf="isSignedUp && !userData">
        <p>Sign up completed! Signing you in automatically...</p>
    </div>
```

## Update app routing

1. Open the *src/app/app.route.ts* file, then add the route for the sign-up component:

    ```typescript
    import { NgModule } from '@angular/core';
    import { RouterModule, Routes } from '@angular/router';
    import { SignUpComponent } from './components/sign-up/sign-up.component';
    import { AuthService } from './services/auth.service';
    import { AppComponent } from './app.component';
    
    export const routes: Routes = [
        { path: 'sign-up', component: SignUpComponent },
    ];
    
    @NgModule({
        imports: [
            RouterModule.forRoot(routes),
            SignUpComponent,
        ],
        providers: [AuthService],
        bootstrap: [AppComponent]
    })
    export class AppRoutingModule { }
    ```

## Test the sign-up flow

1. To start the CORS proxy server, run the following command in your terminal:

    ```console
    npm run cors
    ```
2. To start your application, run the following command in your terminal:

    ```console
    npm start
    ```
3. Open a web browser and navigate to `http://localhost:4200/sign-up`. A sign-up form appears.
4. To sign up for an account, input your details, select the **Continue** button, then follow the prompts.
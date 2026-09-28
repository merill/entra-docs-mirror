---
layout: Conceptual
title: Sign In Users in Angular SPA by Using Native Authentication JavaScript SDK - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-single-page-app-angular-sign-in
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to build Angular single-page app that signs in users into an external tenant by using native authentication JavaScript SDK.
manager: dougeby
ms.subservice: external
ms.topic: tutorial
ms.date: 2025-11-18T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 52130d47-348c-a6bd-337e-dfaf23bb2b40
document_version_independent_id: 52130d47-348c-a6bd-337e-dfaf23bb2b40
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-single-page-app-angular-sign-in.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-single-page-app-angular-sign-in
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-single-page-app-angular-sign-in.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/97159432-14a9-4307-a469-d2f2c75f0e33
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/50565c62-5f6b-4687-be38-323113c72c2e
platformId: f012c2d5-32c5-76bc-ace5-5223af142008
---

# Sign In Users in Angular SPA by Using Native Authentication JavaScript SDK - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this tutorial, you learn how to sign in users into an Angular single-page app (SPA) by using native authentication JavaScript SDK.

In this tutorial, you:

- Update Angular app to sign in users.
- Test the sign-in flow.

## Prerequisites

- Complete the steps in [Sign up users into Angular single-page app by using native authentication JavaScript SDK](tutorial-native-authentication-single-page-app-angular-sign-up).

## Create a sign-in component

1. Use Angular CLI to generate a new component for sign-in page inside the *components* folder by running the following command:

    ```console
    cd components
    ng generate component sign-in
    ```
2. Open the *sign-in/sign-in.component.ts* file and replace its contents with content from [sign-in.component.ts](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/angular-sample/src/app/components/sign-in/sign-in.component.ts)
3. Open the *sign-in/sign-in.component.html* file and add the contents from [sign-in.component.html](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/angular-sample/src/app/components/sign-in/sign-in.component.html).

    - The following logic in *sign-in.component.ts* determines the next step after the initial sign-in attempt. Depending on the result, it displays either the password or one-time code form in *sign-in.component.html* to guide the user through the appropriate part of the sign-in process:

        ```typescript
            const result: SignInResult = await client.signIn({ username: this.username });
        
            if (result.isPasswordRequired()) {
                this.showPassword = true;
                this.showCode = false;
            } else if (result.isCodeRequired()) {
                this.showPassword = false;
                this.showCode = true;
            } else if (result.isCompleted()) {
                this.isSignedIn = true;
                this.userData = result.data;
            }
        ```

        - The SDK's instance method, `signIn()` starts the sign-in flow.

        Note

        The `username` parameter accepts either the user's email address or their username (alias) when the **Username** built-in user attribute is enabled in your tenant's user flow. The user can input either value to sign in. To enable the attribute, see [Enable username in the sign-in identifier policy](../external-id/customers/how-to-sign-in-alias#enable-username-in-sign-in-identifier-policy).

        - In the *sign-in.component.html* file:

        ```html
        <form *ngIf="showPassword" (ngSubmit)="submitPassword()">
            <input type="password" [(ngModel)]="password" name="password" placeholder="Password" required />
            <button type="submit" [disabled]="loading">{{ loading ? 'Verifying...' : 'Submit Password' }}</button>
        </form>
        <form *ngIf="showCode" (ngSubmit)="submitCode()">
            <input type="text" [(ngModel)]="code" name="code" placeholder="OTP Code" required />
            <button type="submit" [disabled]="loading">{{ loading ? 'Verifying...' : 'Submit Code' }}</button>
        </form>
        ```

## Update the routing module

Open the *src/app/app.routes.ts* file, then add the route for the sign-in component:

```typescript
import { SignInComponent } from './components/sign-in/sign-in.component';

export const routes: Routes = [
    ...
    { path: 'sign-in', component: SignInComponent },
];
```

## Test the sign-in functionality

1. To start the CORS proxy server, run the following command in your terminal:

    ```console
    npm run cors
    ```
2. To start the Angular app, open another terminal window, then run the following command:

    ```console
    npm start
    ```
3. Open a web browser and navigate to `http://localhost:4200/sign-in`. A sign-in form appears.
4. To sign in into an existing account, input your details, select the Sign In button, then follow the prompts.
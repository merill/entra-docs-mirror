---
layout: Conceptual
title: Reset Password in Angular SPA App by Using Native Authentication JavaScript SDK - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-single-page-app-angular-reset-password
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to build an Angular single-page app that enables users to reset their passwords by using native authentication JavaScript SDK.
manager: dougeby
ms.subservice: external
ms.topic: tutorial
ms.date: 2025-11-18T00:00:00.0000000Z
locale: en-us
document_id: e4374511-7e3a-2cc5-f28c-c1b8b29b370f
document_version_independent_id: e4374511-7e3a-2cc5-f28c-c1b8b29b370f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-single-page-app-angular-reset-password.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-single-page-app-angular-reset-password
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-single-page-app-angular-reset-password.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/97159432-14a9-4307-a469-d2f2c75f0e33
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/50565c62-5f6b-4687-be38-323113c72c2e
platformId: 5e1624a0-8a97-ab3a-5838-06332b69ce09
---

# Reset Password in Angular SPA App by Using Native Authentication JavaScript SDK - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this tutorial, you learn how to enable password reset in Angular single-page app by using native authentication JavaScript SDK. Password reset is available for user accounts that use email with password authentication flow.

In this tutorial, you:

- Update the Angular app to reset user's password.
- Test password reset flow

## Prerequisites

- Complete the steps in [Tutorial: Sign up users into Angular single-page app by using native authentication JavaScript SDK](tutorial-native-authentication-single-page-app-angular-sign-up).
- [Enable self-service password reset (SSPR)](../external-id/customers/how-to-enable-password-reset-customers) for customer users in the external tenant. SSPR is available for customer users for apps that use email with password authentication flow.

## Create the password reset component

1. Use Angular CLI to generate a new component for password reset inside the components folder by running the following command:

    ```console
    cd components
    ng generate component reset-password
    ```
2. Open the *reset-password/reset-password.component.ts* file and replace its contents with the contents from [reset-password.component.ts](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/angular-sample/src/app/components/reset-password/reset-password.component.ts)
3. Open the *reset-password/reset-password.component.html* file and add the contents from [reset-password.component.html](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/angular-sample/src/app/components/reset-password/reset-password.component.html).

    - The following logic in *reset-password.component.ts* determines the next step after the initial reset password operation. Depending on the result, it displays the code entry form in *reset-password.component.html* to continue the password reset process:

        ```typescript
        const result = await client.resetPassword({ username: this.email });
        if (result.isCodeRequired()) {
                    this.showCode = true;
                    this.isReset = false;
                    this.showNewPassword = false;
                }
        ```

        - The SDK's instance method, resetPassword() starts the password reset flow.
        - In the *reset-password.component.html* file:

        ```html
        <form *ngIf="showCode" (ngSubmit)="submitCode()">
            <input type="text" [(ngModel)]="code" name="code" placeholder="OTP Code" required />
            <button type="button" (click)="submitCode()" [disabled]="loading">{{ loading ? 'Verifying...' : 'Verify Code' }}</button>
            </form>
        ```
    - After `submitCode()` is successfully invoked, the result determines the next step: if password is required, the new password form is displayed for the user to continue the password reset process.

        ```typescript
        if (result.isPasswordRequired()) {
            this.showCode = false;
            this.showNewPassword = true;
            this.isReset = false;
            this.resetState = result.state;
        }
        ```

        In the *reset-password.component.html* file:

    ```html
      <form *ngIf="showNewPassword" (ngSubmit)="submitNewPassword()">
        <input type="password" [(ngModel)]="newPassword" name="newPassword" placeholder="New Password" required />
        <button type="button" (click)="submitNewPassword()" [disabled]="loading">{{ loading ? 'Submitting...' : 'Submit New Password' }}</button>
      </form>
    ```

    - If you want the user to start sign-in flow immediately after reset password is completed, use this snippet:

        ```html
        <div *ngIf="isReset">
            <p>The password has been reset, please click <a href="/sign-in">here</a> to sign in.</p>
        </div>
        ```

### Automatically sign-in after reset password (optional)

You can automatically sign in your users after a successful password reset without starting a fresh sign-in flow. To do so, use the following code snippet. See a complete example at [reset-password.component.ts](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/angular-sample/src/app/components/reset-password/reset-password.component.ts):

```typescript
if (this.resetState instanceof ResetPasswordCompletedState) {
    const result = await this.resetState.signIn();
    
    if (result.isFailed()) {
        this.error = result.error?.errorData?.errorDescription || "An error occurred during auto sign-in";
    }
    
    if (result.isCompleted()) {
        this.userData = result.data;
        this.resetState = result.state;
        this.isReset = true;
        this.showCode = false;
        this.showNewPassword = false;
    }
}
```

When you autosign in a user, use the following snippet in your [reset-password.component.html](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/angular-sample/src/app/components/reset-password/reset-password.component.html):

```html
<div *ngIf="userData && !isSignedIn">
    <p>Password reset completed, and signed in as {{ userData?.getAccount()?.username }}</p>
</div>
<div *ngIf="isReset && !userData">
    <p>Password reset completed! Signing you in automatically...</p>
</div>
```

## Update the routing module

Open the *src/app/app.routes.ts* file, then add the route for the password reset component:

```typescript
import { ResetPasswordComponent } from './reset-password/reset-password.component';

const routes: Routes = [
    { path: 'reset-password', component: ResetPasswordComponent },
    ...
];
```

## Test the password reset functionality

1. To start the CORS proxy server, run the following command in your terminal:

    ```console
    npm run cors
    ```
2. To start your application, run the following command in your terminal:

    ```console
    npm start
    ```
3. Open a web browser and navigate to `http://localhost:4200/reset-password`. A sign-up form appears.
4. To reset password for an existing user account, input your details, select the **Continue** button, then follow the prompts.

## Set up `poweredByHeader: false` in next.config.js

- In Next.js, the x-powered-by header is included by default in HTTP responses to indicate that the application is powered by Next.js. However, for security or customization reasons, you might want to remove or modify this header.

    ```typescript
    const nextConfig: NextConfig = {
      poweredByHeader: false,
      /* other config options here */
    };
    ```
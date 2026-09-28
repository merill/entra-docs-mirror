---
layout: Conceptual
title: Support Social Sign-in in an Angular SPA With Native Auth JS SDK - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-single-page-app-angular-social-sign-in
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to add social sign-in with Apple, Facebook, Google and custom OIDC identity providers to your Angular SPA using native authentication JavaScript SDK.
manager: dougeby
ms.subservice: external
ms.topic: tutorial
ms.date: 2026-04-10T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-108
ai-usage: ai-assisted
locale: en-us
document_id: fe771b4d-24bb-518d-789e-e7f3af771ac7
document_version_independent_id: fe771b4d-24bb-518d-789e-e7f3af771ac7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-single-page-app-angular-social-sign-in.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-single-page-app-angular-social-sign-in
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-single-page-app-angular-social-sign-in.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/97159432-14a9-4307-a469-d2f2c75f0e33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/50565c62-5f6b-4687-be38-323113c72c2e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 4d015344-d959-4dd9-5e30-babf1c7073ef
---

# Support Social Sign-in in an Angular SPA With Native Auth JS SDK - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this tutorial, you learn how to let users sign up and sign in with their existing social accounts, such as Apple, Facebook, Google and custom OIDC social identity providers in your Angular single-page application (SPA) by using native authentication's JavaScript SDK for external tenants.

In this tutorial, you:

- Update the app configuration to set a redirect URI.
- Add federated identity provider buttons to sign-in and sign-up forms.
- Handle sign-in and sign-up with federated identity providers.
- Test the social sign-in flow.

## Prerequisites

- Complete the steps in [sign up](tutorial-native-authentication-single-page-app-angular-sign-up), [sign in](tutorial-native-authentication-single-page-app-angular-sign-in), [password reset](tutorial-native-authentication-single-page-app-angular-reset-password), [register strong authentication method](tutorial-native-authentication-single-page-app-angular-register-strong-method) and [Enable MFA](tutorial-native-authentication-single-page-app-angular-enable-mfa) tutorials.
- [Visual Studio Code](https://visualstudio.microsoft.com/downloads/) or another code editor.
- [Node.js 20.x or later](https://nodejs.org/en/download/).
- Configure the federated identity providers you want to enable. Follow the steps in [Identity providers for external tenants](../external-id/customers/concept-authentication-methods-customers)for your chosen providers:
    - [Apple](../external-id/customers/how-to-apple-federation-customers)
    - [Facebook](../external-id/customers/how-to-facebook-federation-customers)
    - [Google](../external-id/customers/how-to-google-federation-customers)
    - [Custom OIDC identity providers](../external-id/customers/how-to-custom-oidc-federation-customers)

## Update the configuration to set the redirect URI

Make sure that the redirect URI is configured in the `CustomAuthConfiguration` interface and that its value matches one of the redirect URIs [configured in your app registration](how-to-add-redirect-uri) in the Microsoft Entra admin center:

1. Locate the *src/app/config/auth-config.ts* file.
2. In the `auth` object, add or update `redirectUri` property, then make sure that its value matches one of the redirect URIs configured in your app registration in the Microsoft Entra admin center:

    ```typescript
    const customAuthConfig: CustomAuthConfiguration = {
        auth: {
            ...
            redirectUri: "/",
            ...
        },
        ...
    };
    ```

## Create UI components

In this section, you add federated identity provider buttons to your sign-in and sign-up forms, allowing users to authenticate with social identity providers (Apple, Facebook and Google) or custom OIDC identity providers (such as LinkedIn).

### Update the sign-in form

Update your `sign-in.component.html` to include federated identity provider buttons. You can find the complete example in [sign-in.component.html](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/angular-sample/src/app/components/sign-in/sign-in.component.html):

- Open `src/app/components/sign-in/sign-in.component.html` and add the social provider buttons to the initial form:

    ```html
    <div class="auth-container">
        ...
        <form
            *ngIf="!showPassword && !showCode && !isSignedIn && !showAuthMethodsForRegistration && !showChallengeForRegistration && !showMfaAuthMethods && !showMfaChallenge"
            (ngSubmit)="startSignIn()">
            ...
    
            <div class="separator">
                <div class="separator-line"></div>
                <span class="separator-text">OR</span>
                <div class="separator-line"></div>
            </div>
    
            <button *ngFor="let provider of socialProviders" type="button" class="social-button"
                (click)="startSignInWithSocial(provider.domainHint)">
                <img [src]="provider.logo" [alt]="provider.name + ' logo'" class="provider-logo" />
                <span>Sign In with {{ provider.name }}</span>
            </button>
        </form>
        ...
    </div>
    ```

### Update the sign-up form

Similarly, update your `sign-up.component.html` component. You can find the complete example in [sign-up.component.html](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/angular-sample/src/app/components/sign-up/sign-up.component.html):

- Open `src/app/components/sign-up/sign-up.component.html` and add the social provider buttons after the regular sign-up button. Use the same HTML block from the sign-in form to include the social provider buttons.

## Handle form interaction

In this section, you implement the logic to handle sign-in and sign-up with federated identity providers. The implementation uses the `loginPopup` method from MSAL with a `PopupRequest` that includes the `domainHint` property. This property specifies which federated identity provider to use. For more information about `domainHint` configuration and issuer acceleration, see [Identity providers for External ID](../external-id/customers/concept-authentication-methods-customers).

### Update sign-up component to support federated identity providers

Update your `sign-up.component.ts` to handle authentication with federated identity providers. You can find the complete example in [sign-up.component.ts](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/angular-sample/src/app/components/sign-up/sign-up.component.ts).

1. Import the necessary types in `sign-up.component.ts`:

    ```typescript
    import { customAuthConfig } from "../../config/auth-config";
    import { PopupRequest } from "@azure/msal-browser";
    ```
2. Add the identity provider list in `sign-up.component.ts`:

    ```typescript
    socialProviders = [
        { name: "Google", domainHint: "Google", logo: "/logos/google.svg" },
        { name: "Facebook", domainHint: "Facebook", logo: "/logos/facebook.svg" },
        { name: "Apple", domainHint: "Apple", logo: "/logos/apple.svg" },
        { name: "LinkedIn", domainHint: "www.linkedin.com", logo: "/logos/linkedin.svg" },
    ];
    ```
3. Add the handler function for federated identity provider sign-up in `sign-up.component.ts`:

    ```typescript
    async startSignUpWithSocial(domainHint: string) {
        this.error = "";
        this.loading = false;
    
        const popUpRequest: PopupRequest = {
            authority: customAuthConfig.auth.authority,
            scopes: [],
            redirectUri: customAuthConfig.auth.redirectUri || "",
            prompt: "login",
            domainHint: domainHint,
        };
    
        try {
            const client = await this.auth.getClient();
    
            await client.loginPopup(popUpRequest);
    
            const accountResult = client.getCurrentAccount();
    
            if (accountResult.isFailed()) {
                this.error =
                    accountResult.error?.errorData?.errorDescription ??
                    "An error occurred while getting the account from cache";
            }
    
            if (accountResult.isCompleted()) {
                this.userData = accountResult.data;
                this.isSignedIn = true;
            }
        } catch (error) {
            if (error instanceof Error) {
                this.error = error.message;
            } else {
                this.error = "An unexpected error occurred while logging in with popup";
            }
        }
    }
    ```

### Update sign-in component to support federated identity providers

Update your `sign-in.component.ts` to handle authentication with federated identity providers. You can find the complete example in [sign-in.component.ts](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/angular-sample/src/app/components/sign-in/sign-in.component.ts).

1. Add the identity provider list in `sign-in.component.ts`:

    ```typescript
    socialProviders = [
        { name: "Google", domainHint: "Google", logo: "/logos/google.svg" },
        { name: "Facebook", domainHint: "Facebook", logo: "/logos/facebook.svg" },
        { name: "Apple", domainHint: "Apple", logo: "/logos/apple.svg" },
        { name: "LinkedIn", domainHint: "www.linkedin.com", logo: "/logos/linkedin.svg" },
    ];
    ```
2. Add the handler function for federated identity provider sign-in in `sign-in.component.ts`:

    ```typescript
    async startSignInWithSocial(domainHint: string) {
        this.error = "";
        this.loading = false;
    
        const popUpRequest: PopupRequest = {
            authority: customAuthConfig.auth.authority,
            scopes: [],
            redirectUri: customAuthConfig.auth.redirectUri || "",
            prompt: "login",
            domainHint: domainHint,
        };
    
        try {
            const client = await this.auth.getClient();
    
            await client.loginPopup(popUpRequest);
    
            const accountResult = client.getCurrentAccount();
    
            if (accountResult.isFailed()) {
                this.error =
                    accountResult.error?.errorData?.errorDescription ??
                    "An error occurred while getting the account from cache";
            }
    
            if (accountResult.isCompleted()) {
                this.userData = accountResult.data;
                this.isSignedIn = true;
            }
        } catch (error) {
            if (error instanceof Error) {
                this.error = error.message;
            } else {
                this.error = "An unexpected error occurred while logging in with popup";
            }
        }
    }
    ```

Note

Microsoft Entra accounts and Microsoft accounts (MSA) identity providers aren't currently supported.

### PopupRequest configuration details

When you configure the `PopupRequest` for federated identity provider authentication:

- **authority**: Use your configured external tenant authority.
- **redirectUri**: The redirect URI you configured in your app registration.
- **prompt**: Set to `"login"` to force the user to enter credentials.
- **domainHint**: The key parameter that determines which federated identity provider to use.

The `loginPopup` method opens a popup window where the user completes the authentication flow with the selected federated identity provider. After authentication succeeds, the popup closes automatically, and the account information is available in your app.

## Run and test your app

Before you test your app, make sure your CORS proxy and app are running:

1. Make sure your CORS proxy is running:

    ```console
    npm run cors
    ```
2. Start your application:

    ```console
    npm run start
    ```

### Test sign-up with federated identity providers

1. Navigate to `http://localhost:4200/sign-up` to see the sign-up form.
2. Select the button for the federated identity provider that you want to authenticate with, such as **Sign Up with Google**. A popup window opens, redirecting you to the Google authentication page.
3. Sign in with your Google account credentials (or create a new Google account if needed).
4. Grant the necessary permissions when prompted.

After successful authentication, you might be required to complete attribute collection if your tenant is configured to collect additional user attributes during sign-up. For more information, see [Collect user attributes during sign-up](../external-id/customers/concept-user-attributes).

The popup window closes automatically. You should be signed in and see your account information displayed in the app. A new user account is created in your external tenant using the information from your Google profile.

### Test sign-in with federated identity providers

1. Navigate to `http://localhost:4200/sign-in` to see the sign-in form.
2. Select the button for the federated identity provider that you want to authenticate with, such as **Sign In with Google**. A popup window opens, redirecting you to the Google authentication page.
3. Sign in with your Google account credentials. If this is your first time signing in with this identity provider, you might be prompted to consent to sharing your information with the application.

After successful authentication, you might be required to complete attribute collection if your tenant is configured to collect additional user attributes during sign-up. For more information, see [Collect user attributes during sign-up](../external-id/customers/concept-user-attributes).

The popup window closes automatically. You should now be signed in and see your account information displayed in the app.

### Multifactor authentication

When SMS or email one-time passcode (OTP) MFA is enabled, the MFA challenge is presented in the browser-delegated user experience after the social identity provider authentication completes.

For more information about enabling MFA, refer to [Multifactor authentication in external tenants](../external-id/customers/concept-multifactor-authentication-customers) and [Add multifactor authentication to an app](../external-id/customers/how-to-multifactor-authentication-customers).

## Troubleshoot common errors

Use this section to resolve common issues you might encounter when integrating federated identity providers.

### Popup window is blocked by the browser

The `loginPopup` method requires browser popups. If the popup is blocked, the authentication flow fails silently or throws an error.

**Solution**: Check your browser's popup blocker settings and allow popups from your application's domain. Instruct your users to do the same. Most browsers display a notification in the address bar when a popup is blocked.

### Domain hint not recognized

The federated identity provider authentication page doesn't appear, or you receive an error indicating the `domainHint` value is invalid.

**Solution**: Verify that the `domainHint` value in your `PopupRequest` matches exactly what you configured in your external tenant. Use the following values:

| Provider | Expected`domainHint`value |
| --- | --- |
| Apple | `"Apple"` |
| Facebook | `"Facebook"` |
| Google | `"Google"` |
| Custom OIDC (for example, LinkedIn) | The issuer URI you configured, such as `"www.linkedin.com"` |

### Authentication fails after the popup opens

The popup opens and redirects to the identity provider, but the authentication doesn't complete. Check the browser console for error messages.

**Solution**: Verify the following configurations:

1. The `redirectUri` in your `PopupRequest` matches one of the redirect URIs registered in your app registration in the Microsoft Entra admin center.
2. The client ID in your app configuration is correct.
3. The federated identity provider is properly configured in your external tenant and added to the relevant user flow.

### User account isn't created after sign-up

The user completes federated identity provider authentication, but a new account isn't created in the tenant.

**Solution**: Confirm that the federated identity provider is configured and enabled in the user flows for both sign-up and sign-in scenarios in your external tenant. When a user signs in with a federated identity provider for the first time, a new account is automatically created and linked to that provider. Subsequent sign-ins with the same provider use the existing account.

### CORS-related errors appear in the console

You see `Access-Control-Allow-Origin` or similar CORS errors in the browser console.

**Solution**: Make sure your CORS proxy is running correctly. Restart the proxy with `npm run cors` and verify it's accessible before retrying.
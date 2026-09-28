---
layout: Conceptual
title: Support Social Sign-in in a React SPA With Native Auth JS SDK - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-single-page-app-react-social-sign-in
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to add social sign-in with Apple, Facebook, Google and custom OIDC identity providers to your React SPA using native authentication JavaScript SDK.
manager: dougeby
ms.subservice: external
ms.topic: tutorial
ms.date: 2026-04-10T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 0869505f-4da2-e528-df08-428b578866dd
document_version_independent_id: 0869505f-4da2-e528-df08-428b578866dd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-single-page-app-react-social-sign-in.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-single-page-app-react-social-sign-in
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-single-page-app-react-social-sign-in.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/97159432-14a9-4307-a469-d2f2c75f0e33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/50565c62-5f6b-4687-be38-323113c72c2e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: 6711fb35-c29b-b0eb-ddd5-c7cd37252e10
---

# Support Social Sign-in in a React SPA With Native Auth JS SDK - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this tutorial, you learn how to let users sign up and sign in with their existing social accounts, such as Apple, Facebook, Google and custom OIDC social identity providers in your React single-page application (SPA) by using native authentication's JavaScript SDK for external tenants.

In this tutorial, you:

- Update the app configuration to set a redirect URI.
- Add federated identity provider buttons to sign-in and sign-up forms.
- Handle sign-in and sign-up with federated identity providers.
- Test the social sign-in flow.

## Prerequisites

- Complete the steps in [sign up](tutorial-native-authentication-single-page-app-react-sign-up), [sign in](tutorial-native-authentication-single-page-app-react-sign-in), [password reset](tutorial-native-authentication-single-page-app-react-reset-password), [register strong authentication method](tutorial-native-authentication-single-page-app-react-register-strong-method), and [enable MFA](tutorial-native-authentication-single-page-app-react-enable-mfa) tutorials.
- [Visual Studio Code](https://visualstudio.microsoft.com/downloads/) or another code editor.
- [Node.js 20.x or later](https://nodejs.org/en/download/).
- Configure the federated identity providers you want to enable. Follow the steps in [Identity providers for external tenants](../external-id/customers/concept-authentication-methods-customers)for your chosen providers:
    - [Apple](../external-id/customers/how-to-apple-federation-customers)
    - [Facebook](../external-id/customers/how-to-facebook-federation-customers)
    - [Google](../external-id/customers/how-to-google-federation-customers)
    - [Custom OIDC identity providers](../external-id/customers/how-to-custom-oidc-federation-customers)

## Update the configuration to set the redirect URI

Make sure that the redirect URI is configured in the `CustomAuthConfiguration` interface and that its value matches one of the redirect URIs [configured in your app registration](how-to-add-redirect-uri) in the Microsoft Entra admin center:

1. Locate the *src/config/auth-config.ts* file.
2. In the `auth` object, add or update the `redirectUri` property, then make sure that its value matches one of the redirect URIs configured in your app registration in the Microsoft Entra admin center:

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

### Update the sign-in initial form

Update your sign-in `InitialForm.tsx` component to include federated identity provider buttons. You can find the complete example in [InitialForm.tsx](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/sign-in/components/InitialForm.tsx).

1. Open `src/app/sign-in/components/InitialForm.tsx` and update the component to include the social provider buttons:

    ```typescript
    import type { SignInInitialFormProps } from "../types/formProperties";
    
    const socialProviders = [
        {
            name: "Google",
            domainHint: "Google",
        },
        {
            name: "Facebook",
            domainHint: "Facebook",
        },
        {
            name: "Apple",
            domainHint: "Apple",
        },
        {
            name: "LinkedIn",
            domainHint: "www.linkedin.com",
        },
    ];
    
    export const InitialForm = ({
        onSubmit,
        username,
        setUsername,
        loading,
        onSignInWithSocial,
    }: SignInInitialFormProps) => (
        <form onSubmit={onSubmit} style={styles.form}>
            ...
    
            <div style={styles.separator}>
                <div style={styles.separatorLine}></div>
                <span style={styles.separatorText}>OR</span>
                <div style={styles.separatorLine}></div>
            </div>
    
            {socialProviders.map((provider) => (
                <button
                    key={provider.domainHint}
                    type="button"
                    style={styles.socialButton}
                    onClick={() => onSignInWithSocial(provider.domainHint)}
                >
                    <span>Sign In with {provider.name}</span>
                </button>
            ))}
        </form>
    );
    ```
2. Update the `SignInInitialFormProps` interface in `src/app/sign-in/types/formProperties.ts`:

    ```typescript
    import { FormProps } from "@/app/shared/types/formProperties";
    
    export interface SignInInitialFormProps extends FormProps {
        ...
        onSignInWithSocial: (domainHint: string) => Promise<void>;
    }
    ```

### Update the sign-up initial form

Similarly, update your sign-up `InitialForm.tsx` component. You can find the complete example in [InitialForm.tsx](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/sign-up/components/InitialForm.tsx).

1. Open `src/app/sign-up/components/InitialForm.tsx` and add the social providers array and buttons. Use the same structure from the sign-in `InitialForm.tsx`, but update the click handler to call `onSignUpWithSocial` and update the button text to say "Sign Up with."
2. Update the `SignUpInitialFormProps` interface in `src/app/sign-up/types/formProperties.ts`:

    ```typescript
    import { FormProps } from "@/app/shared/types/formProperties";
    
    export interface SignUpInitialFormProps extends FormProps {
        ...
        onSignUpWithSocial: (domainHint: string) => Promise<void>;
    }
    ```

## Handle form interaction

In this section, you implement the logic to handle sign-in and sign-up with federated identity providers. The implementation uses the `loginPopup` method from MSAL with a `PopupRequest` that includes the `domainHint` property. This property specifies which federated identity provider to use. For more information about `domainHint` configuration and issuer acceleration, see [Identity providers for External ID](../external-id/customers/concept-authentication-methods-customers).

### Update sign-up page to support federated identity providers

Update your sign-up `page.tsx` to handle authentication with federated identity providers. You can find the complete example in [page.tsx](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/sign-up/page.tsx).

1. Import the necessary types:

    ```typescript
    import { PopupRequest } from "@azure/msal-browser";
    ```
2. Add the handler function for federated identity provider sign-up in your sign-up `page.tsx`:

    ```typescript
    const startSignUpWithSocial = async (domainHint: string) => {
        setError("");
        setLoading(false);
    
        if (!authClient) return;
    
        const popUpRequest: PopupRequest = {
            authority: customAuthConfig.auth.authority,
            scopes: [],
            redirectUri: customAuthConfig.auth.redirectUri || "",
            prompt: "login",
            domainHint: domainHint,
        };
    
        try {
            await authClient.loginPopup(popUpRequest);
    
            const accountResult = authClient.getCurrentAccount();
    
            if (accountResult.isFailed()) {
                setError(
                    accountResult.error?.errorData?.errorDescription ??
                        "An error occurred while getting the account from cache"
                );
            }
    
            if (accountResult.isCompleted()) {
                setData(accountResult.data);
                setSignInState(true);
            }
        } catch (error) {
            if (error instanceof Error) {
                setError(error.message);
            } else {
                setError("An unexpected error occurred while logging in with popup");
            }
        }
    };
    ```
3. Update the `renderForm()` function to pass the handler to the `InitialForm` component:

    ```typescript
    const renderForm = () => {
    
        ... other state checks ...
    
        if (!signUpState) {
            return (
                <InitialForm
                    ...
                    onSignUpWithSocial={startSignUpWithSocial}
                />
            );
        }
    };
    ```

### Update sign-in page to support federated identity providers

Update your sign-in `page.tsx` to handle authentication with federated identity providers. You can find the complete example in [page.tsx](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/sign-in/page.tsx).

1. Import the necessary types:

    ```typescript
    import { PopupRequest } from "@azure/msal-browser";
    ```
2. Add the handler function for federated identity provider sign-in in your sign-in `page.tsx`:

    ```typescript
    const startSignInWithSocial = async (domainHint: string) => {
        setError("");
        setLoading(false);
    
        if (!authClient) return;
    
        const popUpRequest: PopupRequest = {
            authority: customAuthConfig.auth.authority,
            scopes: [],
            redirectUri: customAuthConfig.auth.redirectUri || "",
            prompt: "login",
            domainHint: domainHint,
        };
    
        try {
            await authClient.loginPopup(popUpRequest);
    
            const accountResult = authClient.getCurrentAccount();
    
            if (accountResult.isFailed()) {
                setError(
                    accountResult.error?.errorData?.errorDescription ??
                        "An error occurred while getting the account from cache"
                );
            }
    
            if (accountResult.isCompleted()) {
                setData(accountResult.data);
                setCurrentSignInStatus(true);
            }
        } catch (error) {
            if (error instanceof Error) {
                setError(error.message);
            } else {
                setError("An unexpected error occurred while logging in with popup");
            }
        }
    };
    ```
3. Update the `renderForm()` function to pass the handler to the `InitialForm` component:

    ```typescript
    const renderForm = () => {
    
        ... other state checks ...
    
        return (
            <InitialForm
                ...
                onSignInWithSocial={startSignInWithSocial}
            />
        );
    };
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
    npm run dev
    ```

### Test sign-up with federated identity providers

1. Navigate to `http://localhost:3000/sign-up` to see the sign-up form.
2. Select the button for the federated identity provider that you want to authenticate with, such as **Sign Up with Google**. A popup window opens, redirecting you to the Google authentication page.
3. Sign in with your Google account credentials (or create a new Google account if needed).
4. Grant the necessary permissions when prompted.

After successful authentication, you might be required to complete attribute collection if your tenant is configured to collect additional user attributes during sign-up. For more information, see [Collect user attributes during sign-up](../external-id/customers/concept-user-attributes).

The popup window closes automatically. You should be signed in and see your account information displayed in the app. A new user account is created in your external tenant using the information from your Google profile.

### Test sign-in with federated identity providers

1. Navigate to `http://localhost:3000/sign-in` to see the sign-in form.
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

**Solution**: Check your browser's popup blocker settings and allow popups from your application's domain (for example, `localhost:3000`). Instruct your users to do the same. Most browsers display a notification in the address bar when a popup is blocked.

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
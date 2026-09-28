---
layout: Conceptual
title: Register Strong Auth Method in a React SPA by Using Native Authentication JavaScript SDK - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-single-page-app-react-register-strong-method
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to register a strong auth method in a React single-page application that uses native authentication JavaScript SDK
manager: dougeby
ms.subservice: external
ms.topic: tutorial
ms.date: 2026-01-18T00:00:00.0000000Z
locale: en-us
document_id: d877f5a1-df7c-a8e7-b707-891cb01c1fa3
document_version_independent_id: d877f5a1-df7c-a8e7-b707-891cb01c1fa3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-single-page-app-react-register-strong-method.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-single-page-app-react-register-strong-method
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-single-page-app-react-register-strong-method.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/97159432-14a9-4307-a469-d2f2c75f0e33
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/50565c62-5f6b-4687-be38-323113c72c2e
platformId: 3cacebea-44a7-328c-e3a2-6ada625bae49
---

# Register Strong Auth Method in a React SPA by Using Native Authentication JavaScript SDK - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this tutorial, you register a strong authentication method for a user in your React single-page application (SPA) by using native authentication's JavaScript SDK.

If you enable multifactor authentication (MFA), but the user has no registered strong authentication method, you need to have the user register one before tokens can be issued.

The strong authentication method registration flow occurs in three scenarios:

- **During sign-in**: The user signs in but does not have a strong authentication method registered.
- **After sign-up**: The user successfully signs up and automatically proceeds to sign in.
- **After self-service password reset (SSPR)**: The user successfully resets their password and automatically proceeds to sign in.

When strong authentication method registration is required, the user selects a method of choice from a list of supported methods. The available methods are **email** and **SMS** one-time passcode.

The flow diagram below illustrates the three scenarios:

![Register strong authentication method.](media/native-authentication-single-page-app-react-register-authentication-method/register-strong-authentication-method.png)

## Prerequisites

- Complete the steps in [sign up](tutorial-native-authentication-single-page-app-react-sdk-sign-up), [sign in](tutorial-native-authentication-single-page-app-react-sdk-sign-in) and [password reset](tutorial-native-authentication-single-page-app-react-sdk-reset-password) tutorials.
- [Visual Studio Code](https://visualstudio.microsoft.com/downloads/) or another code editor.
- [Node.js 20.x or later](https://nodejs.org/en/download/).
- [Enable multifactor authentication (MFA) for your app](../external-id/customers/how-to-multifactor-authentication-customers).

## Enable app to handle strong authentication method registration

To enable the strong authentication method registration in your React app, update the app configuration by adding the required capability.

1. Locate the *src/config/auth-config.ts* file.
2. In the `customAuth` object, add or update the `capabilities` property to include the `registration_required` value in the array as shown in the following code snippet:

    ```typescript
    const customAuthConfig: CustomAuthConfiguration = {
        customAuth: {
            ...
            capabilities: ["registration_required"],
            ...
        },
        ...
    };
    ```

The capability value `registration_required` informs Microsoft Entra that your app can handle strong authentication method registration flow. Learn more about [native authentication challenge types and capabilities](concept-native-authentication-challenge-types).

## Create UI components

You require form components to handle strong authentication method registration. Use the following steps to add these components to your app:

1. Create a new folder named *src/app/shared/components* to store reusable components.
2. In the new folder, create a file named `AuthMethodRegistrationForm.tsx` to display a form that allows users to select and register a strong authentication method. Add the code in [AuthMethodRegistrationForm](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/shared/components/AuthMethodRegistrationForm.tsx) into the file.
3. In the new folder, create another file named `AuthMethodRegistrationChallengeForm.tsx` to display a form for verifying the strong authentication method by using the one-time passcode that the user receives. Add the code in [AuthMethodRegistrationChallengeForm](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/shared/components/AuthMethodRegistrationChallengeForm.tsx) into the file.

When needed, you can import and use reusable components in your sign-in, sign-in after sign-up, and sign-in after SSPR flows.

## Register strong authentication method during sign-in

Update the *src/app/sign-in/page.tsx* file to enable your app to handle strong authentication method registration flow during sign-in. See the complete code in [page.tsx](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/sign-in/page.tsx):

1. Import the required types and components as shown in the following code snippet:

    ```typescript
    import {
        CustomAuthPublicClientApplication,
        ICustomAuthPublicClientApplication,
        SignInCodeRequiredState,
        SignInCompletedState,
        AuthFlowStateBase,
        SignInAuthMethodRegistrationRequiredState,
        SignInAuthMethodRegistrationChallengeRequiredState,
    } from "@azure/msal-browser/custom-auth";
    import { AuthMethodRegistrationForm } from "../components/shared/AuthMethodRegistrationForm";
    import { AuthMethodRegistrationChallengeForm } from "../components/shared/AuthMethodRegistrationChallengeForm";
    ...
    ```
2. Add new state variables for strong authentication method registration:

    ```typescript
    export default function SignIn() {
        ...
        // Authentication method registration states
        const [authMethodsForRegistration, setAuthMethodsForRegistration] = useState<AuthenticationMethod[]>([]);
        const [selectedAuthMethodForRegistration, setSelectedAuthMethodForRegistration] = useState<AuthenticationMethod | undefined>(undefined);
        const [verificationContactForRegistration, setVerificationContactForRegistration] = useState("");
        const [challengeForRegistration, setChallengeForRegistration] = useState("");
    
        // ... initialization code
    }
    ```
3. Update the `startSignIn`, `handlePasswordSubmit` and `handleCodeSubmit` functions to check if strong authentication method registration is required:

    ```typescript
    const startSignIn = async (e: React.FormEvent) => {
        // Start the sign-in flow
        const result = await authClient.signIn({
            username,
        });
    
        ...
    
        // Check for auth method registration requirement
        if (result.isAuthMethodRegistrationRequired()) {
            setAuthMethodsForRegistration(result.state.getAuthMethods());
            // Set default selection to the first auth method
            const methods = result.state.getAuthMethods();
            setSelectedAuthMethodForRegistration(methods.length > 0 ? methods[0] : undefined);
        }
    
        ...
    };
    
    const handlePasswordSubmit = async (e: React.FormEvent) => {
        if (signInState instanceof SignInPasswordRequiredState) {
            const result = await signInState.submitPassword(password);
    
            ...
    
            // Check for auth method registration requirement
            if (result.isAuthMethodRegistrationRequired()) {
                const methods = result.state.getAuthMethods();
                setAuthMethodsForRegistration(methods);
                setSelectedAuthMethodForRegistration(methods.length > 0 ? methods[0] : undefined);
                setSignInState(result.state);
            }
    
            ...
        }
    };
    
    const handleCodeSubmit = async (e: React.FormEvent) => {
        if (signInState instanceof SignInCodeRequiredState) {
            const result = await signInState.submitCode(code);
    
            ...
    
            // Check for auth method registration requirement
            if (result.isAuthMethodRegistrationRequired()) {
                const methods = result.state.getAuthMethods();
                setAuthMethodsForRegistration(methods);
                setSelectedAuthMethodForRegistration(methods.length > 0 ? methods[0] : undefined);
                setSignInState(result.state);
            }
    
            ...
        }
    };
    ```

    In each of the functions, notice that we check if strong authentication method registration is required by using the following code snippet:

    ```typescript
    if (result.isAuthMethodRegistrationRequired()) {...}
    ```
4. Add the handler for strong authentication method selection:

    ```typescript
    const handleAuthMethodRegistrationSubmit = async (e: React.FormEvent) => {
        e.preventDefault();
        setError("");
        setLoading(true);
    
        if (!selectedAuthMethodForRegistration || !verificationContactForRegistration) {
            setError("Please select an authentication method and enter a verification contact.");
            setLoading(false);
            return;
        }
    
        if (signInState instanceof AuthMethodRegistrationRequiredState) {
            const result = await signInState.challengeAuthMethod({
                authMethodType: selectedAuthMethodForRegistration,
                verificationContact: verificationContactForRegistration,
            });
    
            if (result.isFailed()) {
                if (result.error?.isInvalidInput()) {
                    setError("Incorrect verification contact.");
                } else if (result.error?.isVerificationContactBlocked()) {
                    setError(
                        "The verification contact is blocked. Consider using a different contact or a different authentication method"
                    );
                } else {
                    setError(
                        result.error?.errorData?.errorDescription ||
                            "An error occurred while verifying the authentication method"
                    );
                }
            }
    
            if (result.isCompleted()) {
                setData(result.data);
                setCurrentSignInStatus(true);
                setSignInState(result.state);
            }
    
            if (result.isVerificationRequired()) {
                setSignInState(result.state);
            }
        }
    
        setLoading(false);
    };
    ```
5. Add the handler for strong authentication method verification:

    ```typescript
    const handleAuthMethodRegistrationChallengeSubmit = async (e: React.FormEvent) => {
        e.preventDefault();
        setError("");
        setLoading(true);
    
        if (!challengeForRegistration) {
            setError("Please enter a code.");
            setLoading(false);
            return;
        }
    
        if (signInState instanceof AuthMethodVerificationRequiredState) {
            const result = await signInState.submitChallenge(challengeForRegistration);
    
            if (result.isFailed()) {
                if (result.error?.isIncorrectChallenge()) {
                    setError("Incorrect code.");
                } else {
                    setError(
                        result.error?.errorData?.errorDescription ||
                            "An error occurred while verifying the challenge response"
                    );
                }
            }
    
            if (result.isCompleted()) {
                setData(result.data);
                setCurrentSignInStatus(true);
                setSignInState(result.state);
            }
        }
    
        setLoading(false);
    };
    ```
6. Update the `renderForm()` function to display the correct strong authentication method registration forms (method selection or verification):

    ```typescript
    const renderForm = () => {
        if (loadingAccountStatus) {
            return;
        }
    
        ...
    
        // Display AuthMethodRegistrationForm if the current state is authentication method registration required state
        if (signInState instanceof AuthMethodRegistrationRequiredState) {
            return (
                <AuthMethodRegistrationForm
                    onSubmit={handleAuthMethodRegistrationSubmit}
                    authMethods={authMethodsForRegistration}
                    selectedAuthMethod={selectedAuthMethodForRegistration}
                    setSelectedAuthMethod={setSelectedAuthMethodForRegistration}
                    verificationContact={verificationContactForRegistration}
                    setVerificationContact={setVerificationContactForRegistration}
                    loading={loading}
                    styles={styles}
                />
            );
        }
    
        // Display AuthMethodRegistrationChallengeForm if the current state is authentication method verification required state
        if (signInState instanceof AuthMethodVerificationRequiredState) {
            return (
                <AuthMethodRegistrationChallengeForm
                    onSubmit={handleAuthMethodRegistrationChallengeSubmit}
                    challenge={challengeForRegistration}
                    setChallenge={setChallengeForRegistration}
                    loading={loading}
                    styles={styles}
                />
            );
        }
    
        ...
    };
    ```

## Register strong authentication method after sign-up or password reset

Strong authentication method registration flow after sign-up and password reset works similar to the method registration during sign-in flow. After a successful sign-up or password reset, the SDK can automatically continue with the sign-in. If the user doesn't have a strong authentication method registered, the flow transitions to the authentication method registration states.

### Register strong authentication method after sign-up

For strong authentication method registration after sign-up flow, you need you update the */src/app/sign-up/page.tsx* file. See the complete code in [page.tsx](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/sign-up/page.tsx):

1. Make sure you import the required types and components.
2. Handle the strong authentication method registration states in a similar manner as it happens in the sign-in flow. After sign-up completes successfully, you can use the result to automatically trigger a sign-in as shown in the following code snippet:

    ```typescript
    // In your sign-up completion handler
    if (signUpState instanceof SignUpCompletedState) {
        // Continue with sign-in using the continuation token
        const result = await signUpState.signIn();
    
        ...
    
        // Check for auth method registration requirement
        if (result.isAuthMethodRegistrationRequired()) {
            setAuthMethodsForRegistration(result.state.getAuthMethods());
            const methods = result.state.getAuthMethods();
            setSelectedAuthMethodForRegistration(methods.length > 0 ? methods[0] : undefined);
            setSignUpState(result.state);
        }
    
        ...
    }
    
    // Then use the same renderForm logic to display AuthMethodRegistrationForm
    // and AuthMethodRegistrationChallengeForm components
    ```

### Register strong authentication method after password reset

For strong authentication method registration after SSPR, you need to update the */src/app/reset-password/page.tsx* file. See the complete code in [page.tsx](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/reset-password/page.tsx):

1. Make sure you import the required types and components.
2. Handle the strong authentication method registration states in a similar manner as in the sign-in flow. After SSPRS completes successfully, you can use the result to automatically trigger a sign-in as shown in the following code snippet:

    ```typescript
    // In your password reset completion handler
    if (resetPasswordState instanceof ResetPasswordCompletedState) {
        // Continue with sign-in using the continuation token
        const result = await signUpState.signIn();
    
        ...
    
        // Check for auth method registration requirement
        if (result.isAuthMethodRegistrationRequired()) {
            setAuthMethodsForRegistration(result.state.getAuthMethods());
            const methods = result.state.getAuthMethods();
            setSelectedAuthMethodForRegistration(methods.length > 0 ? methods[0] : undefined);
            setSignUpState(result.state);
        }
    
        ...
    }
    
    // Then use the same renderForm logic to display AuthMethodRegistrationForm
    // and AuthMethodRegistrationChallengeForm components
    ```

## Run and test your app

Use the steps in [Run and test your app](tutorial-native-authentication-single-page-app-react-sdk-sign-up#run-and-test-your-app) to run your app, but this time, test the strong authentication method registration flow.

### Test authentication method registration after sign-up

1. Navigate to http://localhost:3000/sign-up to display the sign-up form.
2. Enter the required details, then sign up by following prompts. After you successfully sign up, the app automatically continues to the sign-in flow by displaying the strong authentication method registration form.
3. Select the strong authentication method of choice, such as **Emails OTP**, then enter an email address.
4. Select **Continue** to submit the form details. You should receive a verification code to your email address.
5. Enter the verification code in the challenge form textbox, then select **Continue** button. After the code is verified, your strong authentication method is registered and you're signed in.

### Test strong authentication method registration during sign-in

To test strong authentication method registration during sign-in, make sure you have a user account that doesn't have a strong authentication method registered.

1. Navigate to http://localhost:3000/sign-in to display the sign-in form.
2. Input your details, select the **Continue** button, then follow the prompts. The app enters strong authentication method registration flow.
3. Follow the app prompts to complete strong authentication method registration.

### Test authentication method registration after password reset

To test strong authentication method registration after SSPR, make sure you have a user account that doesn't have a strong authentication method registered.

1. Navigate to http://localhost:3000/reset-password to display the password reset form.
2. Input your details, select the **Continue** button, then follow app prompts to complete the password reset flow. After you successfully reset your password, the app continues to sign-in flow by displaying the strong authentication method registration form.
3. Follow the app prompts to complete strong authentication method registration.
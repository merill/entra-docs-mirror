---
layout: Conceptual
title: Enable MFA in a React SPA by Using Native Authentication JavaScript SDK - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-single-page-app-react-enable-mfa
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to enable multifactor authentication in a React single-page application that uses native authentication JavaScript SDK
manager: dougeby
ms.subservice: external
ms.topic: tutorial
ms.date: 2025-11-18T00:00:00.0000000Z
locale: en-us
document_id: c389cf2a-aabc-74f3-5902-ca60d782222e
document_version_independent_id: c389cf2a-aabc-74f3-5902-ca60d782222e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-single-page-app-react-enable-mfa.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-single-page-app-react-enable-mfa
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-single-page-app-react-enable-mfa.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/97159432-14a9-4307-a469-d2f2c75f0e33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/50565c62-5f6b-4687-be38-323113c72c2e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3311b34b-1e41-68d3-1b2f-dcb96f70c862
---

# Enable MFA in a React SPA by Using Native Authentication JavaScript SDK - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this tutorial, you learn how to add multifactor authentication (MFA) in your React single-page application (SPA) by using native authentication's JavaScript SDK.

Just like in [strong authentication method registration](tutorial-native-authentication-single-page-app-react-register-strong-method), MFA flow occurs in three scenarios:

- **During sign-in**: The user signs in and has a strong authentication method registered.
- **After sign-up**: After the user completes sign-up, they proceed to sign in. New users need to [register a strong authentication method](tutorial-native-authentication-single-page-app-react-register-strong-method) before any MFA challenge. Because the strong authentication method also gets verified during registration, they might not be prompted for an additional MFA challenge.
- **After self-service password reset (SSPR)**: The user successfully resets their password and automatically proceeds to sign in. If the user has a strong authentication method registered, they're prompted to complete MFA challenge.

When MFA is required, the user chooses an MFA challenge method from a list of registered methods. Available options are **email** one-time passcode, **SMS** one-time passcode, or both, depending on what the user previously registered.

The flow diagram below illustrates the three scenarios:

![Complete multifactor authentication challenge.](media/native-authentication-single-page-app-react-register-authentication-method/register-strong-authentication-method.png)

## Prerequisites

- Complete the steps in [sign up](tutorial-native-authentication-single-page-app-react-sdk-sign-up), [sign in](tutorial-native-authentication-single-page-app-react-sdk-sign-in), [password reset](tutorial-native-authentication-single-page-app-react-sdk-reset-password) and [register strong authentication method](tutorial-native-authentication-single-page-app-react-register-strong-method) tutorials.
- [Visual Studio Code](https://visualstudio.microsoft.com/downloads/) or another code editor.
- [Node.js](https://nodejs.org/en/download/).
- [Enable multifactor authentication (MFA) for your app](../external-id/customers/how-to-multifactor-authentication-customers).

## Enable app to handle multifactor authentication

To enable MFA in your React app, update the app configuration by adding the required capability:

1. Locate the *src/config/auth-config.ts* file.
2. In the `customAuth` object, add or update `capabilities` property to include the `mfa_required` value in the array as shown in the following code snippet:

    ```typescript
    const customAuthConfig: CustomAuthConfiguration = {
        customAuth: {
            ...
            capabilities: ["mfa_required"],
            ...
        },
        ...
    };
    ```

The capability value `mfa_required` informs Microsoft Entra that your app can handle an MFA flow. Learn more about [native authentication challenge types and capabilities](concept-native-authentication-challenge-types).

## Create UI components

You require form components in your app to support MFA flow. Use the following steps to add these components to your app:

1. Create a new folder, *src/app/shared/components* for reusable components (if it doesn’t already exist).
2. In the new folder, create a file named *MfaAuthMethodSelectionForm.tsx* to display a form that allows users to select a registered strong authentication method. Add the code in [MfaAuthMethodSelectionForm](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/shared/components/MfaAuthMethodSelectionForm.tsx) into the file.
3. In the new folder, create another file named *MfaChallengeForm.tsx* to display a form for verifying the strong authentication method by using the one-time passcode that the user receives. Add the code in [MfaChallengeForm](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/shared/components/MfaChallengeForm.tsx) into the file.

When needed, you can import and use reusable components in your sign-in, sign-in after sign-up, and sign-in after SSPR flows.

## Handle multifactor authentication during sign-in

Update the *src/app/sign-in/page.tsx* file to enable your app to handle MFA flow during sign-in. See the complete code in [page.tsx](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/sign-in/page.tsx):

1. Import the required types and components as shown in the following code snippet:

    ```typescript
    import {
        CustomAuthPublicClientApplication,
        ICustomAuthPublicClientApplication,
        SignInCodeRequiredState,
        SignInCompletedState,
        AuthFlowStateBase,
        MfaAwaitingState,
        MfaVerificationRequiredState,
    } from "@azure/msal-browser/custom-auth";
    import { MfaAuthMethodSelectionForm } from "../components/shared/MfaAuthMethodSelectionForm";
    import { MfaChallengeForm } from "../components/shared/MfaChallengeForm";
    ```
2. Add new state variables for MFA:

    ```typescript
    export default function SignIn() {
        ...
        // MFA states
    const [mfaAuthMethods, setMfaAuthMethods] = useState<AuthenticationMethod[]>([]);
    const [selectedMfaAuthMethod, setSelectedMfaAuthMethod] = useState<AuthenticationMethod | undefined>(undefined);
    const [mfaChallenge, setMfaChallenge] = useState("");
    
        // ... initialization code
    }
    ```
3. Update the `startSignIn`, `handlePasswordSubmit` and `handleCodeSubmit` functions to check if MFA is required:

    ```typescript
    const startSignIn = async (e: React.FormEvent) => {
        // Start the sign-in flow
        const result = await authClient.signIn({
            username,
        });
    
        ...
    
        if (result.isMfaRequired()) {
            const methods = result.state.getAuthMethods();
            setMfaAuthMethods(methods);
            setSelectedMfaAuthMethod(methods.length > 0 ? methods[0] : undefined);
        }
    
        ...
    };
    
    const handlePasswordSubmit = async (e: React.FormEvent) => {
        if (signInState instanceof SignInPasswordRequiredState) {
            const result = await signInState.submitPassword(password);
    
            ...
    
            // Check for MFA requirement
            if (result.isMfaRequired()) {
                const methods = result.state.getAuthMethods();
                setMfaAuthMethods(methods);
                setSelectedMfaAuthMethod(methods.length > 0 ? methods[0] : undefined);
                setSignInState(result.state);
            }
    
            ...
        }
    };
    
    const handleCodeSubmit = async (e: React.FormEvent) => {
        if (signInState instanceof SignInCodeRequiredState) {
            const result = await signInState.submitCode(code);
    
            ...
    
            // Check for MFA requirement
            if (result.isMfaRequired()) {
                const methods = result.state.getAuthMethods();
                setMfaAuthMethods(methods);
                setSelectedMfaAuthMethod(methods.length > 0 ? methods[0] : undefined);
                setSignInState(result.state);
            }
    
            ...
        }
    };
    ```

    In each of the function, notice that we check if MFA is required by using the following code snippet:

    ```typescript
    if (result.isMfaRequired()) {...}
    ```
4. Add the handler for MFA challenge selection:

    ```typescript
    const handleMfaAuthMethodSubmit = async (e: React.FormEvent) => {
        e.preventDefault();
        setError("");
        setLoading(true);
    
        if (!selectedMfaAuthMethod) {
            setError("Please select an authentication method.");
            setLoading(false);
            return;
        }
    
        if (signInState instanceof MfaAwaitingState) {
            const result = await signInState.requestChallenge(selectedMfaAuthMethod.id);
    
            if (result.isFailed()) {
                if (result.error?.isInvalidInput()) {
                    setError("Incorrect verification contact.");
                } else {
                    setError(
                        result.error?.errorData?.errorDescription ||
                            "An error occurred while verifying the authentication method"
                    );
                }
            }
    
            if (result.isVerificationRequired()) {
                setSignInState(result.state);
            }
        }
    
        setLoading(false);
    };
    ```
5. Add the handler for MFA challenge verification:

    ```typescript
    const handleMfaChallengeSubmit = async (e: React.FormEvent) => {
        e.preventDefault();
        setError("");
        setLoading(true);
    
        if (!mfaChallenge) {
            setError("Please enter a code.");
            setLoading(false);
            return;
        }
    
        if (signInState instanceof MfaVerificationRequiredState) {
            const result = await signInState.submitChallenge(mfaChallenge);
    
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
6. Update the `renderForm()` function to display the correct MFA challenge forms (MFA challenge method selection or MFA challenge method verification):

    ```typescript
    const renderForm = () => {
        if (loadingAccountStatus) {
            return;
        }
    
        ...
    
        // Display MfaAuthMethodSelectionForm if the current state is MFA awaiting state
        if (signInState instanceof MfaAwaitingState) {
            return (
                <MfaAuthMethodSelectionForm
                    onSubmit={handleMfaAuthMethodSubmit}
                    authMethods={mfaAuthMethods}
                    selectedAuthMethod={selectedMfaAuthMethod}
                    setSelectedAuthMethod={setSelectedMfaAuthMethod}
                    loading={loading}
                    styles={styles}
                />
            );
        }
    
        // Display MfaChallengeForm if the current state is MFA verification required state
        if (signInState instanceof MfaVerificationRequiredState) {
            return (
                <MfaChallengeForm
                    onSubmit={handleMfaChallengeSubmit}
                    challenge={mfaChallenge}
                    setChallenge={setMfaChallenge}
                    loading={loading}
                    styles={styles}
                />
            );
        }
    
        ...
    };
    ```

## Handle multifactor authentication after sign-up or password reset

MFA flow after sign-up and password reset works similar to the MFA in the sign-in flow. After a successful sign-up or password reset, the SDK can automatically continue with the sign-in flow. If the user has a strong authentication method registered, the flow transitions to MFA challenge verification.

### Handle multifactor authentication after sign-up

For MFA flow after sign-up, you need you update the */src/app/sign-up/page.tsx* file. See the complete code in [page.tsx](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/sign-up/page.tsx):

1. Make sure you import the required types and components.
2. Handle MFA requirements states in a similar manner as it happens in the sign-in flow; after sign-up completes successfully, use the result to automatically trigger a sign-in flow as shown in the following code snippet:

    ```typescript
    // In your sign-up completion handler
    if (signUpState instanceof SignUpCompletedState) {
        // Continue with sign-in using the continuation token
        const result = await signUpState.signIn();
    
        ...
    
        if (result.isMfaRequired()) {
            const methods = result.state.getAuthMethods();
            setMfaAuthMethods(methods);
            setSelectedMfaAuthMethod(methods.length > 0 ? methods[0] : undefined);
            setSignUpState(state);
        }
    
        ...
    }
    
    // Then use the same renderForm logic to display MfaAuthMethodSelectionForm
    // and MfaChallengeForm components
    ```

### Handle multifactor authentication after password reset

For MFA flow after SSPR, you need to update the */src/app/reset-password/page.tsx* file. See the complete code in [page.tsx](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/reset-password/page.tsx):

1. Make sure you import the required types and components.
2. Handle MFA requirement states in a similar manner as in the sign-in flow. After SSPRS completes successfully, you can use the result to automatically trigger a sign-in as shown in the following code snippet:

    ```typescript
    // In your password reset completion handler
    if (resetPasswordState instanceof ResetPasswordCompletedState) {
        // Continue with sign-in using the continuation token
        const result = await signUpState.signIn();
    
        ...
    
        if (result.isMfaRequired()) {
            const methods = result.state.getAuthMethods();
            setMfaAuthMethods(methods);
            setSelectedMfaAuthMethod(methods.length > 0 ? methods[0] : undefined);
            setResetState(state);
        }
    
        ...
    }
    
    // Then use the same renderForm logic to display MfaAuthMethodSelectionForm
    // and MfaChallengeForm components
    ```

## Run and test your app

Before you test your app, make sure you have a user account that has a registered strong authentication method. Use the steps in [Run and test your app](tutorial-native-authentication-single-page-app-react-register-strong-method#run-and-test-your-app) to run your app, but this time, test the MFA flow.
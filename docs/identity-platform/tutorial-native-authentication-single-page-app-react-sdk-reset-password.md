---
layout: Conceptual
title: Reset Password in a React SPA App by Using Native Authentication JavaScript SDK - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-single-page-app-react-sdk-reset-password
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to build a React single-page app that enables users to reset their passwords in a React single-page app into an external tenant by using native authentication JavaScript SDK.
manager: dougeby
ms.subservice: external
ms.topic: tutorial
ms.date: 2025-11-18T00:00:00.0000000Z
locale: en-us
document_id: acecb2df-488c-fa0a-06bb-2f4b11169fb4
document_version_independent_id: acecb2df-488c-fa0a-06bb-2f4b11169fb4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-single-page-app-react-sdk-reset-password.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-single-page-app-react-sdk-reset-password
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-single-page-app-react-sdk-reset-password.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/97159432-14a9-4307-a469-d2f2c75f0e33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/50565c62-5f6b-4687-be38-323113c72c2e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: b3607e90-7b85-d5cc-4b84-acd918ac6a18
---

# Reset Password in a React SPA App by Using Native Authentication JavaScript SDK - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this tutorial, you learn how to enable password reset in a React single-page app by using native authentication JavaScript SDK.

In this tutorial, you:

- Update the React app to reset user's password.
- Test password reset flow

## Prerequisites

- Complete the steps in [Tutorial: Sign up users into a React single-page app by using native authentication JavaScript SDK](tutorial-native-authentication-single-page-app-react-sdk-sign-up).
- [Enable self-service password reset (SSPR)](../external-id/customers/how-to-enable-password-reset-customers) for customer users in the external tenant. SSPR is available for customer users for apps that use email with password authentication flow.

## Create UI components

During password reset flow, this app, collects the user's username (email), a one-time passcode, and a new user password on different screens. In this section, you create the forms that collect the information the app requires to reset the password.

1. Create a folder called *src/app/reset-password*.
2. Create *reset-password/components/InitialForm.tsx* file, then paste the code from [reset-password/components/InitialForm.tsx](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/reset-password/components/InitialForm.tsx). This component displays a form that collects a user's username (email).
3. Create *reset-password/components/CodeForm.tsx* file, then paste the code from [reset-password/components/CodeForm.tsx](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/shared/components/CodeForm.tsx). This component displays a form that collects the one-time passcode that the user receives in their email inbox.
4. Create *reset-password/components/NewPasswordForm.tsx* file, then paste the code from [reset-password/components/NewPasswordForm.tsx](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/reset-password/components/NewPasswordForm.tsx). This component displays a form that collects a user's new password.

### Handle form interactions

Create *reset-password/page.tsx* file to handle logic for a sign-in flow. In this file:

- Import the necessary components and display the proper form based on the state. See a full example in [reset-password/page.tsx](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/reset-password/page.tsx):

    ```typescript
    import {
      CustomAuthPublicClientApplication,
      ICustomAuthPublicClientApplication,
      ResetPasswordCodeRequiredState,
      ResetPasswordPasswordRequiredState,
      ResetPasswordCompletedState,
      AuthFlowStateBase,
    } from "@azure/msal-browser/custom-auth";
    
    export default function ResetPassword() {
      const [app, setApp] = useState<ICustomAuthPublicClientApplication | null>(
        null
      );
      const [loadingAccountStatus, setLoadingAccountStatus] = useState(true);
      const [isSignedIn, setSignInState] = useState(false);
      const [email, setEmail] = useState("");
      const [code, setCode] = useState("");
      const [newPassword, setNewPassword] = useState("");
      const [error, setError] = useState("");
      const [loading, setLoading] = useState(false);
      const [resetState, setResetState] = useState<AuthFlowStateBase | null>(
        null
      );
    
      useEffect(() => {
        const initializeApp = async () => {
          const appInstance = await CustomAuthPublicClientApplication.create(
            customAuthConfig
          );
          setApp(appInstance);
        };
    
        initializeApp();
      }, []);
    
      useEffect(() => {
        const checkAccount = async () => {
          if (!app) return;
    
          const accountResult = app.getCurrentAccount();
    
          if (accountResult.isCompleted()) {
            setSignInState(true);
          }
    
          setLoadingAccountStatus(false);
        };
    
        checkAccount();
      }, [app]);
    
      const renderForm = () => {
        if (loadingAccountStatus) {
          return;
        }
    
        if (isSignedIn) {
          return (
            <div style={styles.signed_in_msg}>
              Please sign out before processing the password reset.
            </div>
          );
        }
    
        if (resetState instanceof ResetPasswordPasswordRequiredState) {
          return (
            <NewPasswordForm
              onSubmit={handleNewPasswordSubmit}
              newPassword={newPassword}
              setNewPassword={setNewPassword}
              loading={loading}
            />
          );
        }
    
        if (resetState instanceof ResetPasswordCodeRequiredState) {
          return (
            <CodeForm
              onSubmit={handleCodeSubmit}
              code={code}
              setCode={setCode}
              loading={loading}
            />
          );
        }
    
        if (resetState instanceof ResetPasswordCompletedState) {
          return <ResetPasswordResultPage />;
        }
    
        return (
          <InitialForm
            onSubmit={handleInitialSubmit}
            email={email}
            setEmail={setEmail}
            loading={loading}
          />
        );
      };
    
      return (
        <div style={styles.container}>
          <h2 style={styles.h2}>Reset Password</h2>
          {renderForm()}
          {error && <div style={styles.error}>{error}</div>}
        </div>
      );
    }
    ```
- To start the password reset flow, use the following code snippet. See a full example at [reset-password/page.tsx](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/reset-password/page.tsx) to learn where to place the code snippet:

    ```typescript
    const handleInitialSubmit = async (e: React.FormEvent) => {
        if (!app) return;
        e.preventDefault();
        setError("");
        setLoading(true);
        const result = await app.resetPassword({
            username: email,
        });
        const state = result.state;
        if (result.isFailed()) {
            if (result.error?.isInvalidUsername()) {
                setError("Invalid email address");
            } else if (result.error?.isUserNotFound()) {
                setError("User not found");
            } else {
                setError(
                    result.error?.errorData.errorDescription || "An error occurred while initiating password reset"
                );
            }
        } else {
            setResetState(state);
        }
        setLoading(false);
    };
    ```

    The SDK's instance method, `resetPassword()`, starts the password reset flow.
- To submit the one-time passcode, use the following code snippet. See a full example at [reset-password/page.tsx](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/reset-password/page.tsx) to learn where to place the code snippet:

    ```typescript
    const handleCodeSubmit = async (e: React.FormEvent) => {
        e.preventDefault();
        setError("");
        setLoading(true);
        if (resetState instanceof ResetPasswordCodeRequiredState) {
            const result = await resetState.submitCode(code);
            const state = result.state;
            if (result.isFailed()) {
                if (result.error?.isInvalidCode()) {
                    setError("Invalid verification code");
                } else {
                    setError(result.error?.errorData.errorDescription || "An error occurred while verifying the code");
                }
            } else {
                setResetState(state);
            }
        }
        setLoading(false);
    };
    ```

    Password reset state's `submitCode()` submits the one-time passcode.
- To submit the user's new password, use the following code snippet. See a full example at [reset-password/page.tsx](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/reset-password/page.tsx) to learn where to place the code snippet:

    ```typescript
    const handleNewPasswordSubmit = async (e: React.FormEvent) => {
        e.preventDefault();
        setError("");
        setLoading(true);
        if (resetState instanceof ResetPasswordPasswordRequiredState) {
            const result = await resetState.submitNewPassword(newPassword);
            const state = result.state;
            if (result.isFailed()) {
                if (result.error?.isInvalidPassword()) {
                    setError("Invalid password");
                } else {
                    setError(result.error?.errorData.errorDescription || "An error occurred while setting new password");
                }
            } else {
                setResetState(state);
            }
        }
        setLoading(false);
    };
    ```

    Password reset state's `submitNewPassword()` submits the user's new password.
- To use the reset password result, use the following code snippet. See a full example at [reset-password/page.tsx](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/reset-password/page.tsx) to learn where to place the code snippet:

    ```typescript
    if (resetState instanceof ResetPasswordCompletedState) {
        return <ResetPasswordResultPage/>;
    }
    
    ```

## Optional: Sign in users automatically after password reset

After a user successfully resets their password, you can directly sign them into the app without initiating a new sign-in flow. To do so, use the following code snippet. See a full example at [reset-password/page.tsx](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/blob/main/typescript/native-auth/react-nextjs-sample/src/app/reset-password/page.tsx):

```typescript
if (resetState instanceof ResetPasswordCompletedState) {
    const result = await resetState.signIn();
    const state = result.state;
    if (result.isFailed()) {
        setError(result.error?.errorData?.errorDescription || "An error occurred during auto sign-in");
    }
    if (result.isCompleted()) {
        setData(result.data);
        setResetState(state);
    }
}
```

## Run and test your app

Use the steps in [Run and test your app](tutorial-native-authentication-single-page-app-react-sdk-sign-up#run-and-test-your-app) to run your app, then test sign-in flow.
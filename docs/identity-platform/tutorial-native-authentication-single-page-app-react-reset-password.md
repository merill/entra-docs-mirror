---
layout: Conceptual
title: Reset password in a React SPA by using native auth - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-single-page-app-react-reset-password
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to build a React single-page app that reset password for users in an external tenant by using native authentication.
manager: dougeby
ms.subservice: external
ms.topic: tutorial
ms.date: 2025-02-07T00:00:00.0000000Z
locale: en-us
document_id: 5d89435d-b1cc-4c61-7466-51cab14aeb2d
document_version_independent_id: 5d89435d-b1cc-4c61-7466-51cab14aeb2d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-single-page-app-react-reset-password.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-single-page-app-react-reset-password
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-single-page-app-react-reset-password.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/97159432-14a9-4307-a469-d2f2c75f0e33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/50565c62-5f6b-4687-be38-323113c72c2e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 10e5943f-9aff-6f3a-e537-7643418fcda3
---

# Reset password in a React SPA by using native auth - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this tutorial, you learn how to reset password in a React single-page app (SPA) by using native authentication.

In this tutorial, you:

- Update the React app to reset user's password.
- Test password reset flow

## Prerequisites

- Complete the steps in [Tutorial: Set up CORS Proxy server to manage CORS headers for native authentication](tutorial-native-authentication-single-page-app-react-set-up-local-cors).

## Define types of calls the app makes to the native authentication API

During the password reset flow, the app makes multiple calls to the native authentication API such as initiating a password reset request and submitting a password reset form.

To define these calls, open the *scr/client/RequestTypes.ts* file, then append following code snippet:

```typescript
    export interface ResetPasswordStartRequest {
        username: string;
        challenge_type: string;
        client_id: string;
    }

    export interface ResetPasswordSubmitRequest {
        client_id: string;
        continuation_token: string;
        new_password: string;
    }

    export interface ResetPasswordSubmitForm {
        continuation_token: string;
        new_password: string;
    }
```

## Define the type of responses app receives from the native authentication API

To define the type of responses the app can receive from the native authentication API for the password reset operation, open the *src/client/ResponseTypes.ts* file, then append the following code snippet:

```typescript
    export interface ChallengeResetResponse {
        continuation_token: string;
        expires_in: number;
    }

    export interface ResetPasswordSubmitResponse {
        continuation_token: string;
        poll_interval: number;
    }
```

## Process password reset requests

In this section, you add code that processes password reset flow requests. Examples of these requests are initiating a password reset request and submitting a password reset form.

To do so, create a file called *src/client/ResetPasswordService.ts*, then add the following code snippet:

```typescript
    import { CLIENT_ID, ENV } from "../config";
    import { postRequest } from "./RequestClient";
    import { ChallengeForm, ChallengeRequest, ResetPasswordStartRequest, ResetPasswordSubmitForm, ResetPasswordSubmitRequest } from "./RequestTypes";
    import { ChallengeResetResponse, ChallengeResponse, ResetPasswordSubmitResponse } from "./ResponseTypes";

    export const resetStart = async ({ username }: { username: string }) => {
        const payloadExt: ResetPasswordStartRequest = {
            username,
            client_id: CLIENT_ID,
            challenge_type: "password oob redirect",
        };

        return await postRequest(ENV.urlResetPwdStart, payloadExt);
    };

    export const resetChallenge = async ({ continuation_token }: { continuation_token: string }): Promise<ChallengeResponse> => {
        const payloadExt: ChallengeRequest = {
            continuation_token,
            client_id: CLIENT_ID,
            challenge_type: "oob redirect",
        };

        return await postRequest(ENV.urlResetPwdChallenge, payloadExt);
    };

    export const resetSubmitOTP = async (payload: ChallengeForm): Promise<ChallengeResetResponse> => {
        const payloadExt = {
            client_id: CLIENT_ID,
            continuation_token: payload.continuation_token,
            oob: payload.oob,
            grant_type: "oob",
        };

        return await postRequest(ENV.urlResetPwdContinue, payloadExt);
    };

    export const resetSubmitNewPassword = async (payload: ResetPasswordSubmitForm): Promise<ResetPasswordSubmitResponse> => {
        const payloadExt: ResetPasswordSubmitRequest = {
            client_id: CLIENT_ID,
            continuation_token: payload.continuation_token,
            new_password: payload.new_password,
        };

        return await postRequest(ENV.urlResetPwdSubmit, payloadExt);
    };

    export const resetPoll = async (continuation_token: string): Promise<ChallengeResetResponse> => {
        const payloadExt = {
            client_id: CLIENT_ID,
            continuation_token,
        };
        return await postRequest(ENV.urlResetPwdPollComp, payloadExt);
    };
```

The `challenge_type` property shows the authentication methods that the client app supports. Read more about [challenge types](concept-native-authentication-challenge-types).

## Create UI components

During password reset flow, this app, on different screens, collects the user's username (email), a one-time passcode, and a new user password.

1. Create a folder called */pages/resetpassword* in the *src* folder.
2. To create, display and submit the password reset forms, create a file *src/pages/resetpassword/ResetPassword.tsx*, then add the following code:

    ```typescript
    // ResetPassword.tsx
    import React, { useState } from "react";
    import { resetChallenge, resetStart, resetSubmitNewPassword, resetSubmitOTP } from "../../client/ResetPasswordService";
    import { ChallengeResetResponse, ChallengeResponse, ErrorResponseType } from "../../client/ResponseTypes";
    
    export const ResetPassword: React.FC = () => {
      const [username, setUsername] = useState<string>("");
      const [otp, setOTP] = useState<string>("");
      const [newPassword, setNewPassword] = useState<string>("");
      const [error, setError] = useState<string>("");
      const [step, setStep] = useState<number>(1);
      const [isLoading, setIsloading] = useState<boolean>(false);
      const [tokenRes, setTokenRes] = useState<ChallengeResponse>({
        binding_method: "",
        challenge_channel: "",
        challenge_target_label: "",
        challenge_type: "",
        code_length: 0,
        continuation_token: "",
        interval: 0,
      });
      const [otpRes, setOTPRes] = useState<ChallengeResetResponse>({
        expires_in: 0,
        continuation_token: "",
      });
    
      const handleResetPassword = async (e: React.FormEvent<HTMLFormElement>) => {
        e.preventDefault();
        if (!username) {
          setError("Username is required");
          return;
        }
        setError("");
        try {
          setIsloading(true);
          const res1 = await resetStart({ username });
          const tokenRes = await resetChallenge({ continuation_token: res1.continuation_token });
          setTokenRes(tokenRes);
          setStep(2);
        } catch (err) {
          setError("An error occurred during password reset " + (err as ErrorResponseType).error_description);
        } finally {
          setIsloading(false);
        }
      };
    
      const handleSubmitCode = async (e: React.FormEvent<HTMLFormElement>) => {
        e.preventDefault();
        if (!otp) {
          setError("All fields are required");
          return;
        }
        setError("");
        try {
          setIsloading(true);
          const res = await resetSubmitOTP({
            continuation_token: tokenRes.continuation_token,
            oob: otp,
          });
          setOTPRes(res);
          setStep(3);
        } catch (err) {
          setError("An error occurred while submitting the otp code " + (err as ErrorResponseType).error_description);
        } finally {
          setIsloading(false);
        }
      };
    
      const handleSubmitNewPassword = async (e: React.FormEvent<HTMLFormElement>) => {
        e.preventDefault();
        if (!newPassword) {
          setError('All fields are required');
          return;
        }
        setError('');
        try {
          setIsloading(true);
          await resetSubmitNewPassword({
            continuation_token: otpRes.continuation_token,
            new_password: newPassword,
          });
          setStep(4);
        } catch (err) {
          setError("An error occurred while submitting the new password " + (err as ErrorResponseType).error_description);
        } finally {
          setIsloading(false);
        }
      };
    
      return (
        <div className="reset-password-form">
        //collect username to initiate password reset flow
          {step === 1 && (
            <form onSubmit={handleResetPassword}>
              <h2>Reset Password</h2>
              <div className="form-group">
                <label>Username:</label>
                <input type="text" value={username} onChange={(e) => setUsername(e.target.value)} required />
              </div>
              {error && <div className="error">{error}</div>}
              {isLoading && <div className="warning">Sending request...</div>}
              <button type="submit">Reset Password</button>
            </form>
          )}
            //collect OTP
          {step === 2 && (
            <form onSubmit={handleSubmitCode}>
              <h2>Submit one time code received via email at {tokenRes.challenge_target_label}</h2>
              <div className="form-group">
                <label>One time code:</label>
                <input type="text" maxLength={tokenRes.code_length} value={otp} onChange={(e) => setOTP(e.target.value)} required />
              </div>
              {error && <div className="error">{error}</div>}
              {isLoading && <div className="warning">Sending request...</div>}
              <button type="submit">Submit code</button>
            </form>
          )}
            //Collect new password
          {step === 3 && (
            <form onSubmit={handleSubmitNewPassword}>
              <h2>Submit New Password</h2>
              <div className="form-group">
                <label>New Password:</label>
                <input type="password" value={newPassword} onChange={(e) => setNewPassword(e.target.value)} required />
              </div>
              {error && <div className="error">{error}</div>}
              {isLoading && <div className="warning">Sending request...</div>}
              <button type="submit">Submit New Password</button>
            </form>
          )}
            //report success after password reset is successful
          {step === 4 && (
            <div className="reset-password-success">
              <h2>Password Reset Successful</h2>
              <p>Your password has been reset successfully. You can now log in with your new password.</p>
            </div>
          )}
        </div>
      );
    };
    ```

## Add app routes

Open the *src/AppRoutes.tsx* file, then uncomment the following lines of code:

```typescript
    //uncomment
    import { ResetPassword } from "./pages/ResetAccount/ResetPassword";
    //...
    
    export const AppRoutes = () => {
      return (
        <Routes>
            //uncomment
            <Route path="/reset" element={<ResetPassword />} />
        </Routes>
      );
    };
```

## Run and test your app

Use the steps in [Run and test your app](tutorial-native-authentication-single-page-app-react-set-up-local-cors#run-and-test-you-app) to run your app. However, test the password reset flow only using the user account you signed up earlier.
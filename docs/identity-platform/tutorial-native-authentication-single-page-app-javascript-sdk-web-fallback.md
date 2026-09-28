---
layout: Conceptual
title: Support web fallback in native authentication JavaScript SDK - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-single-page-app-javascript-sdk-web-fallback
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to handle web fallback in native authentication JavaScript SDK
manager: dougeby
ms.subservice: external
ms.topic: tutorial
ms.date: 2025-06-30T00:00:00.0000000Z
locale: en-us
document_id: 19b5bb36-5d56-1396-1a48-533b8d93b2bc
document_version_independent_id: 19b5bb36-5d56-1396-1a48-533b8d93b2bc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-single-page-app-javascript-sdk-web-fallback.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-single-page-app-javascript-sdk-web-fallback
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-single-page-app-javascript-sdk-web-fallback.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 048b2071-b46c-be98-f3c1-a46057bcf5d9
---

# Support web fallback in native authentication JavaScript SDK - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This tutorial demonstrates how to acquire security tokens through a browser-based authentication where native authentication isn't sufficient to complete the authentication flow by using a mechanism called *web fallback*.

Web fallback allows a client app that uses native authentication to use browser-delegated authentication as a fallback mechanism to improve resilience. This scenario happens when native authentication isn't sufficient to complete the authentication flow. For example, if the authorization server requires capabilities that the client can't provide. Learn more about [web fallback](concept-native-authentication-web-fallback).

In this tutorial, you:

- Check `isRedirectRequired` error.
- Handle `isRedirectRequired` error.

## Prerequisites

# [React](#tab/react)
- Complete the steps in [Tutorial: Sign in users into a React single-page app by using native authentication JavaScript SDK](tutorial-native-authentication-single-page-app-react-sdk-sign-in).

# [Angular](#tab/angular)
- Complete the steps in [Tutorial: Sign in users into Angular single-page app by using native authentication JavaScript SDK](tutorial-native-authentication-single-page-app-angular-sign-in).

---

## Check and handle web fallback

One of the errors you can encounter when you use the JavaScript SDK's `signIn()` or `SignUp()` method is `result.error?.isRedirectRequired()`. The utility method `isRedirectRequired()` checks the need to fall back to browser-delegated authentication. Use the following code snippet to support web fallback:

```typescript
const result = await authClient.signIn({
         username,
     });

if (result.isFailed()) {
   if (result.error?.isRedirectRequired()) {
      // Fallback to the delegated authentication flow.
      const popUpRequest: PopupRequest = {
         authority: customAuthConfig.auth.authority,
         scopes: [],
         redirectUri: customAuthConfig.auth.redirectUri || "",
         prompt: "login", // Forces the user to enter their credentials on that request, negating single-sign on.
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
            result.state = new SignInCompletedState();
            result.data = accountResult.data;
         }
      } catch (error) {
         if (error instanceof Error) {
            setError(error.message);
         } else {
            setError("An unexpected error occurred while logging in with popup");
         }
      }
   } else {
         setError(`An error occurred: ${result.error?.errorData?.errorDescription}`);
   }
}
```

When the app uses the fallback mechanism, the app acquires security tokens by using the `loginPopup()` method.
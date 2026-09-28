---
layout: Conceptual
title: Add custom headers to native authentication requests in JavaScript SPAs - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-single-page-app-javascript-custom-headers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to attach custom x-* headers to native authentication requests in a React or Angular SPA to integrate fraud-detection SDKs with Microsoft Entra External ID.
manager: dougeby
ms.subservice: external
ms.topic: tutorial
ms.date: 2026-05-20T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1012
ai-usage: ai-assisted
locale: en-us
document_id: 8c2ee06f-e903-5943-fa5d-76d647b762eb
document_version_independent_id: 8c2ee06f-e903-5943-fa5d-76d647b762eb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-single-page-app-javascript-custom-headers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-single-page-app-javascript-custom-headers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-single-page-app-javascript-custom-headers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://authoring-docs-microsoft.poolparty.biz/devrel/80beb97b-18aa-44f8-9420-8f2a4cd448eb
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://authoring-docs-microsoft.poolparty.biz/devrel/8c09e0ef-0fde-4b6d-bf1b-b517e4db7f80
platformId: 0ea2ae5a-c9b0-f87e-9c7e-ed19ea9082bf
---

# Add custom headers to native authentication requests in JavaScript SPAs - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This tutorial shows you how to add custom `x-*` headers to native authentication network requests in a React or Angular single-page app (SPA). Use the `CustomAuthRequestInterceptor` from the native authentication JavaScript SDK to integrate with third-party fraud and bot-detection providers.

In this tutorial, you:

- Learn the header naming rules that our SDK enforces.
- Register the interceptor on your app configuration.
- Verify that your headers reach the intended endpoints.

## Prerequisites

A React or Angular SPA that uses native authentication JavaScript SDK. If you don't have one, complete one of the following tutorials first:

- [Sign in users into a React single-page app by using native authentication JavaScript SDK](tutorial-native-authentication-single-page-app-react-sdk-sign-in)
- [Sign in users in an Angular single-page app by using native authentication](tutorial-native-authentication-single-page-app-angular-sign-in)

## Understand header naming rules

The Microsoft Authentication Library (MSAL) applies the following rules when it evaluates the headers that you provide. Use these rules to verify your vendor-required header names before you implement the interceptor:

- Headers **must** start with `x-` (case-insensitive). MSAL ignores headers that don't start with `x-`.
- MSAL ignores headers that start with any of the following reserved prefixes, because they're owned by the SDK:
    - `x-client-`
    - `x-ms-`
    - `x-broker-`
    - `x-app-`

MSAL adds any header that passes both rules to the network request. If a header name you provide conflicts with one the SDK would set, your value takes precedence.

## Implement the request interceptor

The `CustomAuthRequestInterceptor` interface declares a single method, `addAdditionalHeaderFields`, that our SDK calls before it sends each native authentication network request. Your implementation receives the request URL and returns a dictionary of headers to add, or `null` if no headers are needed for that request.

1. Open your app configuration file such as:

    - `src/app/config/auth-config.ts` for Angular.
    - `src/config/auth-config.ts` for React.
2. Add the following interceptor above your existing `customAuthConfig` definition:

```typescript
import { CustomAuthConfiguration, LogLevel } from "@azure/msal-browser/custom-auth";
import type { CustomAuthRequestInterceptor } from "@azure/msal-browser/custom-auth";

const requestInterceptor: CustomAuthRequestInterceptor = {
    addAdditionalHeaderFields(requestUrl: URL) {
        // Scope headers to specific endpoints only.
        if (requestUrl.pathname.endsWith("/oauth2/v2.0/initiate")) {
            return {
                value_1: "customer_header_1",            // Ignored: doesn't start with "x-".
                "x-client-header": "customer_header_2",  // Ignored: starts with reserved prefix "x-client-".
                "X-my-custom-header": "my data",         // Added to the network request.
            };
        }

        // Return null for all other requests to avoid over-sending signals.
        return null;
    },
};
```

The `addAdditionalHeaderFields` method receives the full URL of the outgoing request in `requestUrl`. Use the URL to scope your headers to the specific endpoints that your fraud or bot-detection vendor requires, such as sign-in or sign-up initiation endpoints. Sending headers to unrelated endpoints can degrade signal quality and increase false positives.

Note

MSAL evaluates the naming rules *after* your interceptor returns. Logging from inside `addAdditionalHeaderFields` shows only the headers that you provided, not the final set that MSAL sends. Inspect the actual network request to verify the final headers.

## Register the interceptor

After you implement the interceptor, assign it to the `requestInterceptor` property on the `customAuth` block of your `CustomAuthConfiguration`:

```typescript
export const customAuthConfig: CustomAuthConfiguration = {
    customAuth: {
        challengeTypes: ["password", "oob", "redirect"],
        authApiProxyUrl: "http://localhost:3001/api",
        requestInterceptor: requestInterceptor,
    },
    auth: {
        clientId: "Enter_the_Application_Id_Here",
        // ...
    },
};
```

The configuration is identical for both React and Angular.

## Verify headers are applied

To confirm that your headers reach the intended endpoints, inspect the outgoing network traffic by using your browser's developer tools (Network tab) or a network proxy tool such as Fiddler. Check that:

- Headers that start with `x-` and don't use a reserved prefix appear in the request.
- Headers that use reserved prefixes (`x-client-`, `x-ms-`, `x-broker-`, `x-app-`) don't appear in the request.
- Headers appear only on the endpoints you targeted in your interceptor.
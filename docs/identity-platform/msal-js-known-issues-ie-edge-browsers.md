---
layout: Conceptual
title: Issues on Internet Explorer & Microsoft Edge (MSAL.js) - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/msal-js-known-issues-ie-edge-browsers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn about know issues when using the Microsoft Authentication Library for JavaScript (MSAL.js) with Internet Explorer and Microsoft Edge browsers.
manager: pmwongera
ms.custom: 
ms.date: 2020-05-18T00:00:00.0000000Z
ms.reviewer: 
ms.topic: troubleshooting
locale: en-us
document_id: 7f2eafe2-28c3-1b5b-26bf-adf17d01b82e
document_version_independent_id: 13c6fbce-9b73-f08e-ef9a-7f8f7d28ff87
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/msal-js-known-issues-ie-edge-browsers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/msal-js-known-issues-ie-edge-browsers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/msal-js-known-issues-ie-edge-browsers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
platformId: 77e158b4-3907-4402-9bb0-98c1269eb516
---

# Issues on Internet Explorer & Microsoft Edge (MSAL.js) - Microsoft identity platform | Microsoft Learn

## Issues due to security zones

We had multiple reports of issues with authentication in, that is, and Microsoft Edge (since the update of the *Microsoft Edge browser version to 40.15063.0.0*). We're tracking these and have informed the Microsoft Edge team. While Microsoft Edge works on a resolution, here's a description of the frequently occurring issues and the possible workarounds that can be implemented.

### Cause

The cause for most of these issues is as follows. The session storage and local storage are partitioned by security zones in the Microsoft Edge browser. In this particular version of Microsoft Edge, when the application is redirected across zones, the session storage and local storage are cleared. Specifically, the session storage is cleared in the regular browser navigation, and both the session and local storage are cleared in the InPrivate mode of the browser. MSAL.js saves certain state in the session storage and relies on checking this state during the authentication flows. When the session storage is cleared, this state is lost and hence results in broken experiences.

### Issues

- **Infinite redirect loops and page reloads during authentication**. When users sign in to the application on Microsoft Edge, they're redirected back from the Microsoft Entra login page and are stuck in an infinite redirect loop resulting in repeated page reloads. This is usually accompanied by an `invalid_state` error in the session storage.
- **Infinite acquire token loops and AADSTS50058 error**. When an application that is run on Microsoft Edge tries to acquire a token for a resource, the application may get stuck in an infinite loop of the acquire token call. The following error is returned from Microsoft Entra ID in your network trace:

    `Error :login_required; Error description:AADSTS50058: A silent sign-in request was sent but no user is signed in. The cookies used to represent the user's session were not sent in the request to Azure AD. This can happen if the user is using Internet Explorer or Edge, and the web app sending the silent sign-in request is in different IE security zone than the Azure AD endpoint (login.microsoftonline.com)`
- **Pop-up window doesn't close or is stuck when using login through pop-up window to authenticate**. When authenticating through a pop-up window in Microsoft Edge or Internet Explorer (InPrivate), after entering credentials and signing in, if multiple domains across security zones are involved in the navigation, the pop-up window doesn't close because `MSAL.js` loses the handle to the pop-up window.
- **Cannot log in using redirect URL prefixed with tauri**. The only supported schemes for redirect URIs are `https:` for production apps and `http://localhost` for local development. If you attempt to use a different scheme, like `tauri://localhost`, for a mobile or desktop application, the below error message appears. This error arises as a result of how the backend of the SPA is designed.

    `AADSTS90023: Cross-origin token redemption is permitted only for the 'Single-Page Application' client-type or 'Native' client-type with origin registered in AllowedOriginForNativeAppCorsRequestInOAuthToken allow list.`

### Update: Fix available in MSAL.js 0.2.3

Fixes for the authentication redirect loop issues have been released in [MSAL.js 0.2.3](https://github.com/AzureAD/microsoft-authentication-library-for-js/releases). Enable the flag `storeAuthStateInCookie` in the MSAL.js config to take advantage of this fix. By default this flag is set to false.

When the `storeAuthStateInCookie` flag is enabled, MSAL.js uses the browser cookies to store the request state required for validation of the auth flows.

Note

This fix is not yet available for the `msal-angular` and `msal-angularjs` wrappers. This fix doesn't address the issue with pop-up windows.

#### Other workarounds

Make sure to test that your issue is occurring only on the specific version of Microsoft Edge browser and works on the other browsers before adopting these workarounds.

1. As a first step to get around these issues, ensure that the application domain and any other sites involved in the redirects of the authentication flow are added as trusted sites in the security settings of the browser. This ensures the redirects belong to the same security zone. To do so, follow these steps:

    - Open **Internet Explorer** and click on the **settings** (gear icon) in the top-right corner
    - Select **Internet Options**
    - Select the **Security** tab
    - Under the **Trusted Sites** option, click on the **sites** button and add the URLs in the dialog box that opens.
2. As mentioned before, since only the session storage is cleared during the regular navigation, you may configure MSAL.js to use the local storage instead. This can be set as the `cacheLocation` config parameter while initializing MSAL.

Note, these workarounds won't solve the issue for InPrivate browsing since both session and local storage are cleared.

## Issues due to popup blockers

There are cases when popups are blocked in, that is, or Microsoft Edge, for example when a second popup occurs during [multi-factor authentication](../identity/authentication/concept-mfa-howitworks). You'll get an alert in the browser to allow for the pop-up window once or always. If you choose to allow, the browser opens the pop-up window automatically and returns a `null` handle for it. As a result, the library doesn't have a handle for the window and there's no way to close the pop-up window. The same issue doesn't happen in Chrome when it prompts you to allow pop-up windows because it doesn't automatically open a pop-up window.

As a **workaround**, developers need to allow popups in, that is, and Microsoft Edge before they start using their app to avoid this issue.
---
layout: Conceptual
title: Overview of the Microsoft Authentication Library (MSAL) - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/msal-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: The Microsoft Authentication Library (MSAL) enables application developers to acquire tokens in order to call secured web APIs. These web APIs can be the Microsoft Graph, other Microsoft APIs, third-party web APIs, or your own web API. MSAL supports multiple application architectures and platforms.
manager: pmwongera
ms.custom: has-adal-ref
ms.date: 2024-11-13T00:00:00.0000000Z
ms.reviewer: 
ms.topic: concept-article
locale: en-us
document_id: 52984432-b89a-b94b-fd37-af459880cb45
document_version_independent_id: d2e775ac-03db-ea51-087f-294c13da7582
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/msal-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/msal-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/msal-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
platformId: 9cd57bcb-6568-de2f-09eb-74d7ddc8cd23
---

# Overview of the Microsoft Authentication Library (MSAL) - Microsoft identity platform | Microsoft Learn

The Microsoft Authentication Library (MSAL) enables developers to acquire [security tokens](developer-glossary#security-token) from the Microsoft identity platform to authenticate users and access secured web APIs. It can be used to provide secure access to Microsoft Graph, other Microsoft APIs, third-party web APIs, or your own web API. MSAL supports many different application architectures and platforms including .NET, JavaScript, Java, Python, Android, and iOS.

MSAL provides multiple ways to get security tokens, with a consistent API for many platforms. Using MSAL provides the following benefits:

- There's no need to directly use the OAuth libraries or code against the protocol in your application.
- Can acquire tokens on behalf of a user or application (when applicable to the platform).
- Maintains a token cache for you and handles token refreshes when they're close to expiring.
- Helps you specify which audience you want your application to sign in. The sign in audience can include personal Microsoft accounts, social identities with Microsoft Entra External ID, work, school, or users in sovereign and national clouds.
- Helps you set up your application from configuration files.
- Helps you troubleshoot your app by exposing actionable exceptions, logging, and telemetry.

| Application types and scenarios | Tutorials |
| --- | --- |
| Single-page apps (JavaScript) | [Tutorial: Sign-in users to a React Single-page application (SPA)](tutorial-single-page-app-react-prepare-app) |
| Web applications | [Tutorial: Sign-in users to a ASP.NET Core Web application](tutorial-web-app-dotnet-prepare-app) |
| Web APIs | [Tutorial: Implement a protected endpoint a ASP.NET Core API](tutorial-web-api-dotnet-register-app) |
| Mobile and native applications | [Mobile application calling a web API on behalf of the user who's signed-in interactively](scenario-mobile-app-configuration). |
| Daemons and server-side applications | [Desktop/service daemon application calling web API on behalf of itself](scenario-daemon-app-configuration) |

## MSAL Languages and Frameworks

You can refer to the following documentation to learn more about the different MSAL libraries.

| MSAL Documentation | MSAL Library | Supported platforms and frameworks |
| --- | --- | --- |
| [MSAL.NET](/en-us/entra/msal/dotnet/) | [MSAL.NET](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | .NET Framework, .NET, .NET MAUI, WINUI |
| [MSAL for Android](https://github.com/AzureAD/microsoft-authentication-library-for-android/tree/dev/docs) | [MSAL for Android](https://github.com/AzureAD/microsoft-authentication-library-for-android) | Android |
| [MSAL Angular](/en-us/javascript/api/@azure/msal-angular/) | [MSAL Angular](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-angular) | Single-page apps with Angular and Angular.js frameworks |
| [MSAL for iOS and macOS](https://github.com/AzureAD/microsoft-authentication-library-for-objc/tree/dev/docs) | [MSAL for iOS and macOS](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | iOS and macOS |
| [MSAL Java](/en-us/entra/msal/java/) | [MSAL Java](https://github.com/AzureAD/microsoft-authentication-library-for-java) | Windows, macOS, Linux |
| [MSAL.js](/en-us/javascript/api/overview/msal-overview) | [MSAL.js](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-browser) | JavaScript/TypeScript frameworks such as Vue.js, Ember.js, or Durandal.js |
| [MSAL Node](/en-us/javascript/api/%40azure/msal-node/) | [MSAL Node](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-node) | Web apps with Express, desktop apps with Electron, Cross-platform console apps |
| [MSAL Python](/en-us/entra/msal/python/) | [MSAL Python](https://github.com/AzureAD/microsoft-authentication-library-for-python) | Windows, macOS, Linux |
| [MSAL React](/en-us/javascript/api/%40azure/msal-react/) | [MSAL React](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-react) | Single-page apps with React and React-based libraries (Next.js, Gatsby.js) |
| [MSAL Go (Preview)](/en-us/entra/msal/go/) | [MSAL Go (Preview)](https://github.com/AzureAD/microsoft-authentication-library-for-go) | Windows, macOS, Linux |

Important

Active Directory Authentication Library (ADAL) has ended support. Customers need to ensure their applications are migrated to MSAL. MSAL integrates with the Microsoft identity platform (v2.0) endpoint, which is the unification of Microsoft personal accounts and work accounts into a single authentication system. ADAL integrates with a v1.0 endpoint which doesn't support personal accounts.
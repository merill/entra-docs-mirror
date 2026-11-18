---
layout: Conceptual
title: Microsoft Entra External ID app samples and guides - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/samples-ciam-all
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to build and integrate apps with Microsoft Entra External ID for scenarios such as sign-up, sign-in, and getting an access token to call an API.
ms.topic: sample
ms.date: 2026-11-17T00:00:00.0000000Z
ms.custom: it-pro, seo-july-2024, msecd-doc-authoring-1030
ai-usage: ai-assisted
locale: en-us
document_id: f90ca42e-b36c-1d67-b635-1bb4750968b1
document_version_independent_id: 01bcb6b2-cc5a-ef80-4550-822d22b34250
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/samples-ciam-all.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/samples-ciam-all
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/samples-ciam-all.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: a527b1ed-bab1-01b4-5143-24b5ca7408aa
---

# Microsoft Entra External ID app samples and guides - Microsoft Entra External ID | Microsoft Learn

Use these samples and guides to integrate authentication and authorization with Microsoft Entra External ID. Choose by app type, language, or platform. Each guide explains how to build and run a sample or develop your own app, with code comments that explain the integration.

**Applies to external tenants:** Feature support varies by authentication approach and API or SDK version. Compare Microsoft-hosted authentication, Embedded native authentication, and Bring Your Own UX (BYO UX) in the [authentication approach overview](concept-choose-authentication-approach). Check feature availability in the [authentication support matrix](concept-supported-features-customers#authentication-approach-supportability).

**Sample inventory:** This index lists Microsoft-hosted and Embedded native authentication examples. No Bring Your Own UX (BYO UX) sample is listed here.

For Embedded native authentication, start with the [quickstart](../../identity-platform/quickstart-native-authentication) and [application configuration guide](../../identity-platform/how-to-native-authentication-configure-app). For an existing integration, review [SDK compatibility and migration requirements](../../identity-platform/how-to-migrate-native-authentication-v1-v2#sdk-compatibility).

## Embedded native authentication

Use the following onboarding guidance for the Microsoft Authentication Library (MSAL) interfaces. Check the [SDK compatibility table](../../identity-platform/how-to-migrate-native-authentication-v1-v2#sdk-compatibility) for the documented package versions and supported continuation interfaces. For direct HTTP integration, use the [Native Authentication API reference](../../identity-platform/reference-native-authentication).

| Platform | SDK | Guidance |
| --- | --- | --- |
| **JavaScript and TypeScript** | [MSAL for JavaScript releases](https://github.com/AzureAD/microsoft-authentication-library-for-js/releases), `@azure/msal-browser` 5.29.1 or later. | [JavaScript samples](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples), [React Next.js quickstart](../../identity-platform/quickstart-native-authentication), and [browser CORS requirements](../../identity-platform/concept-native-authentication-cors#proxy-contract). |
| **Android** | [MSAL for Android](https://github.com/AzureAD/microsoft-authentication-library-for-android/), `com.microsoft.identity.client:msal` 8.7.0 or later. | [Android sample](https://github.com/Azure-Samples/ms-identity-ciam-native-auth-android-sample) and [Android SDK compatibility and migration](../../identity-platform/how-to-migrate-native-authentication-v1-v2#android-migration). |
| **Apple** | [MSAL for iOS and macOS releases](https://github.com/AzureAD/microsoft-authentication-library-for-objc/releases), 2.18.1 or later. | [iOS sample](https://github.com/Azure-Samples/ms-identity-ciam-native-auth-ios-sample) and [Apple SDK compatibility and migration](../../identity-platform/how-to-migrate-native-authentication-v1-v2#ios-migration). |

Existing V1 integrations can use the [V1 API reference and SDK library links](../../identity-platform/reference-native-authentication-api-v1). The passkey samples are separate credential-management integrations, not passkey sign-in through the Native Authentication API.

CORS and proxy guidance applies to cross-origin browser API calls from SPAs with Embedded native authentication and BYO UX websites. Android and iOS apps using native HTTP transports don't need a CORS proxy.

## Samples and guides

Use the tabs to sort samples either by app type or your preferred language or platform.

These tables list examples, not overall feature support. A missing sample doesn't mean a feature is unsupported. Check the [authentication support matrix](concept-supported-features-customers#authentication-approach-supportability) for availability.

# [By app type](#tab/apptype)
### Single-page application (SPA)

These samples and how-to guides demonstrate how to integrate a single-page application with Microsoft Entra External ID.

| Language/Platform | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| JavaScript | • [Sign in users](/en-us/entra/identity-platform/quickstart-single-page-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=javascript-external) • [List, register, and delete passkeys (GitHub sample)](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/tree/main/passkey-sample) | • [Sign in users](/en-us/entra/identity-platform/tutorial-single-page-app-javascript-prepare-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;tabs=external-tenant) • [Sign in with passkeys](how-to-sign-in-with-passkey) |
| Angular | • [Sign in users](/en-us/entra/identity-platform/quickstart-single-page-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=angular-external) | • [Sign in users](/en-us/entra/identity-platform/tutorial-single-page-apps-angular-prepare-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;tabs=external-tenant) |
| React | • [Sign in users](/en-us/entra/identity-platform/quickstart-single-page-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=react-external) • [List, register, and delete passkeys (GitHub sample)](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/tree/main/passkey-sample) | • [Sign in users](/en-us/entra/identity-platform/tutorial-single-page-app-react-prepare-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;tabs=external-tenant) • [Sign in with passkeys](how-to-sign-in-with-passkey) |

### Web app

These samples and how-to guides demonstrate how to write a web application that integrates with Microsoft Entra External ID.

| Language/Platform | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| JavaScript, Node.js (Express) | • [Sign in users](/en-us/entra/identity-platform/quickstart-web-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=node-external) • [Sign in users and call an API](/en-us/entra/identity-platform/quickstart-web-app-node-sign-in-call-api?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) | • [Sign in users](/en-us/entra/identity-platform/tutorial-web-app-node-sign-in-prepare-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) • [Sign in users and call an API](how-to-web-app-node-sign-in-call-api-prepare-tenant) |
| ASP.NET Core | • [Sign in users](/en-us/entra/identity-platform/quickstart-web-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=asp-dot-net-core-external) | • [Sign in users](/en-us/entra/identity-platform/tutorial-web-app-dotnet-prepare-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;tabs=external-tenant) |
| Python Django | • [Sign in users](/en-us/entra/identity-platform/quickstart-web-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=python-django-external) | --- |
| Python Flask | • [Sign in users](/en-us/entra/identity-platform/quickstart-web-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=python-flask-external) | --- |

### Web API

These samples and how-to guides demonstrate how to protect a web API with the Microsoft identity platform, and how to call a downstream API from the web API.

| Language/Platform | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| ASP.NET Core | --- | • [Secure an ASP.NET web API](/en-us/entra/identity-platform/tutorial-web-api-dotnet-core-build-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) |

### Desktop

These samples and how-to guides demonstrate how to write a desktop application that integrates with Microsoft Entra External ID.

| Language/Platform | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| JavaScript, Electron | • [Sign in users](/en-us/entra/identity-platform/quickstart-desktop-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=node-js-external) | --- |
| ASP.NET (MAUI) | • [Sign in users](/en-us/entra/identity-platform/quickstart-desktop-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=wpfdotnet-maui-external) | • [Sign in users](/en-us/entra/identity-platform/tutorial-desktop-app-maui-sign-in-prepare-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) |
| .NET (MAUI) WPF | • [Sign in users](/en-us/entra/identity-platform/quickstart-desktop-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=wpfdotnet-wpf-external) | --- |

### Mobile: Microsoft-hosted authentication

These samples and how-to guides show you how to write a public client mobile application with browser-delegated authentication that integrates with Microsoft Entra External ID.

| Language/Platform | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| ASP.NET Core MAUI | • [Sign in users](/en-us/entra/identity-platform/quickstart-mobile-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=android-netmaui-external) | • [Sign in users](tutorial-mobile-app-maui-sign-in-prepare-tenant) |
| Android (Kotlin) | • [Sign in users](/en-us/entra/identity-platform/quickstart-mobile-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=android-external) • [Sign in users and call an API](/en-us/entra/identity-platform/quickstart-mobile-app-call-api?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=android-external) | • [Sign in users, call an API](tutorial-mobile-app-android-kotlin-prepare-tenant) |
| iOS (Swift) | • [Sign in users](/en-us/entra/identity-platform/quickstart-mobile-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=ios-macos-external) • [Sign in users and call an API](sample-mobile-app-ios-swift-sign-in-call-api) | • [Sign in users, call an API](/en-us/entra/identity-platform/tutorial-mobile-app-ios-swift-prepare-tenant?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external) |

### Desktop: Embedded native authentication

For macOS, use the [MSAL iOS/macOS SDK reference](https://azuread.github.io/microsoft-authentication-library-for-objc/) and [Apple SDK compatibility and migration guidance](../../identity-platform/how-to-migrate-native-authentication-v1-v2#ios-migration).

### Mobile: Embedded native authentication

Use these samples with the onboarding guidance for the response-driven integration.

| Language/Platform | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| Android (Kotlin) | • [Android sample](https://github.com/Azure-Samples/ms-identity-ciam-native-auth-android-sample) | • [SDK compatibility and migration](../../identity-platform/how-to-migrate-native-authentication-v1-v2#android-migration) |
| iOS (Swift) | • [iOS sample](https://github.com/Azure-Samples/ms-identity-ciam-native-auth-ios-sample) | • [SDK compatibility and migration](../../identity-platform/how-to-migrate-native-authentication-v1-v2#ios-migration) |

### Daemon

These samples and how-to guides demonstrate how to write a daemon application that integrates with Microsoft Entra External ID.

| Language/Platform | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| Node.js | • [Call an API](/en-us/entra/identity-platform/quickstart-daemon-app-call-api?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=node-external) | • [Call an API](/en-us/entra/identity-platform/tutorial-daemon-node-call-api-build-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=asp-dot-net-core-external) |
| .NET | • [Call an API](/en-us/entra/identity-platform/quickstart-daemon-app-call-api?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=asp-dot-net-core-external) | • [Call an API](/en-us/entra/identity-platform/tutorial-dotnet-daemon-call-api?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) |

# [By language/platform](#tab/language)
### .NET

| App type | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| Daemon | • [Call an API](/en-us/entra/identity-platform/quickstart-daemon-app-call-api?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=asp-dot-net-core-external) | • [Call an API](/en-us/entra/identity-platform/tutorial-dotnet-daemon-call-api?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) |

### Android (Kotlin)

| App type | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| Mobile: Microsoft-hosted authentication | • [Sign in users](sample-mobile-app-android-kotlin-sign-in) • [Sign in users and call an API](sample-mobile-app-android-kotlin-sign-in-call-api) | • [Sign in users, call an API](tutorial-mobile-app-android-kotlin-prepare-tenant) |
| Mobile: Embedded native authentication | • [Android sample](https://github.com/Azure-Samples/ms-identity-ciam-native-auth-android-sample) | • [SDK compatibility and migration](../../identity-platform/how-to-migrate-native-authentication-v1-v2#android-migration) |

### ASP.NET Core

| App type | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| Web API | --- | • [Secure an ASP.NET web API](/en-us/entra/identity-platform/tutorial-web-api-dotnet-core-build-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) |
| Web app | • [Sign in users](/en-us/entra/identity-platform/quickstart-web-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=asp-dot-net-core-external) | • [Sign in users](/en-us/entra/identity-platform/tutorial-web-app-dotnet-prepare-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;tabs=external-tenant) |

### .NET (MAUI)

| App type | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| Desktop | • [Sign in users](/en-us/entra/identity-platform/quickstart-desktop-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=wpfdotnet-maui-external) | • [Sign in users](/en-us/entra/identity-platform/tutorial-desktop-app-maui-sign-in-prepare-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) |
| Mobile: Microsoft-hosted authentication | • [Sign in users](/en-us/entra/identity-platform/quickstart-mobile-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=android-netmaui-external) | • [Sign in users](tutorial-mobile-app-maui-sign-in-prepare-tenant) |

### Python, Django

| App type | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| Web app | • [Sign in users](/en-us/entra/identity-platform/quickstart-web-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=python-django-external) | --- |

### Python, Flask

| App type | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| Web app | • [Sign in users](/en-us/entra/identity-platform/quickstart-web-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=python-flask-external) | --- |

### iOS/macOS (Swift)

| App type | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| Mobile: Microsoft-hosted authentication | • [Sign in users](/en-us/entra/identity-platform/quickstart-mobile-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=ios-macos-external) • [Sign in users and call an API](sample-mobile-app-ios-swift-sign-in-call-api) | • [Sign in users, call an API](/en-us/entra/identity-platform/tutorial-mobile-app-ios-swift-prepare-tenant?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external) |
| Mobile: Embedded native authentication | • [iOS sample](https://github.com/Azure-Samples/ms-identity-ciam-native-auth-ios-sample) | • [SDK compatibility and migration](../../identity-platform/how-to-migrate-native-authentication-v1-v2#ios-migration) |
| Desktop: Embedded native authentication | --- | • [MSAL iOS/macOS SDK reference](https://azuread.github.io/microsoft-authentication-library-for-objc/) • [SDK compatibility and migration](../../identity-platform/how-to-migrate-native-authentication-v1-v2#ios-migration) |

### JavaScript

| App type | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| Single-page application | • [Sign in users](/en-us/entra/identity-platform/quickstart-single-page-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=javascript-external) • [List, register, and delete passkeys (GitHub sample)](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/tree/main/passkey-sample) | • [Sign in users](/en-us/entra/identity-platform/tutorial-single-page-app-javascript-prepare-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;tabs=external-tenant) • [Sign in with passkeys](how-to-sign-in-with-passkey) |

### JavaScript, Angular

| App type | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| Single-page application | • [Sign in users](/en-us/entra/identity-platform/quickstart-single-page-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=angular-external) | • [Sign in users](/en-us/entra/identity-platform/tutorial-single-page-apps-angular-prepare-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;tabs=external-tenant) |

### JavaScript, React

| App type | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| Single-page application | • [Sign in users](/en-us/entra/identity-platform/quickstart-single-page-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=react-external) • [List, register, and delete passkeys (GitHub sample)](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/tree/main/passkey-sample) | • [Sign in users](/en-us/entra/identity-platform/tutorial-single-page-app-react-prepare-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;tabs=external-tenant) • [Sign in with passkeys](how-to-sign-in-with-passkey) |

### JavaScript, Node

| App type | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| Daemon | • [Call an API](/en-us/entra/identity-platform/quickstart-daemon-app-call-api?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=node-external) | • [Call an API](/en-us/entra/identity-platform/tutorial-daemon-node-call-api-build-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=asp-dot-net-core-external) |

### JavaScript, Node.js (Express)

| App type | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| Web app | • [Sign in users](/en-us/entra/identity-platform/quickstart-web-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=node-external) • [Sign in users and call an API](/en-us/entra/identity-platform/quickstart-web-app-node-sign-in-call-api?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) | • [Sign in users](/en-us/entra/identity-platform/tutorial-web-app-node-sign-in-prepare-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) • [Sign in users and call an API](how-to-web-app-node-sign-in-call-api-prepare-tenant) |

### JavaScript, Electron

| App type | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| Desktop | • [Sign in users](/en-us/entra/identity-platform/quickstart-desktop-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=node-js-external) | --- |

---
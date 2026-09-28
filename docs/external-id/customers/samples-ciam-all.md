---
layout: Conceptual
title: Samples and guides for integrating apps with External ID - Microsoft Entra External ID | Microsoft Learn
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
description: Learn how to build and integrate apps with external tenants with scenarios such as sign-up, sign in, and getting an access token to call an API.
ms.topic: sample
ms.date: 2025-03-11T00:00:00.0000000Z
ms.custom: it-pro, seo-july-2024
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

# Samples and guides for integrating apps with External ID - Microsoft Entra External ID | Microsoft Learn

Microsoft maintains code samples that demonstrate how to integrate various application types with Microsoft Entra External ID. We provide instructions for downloading and using samples or building your own app based on common authentication and authorization scenarios, development languages, and platforms. Included are instructions for building the project (if applicable) and running the sample application. Within the sample code, comments help you understand how these libraries are used in the application to perform authentication and authorization in an external tenant.

Tip

Microsoft Entra External ID supports two authentication approaches: **browser-delegated authentication**, which redirects users to a Microsoft-hosted sign-in page, and **native authentication**, which lets you build the sign-in UI directly in your app. The samples in this article include both. If you're not sure which approach to use, see [Choose an authentication approach](concept-choose-authentication-approach).

## Samples and guides

Use the tabs to sort samples either by app type or your preferred language or platform.

# [By app type](#tab/apptype)
### Single-page application (SPA)

These samples and how-to guides demonstrate how to integrate a single-page application with Microsoft Entra External ID.

| Language/Platform | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| JavaScript | • [Sign in users](/en-us/entra/identity-platform/quickstart-single-page-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=javascript-external) • [Sign in users and manage passkeys (GitHub sample)](https://github.com/Azure-Samples/ms-identity-ciam-native-javascript-samples/tree/main/passkey-sample) | • [Sign in users](/en-us/entra/identity-platform/tutorial-single-page-app-javascript-prepare-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;tabs=external-tenant) • [Sign in with passkeys](how-to-sign-in-with-passkey) |
| Angular | • [Sign in users](/en-us/entra/identity-platform/quickstart-single-page-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=angular-external) | • [Sign in users](/en-us/entra/identity-platform/tutorial-single-page-apps-angular-prepare-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;tabs=external-tenant) |
| React | • [Sign in users](/en-us/entra/identity-platform/quickstart-single-page-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=react-external) • [Sign in users and manage passkeys (GitHub sample)](https://github.com/Azure-Samples/ms-eeid-passkey-sample-app) | • [Sign in users](/en-us/entra/identity-platform/tutorial-single-page-app-react-prepare-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;tabs=external-tenant) • [Sign in with passkeys](how-to-sign-in-with-passkey) |

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

### Mobile: Browser delegated authentication

These samples and how-to guides show you how to write a public client mobile application with browser-delegated authentication that integrates with Microsoft Entra External ID.

| Language/Platform | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| ASP.NET Core MAUI | • [Sign in users](/en-us/entra/identity-platform/quickstart-mobile-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=android-netmaui-external) | • [Sign in users](tutorial-mobile-app-maui-sign-in-prepare-tenant) |
| Android (Kotlin) | • [Sign in users](/en-us/entra/identity-platform/quickstart-mobile-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=android-external) • [Sign in users and call an API](/en-us/entra/identity-platform/quickstart-mobile-app-call-api?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=android-external) | • [Sign in users, call an API](tutorial-mobile-app-android-kotlin-prepare-tenant) |
| iOS (Swift) | • [Sign in users](/en-us/entra/identity-platform/quickstart-mobile-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=ios-macos-external) • [Sign in users and call an API](sample-mobile-app-ios-swift-sign-in-call-api) | • [Sign in users, call an API](/en-us/entra/identity-platform/tutorial-mobile-app-ios-swift-prepare-tenant?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external) |

### Desktop: Native authentication

These samples and how-to guides demonstrate how to write a desktop application that integrates with Microsoft Entra External ID.

| Language/Platform | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| macOS (Swift) | • [Sign in users](/en-us/entra/identity-platform/quickstart-native-authentication-macos-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) | • [Sign in users](/en-us/entra/identity-platform/tutorial-native-authentication-prepare-ios-macos-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) |

### Mobile: Native authentication

These samples and how-to guides demonstrate how to write a public client mobile application with native authentication that integrates with Microsoft Entra External ID.

| Language/Platform | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| Android (Kotlin) | • [Sign in users](/en-us/entra/identity-platform/quickstart-native-authentication-android-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) • [Sign in users and call an API](/en-us/entra/identity-platform/quickstart-native-authentication-android-call-api?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) | • [Sign in users](/en-us/entra/identity-platform/tutorial-native-authentication-prepare-android-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) |
| iOS (Swift) | • [Sign in users](/en-us/entra/identity-platform/quickstart-native-authentication-ios-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) • [Sign in users and call an API](/en-us/entra/identity-platform/quickstart-native-authentication-ios-call-api?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) | • [Sign in users](/en-us/entra/identity-platform/tutorial-native-authentication-prepare-ios-macos-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) |

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
| Mobile: Browser delegated authentication | • [Sign in users](sample-mobile-app-android-kotlin-sign-in) • [Sign in users and call an API](sample-mobile-app-android-kotlin-sign-in-call-api) | • [Sign in users, call an API](tutorial-mobile-app-android-kotlin-prepare-tenant) |
| Mobile: Native authentication | • [Sign in users](/en-us/entra/identity-platform/quickstart-native-authentication-android-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) • [Sign in users and call an API](/en-us/entra/identity-platform/quickstart-native-authentication-android-call-api?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) | • [Sign in users](/en-us/entra/identity-platform/tutorial-native-authentication-prepare-android-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) |

### ASP.NET Core

| App type | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| Web API | --- | • [Secure an ASP.NET web API](/en-us/entra/identity-platform/tutorial-web-api-dotnet-core-build-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) |
| Web app | • [Sign in users](/en-us/entra/identity-platform/quickstart-web-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=asp-dot-net-core-external) | • [Sign in users](/en-us/entra/identity-platform/tutorial-web-app-dotnet-prepare-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;tabs=external-tenant) |

### .NET (MAUI)

| App type | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| Desktop | • [Sign in users](/en-us/entra/identity-platform/quickstart-desktop-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=wpfdotnet-maui-external) | • [Sign in users](/en-us/entra/identity-platform/tutorial-desktop-app-maui-sign-in-prepare-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) |
| Mobile: Browser delegated authentication | • [Sign in users](/en-us/entra/identity-platform/quickstart-mobile-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=android-netmaui-external) | • [Sign in users](tutorial-mobile-app-maui-sign-in-prepare-tenant) |

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
| Mobile: Browser delegated authentication | • [Sign in users](/en-us/entra/identity-platform/quickstart-mobile-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=ios-macos-external) • [Sign in users and call an API](sample-mobile-app-ios-swift-sign-in-call-api) | • [Sign in users, call an API](/en-us/entra/identity-platform/tutorial-mobile-app-ios-swift-prepare-tenant?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external) |
| Mobile: Native authentication | • iOS (Swift) [Sign in users](/en-us/entra/identity-platform/quickstart-native-authentication-ios-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) • [Sign in users and call an API](/en-us/entra/identity-platform/quickstart-native-authentication-ios-call-api?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) | • [Sign in users](/en-us/entra/identity-platform/tutorial-native-authentication-prepare-ios-macos-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) |
| Desktop: Native authentication | • macOS (Swift) [Sign in users](/en-us/entra/identity-platform/quickstart-native-authentication-macos-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) | • [Sign in users](/en-us/entra/identity-platform/tutorial-native-authentication-prepare-ios-macos-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) |

### JavaScript

| App type | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| Single-page application | • [Sign in users](/en-us/entra/identity-platform/quickstart-single-page-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=javascript-external) | • [Sign in users](/en-us/entra/identity-platform/tutorial-single-page-app-javascript-prepare-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;tabs=external-tenant) |

### JavaScript, Angular

| App type | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| Single-page application | • [Sign in users](/en-us/entra/identity-platform/quickstart-single-page-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=angular-external) | • [Sign in users](/en-us/entra/identity-platform/tutorial-single-page-apps-angular-prepare-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;tabs=external-tenant) |

### JavaScript, React

| App type | Code sample guide | Build and integrate guide |
| --- | --- | --- |
| Single-page application | • [Sign in users](/en-us/entra/identity-platform/quickstart-single-page-app-sign-in?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;pivots=external&amp;tabs=react-external) • [Sign in users and manage passkeys (GitHub sample)](https://github.com/Azure-Samples/ms-eeid-passkey-sample-app) | • [Sign in users](/en-us/entra/identity-platform/tutorial-single-page-app-react-prepare-app?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;tabs=external-tenant) • [Sign in with passkeys](how-to-sign-in-with-passkey) |

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
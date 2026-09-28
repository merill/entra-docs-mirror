---
layout: Conceptual
title: Microsoft identity platform authentication libraries - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/reference-v2-libraries
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: List of client libraries and middleware compatible with the Microsoft identity platform. Use these libraries to add support for user sign-in (authentication) and protected web API access (authorization) to your applications.
manager: pmwongera
ms.custom: 
ms.date: 2022-10-28T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.topic: reference
locale: en-us
document_id: 0b787325-589c-b5f5-f530-7f1fe12e075e
document_version_independent_id: 6d678569-0ebe-f2ef-ecd7-69cc62b4b7be
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/reference-v2-libraries.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/reference-v2-libraries
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/reference-v2-libraries.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
platformId: 071c780b-2396-9657-4566-42b9fd19f0d3
---

# Microsoft identity platform authentication libraries - Microsoft identity platform | Microsoft Learn

The following tables show Microsoft Authentication Library support for several application types. They include links to library source code, where to get the package for your app's project, and whether the library supports user sign-in (authentication), access to protected web APIs (authorization), or both.

The Microsoft identity platform has been certified by the OpenID Foundation as a [certified OpenID provider](https://openid.net/certification/). If you prefer to use a library other than the Microsoft Authentication Library (MSAL) or another Microsoft-supported library, choose one with a [certified OpenID Connect implementation](https://openid.net/developers/certified/).

If you choose to hand-code your own protocol-level implementation of [OAuth 2.0 or OpenID Connect 1.0](v2-protocols), pay close attention to the security considerations in each standard's specification and follow secure software design and development practices like those in the [Microsoft SDL](https://www.microsoft.com/securityengineering/sdl/).

## Single-page application (SPA)

A single-page application runs entirely in the browser and fetches page data (HTML, CSS, and JavaScript) dynamically or at application load time. It can call web APIs to interact with back-end data sources.

Because a SPA's code runs entirely in the browser, it's considered a *public client* that's unable to store secrets securely.

| Language / framework | Project onGitHub | Package | Gettingstarted | Sign in users | Access web APIs |
| --- | --- | --- | --- | --- | --- |
| React | [MSAL React](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-react)^2^ | [msal-react](https://www.npmjs.com/package/@azure/msal-react) | [Quickstart](quickstart-register-app) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) |
| JavaScript | [MSAL.js](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-browser)^2^ | [msal-browser](https://www.npmjs.com/package/@azure/msal-browser) | [Quickstart](quickstart-register-app) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) |
| Angular | [MSAL Angular](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular)^2^ | [msal-angular](https://www.npmjs.com/package/@azure/msal-angular) | [Quickstart](quickstart-register-app) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) |

## Web application

A web application runs code on a server that generates and sends HTML, CSS, and JavaScript to a user's web browser to be rendered. The user's identity is maintained as a session between the user's browser (the front end) and the web server (the back end).

Because a web application's code runs on the web server, it's considered a *confidential client* that can store secrets securely.

| Language / framework | Project onGitHub | Package | Gettingstarted | Sign in users | Access web APIs | Generally available (GA)*or*Public preview^1^ |
| --- | --- | --- | --- | --- | --- | --- |
| .NET | [MSAL.NET](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client) | — | ![Library cannot request ID tokens for user sign-in.](media/common/no.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| .NET | [Microsoft.IdentityModel](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | [Microsoft.IdentityModel](https://www.nuget.org/packages?q=Microsoft.IdentityModel) | — | ![Library cannot request ID tokens for user sign-in.](media/common/no.png)^2^ | ![Library cannot request access tokens for protected web APIs.](media/common/no.png)^2^ | GA |
| ASP.NET Core | [Microsoft.Identity.Web](https://github.com/AzureAD/microsoft-identity-web) | [Microsoft.Identity.Web](https://www.nuget.org/packages/Microsoft.Identity.Web) | [Quickstart](quickstart-web-app-dotnet-core-sign-in) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| Java | [MSAL4J](https://github.com/AzureAD/microsoft-authentication-library-for-java) | [msal4j](https://central.sonatype.com/artifact/com.microsoft.azure/msal4j) | [Quickstart](quickstart-web-app-java-sign-in) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| Spring | [spring-cloud-azure-starter-active-directory](https://github.com/Azure/azure-sdk-for-java/tree/spring-cloud-azure-autoconfigure_4.3.0/sdk/spring/spring-cloud-azure-starter-active-directory) | [spring-cloud-azure-starter-active-directory](https://central.sonatype.com/artifact/com.azure.spring/spring-cloud-azure-starter-active-directory) | [Tutorial](/en-us/azure/developer/java/spring-framework/configure-spring-boot-starter-java-app-with-azure-active-directory) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| Node.js | [MSAL Node](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-node) | [msal-node](https://www.npmjs.com/package/@azure/msal-node) | [Quickstart](quickstart-web-app-nodejs-sign-in) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| Python | [MSAL Python](https://github.com/AzureAD/microsoft-authentication-library-for-python) | [msal](https://pypi.org/project/msal) | — | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| Python | [identity](https://github.com/rayluo/identity) | [identity](https://pypi.org/project/identity/) | [Quickstart](quickstart-web-app-python-flask) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | -- |

^(1)^[Universal License Terms for Online Services](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/all) apply to libraries in *Public preview*.

^(2)^ The [Microsoft.IdentityModel](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) library only *validates* tokens - it can't request ID or access tokens.

## Desktop application

A desktop application is typically binary (compiled) code that displays a user interface and is intended to run on a user's desktop.

Because a desktop application runs on the user's desktop, it's considered a *public client* that's unable to store secrets securely.

| Language / framework | Project onGitHub | Package | Gettingstarted | Sign in users | Access web APIs | Generally available (GA)*or*Public preview^1^ |
| --- | --- | --- | --- | --- | --- | --- |
| Electron | [MSAL Node.js](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-node) | [msal-node](https://www.npmjs.com/package/@azure/msal-node) | — | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | Public preview |
| Java | [MSAL4J](https://github.com/AzureAD/microsoft-authentication-library-for-java) | [msal4j](https://mvnrepository.com/artifact/com.microsoft.azure/msal4j) | — | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| macOS (Swift/Obj-C) | [MSAL for iOS and macOS](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [MSAL](https://cocoapods.org/pods/MSAL) | [Tutorial](tutorial-v2-ios) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| UWP | [MSAL.NET](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client) | [Tutorial](tutorial-v2-windows-uwp) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| WPF | [MSAL.NET](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client) | [Tutorial](tutorial-v2-windows-desktop) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |

^1^[Universal License Terms for Online Services](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/all) apply to libraries in *Public preview*.

## Mobile application

A mobile application is typically binary (compiled) code that displays a user interface and is intended to run on a user's mobile device.

Because a mobile application runs on the user's mobile device, it's considered a *public client* that's unable to store secrets securely.

| Platform | Project onGitHub | Package | Gettingstarted | Sign in users | Access web APIs | Generally available (GA)*or*Public preview^1^ |
| --- | --- | --- | --- | --- | --- | --- |
| Android (Java) | [MSAL Android](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [MSAL](https://mvnrepository.com/artifact/com.microsoft.identity.client/msal) | [Quickstart](quickstart-mobile-app-android-sign-in) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| Android (Kotlin) | [MSAL Android](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [MSAL](https://mvnrepository.com/artifact/com.microsoft.identity.client/msal) | — | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| iOS (Swift/Obj-C) | [MSAL for iOS and macOS](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [MSAL](https://cocoapods.org/pods/MSAL) | [Tutorial](tutorial-v2-ios) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |

^1^[Universal License Terms for Online Services](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/all) apply to libraries in *Public preview*.

## Service / daemon

Services and daemons are commonly used for server-to-server and other unattended (sometimes called *headless*) communication. Because there's no user at the keyboard to enter credentials or consent to resource access, these applications authenticate as themselves, not a user, when requesting authorized access to a web API's resources.

A service or daemon that runs on a server is considered a *confidential client* that can store its secrets securely.

| Language / framework | Project onGitHub | Package | Gettingstarted | Sign in users | Access web APIs | Generally available (GA)*or*Public preview^1^ |
| --- | --- | --- | --- | --- | --- | --- |
| .NET | [MSAL.NET](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client/) | [Quickstart](quickstart-daemon-dotnet-acquire-token) | ![Library cannot request ID tokens for user sign-in.](media/common/no.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| Java | [MSAL4J](https://github.com/AzureAD/microsoft-authentication-library-for-java) | [msal4j](https://javadoc.io/doc/com.microsoft.azure/msal4j/latest/index.html) | — | ![Library cannot request ID tokens for user sign-in.](media/common/no.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| Node | [MSAL Node](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-node) | [msal-node](https://www.npmjs.com/package/@azure/msal-node) | [Quickstart](quickstart-console-app-nodejs-acquire-token) | ![Library cannot request ID tokens for user sign-in.](media/common/no.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| Python | [MSAL Python](https://github.com/AzureAD/microsoft-authentication-library-for-python) | [msal-python](https://github.com/AzureAD/microsoft-authentication-library-for-python) | [Quickstart](quickstart-daemon-app-python-acquire-token) | ![Library cannot request ID tokens for user sign-in.](media/common/no.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |

^1^[Universal License Terms for Online Services](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/all) apply to libraries in *Public preview*.
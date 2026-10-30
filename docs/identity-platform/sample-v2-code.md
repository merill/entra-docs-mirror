---
layout: Conceptual
title: Code samples for authentication and authorization - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/sample-v2-code
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: An index of identity platform code samples, grouped by app types, languages, and frameworks, shows how these libraries enable app authentication and authorization.
manager: pmwongera
ms.date: 2025-01-27T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.topic: sample
locale: en-us
document_id: b90331e5-cca5-b157-eaa1-6f8f90003b32
document_version_independent_id: 4b1b803d-e30d-10b2-90a1-3f0ccd8d7d44
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/sample-v2-code.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/sample-v2-code
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/sample-v2-code.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: df47aa71-d4ec-802e-e204-4a75b0dbd3bb
---

# Code samples for authentication and authorization - Microsoft identity platform | Microsoft Learn

These code samples are built and maintained by Microsoft to demonstrate usage of our authentication libraries with the Microsoft identity platform. Common authentication and authorization scenarios are implemented in several [application types](v2-app-types), development languages, and frameworks.

- Sign in users to web applications and provide authorized access to protected web APIs.
- Protect a web API by requiring an access token to perform API operations.

Each code sample includes a *README.md* file describing how to build the project (if applicable) and run the sample application. Comments in the code help you understand how these libraries are used in the application to perform authentication and authorization by using the identity platform.

## Samples and guides

Use the tabs to sort the samples by application type, or your preferred language/framework.

# [By app type](#tab/apptype)
### Single-page applications

These samples show how to write a single-page application secured with Microsoft identity platform. These samples use one of the flavors of MSAL.js.

| Language /Platform | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| React | • [Sign in users](https://github.com/Azure-Samples/ms-identity-docs-code-javascript/tree/main/react-spa) | [MSAL React](/en-us/javascript/api/@azure/msal-react) | Authorization code with PKCE | [Quickstart](quickstart-single-page-app-react-sign-in) | [Tutorial](tutorial-single-page-app-react-prepare-app) |
| Angular | • [Sign in users](https://github.com/Azure-Samples/ms-identity-docs-code-javascript/tree/main/angular-spa) | [MSAL Angular](/en-us/javascript/api/@azure/msal-angular) | Authorization code with PKCE | [Quickstart](quickstart-single-page-app-angular-sign-in) | [Tutorial](tutorial-v2-angular-auth-code) |
| JavaScript | • [Sign in users](https://github.com/Azure-Samples/ms-identity-docs-code-javascript/tree/main/vanillajs-spa) • [Call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-javascript-tutorial/tree/main/2-Authorization-I/1-call-graph/README.md)• [Call Node.js web API](https://github.com/Azure-Samples/ms-identity-javascript-tutorial/tree/main/3-Authorization-II/1-call-api/README.md)• [Deploy to Azure Storage and App Service](https://github.com/Azure-Samples/ms-identity-javascript-tutorial/tree/main/4-Deployment/README.md) | [MSAL.js](/en-us/javascript/api/overview/msal-overview) | Authorization code with PKCE | [Quickstart](quickstart-single-page-app-sign-in) |  |
| Blazor WebAssembly | • [Sign in users](https://github.com/Azure-Samples/ms-identity-docs-code-dotnet/tree/main/spa-blazor-wasm)• [Call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-blazor-wasm/blob/main/WebApp-graph-user/Call-MSGraph/README.md)• [Deploy to Azure App Service](https://github.com/Azure-Samples/ms-identity-blazor-wasm/blob/main/Deploy-to-Azure/README.md) | [MSAL.js](/en-us/javascript/api/overview/msal-overview) | Authorization code with PKCE | [Quickstart](quickstart-single-page-app-blazor-wasm-sign-in) |  |

### Web applications

The following samples illustrate web applications that sign in users. Some samples also demonstrate the application calling Microsoft Graph, or your own web API with the user's identity.

| Language / Platform | Code sample(s) on GitHub | Auth libraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| ASP.NET | • [Microsoft Graph Training Sample](https://github.com/microsoftgraph/msgraph-training-aspnetmvcapp) • [Sign in users and call Microsoft Graph with admin restricted scope](https://github.com/azure-samples/active-directory-dotnet-admin-restricted-scopes-v2) | • [MSAL.NET](/en-us/entra/msal/dotnet)• [Microsoft.Identity.Web](/en-us/dotnet/api/microsoft-authentication-library-dotnet/confidentialclient)• [Advanced Token Cache Scenarios](https://github.com/Azure-Samples/ms-identity-dotnet-advanced-token-cache) | • OpenID connect • Authorization code • On-Behalf-Of (OBO) | [Quickstart](https://github.com/AzureAdQuickstarts/AppModelv2-WebApp-OpenIDConnect-DotNet) |  |
| ASP.NET Core | • [Sign in users](https://github.com/Azure-Samples/ms-identity-docs-code-dotnet/tree/main/web-app-aspnet)• [Call Microsoft Graph](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/blob/master/2-WebApp-graph-user/2-1-Call-MSGraph/README.md)• [Customize token cache](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/blob/master/2-WebApp-graph-user/2-2-TokenCache/README.md)• [Use the Conditional Access auth context to perform step-up authentication](https://github.com/Azure-Samples/ms-identity-dotnetcore-ca-auth-context-app/blob/main/README.md)• [Call Graph (multitenant)](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/blob/master/2-WebApp-graph-user/2-3-Multi-Tenant/README.md)• [Call Azure REST APIs](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/blob/master/3-WebApp-multi-APIs/README.md)• [Protect web API](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/blob/master/4-WebApp-your-API/4-1-MyOrg/README.md)• [Protect multitenant web API](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/blob/master/4-WebApp-your-API/4-3-AnyOrg/Readme.md)• [Use App Roles for access control](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/blob/master/5-WebApp-AuthZ/5-1-Roles/README.md)• [Use Security Groups for access control](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/blob/master/5-WebApp-AuthZ/5-2-Groups/README.md)• [Deploy to Azure Storage and App Service](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/blob/master/6-Deploy-to-Azure/README.md)• [Active Directory Federation Services to Microsoft Entra migration](https://github.com/Azure-Samples/ms-identity-dotnet-adfs-to-aad) | [Microsoft.Identity.Web](/en-us/dotnet/api/microsoft-authentication-library-dotnet/confidentialclient) | • OpenID connect • Authorization code • On-Behalf-Of Flow (OBO) | [Quickstart](quickstart-web-app-dotnet-core-sign-in) | [Tutorial](tutorial-web-app-dotnet-prepare-app) |
| Blazor | • [Sign in users](https://github.com/Azure-Samples/ms-identity-docs-code-dotnet/tree/main/spa-blazor-wasm)• [Call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-blazor-server/tree/main/WebApp-graph-user/Call-MSGraph)• [Call web API](https://github.com/Azure-Samples/ms-identity-blazor-server/tree/main/WebApp-your-API/MyOrg) | [MSAL.NET](/en-us/entra/msal/dotnet) | Hybrid flow |  |  |
| Java Spring | • [Sign in users](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/4-spring-web-app/1-Authentication/sign-in)• [Call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/4-spring-web-app/2-Authorization-I/call-graph)• [Use App Roles for access control](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/4-spring-web-app/3-Authorization-II/roles)• [Use Groups for access control](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/4-spring-web-app/3-Authorization-II/groups)• [Protect a web API](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/4-spring-web-app/3-Authorization-II/protect-web-api)• [Deploy to Azure App Service](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/4-spring-web-app/4-Deployment/deploy-to-azure-app-service) | [MSAL Java](/en-us/java/api/com.microsoft.aad.msal4j) | Authorization code |  | [Tutorial](/en-us/azure/developer/java/spring-framework/configure-spring-boot-starter-java-app-with-azure-active-directory) |
| Java Servlets | • [Sign in users](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/3-java-servlet-web-app/1-Authentication/sign-in)• [Call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/3-java-servlet-web-app/2-Authorization-I/call-graph)• [Use App Roles for access control](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/3-java-servlet-web-app/3-Authorization-II/roles)• [Use Security Groups for access control](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/3-java-servlet-web-app/3-Authorization-II/groups)• [Deploy to Azure App Service](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/3-java-servlet-web-app/4-Deployment/deploy-to-azure-app-service) | [MSAL Java](/en-us/java/api/com.microsoft.aad.msal4j) | Authorization code | [Quickstart](quickstart-web-app-java-sign-in) |  |
| Node.js Express | • [Sign in users](https://github.com/Azure-Samples/ms-identity-javascript-nodejs-tutorial/blob/main/1-Authentication/1-sign-in/README.md)• [Express web application built with MSAL Node and Microsoft identity platform](https://github.com/Azure-Samples/ms-identity-node/blob/main/README.md)• [Call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-javascript-nodejs-tutorial/blob/main/2-Authorization/1-call-graph/README.md)• [Use App Roles for access control](https://github.com/Azure-Samples/ms-identity-javascript-nodejs-tutorial/blob/main/4-AccessControl/1-app-roles/README.md)• [Use Security Groups for access control](https://github.com/Azure-Samples/ms-identity-javascript-nodejs-tutorial/blob/main/4-AccessControl/2-security-groups/README.md)• [Deploy to Azure App Service](https://github.com/Azure-Samples/ms-identity-javascript-nodejs-tutorial/blob/main/3-Deployment/README.md) | [MSAL Node](/en-us/javascript/api/@azure/msal-node) | • Authorization code • Backend-for-Frontend (BFF) proxy | [Quickstart](quickstart-web-app-nodejs-sign-in) | [Tutorial](tutorial-v2-nodejs-webapp-msal) |
| Python Flask | • [Sign in users](https://github.com/Azure-Samples/ms-identity-docs-code-python/tree/main/flask-web-app)• [Template to sign in Microsoft Entra ID, and optionally call a downstream API (Microsoft Graph)](https://github.com/Azure-Samples/ms-identity-python-webapp) | [MSAL Python](/en-us/entra/msal/python) | Authorization code | [Quickstart](quickstart-web-app-python-flask) | [Tutorial](tutorial-web-app-python-register-app) |
| Python Django | • [Sign in users](https://github.com/Azure-Samples/ms-identity-docs-code-python/tree/main/django-web-app) | [MSAL Python](/en-us/entra/msal/python) | Authorization code |  |  |
| Ruby | • [Sign in users and call Microsoft Graph](https://github.com/microsoftgraph/msgraph-training-rubyrailsapp) | OmniAuth OAuth2 | Authorization code |  |  |

### Web API

The following samples show how to protect a web API with the Microsoft identity platform, and how to call a downstream API from the web API.

| Language /Platform | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| ASP.NET | • [Call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-aspnet-webapi-onbehalfof) | [MSAL.NET](/en-us/entra/msal/dotnet) | On-Behalf-Of (OBO) | [Quickstart](quickstart-web-api-aspnet-protect-api) |  |
| ASP.NET Core | • [Access control (protected routes) with the Microsoft identity platform](https://github.com/Azure-Samples/ms-identity-docs-code-dotnet/tree/main/web-api) | [MSAL.NET](/en-us/entra/msal/dotnet) | On-Behalf-Of (OBO) | [Quickstart](quickstart-web-api-aspnet-core-protect-api) | [Tutorial](tutorial-web-api-dotnet-register-app) |
| Java | • [Protect your Java Spring Boot web API with the Microsoft identity platform](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/4-spring-web-app/3-Authorization-II/protect-web-api) | [MSAL Java](/en-us/java/api/com.microsoft.aad.msal4j) | On-Behalf-Of (OBO) |  |  |
| Node.js | • [Protect a Node.js web API](https://github.com/Azure-Samples/ms-identity-javascript-tutorial/tree/main/3-Authorization-II/1-call-api) | [MSAL Node](/en-us/javascript/api/@azure/msal-node) | Authorization bearer |  |  |

### Desktop

The following samples show public client desktop applications that access the Microsoft Graph API, or your own web API in the name of the user. Apart from the *Desktop (Console) with Web Authentication Manager (WAM)* sample, all these client applications use the Microsoft Authentication Library (MSAL).

| Language /Platform | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| .NET Core | • [Call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-dotnet-desktop-tutorial/tree/master/1-Calling-MSGraph/1-1-AzureAD) • [Call Microsoft Graph with token cache](https://github.com/Azure-Samples/ms-identity-dotnet-desktop-tutorial/tree/master/2-TokenCache) • [Call Microsoft Graph with custom web UI HTML](https://github.com/Azure-Samples/ms-identity-dotnet-desktop-tutorial/tree/master/3-CustomWebUI/3-1-CustomHTML) • [Call Microsoft Graph with custom web browser](https://github.com/Azure-Samples/ms-identity-dotnet-desktop-tutorial/tree/master/3-CustomWebUI/3-2-CustomBrowser) • [Sign in users with device code flow](https://github.com/Azure-Samples/ms-identity-dotnet-desktop-tutorial/tree/master/4-DeviceCodeFlow)• [Call Microsoft Graph by signing in users using username/password](https://github.com/azure-samples/active-directory-dotnetcore-console-up-v2) | [MSAL.NET](/en-us/entra/msal/dotnet) | • Authorization code with PKCE  • Device code  • Resource owner password credentials |  |  |
| Java | • [Call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/2-client-side/Integrated-Windows-Auth-Flow) | [MSAL Java](/en-us/java/api/com.microsoft.aad.msal4j) | Integrated Windows authentication |  |  |
| Node.js | • [Sign in users](https://github.com/Azure-Samples/ms-identity-javascript-nodejs-desktop) | [MSAL Node](/en-us/javascript/api/@azure/msal-node) | Authorization code with PKCE | [Quickstart](quickstart-desktop-app-nodejs-electron-sign-in) | [Tutorial](tutorial-v2-nodejs-desktop) |
| Python | • [Sign in users](https://github.com/Azure-Samples/ms-identity-python-desktop) | [MSAL Python](/en-us/entra/msal/python) | Resource owner password credentials |  |  |
| Windows Presentation Foundation (WPF) | • [Sign in users and call Microsoft Graph](https://github.com/Azure-Samples/active-directory-dotnet-native-aspnetcore-v2/tree/master/2.%20Web%20API%20now%20calls%20Microsoft%20Graph)• [Windows Presentation Foundation (WPF) user sign-in, protected web API access (Microsoft Graph)](https://github.com/Azure-Samples/ms-identity-docs-code-dotnet/tree/main/desktop-wpf)• [Sign in users and call ASP.NET Core web API](https://github.com/Azure-Samples/active-directory-dotnet-native-aspnetcore-v2/tree/master/1.%20Desktop%20app%20calls%20Web%20API) • [Sign in users and call Microsoft Graph](https://github.com/azure-samples/active-directory-dotnet-desktop-msgraph-v2) | [MSAL.NET](/en-us/entra/msal/dotnet) | Authorization code with PKCE | [Quickstart](quickstart-desktop-app-uwp-sign-in) | [Tutorial](quickstart-desktop-app-wpf-sign-in) |

### Mobile

The following samples show public client mobile applications that access the Microsoft Graph API. These client applications use the Microsoft Authentication Library (MSAL).

| Language /Platform | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| .NET Core | • [Call Microsoft Graph using MAUI](https://github.com/Azure-Samples/ms-identity-dotnetcore-maui/tree/main/MauiAppBasic) • [Call Microsoft Graph using MAUI with broker](https://github.com/Azure-Samples/ms-identity-dotnetcore-maui/tree/main/MauiAppWithBroker) | [MSAL.NET](/en-us/entra/msal/dotnet) | Authorization code with PKCE |  |  |
| iOS | • [Call Microsoft Graph native](https://github.com/Azure-Samples/ms-identity-mobile-apple-swift-objc) | [MSAL iOS](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | Authorization code with PKCE | [Quickstart](quickstart-mobile-app-ios-sign-in) | [Tutorial](tutorial-v2-ios) |
| Java | • [Sign in users and call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-android-java) | [MSAL Android](https://github.com/AzureAD/microsoft-authentication-library-for-android) | Authorization code with PKCE | [Quickstart](quickstart-mobile-app-android-sign-in) | [Tutorial](tutorial-v2-android) |
| Kotlin | • [Sign in users and call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-android-kotlin) | [MSAL Android](https://github.com/AzureAD/microsoft-authentication-library-for-android) | Authorization code with PKCE |  |  |

### Service / daemon

The following samples show an application that accesses the Microsoft Graph API with its own identity (with no user).

| Language /Platform | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| .NET | • [.NET console app that accesses a protected web API](https://github.com/Azure-Samples/ms-identity-docs-code-dotnet/tree/main/console-daemon) • [Multitenant with Microsoft identity platform endpoint](https://github.com/Azure-Samples/ms-identity-aspnet-daemon-webapp) | [MSAL.NET](/en-us/entra/msal/dotnet) | Client credentials grant | [Quickstart](quickstart-daemon-dotnet-acquire-token) | [Tutorial](tutorial-v2-aspnet-daemon-web-app) |
| .NET Core | • [Call Microsoft Graph](https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2/tree/master/1-Call-MSGraph) • [Call web API](https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2/tree/master/2-Call-OwnApi) • [Using managed identity to call MSGraph](https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2/tree/master/5-Call-MSGraph-ManagedIdentity) • [Using managed identity to call an API](https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2/tree/master/6-Call-OwnApi-ManagedIdentity) • [Worker role calling an API](https://github.com/AzureAD/microsoft-identity-web/tree/master/tests/DevApps/ContosoWorker) | Microsoft.Identity.Web | Client credentials grant |  |  |
| Java | • [Call Microsoft Graph with Secret](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/1-server-side/msal-client-credential-secret) • [Call Microsoft Graph with Certificate](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/1-server-side/msal-client-credential-certificate) | [MSAL Java](/en-us/java/api/com.microsoft.aad.msal4j) | Client credentials grant | [Quickstart](quickstart-daemon-app-java-acquire-token) |  |
| Node.js | • [Call Microsoft Graph with secret](https://github.com/Azure-Samples/ms-identity-javascript-nodejs-console) | [MSAL Node](/en-us/javascript/api/@azure/msal-node) | Client credentials grant | [Quickstart](quickstart-console-app-nodejs-acquire-token) | [Tutorial](tutorial-v2-nodejs-console) |
| Python | • [Call Microsoft Graph with secret](https://github.com/Azure-Samples/ms-identity-python-daemon/tree/master/1-Call-MsGraph-WithSecret) • [Call Microsoft Graph with certificate](https://github.com/Azure-Samples/ms-identity-python-daemon/tree/master/2-Call-MsGraph-WithCertificate) | [MSAL Python](/en-us/entra/msal/python) | Client credentials grant | [Quickstart](quickstart-daemon-app-python-acquire-token) |  |

### Browserless (Headless)

The following sample shows a public client application running on a device without a web browser. The app can be a command-line tool, an app running on Linux or Mac, or an IoT application. The sample features an app accessing the Microsoft Graph API, in the name of a user who signs in interactively on another device (such as a mobile phone). This client application uses the Microsoft Authentication Library (MSAL).

| Language /Platform | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| .NET Core | • [Invoke protected API from text-only device](https://github.com/azure-samples/active-directory-dotnetcore-devicecodeflow-v2) | [MSAL.NET](/en-us/entra/msal/dotnet) | Device code |  |  |
| Java | • [Sign in users and invoke protected API from text-only device](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/2-client-side/Device-Code-Flow) | [MSAL Java](/en-us/java/api/com.microsoft.aad.msal4j) | Device code |  |  |
| Python | • [Call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-python-devicecodeflow) | [MSAL Python](/en-us/entra/msal/python) | Device code |  |  |

### Azure Functions as web APIs

The following samples show how to protect an Azure Function using HttpTrigger and exposing a web API with the Microsoft identity platform, and how to call a downstream API from the web API.

| Language /Platform | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| Python | • [Python Azure function web API secured by Microsoft Entra ID](https://github.com/Azure-Samples/ms-identity-python-webapi-azurefunctions) | [MSAL Python](/en-us/entra/msal/python) | Authorization code |  |  |

### Microsoft Teams applications

The following sample illustrates Microsoft Teams Tab application that signs in users. Additionally it demonstrates how to call Microsoft Graph API with the user's identity using the Microsoft Authentication Library (MSAL).

| Language /Platform | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| Node.js | • [Teams Tab app: single sign-on (SSO) and call Microsoft Graph](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/nodejs) | [MSAL Node](/en-us/javascript/api/@azure/msal-node) | On-Behalf-Of (OBO) |  |  |

### Multitenant SaaS

The following samples show how to configure your application to accept sign-ins from any Microsoft Entra tenant. Configuring your application to be *multitenant* means that you can offer a **Software as a Service** (SaaS) application to many organizations, allowing their users to be able to sign-in to your application after providing consent.

| Language /Platform | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| ASP.NET Core | • [ASP.NET Core MVC web application calls Microsoft Graph API](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/tree/master/2-WebApp-graph-user/2-3-Multi-Tenant) • [ASP.NET Core MVC web application calls ASP.NET Core web API](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/tree/master/4-WebApp-your-API/4-3-AnyOrg) | [MSAL.NET](/en-us/entra/msal/dotnet) | • OpenID connect  • Authorization code |  |  |

# [By language/framework](#tab/framework)
### C#

The following samples show how to build applications using the C# language and frameworks

#### .NET Core

| App type | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| Desktop | • [Call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-dotnet-desktop-tutorial/tree/master/1-Calling-MSGraph/1-1-AzureAD) • [Call Microsoft Graph with token cache](https://github.com/Azure-Samples/ms-identity-dotnet-desktop-tutorial/tree/master/2-TokenCache) • [Call Microsoft Graph with custom web UI HTML](https://github.com/Azure-Samples/ms-identity-dotnet-desktop-tutorial/tree/master/3-CustomWebUI/3-1-CustomHTML) • [Call Microsoft Graph with custom web browser](https://github.com/Azure-Samples/ms-identity-dotnet-desktop-tutorial/tree/master/3-CustomWebUI/3-2-CustomBrowser) • [Sign in users with device code flow](https://github.com/Azure-Samples/ms-identity-dotnet-desktop-tutorial/tree/master/4-DeviceCodeFlow)• [Call Microsoft Graph by signing in users using username/password](https://github.com/azure-samples/active-directory-dotnetcore-console-up-v2) | [MSAL.NET](/en-us/entra/msal/dotnet) | • Authorization code with PKCE  • Device code |  |  |
| Mobile | • [Call Microsoft Graph using MAUI](https://github.com/Azure-Samples/ms-identity-dotnetcore-maui/tree/main/MauiAppBasic) • [Call Microsoft Graph using MAUI with broker](https://github.com/Azure-Samples/ms-identity-dotnetcore-maui/tree/main/MauiAppWithBroker) | [MSAL.NET](/en-us/entra/msal/dotnet) | Authorization code with PKCE |  |  |
| Service/ |

daemon • [Call Microsoft Graph](https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2/tree/master/1-Call-MSGraph) • [Call web API](https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2/tree/master/2-Call-OwnApi) • [Using managed identity and Azure key vault](https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2/tree/master/3-Using-KeyVault) | [MSAL.NET](/en-us/entra/msal/dotnet) | Client credentials grant |  |  || Headless | • [Invoke protected API from text-only device](https://github.com/azure-samples/active-directory-dotnetcore-devicecodeflow-v2) | [MSAL.NET](/en-us/entra/msal/dotnet) | Device code |  |  |

---

#### ASP.NET

| App type | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| Web application | • [Microsoft Graph Training Sample](https://github.com/microsoftgraph/msgraph-training-aspnetmvcapp) • [Sign in users and call Microsoft Graph with admin restricted scope](https://github.com/azure-samples/active-directory-dotnet-admin-restricted-scopes-v2) | [MSAL.NET](/en-us/entra/msal/dotnet) | • OpenID connect  • Authorization code | [Quickstart](https://github.com/AzureAdQuickstarts/AppModelv2-WebApp-OpenIDConnect-DotNet) |  |
| Web API | • [Call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-aspnet-webapi-onbehalfof) | [MSAL.NET](/en-us/entra/msal/dotnet) | On-Behalf-Of (OBO) |  |  |
| Service/daemon | • [Multitenant with Microsoft identity platform endpoint](https://github.com/Azure-Samples/ms-identity-aspnet-daemon-webapp) | [MSAL.NET](/en-us/entra/msal/dotnet) | Client credentials grant |  |  |

#### ASP.NET Core

| App type | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| Web application | • [Sign in users](https://github.com/Azure-Samples/ms-identity-docs-code-dotnet/tree/main/web-app-aspnet)• [Call Microsoft Graph](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/blob/master/2-WebApp-graph-user/2-1-Call-MSGraph/README.md)• [Customize token cache](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/blob/master/2-WebApp-graph-user/2-2-TokenCache/README.md)• [Use the Conditional Access auth context to perform step-up authentication](https://github.com/Azure-Samples/ms-identity-dotnetcore-ca-auth-context-app/blob/main/README.md)• [Call Graph (multitenant)](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/blob/master/2-WebApp-graph-user/2-3-Multi-Tenant/README.md)• [Call Azure REST APIs](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/blob/master/3-WebApp-multi-APIs/README.md)• [Protect web API](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/blob/master/4-WebApp-your-API/4-1-MyOrg/README.md)• [Protect multitenant web API](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/blob/master/4-WebApp-your-API/4-3-AnyOrg/Readme.md)• [Use App Roles for access control](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/blob/master/5-WebApp-AuthZ/5-1-Roles/README.md)• [Use Security Groups for access control](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/blob/master/5-WebApp-AuthZ/5-2-Groups/README.md)• [Deploy to Azure Storage and App Service](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/blob/master/6-Deploy-to-Azure/README.md)• [Active Directory Federation Services to Microsoft Entra migration](https://github.com/Azure-Samples/ms-identity-dotnet-adfs-to-aad)• [Active Directory Federation Services to Microsoft Entra migration](https://github.com/Azure-Samples/ms-identity-dotnet-adfs-to-aad)[Use the Conditional Access auth context to perform step-up authentication](https://github.com/Azure-Samples/ms-identity-dotnetcore-ca-auth-context-app/blob/main/README.md)[Advanced Token Cache Scenarios](https://github.com/Azure-Samples/ms-identity-dotnet-advanced-token-cache) | [Microsoft.Identity.Web](/en-us/dotnet/api/microsoft-authentication-library-dotnet/confidentialclient) | • OpenID connect  • Authorization code • On-Behalf-Of | [Quickstart](quickstart-web-app-dotnet-core-sign-in) | [Tutorial](tutorial-web-app-dotnet-prepare-app) |
| Web API | • [Sign in users and call Microsoft Graph](https://github.com/Azure-Samples/active-directory-dotnet-native-aspnetcore-v2/tree/master/2.%20Web%20API%20now%20calls%20Microsoft%20Graph) | [MSAL.NET](/en-us/entra/msal/dotnet) | On-Behalf-Of (OBO) | [Quickstart](quickstart-web-api-aspnet-core-protect-api) | [Tutorial](tutorial-web-api-dotnet-register-app) |
| Multitenant SaaS | • [ASP.NET Core MVC web application calls Microsoft Graph API](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/tree/master/2-WebApp-graph-user/2-3-Multi-Tenant)• [ASP.NET Core MVC web application calls ASP.NET Core web API](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/tree/master/4-WebApp-your-API/4-3-AnyOrg) | [MSAL.NET](/en-us/entra/msal/dotnet) | OpenID connect |  |  |

#### Blazor

| App type | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| Single-page application | • [Sign in users](https://github.com/Azure-Samples/ms-identity-docs-code-dotnet/tree/main/spa-blazor-wasm)• [Call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-blazor-wasm/blob/main/WebApp-graph-user/Call-MSGraph/README.md)• [Deploy to Azure App Service](https://github.com/Azure-Samples/ms-identity-blazor-wasm/blob/main/Deploy-to-Azure/README.md) | [MSAL.js](/en-us/javascript/api/overview/msal-overview) | Implicit Flow | [Quickstart](quickstart-single-page-app-blazor-wasm-sign-in) |  |
| Web application | • [Sign in users](https://github.com/Azure-Samples/ms-identity-blazor-server/tree/main/WebApp-OIDC/MyOrg) • [Call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-blazor-server/tree/main/WebApp-graph-user/Call-MSGraph) • [Call web API](https://github.com/Azure-Samples/ms-identity-blazor-server/tree/main/WebApp-your-API/MyOrg) | [MSAL.NET](/en-us/entra/msal/dotnet) | Implicit/Hybrid flow |  |  |

### iOS

The following samples show how to build applications for the iOS platform.

| App type | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| Mobile | • [Call Microsoft Graph native](https://github.com/Azure-Samples/ms-identity-mobile-apple-swift-objc) | [MSAL iOS](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | Authorization code with PKCE | [Quickstart](quickstart-mobile-app-ios-sign-in) | [Tutorial](tutorial-v2-ios) |

### JavaScript

#### Vanilla JavaScript

The following samples show how to build applications for the JavaScript language and platform.

| App type | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| Single-page application | • [Sign in users](https://github.com/Azure-Samples/ms-identity-docs-code-javascript/tree/main/vanillajs-spa) • [Call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-javascript-tutorial/tree/main/2-Authorization-I/1-call-graph/README.md)• [Call Node.js web API](https://github.com/Azure-Samples/ms-identity-javascript-tutorial/tree/main/3-Authorization-II/1-call-api/README.md)• [Deploy to Azure Storage and App Service](https://github.com/Azure-Samples/ms-identity-javascript-tutorial/tree/main/4-Deployment/README.md) | [MSAL.js](/en-us/javascript/api/overview/msal-overview) | Authorization code with PKCE | [Quickstart](quickstart-single-page-app-sign-in) |  |

#### Angular

| App type | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| Single-page application | • [Sign in users](https://github.com/Azure-Samples/ms-identity-docs-code-javascript/tree/main/angular-spa) | [MSAL Angular](/en-us/javascript/api/@azure/msal-angular) | Authorization code with PKCE | [Quickstart](quickstart-single-page-app-angular-sign-in) | [Tutorial](tutorial-v2-angular-auth-code) |

#### Node.js

| App type | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| Web API | • [Protect a Node.js web API](https://github.com/Azure-Samples/ms-identity-javascript-tutorial/tree/main/3-Authorization-II/1-call-api) | [MSAL Node](/en-us/javascript/api/@azure/msal-node) | Authorization bearer |  |  |
| Desktop | • [Sign in users](https://github.com/Azure-Samples/ms-identity-javascript-nodejs-desktop) | [MSAL Node](/en-us/javascript/api/@azure/msal-node) | Authorization code with PKCE |  | [Tutorial](tutorial-v2-nodejs-desktop) |
| Service, daemon | • [Call Microsoft Graph with secret](https://github.com/Azure-Samples/ms-identity-javascript-nodejs-console) | [MSAL Node](/en-us/javascript/api/@azure/msal-node) | Client credentials grant | [Quickstart](quickstart-console-app-nodejs-acquire-token) |  |
| Microsoft Teams applications | • [Teams Tab app: single sign-on (SSO) and call Microsoft Graph](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/nodejs) | [MSAL Node](/en-us/javascript/api/@azure/msal-node) | On-Behalf-Of (OBO) |  |  |

#### Node.js (Express)

| App type | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| Web application | • [Sign in users](https://github.com/Azure-Samples/ms-identity-javascript-nodejs-tutorial/blob/main/1-Authentication/1-sign-in/README.md) • [Call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-javascript-nodejs-tutorial/blob/main/2-Authorization/1-call-graph/README.md) • [Deploy to Azure App Service](https://github.com/Azure-Samples/ms-identity-javascript-nodejs-tutorial/blob/main/3-Deployment/README.md) • [Use App Roles for access control](https://github.com/Azure-Samples/ms-identity-javascript-nodejs-tutorial/blob/main/4-AccessControl/1-app-roles/README.md) • [Use Security Groups for access control](https://github.com/Azure-Samples/ms-identity-javascript-nodejs-tutorial/blob/main/4-AccessControl/2-security-groups/README.md) • [Express web application built with MSAL Node and Microsoft identity platform](https://github.com/Azure-Samples/ms-identity-node) | [MSAL Node](/en-us/javascript/api/@azure/msal-node) | Authorization code | [Quickstart](quickstart-web-app-nodejs-sign-in) | [Tutorial](tutorial-v2-nodejs-webapp-msal) |

#### React

| App type | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| Single-page application | • [Sign in users](https://github.com/Azure-Samples/ms-identity-docs-code-javascript/tree/main/react-spa) | [MSAL React](/en-us/javascript/api/@azure/msal-react) | • Authorization code with PKCE | [Quickstart](quickstart-single-page-app-react-sign-in) | [Tutorial](tutorial-single-page-app-react-prepare-app) |

### Java

The following samples show how to build applications for the Java language and platform.

| App type | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| Web API | • [Sign in users](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/4-spring-web-app/3-Authorization-II/protect-web-api) | [MSAL Java](/en-us/java/api/com.microsoft.aad.msal4j) | On-Behalf-Of (OBO) |  |  |
| Desktop | • [Call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/2-client-side/Integrated-Windows-Auth-Flow) | [MSAL Java](/en-us/java/api/com.microsoft.aad.msal4j) | Integrated Windows authentication |  |  |
| Mobile | • [Sign in users and call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-android-java) | [MSAL Android](https://github.com/AzureAD/microsoft-authentication-library-for-android) | Authorization code with PKCE |  |  |
| Service/daemon | • [Call Microsoft Graph with Secret](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/1-server-side/msal-client-credential-secret) • [Call Microsoft Graph with Certificate](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/1-server-side/msal-client-credential-certificate) | [MSAL Java](/en-us/java/api/com.microsoft.aad.msal4j) | Client credentials grant | [Quickstart](quickstart-daemon-app-java-acquire-token) |  |

#### Java Spring

| App type | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| Web application | Microsoft Entra Spring Boot Starter Series  • [Sign in users](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/4-spring-web-app/1-Authentication/sign-in) • [Call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/4-spring-web-app/2-Authorization-I/call-graph) • [Use App Roles for access control](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/4-spring-web-app/3-Authorization-II/roles) • [Use Groups for access control](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/4-spring-web-app/3-Authorization-II/groups) • [Deploy to Azure App Service](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/4-spring-web-app/4-Deployment/deploy-to-azure-app-service) • [Protect a web API](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/4-spring-web-app/3-Authorization-II/protect-web-api) | • [MSAL Java](/en-us/java/api/com.microsoft.aad.msal4j) • Microsoft Entra ID Boot Starter | Authorization code |  | [Tutorial](/en-us/azure/developer/java/spring-framework/configure-spring-boot-starter-java-app-with-azure-active-directory) |

#### Java Servlet

| App type | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| Web application | Spring-less Servlet Series  • [Sign in users](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/3-java-servlet-web-app/1-Authentication/sign-in) • [Call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/3-java-servlet-web-app/2-Authorization-I/call-graph) • [Use App Roles for access control](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/3-java-servlet-web-app/3-Authorization-II/roles) • [Use Security Groups for access control](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/3-java-servlet-web-app/3-Authorization-II/groups) • [Deploy to Azure App Service](https://github.com/Azure-Samples/ms-identity-msal-java-samples/tree/main/3-java-servlet-web-app/4-Deployment/deploy-to-azure-app-service) | [MSAL Java](/en-us/java/api/com.microsoft.aad.msal4j) | Authorization code |  |  |

### Python

The following samples show how to build applications for the Python language and platform.

| App type | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| Azure Functions as web APIs | • [Python Azure function web API secured by Microsoft Entra ID](https://github.com/Azure-Samples/ms-identity-python-webapi-azurefunctions) | [MSAL Python](/en-us/entra/msal/python) | Authorization code |  |  |
| Desktop | • [Sign in users](https://github.com/Azure-Samples/ms-identity-python-desktop) | [MSAL Python](/en-us/entra/msal/python) | Resource owner password credentials |  |  |
| Headless | • [Call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-python-devicecodeflow) | [MSAL Python](/en-us/entra/msal/python) | Device code |  |  |
| Daemon | • [Call Microsoft Graph with secret](https://github.com/Azure-Samples/ms-identity-python-daemon/tree/master/1-Call-MsGraph-WithSecret) • [Call Microsoft Graph with certificate](https://github.com/Azure-Samples/ms-identity-python-daemon/tree/master/2-Call-MsGraph-WithCertificate) | [MSAL Python](/en-us/entra/msal/python) | Client credentials grant | [Quickstart](quickstart-daemon-app-python-acquire-token) |  |

#### Flask

| App type | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| Web application | • [Sign in users](https://github.com/Azure-Samples/ms-identity-docs-code-python/tree/main/flask-web-app)• [A template to sign in Microsoft Entra ID, and optionally call a downstream API (Microsoft Graph)](https://github.com/Azure-Samples/ms-identity-python-webapp) | [MSAL Python](/en-us/entra/msal/python) | Authorization code | [Quickstart](quickstart-web-app-python-flask) | [Tutorial](tutorial-web-app-python-register-app) |

#### Django

| App type | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| Web application | • [Sign in users](https://github.com/Azure-Samples/ms-identity-docs-code-python/tree/main/django-web-app) • [Integrating Microsoft Entra ID with a Python web application written in Django](https://github.com/Azure-Samples/ms-identity-python-webapp-django) | [MSAL Python](/en-us/entra/msal/python/) | Authorization code |  |  |

### Kotlin

The following samples show how to build applications with Kotlin.

| App type | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| Mobile | • [Sign in users and call Microsoft Graph](https://github.com/Azure-Samples/ms-identity-android-kotlin) | [MSAL Android](https://github.com/AzureAD/microsoft-authentication-library-for-android) | Authorization code with PKCE |  |  |

### Ruby

The following samples show how to build applications with Ruby.

| App type | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| Web application | Graph Training  • [Sign in users and call Microsoft Graph](https://github.com/microsoftgraph/msgraph-training-rubyrailsapp) | OmniAuth OAuth2 | Authorization code |  |  |

### Windows Presentation Foundation (WPF)

The following samples show how to build applications with Windows Presentation Foundation (WPF).

| App type | Code sample(s)on GitHub | Authlibraries | Auth flow | Quickstart | Tutorial |
| --- | --- | --- | --- | --- | --- |
| Desktop | • [Sign in users and call Microsoft Graph](https://github.com/Azure-Samples/active-directory-dotnet-native-aspnetcore-v2/tree/master/2.%20Web%20API%20now%20calls%20Microsoft%20Graph) | [MSAL.NET](/en-us/entra/msal/dotnet) | Authorization code with PKCE |  |  |
| Desktop | • [Sign in users and call ASP.NET Core web API](https://github.com/Azure-Samples/active-directory-dotnet-native-aspnetcore-v2/tree/master/1.%20Desktop%20app%20calls%20Web%20API) • [Sign in users and call Microsoft Graph](https://github.com/azure-samples/active-directory-dotnet-desktop-msgraph-v2) | [MSAL.NET](/en-us/entra/msal/dotnet/) | Authorization code with PKCE | [Quickstart](quickstart-desktop-app-uwp-sign-in) | [Tutorial](quickstart-desktop-app-wpf-sign-in) |
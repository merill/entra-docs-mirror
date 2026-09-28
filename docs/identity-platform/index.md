---
layout: Hub
title: Microsoft identity platform documentation - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/
summary: >
  Use the Microsoft identity platform and our open-source authentication libraries to sign in users with Microsoft Entra accounts, Microsoft personal accounts, and social accounts like Facebook and Google. Protect your web APIs and access protected APIs like Microsoft Graph to work with your users' and organization's data.
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: 'Use Microsoft Entra with OAuth 2.0 and OpenID Connect (OIDC) to protect the apps and web APIs you build. Learn how to sign in users and manage their access through our quickstarts, tutorials, code samples, and API reference documentation. '
manager: dougeby
ms.date: 2025-02-11T00:00:00.0000000Z
ms.topic: hub-page
locale: en-us
document_id: 039b10ff-037e-2601-382a-c623794bd411
document_version_independent_id: afd53183-ada3-6ccc-51c3-93fb1b547054
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/index.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: hub
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/index
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/index.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: 0aa090fd-f61f-fdad-c23b-f2fda288f8c9
---

# Microsoft identity platform documentation

Use the Microsoft identity platform and our open-source authentication libraries to sign in users with Microsoft Entra accounts, Microsoft personal accounts, and social accounts like Facebook and Google. Protect your web APIs and access protected APIs like Microsoft Graph to work with your users' and organization's data. 

![](/en-us/media/hubs/shared/icon-overview.svg?branch=main)

Overview
[What is the Microsoft identity platform?](v2-overview)

![](/en-us/media/hubs/shared/icon-concept.svg?branch=main)

Concept
[Authentication and authorization basics](authentication-vs-authorization)

![](/en-us/media/hubs/shared/icon-concept.svg?branch=main)

Concept
[App types and authentication flows](authentication-flows-app-scenarios)

![](/en-us/media/hubs/shared/icon-sample.svg?branch=main)

sample
[Code samples](sample-v2-code)

![](/en-us/media/hubs/shared/icon-whats-new.svg?branch=main)

What's new
[What's new in docs](whats-new-docs)

![](/en-us/media/hubs/shared/icon-concept.svg?branch=main)

Concept
[OAuth 2.0 and OpenID Connect (OIDC)](v2-protocols)

![](/en-us/media/hubs/shared/icon-concept.svg?branch=main)

Concept
[Migrate apps to MSAL](msal-migration)

![](/en-us/media/hubs/shared/icon-quickstart.svg?branch=main)

Quickstart
[Register an application](quickstart-register-app)

## Authentication and authorization for any app

Focus on documentation for the app you're building or extending with identity and access management (IAM) support by selecting its type.

![](media/hub/app-type-spa.svg)[Single-page app (SPA)](index-spa)
A web app whose code is downloaded and run in the browser itself.

![](media/hub/app-type-web.svg)[Web app](index-web-app)
A traditional, or "classic," web app whose code runs on a server, returning page data for the browser to render.

![](media/hub/app-type-api.svg)[Web API](index-web-api)
A RESTful web service accessed by apps or other web APIs, typically to work with data served by the API.

![](media/hub/app-type-desktop.svg)[Desktop app](index-desktop)
Apps with a user interface (UI) whose code runs on a user's desktop, laptop, or notebook computer.

![](media/hub/app-type-mobile.svg)[Mobile app](index-mobile)
Apps with a UI whose code runs on a user's phone, tablet, or other mobile device.

![](media/hub/app-type-daemon-console.svg)[Background service, daemon, or script](index-service)
An app or script without a UI that performs non-interactive tasks like server-to-server communication or scheduled jobs.

## Get started

Quick access to guidance on adding core IAM features to your apps and best practices for keeping your apps secure and available.

### Sign in users

- [Single-page web app (SPA)](quickstart-single-page-app-sign-in)
- [Web app](quickstart-web-app-dotnet-core-sign-in)
- [Desktop app](quickstart-desktop-app-nodejs-electron-sign-in)
- [Mobile app](quickstart-mobile-app-android-sign-in)

### Protect a web API

- [Configure an app to expose a web API](quickstart-configure-app-expose-web-apis)
- [Build a protected web API](web-api-tutorial-01-register-app)
- [Call an API from a non-interactive app or script](quickstart-web-api-aspnet-protect-api)

### Test and deploy apps

- [Build a test environment](test-setup-environment)
- [Run integration tests](test-automate-integration-testing)

### Build for security and resilience

- [Build Zero Trust-ready apps](zero-trust-for-developers)
- [Prevent an over-privileged app](secure-least-privileged-access)
- [Build auth resilience into your apps](../architecture/resilience-app-development-overview?toc=/azure/active-directory/develop/toc.json&amp;bc=/azure/active-directory/develop/breadcrumb/toc.json)

## Microsoft authentication libraries

The open-source Microsoft Authentication Library (MSAL) is built and supported by Microsoft. We recommend MSAL for any app that uses the Microsoft identity platform for authentication and authorization. 

![](/en-us/media/logos/logo_Csharp.svg)

[.NET](/en-us/entra/msal/dotnet/)

![](media/hub/android.svg)

[Android](https://github.com/AzureAD/microsoft-authentication-library-for-android)

![](media/hub/angular.svg)

[Angular](/en-us/javascript/api/%40azure/msal-angular/)

![](/en-us/media/logos/logo_ios.svg)

[iOS & macOS](https://github.com/AzureAD/microsoft-authentication-library-for-objc)

![](/en-us/media/logos/logo_java.svg)

[Java](/en-us/java/api/com.microsoft.aad.msal4j)

![](/en-us/media/logos/logo_js.svg)

[JavaScript](/en-us/javascript/api/overview/msal-overview)

![](media/hub/node.svg)

[Node.js](/en-us/javascript/api/%40azure/msal-node/)

![](/en-us/media/logos/logo_python.svg)

[Python](/en-us/entra/msal/python/)

![](media/hub/react.svg)

[React](/en-us/javascript/api/%40azure/msal-react/)

### Authenticate partners and customers

Sign in users from partner organizations in a business-to-business (B2B) scenario or create custom sign-up and sign-in experiences for your customers in a business-to-customer (B2C) scenario. 

- [External Identities documentation](../external-id/)

### Connect to Microsoft Graph

Programmatic access to organizational, user, and app data stored in Microsoft Entra ID. Call Microsoft Graph from your app to create and manage Microsoft Entra users and groups, get, and modify your users' data like their profiles, calendars, email, and more. 

- [Microsoft Graph API documentation](/en-us/graph/overview?toc=/azure/active-directory/develop/toc.json&amp;bc=/azure/active-directory/develop/breadcrumb/toc.json)

### Manage and market your apps

Make existing SaaS apps like Dropbox, Salesforce, and ServiceNow available to your organization's users, configure single sign-on (SSO), and manage security. Or, become an independent software vendor (ISV) by publishing your own SaaS app for use by \*other\* organizations that use Microsoft Entra ID. 

- [App management documentation](../identity/enterprise-apps/what-is-application-management)

### Manage app users and their access

Automatically create user identities and their roles in your organization's SaaS apps. HR-driven provisioning, System for Cross-domain Identity Management (SCIM), and more.

- [App user and role provisioning documentation](../identity/app-provisioning/user-provisioning)
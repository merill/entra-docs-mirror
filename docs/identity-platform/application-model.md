---
layout: Conceptual
title: Application model - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/application-model
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn about the process of registering your application so it can integrate with the Microsoft identity platform.
manager: pmwongera
ms.custom: 
ms.date: 2024-04-26T00:00:00.0000000Z
ms.reviewer: jmprieur, sureshja, ludwignick
ms.topic: concept-article
locale: en-us
document_id: 882c6669-2244-1cb1-5315-aa5feec7c95b
document_version_independent_id: 697dfa71-6336-ebf6-b532-74144e62a87b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/application-model.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/application-model
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/application-model.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: 103e6cd2-4bec-eb4e-533c-dce35901c1bf
---

# Application model - Microsoft identity platform | Microsoft Learn

Applications can sign in users themselves or delegate sign-in to an identity provider. This article discusses the steps that are required to register an application with the Microsoft identity platform.

## Register an application

For an identity provider to know that a user has access to a particular app, both the user and the application must be registered with the identity provider. When you register your application with Microsoft Entra ID, you're providing an identity configuration for your application that allows it to integrate with the Microsoft identity platform. Registering the app also allows you to:

- Customize the branding of your application in the sign-in dialog box. This branding is important because signing in is the first experience a user will have with your app.
- Decide if you want to allow users to sign in only if they belong to your organization. This architecture is known as a single-tenant application. Or, you can allow users to sign in by using any work or school account, which is known as a multitenant application. You can also allow personal Microsoft accounts or a social account from LinkedIn, Google, and so on.
- Request scope permissions. For example, you can request the "user.read" scope, which grants permission to read the profile of the signed-in user.
- Define scopes that define access to your web API. Typically, when an app wants to access your API, it will need to request permissions to the scopes you define.
- Share a secret with the Microsoft identity platform that proves the app's identity. Using a secret is relevant in the case where the app is a confidential client application. A confidential [client application](developer-glossary#client-application) is an application that can hold credentials securely, like a [web client](developer-glossary#web-client). A trusted back-end server is required to store the credentials.

After the app is registered, it's given a unique identifier that it shares with the Microsoft identity platform when it requests tokens. If the app is a confidential client application, it will also share the secret or the public key depending on whether certificates or secrets were used.

The Microsoft identity platform represents applications by using a model that fulfills two main functions:

- Identify the app by the authentication protocols it supports.
- Provide all the identifiers, URLs, secrets, and related information that are needed to authenticate.

The Microsoft identity platform:

- Holds all the data required to support authentication at runtime.
- Holds all the data for deciding what resources an app might need to access, and under what circumstances a given request should be fulfilled.
- Provides infrastructure for implementing app provisioning within the app developer's tenant, and to any other Microsoft Entra tenant.
- Handles user consent during token request time and facilitates the dynamic provisioning of apps across tenants.

[*Consent*](developer-glossary#consent) is the process of a resource owner granting authorization for a client application to access protected resources, under specific permissions, on behalf of the resource owner. The Microsoft identity platform enables:

- Users and administrators to dynamically grant or deny consent for the app to access resources on their behalf.
- Administrators to ultimately decide what apps are allowed to do and which users can use specific apps, and how the directory resources are accessed.

## Multitenant apps

Important

Multitenant applications (MTAs) don't function across cloud boundaries due to the segregation of service principal authorities within each cloud. For instance, if the application object is hosted in the commercial cloud, the associated service principal is created locally during customer onboarding. This process fails when crossing cloud boundaries because the authority URLs differ (e.g., `.com` vs. `.us`), causing an incompatibility.

In the Microsoft identity platform, an [application object](developer-glossary#application-object) describes an application. At deployment time, the Microsoft identity platform uses the application object as a blueprint to create a [service principal](developer-glossary#service-principal-object), which represents a concrete instance of an application within a directory or tenant. The service principal defines what the app can actually do in a specific target directory, who can use it, what resources it has access to, and so on. The Microsoft identity platform creates a service principal from an application object through consent.

The following diagram shows a simplified Microsoft identity platform provisioning flow driven by consent. It shows two tenants: *A* and *B*.

- *Tenant A* owns the application.
- *Tenant B* is instantiating the application via a service principal.

![Diagram that shows a simplified provisioning flow driven by consent.](media/authentication-scenarios/simplified-provisioning-flow-consent-driven.svg)

In this provisioning flow:

1. A user from tenant B attempts to sign in with the app. The authorization endpoint requests a token for the application.
2. The user credentials are acquired and verified for authentication.
3. The user is prompted to provide consent for the app to gain access to tenant B.
4. The Microsoft identity platform uses the application object in tenant A as a blueprint for creating a service principal in tenant B.
5. The user receives the requested token.

You can repeat this process for more tenants. Tenant A retains the blueprint for the app (application object). Users and admins of all the other tenants where the app is given consent keep control over what the application is allowed to do via the corresponding service principal object in each tenant. For more information, see [Application and service principal objects in the Microsoft identity platform](app-objects-and-service-principals).
---
layout: Conceptual
title: Microsoft Entra External ID deployment guide for authentication and access control architecture - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/deployment-external-authentication-access-control
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra-external-id
manager: martinco
description: Learn about authentication protocol endpoints, extension design, event handler details, and more in Microsoft Entra External ID.
ms.topic: concept-article
ms.date: 2025-05-22T00:00:00.0000000Z
ms.reviewer: gasinh
locale: en-us
document_id: 64af8f28-3175-6430-75d9-fbe2e7329286
document_version_independent_id: 64af8f28-3175-6430-75d9-fbe2e7329286
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/deployment-external-authentication-access-control.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/deployment-external-authentication-access-control
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/deployment-external-authentication-access-control.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: 16f8fd91-1f6e-760d-fa7c-566724af49fb
---

# Microsoft Entra External ID deployment guide for authentication and access control architecture - Microsoft Entra | Microsoft Learn

Authentication helps verify identity, and access control is a process of authorizing users and groups to access resources.

## Authentication protocol and endpoints: customer apps and authentication

Customer-facing applications can authenticate with Microsoft Entra External ID using Open Authorization 2.0 ([OAuth 2](../identity-platform/v2-protocols)) or Security Assertion Markup Language 2.0 ([SAML 2](https://en.wikipedia.org/wiki/SAML_2.0)).

The following table summarizes the application integration options for OAuth 2 and OpenID Connect (OIDC).

| Application type | Authentication initiator | Authentication options |
| --- | --- | --- |
| Native client: mobile and platform apps | User interacting with the app | - [Native authentication](../external-id/customers/concept-native-authentication) with Microsoft Authentication Libraries (MSAL)  - [Authorization code](../identity-platform/v2-oauth2-auth-code-flow) - [Hybrid](../identity-platform/v2-oauth2-auth-code-flow) |
| Web applications running on a server | A user interacting with the application | Authorization code |
| Web application running on the browser, a single-page application (SPA) | A user interacting with the application | - [Native authentication](../external-id/customers/concept-native-authentication) with MSAL  - Authorization code  - [Hybrid or implicit](../identity-platform/v2-oauth2-auth-code-flow), with proof key for code exchange (PKCE) |
| Web application running on a server: middleware | An application on behalf of a user | [On behalf of](../identity-platform/v2-oauth2-on-behalf-of-flow) |
| Web application running on a server | Headless service or application | [Client credentials](../identity-platform/v2-oauth2-client-creds-grant-flow) |
| Limited input device | User interacting with the device | [Device code flow](../identity-platform/v2-oauth2-on-behalf-of-flow) |

Note

Regarding **on behalf of**, the sub (subject) claim presented to the middleware and the back end differ. See payloads in [access token claims reference](../identity-platform/access-token-claims-reference). The subject is a pairwise identifier unique to an application ID. If a user signs in to two applications using different client IDs, the applications receive two subject claim values. Use if the two values depend on architecture and privacy requirements. Note the object identifier (OID) claim, which remains the same across applications in a tenant.

The following diagram of OAuth 2 and OIDC flows shows OAuth application integration options.

[![Diagram of OAuth 2 and OIDC flow with OAuth app integration options.](media/deployment-external/oauth-flows.png)](media/deployment-external/oauth-flows-expanded.png#lightbox)

Application integration options for SAML are based on the service-provider (SP) initiated flow. The SAML flow is detailed in authentication with Microsoft Entra ID.

### Custom authentication extension design

Use custom authentication extensions to customize the Microsoft Entra authentication experience by integrating with external systems. In the following diagram, note the progress from sign-up to the returned token.

See the [custom authentication extensions overview](../identity-platform/custom-extension-overview).

The following diagram shows a custom authentication flow.

[![Diagram of a custom extension flow.](media/deployment-external/custom-authentication-extension.png)](media/deployment-external/custom-authentication-extension-expanded.png#lightbox)

### API and event handler considerations

Implement the API as a dedicated API, or by using an [API Facade](https://en.wikipedia.org/wiki/Facade_pattern) using a middleware solution like an API manager. Each custom extension has a strictly typed API contract. Give attention to definitions.

Learn more about the [authenticationEventListener resource type](/en-us/graph/api/resources/authenticationeventlistener?view=graph-rest-beta&amp;preserve-view=true).

Note

The list in the previous article grows as we add more resource types.

Microsoft provides a [NuGet package for .NET developers](/en-us/dotnet/api/overview/azure/functions) building [Azure Functions](/en-us/azure/azure-functions/) apps. This solution handles the back-end processing for incoming HTTP requests for Microsoft Entra authentication events. Find token validation to secure the API call, object model, type with IDE IntelliSense. Also find inbound and outbound validation of the API request and response schemas.

Authentication extensions are executed in-line with sign-in and sign-up flows. Ensure the scenario is highly performant, robust, and secure. Azure Functions offers secure infrastructure, including libraries, [Azure Key Vault](/en-us/azure/key-vault/general/basic-concepts) for secret storage, caching, autoscaling, and monitoring. There are more recommendations in [Security operations](deployment-external-operations).
---
layout: Conceptual
title: 'Backup Authentication System: Application Guidelines - Microsoft Entra | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/backup-authentication-system-apps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: dougeby
description: Learn how to configure your application to support the Microsoft Entra backup authentication system for enhanced resilience and security.
ms.topic: concept-article
ms.date: 2025-07-22T00:00:00.0000000Z
ms.reviewer: ludwignick
ms.custom:
- sfi-ropc-nochange
- ai-gen-docs-bap
- ai-gen-title
- ai-seo-date:07/22/2025
- ai-gen-description
ms.subservice: architecture
locale: en-us
document_id: 764bcd9f-2151-aa07-5893-bb9d2c73f05b
document_version_independent_id: 06880dbd-eca1-d7d2-873a-6e9d1e09c041
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/backup-authentication-system-apps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/backup-authentication-system-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/backup-authentication-system-apps.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 66b87083-11f0-3837-7cab-7e10cc6f8012
---

# Backup Authentication System: Application Guidelines - Microsoft Entra | Microsoft Learn

The Microsoft Entra backup authentication system provides resilience to applications that use supported protocols and flows. For more information about the backup authentication system, see [Microsoft Entra ID's backup authentication system](backup-authentication-system).

## Application requirements for protection

Applications must communicate with a supported hostname for the given Azure environment and use protocols currently supported by the backup authentication system. Use of authentication libraries, such as the [Microsoft Authentication Library (MSAL)](../identity-platform/msal-overview), ensures that you're using authentication protocols supported by the backup authentication system.

### Hostnames supported by the backup authentication system

| Azure environment | Supported hostname |
| --- | --- |
| Azure Commercial | login.microsoftonline.com |
| Azure Government | login.microsoftonline.us |

### Authentication protocols supported by the backup authentication system

#### OAuth 2.0 and OpenID Connect (OIDC)

##### Common guidance

All applications using the Open Authorization (OAuth) 2.0 or OIDC protocols should adhere to the following practices to ensure resilience:

- Your application uses MSAL or strictly adheres to the OpenID Connect & OAuth2 specifications. Microsoft recommends using MSAL libraries appropriate to your platform and use case. Using these libraries ensures the use of APIs and call patterns are supportable by the backup authentication system.
- Your application uses a fixed set of scopes instead of [dynamic consent](../identity-platform/scopes-oidc) when acquiring access tokens.
- Your application doesn't use the [Resource Owner Password Credentials Grant](../identity-platform/v2-oauth-ropc). **This grant type won't be supported** by the backup authentication system for any client type. Microsoft strongly recommends switching to alternative grant flows for better security and resilience.
- Your application doesn't rely upon the [UserInfo endpoint](../identity-platform/userinfo). Switching to using an ID token instead reduces latency by eliminating up to two network requests, and use existing support for ID token resilience within the backup authentication system.

##### Native applications

Native applications are public client applications that run directly on desktop or mobile devices and not in a web browser. They're registered as public clients in their application registration on the Microsoft Entra admin center or Azure portal.

Native applications are protected by the backup authentication system when all the following are true:

1. Your application persists the token cache for at least three days. Applications should use the device's token cache location or the [token cache serialization API](/en-us/entra/msal/dotnet/how-to/token-cache-serialization) to persist the token cache even when the user closes the application.
2. Your application makes use of the MSAL [AcquireTokenSilent API](/en-us/entra/msal/dotnet/acquiring-tokens/acquire-token-silently) to retrieve tokens using cached Refresh Tokens. The use of the [AcquireTokenInteractive API](../identity-platform/scenario-desktop-acquire-token-interactive) might fail to acquire a token from the backup authentication system if user interaction is required.

The backup authentication system doesn't currently support the [device authorization grant](../identity-platform/v2-oauth2-device-code).

##### Single-page web applications

Single-page web applications (SPAs) have limited support in the backup authentication system. SPAs that use the [implicit grant flow](../identity-platform/v2-oauth2-implicit-grant-flow) and request only OpenID Connect ID tokens are protected. Only apps that either use MSAL.js 1.x or implement the implicit grant flow directly can use this protection, as MSAL.js 2.x doesn't support the implicit flow.

The backup authentication system doesn't currently support the [authorization code flow with Proof Key for Code Exchange](../identity-platform/v2-oauth2-auth-code-flow).

##### Web applications and services

The backup authentication system doesn't currently support web applications and services that are configured as confidential clients. Protection for the [authorization code grant flow](../identity-platform/v2-oauth2-auth-code-flow) and subsequent token acquisition using refresh tokens and client secrets or [certificate credentials](../identity-platform/certificate-credentials) isn't currently supported. The OAuth 2.0 [on-behalf-of flow](../identity-platform/v2-oauth2-on-behalf-of-flow) isn't currently supported.

#### SAML 2.0 single sign-on (SSO)

The backup authentication system partially supports the Security Assertion Markup Language (SAML) 2.0 single sign-on (SSO) protocol. Flows that use the SAML 2.0 Identity Provider (IdP) Initiated flow are protected by the backup authentication system. Applications that use the [Service Provider (SP) Initiated flow](../identity-platform/single-sign-on-saml-protocol), aren't currently protected by the backup authentication system.

### Workload identity authentication protocols supported by the backup authentication system

#### OAuth 2.0

##### Managed identity

Applications that use Managed Identities to acquire Microsoft Entra access tokens are protected. Microsoft recommends the use of user-assigned managed identities in most scenarios. This protection applies to both [user and system-assigned managed identities](../identity/managed-identities-azure-resources/overview).

##### Service principal

The backup authentication system doesn't currently support service principal-based Workload identity authentication using the [client credentials grant flow](../identity-platform/v2-oauth2-client-creds-grant-flow). Microsoft recommends using the version of MSAL appropriate to your platform so your application is protected by the backup authentication system when the protection becomes available.
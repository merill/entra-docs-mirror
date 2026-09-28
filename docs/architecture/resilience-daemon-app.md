---
layout: Conceptual
title: Increase the resilience of authentication and authorization in daemon applications you develop - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/resilience-daemon-app
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Learn to increase authentication and authorization resiliency in daemon application using the Microsoft identity platform
ms.topic: how-to
ms.date: 2023-03-03T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 25fb0d6f-3f4a-c633-047b-64ab0a07710d
document_version_independent_id: 6fc16785-2c6c-23f4-1859-81895d1fb2b5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/resilience-daemon-app.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/resilience-daemon-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/resilience-daemon-app.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 15d0c9a9-b2bf-7d62-125e-35994bc76d83
---

# Increase the resilience of authentication and authorization in daemon applications you develop - Microsoft Entra | Microsoft Learn

Learn to use the Microsoft identity platform and Microsoft Entra ID to increase the resilience of daemon applications. Find information about background processes, services, server to server apps, and applications without users.

See, [What is the Microsoft identity platform?](../identity-platform/v2-overview)

The following diagram illustrates a daemon application making a call to Microsoft identity platform.

![A daemon application making a call to Microsoft identity platform.](media/resilience-daemon-app/calling-microsoft-identity.png)

## Managed identities for Azure resources

If you're building daemon apps on Microsoft Azure, use managed identities for Azure resources, which handle secrets and credentials. The feature improves resilience by handling certificate expiry, rotation, or trust.

See, [What are managed identities for Azure resources?](../identity/managed-identities-azure-resources/overview)

Managed identities use long-lived access tokens and information from Microsoft identity platform to acquire new tokens before tokens expire. Your app runs while acquiring new tokens.

Managed identities use regional endpoints, which help prevent out-of-region failures by consolidating service dependencies. Regional endpoints help keep traffic in a geographical area. For example, if your Azure resource is in WestUS2, all traffic stays in WestUS2.

## Microsoft Authentication Library

If you develop daemon apps and don't use managed identities, use the Microsoft Authentication Library (MSAL) for authentication and authorization. MSAL eases the process of providing client credentials. For example, your application doesn't need to create and sign JSON web token assertions with certificate-based credentials.

See, [Overview of the Microsoft Authentication Library (MSAL)](../identity-platform/msal-overview)

### Microsoft.Identity.Web for .NET developers

If you develop daemon apps on ASP.NET Core, use the Microsoft.Identity.Web library to ease authorization. It includes distributed token cache strategies for distributed apps that run in multiple regions.

Learn more:

- [Microsoft Identity Web authentication library](/en-us/entra/msal/dotnet/microsoft-identity-web/)
- [Distributed token cache](https://github.com/AzureAD/microsoft-identity-web/wiki/token-cache-serialization#distributed-token-cache)

## Cache and store tokens

If you don't use MSAL for authentication and authorization, there are best practices for caching and storing tokens. MSAL implements and follows these best practices.

An application acquires tokens from an identity provider (IdP) to authorize the application to call protected APIs. When your app receives tokens, the response with the tokens contains an `expires\_in` property that tells the application how long to cache, and reuse, the token. Ensure applications use the `expires\_in` property to determine token lifespan. Confirm application don't attempt to decode an API access token. Using the cached token prevents unnecessary traffic between an app and Microsoft identity platform. Users are signed in to your application for the token's lifetime.

The [Microsoft Entra ID backup authentication system](backup-authentication-system) provides resilience to applications that use supported protocols and flows. For more information on the application requirements to benefit from backup authentication, see [application requirements for the backup authentication system](backup-authentication-system-apps).

## HTTP 429 and 5xx error codes

Use the following sections to learn about HTTP 429 and 5xx error codes

### HTTP 429

There are HTTP errors that affect resilience. If your application receives an HTTP 429 error code, Too Many Requests, Microsoft identity platform is throttling your requests, which prevents your app from receiving tokens. Ensure your apps don't attempt to acquire a token until the time in the **Retry-After** response field expires. The 429 error often indicates the application doesn't cache and reuse tokens correctly.

### HTTP 5xx

If an application receives an HTTP 5x error code, the app must not enter a fast retry loop. Ensure applications wait until the **Retry-After** field expires. If the response provides no Retry-After header, use an exponential back-off retry with the first retry, at least 5 seconds after the response.

When a request times out, confirm that applications don't retry immediately. Use the previously cited exponential back-off retry.
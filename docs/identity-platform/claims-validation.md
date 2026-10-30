---
layout: Conceptual
title: Secure applications and APIs by validating claims - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/claims-validation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn about securing the business logic of your applications and APIs by validating claims in tokens.
manager: pmwongera
ms.custom: 
ms.date: 2025-03-21T00:00:00.0000000Z
ms.topic: concept-article
locale: en-us
document_id: e5e267a4-887e-7892-7ba9-ff1d66456084
document_version_independent_id: ca88579b-110a-5c68-e3c0-9d5ab7f4e4ba
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/claims-validation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/claims-validation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/claims-validation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 0ec6b964-1b59-11c0-5d2c-b9a1bc58f834
---

# Secure applications and APIs by validating claims - Microsoft identity platform | Microsoft Learn

Interacting with tokens is a core piece of building applications to authorize users. In accordance with the [Zero Trust principle](zero-trust-for-developers) for least privileged access, it's essential that applications validate the values of certain claims present in the access token when performing authorization.

Claims based authorization allows applications to ensure that the token contains the correct values for things such as the tenant, subject, and actor present in the token. That being said, claims based authorization can seem complex given the various methods to utilize and scenarios to keep track of. This article intends to simplify the claims based authorization process so that you can ensure your applications adhere to the most secure practices.

To make sure that your authorization logic is secure, you must validate the following information in claims:

- The appropriate audience is specified for the token.
- The tenant ID of the token matches the ID of the tenant where data is stored.
- The subject of the token is appropriate.
- The actor (client app) is authorized.

Note

Access tokens are only validated in the web APIs for which they were acquired by a client. The client shouldn't validate access tokens.

For more information about the claims mentioned in this article, see [Microsoft identity platform access tokens](access-tokens).

## Validate the audience

The `aud` claim identifies the intended audience of the token. Before validating claims, you must always verify that the value of the `aud` claim contained in the access token matches the Web API. The value can depend on how the client requested the token. The audience in the access token depends on the endpoint:

- For v2.0 tokens, the audience is the client ID of the web API. It's a GUID.
- For v1.0 tokens, the audience is one of the appID URIs declared in the web API that validates the token. For example, `api://{ApplicationID}`, or a unique name starting with a domain name (if the domain name is associated with a tenant).

For more information about the appID URI of an application, see [Application ID URI](security-best-practices-for-app-registration#application-id-uri-also-known-as-identifier-uri).

## Validate the tenant

Always check that the `tid` in a token matches the tenant ID used to store data with the application. When information is stored for an application in the context of a tenant, it should only be accessed again later in the same tenant. Never allow data in one tenant to be accessed from another tenant.

Validation of the tenant is the first step, but the checks on subject and actor described in this article are still necessary. If you intend to authorize all users in a tenant, it's strongly recommended to explicitly add these users into a group and authorize based on the group. For example, by only checking the tenant ID and the presence of an `oid` claim, your API could inadvertently authorize all service principals in that tenant in addition to users.

## Validate the subject

Determine if the token subject, such as the user (or application itself for an app-only token), is authorized.

You can either check for specific `sub` or `oid` claims.

Or,

You can check that the subject belongs to an appropriate role or group with the `roles`, `scp`, `groups`, `wids` claims. For example, use the immutable claim values `tid` and `oid` as a combined key for application data and determining whether a user should be granted access.

The `roles`, `groups` or `wids` claims can also be used to determine if the subject has authorization to perform an operation, although they aren't an exhaustive list of all of the ways a subject can be granted permissions. For example, an administrator may have permission to write to an API, but not a normal user, or the user may be in a group allowed to do some action. The `wid` claim represents the tenant-wide roles assigned to the user from the roles present in the Microsoft Entra built-in roles. For more information, see [Microsoft Entra built-in roles](../identity/role-based-access-control/permissions-reference).

Warning

Never use claims like `email`, `preferred_username` or `unique_name` to store or determine whether the user in an access token should have access to data. These claims aren't unique and can be controllable by tenant administrators or sometimes users, which make them unsuitable for authorization decisions. They're only usable for display purposes. Also don't use the `upn` claim for authorization. While the UPN is unique, it often changes over the lifetime of a user principal, which makes it unreliable for authorization.

## Validate the actor

A client application that's acting on behalf of a user (referred to as the *actor*), must also be authorized. Use the `scp` claim (scope) to validate that the application has permission to perform an operation. The permissions in `scp` should be limited to what the user actually needs and follows the principles of [least privilege](secure-least-privileged-access).

However, there are occurrences where `scp` isn't present in the token. You should check for the absence of the `scp` claim for the following scenarios:

- Daemon apps / app only permission
- ID tokens

For more information about scopes and permissions, see [Scopes and permissions in the Microsoft identity platform](scopes-oidc).

Note

An application may handle app-only tokens (requests from applications without users, such as daemon apps) and want to authorize a specific application across multiple tenants, rather than individual service principal IDs. In that case, the `appid` claim (for v1.0 tokens) or the `azp` claim (for v2.0 tokens) can be used for subject authorization. However, when using these claims, the application must ensure that the token was issued directly for the application by validating the `idtyp` optional claim. Only tokens of type `app` can be authorized this way, as delegated user tokens can potentially be obtained by entities other than the application.
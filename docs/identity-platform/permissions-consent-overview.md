---
layout: Conceptual
title: Overview of permissions and consent in the Microsoft identity platform - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/permissions-consent-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn the foundational concepts and scenarios around consent and permissions in the Microsoft identity platform
manager: pmwongera
ms.custom: 
ms.date: 2025-03-18T00:00:00.0000000Z
ms.reviewer: jawoods, ludwignick, phsignor
ms.topic: overview
locale: en-us
document_id: cf54efe2-d8db-ec17-a062-5bd4428a4dff
document_version_independent_id: 0f701df5-cd9a-4dda-25f3-f928fa9962e5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/permissions-consent-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/permissions-consent-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/permissions-consent-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: e1452d80-024f-468b-c21b-0b7c43183065
---

# Overview of permissions and consent in the Microsoft identity platform - Microsoft identity platform | Microsoft Learn

In the Microsoft identity platform, understanding permissions and consent is crucial for developing secure applications that require access to protected resources. This article provides an overview of the foundational concepts and scenarios related to permissions and consent, helping application developers request the necessary authorizations from users and administrators. By understanding these concepts, you can ensure your applications only request the access they need, fostering trust and security.

To access a protected resource like email or calendar data, your application needs the resource owner's authorization. The resource owner can consent to or deny your app's request. Understanding these foundational concepts helps you build more secure and trustworthy applications that request only the access they need, when they need it, from users and administrators.

## Access scenarios

As an application developer, you must identify how your application accesses data. The application can use delegated access, acting on behalf of a signed-in user, or app-only access, acting only as the application's own identity.

![Image shows illustration of access scenarios.](media/permissions-consent-overview/access-scenarios.png)

### Delegated access (access on behalf of a user)

In this access scenario, a user has signed into a client application. The client application accesses the resource on behalf of the user. Delegated access requires delegated permissions. Both the client and the user must be authorized separately to make the request. For more information about the delegated access scenario, see [delegated access scenario](delegated-access-primer).

For the client app, the correct delegated permissions must be granted. Delegated permissions can also be referred to as scopes. Scopes are permissions for a given resource that represent what a client application can access on behalf of the user. For more information about scopes, see [scopes and permissions](scopes-oidc).

For the user, the authorization relies on the privileges that the user is granted for them to access the resource. For example, the user could be authorized to access directory resources by [Microsoft Entra role-based access control (RBAC)](../identity/role-based-access-control/custom-overview) or to access mail and calendar resources by Exchange Online RBAC. For more information about RBAC for applications, see [RBAC for applications](custom-rbac-for-developers).

### App-only access (Access without a user)

In this access scenario, the application acts on its own with no user signed in. Application access is used in scenarios such as automation, and backup. This scenario includes apps that run as background services or daemons. It's appropriate when it's undesirable to have a specific user signed in, or when the data required can't be scoped to a single user. For more information about the app-only access scenario, see [app-only-access](app-only-access-primer).

App-only access uses app roles instead of delegated scopes. When granted through consent, app roles might also be called applications permissions. The client app must be granted appropriate application permissions of the resource app it's calling. Once granted, the client app can access the requested data. For more information about assigning app roles to client applications, see [Assigning app roles to applications](howto-add-app-roles-in-apps#assign-app-roles-to-applications).

## Types of permissions

**Delegated permissions** are used in the delegated access scenario. They're permissions that allow the application to act on a user's behalf. The application isn't able to access anything the signed in user couldn't access.

For example, take an application that is granted the `Files.Read.All` delegated permission on behalf of the user. The application is only able to read files that the user can personally access.

**Application permissions**, also known as app roles, are used in the app-only access scenario, without a signed-in user present. The application is able to access any data that the permission is associated with.

For example, an application granted the Microsoft Graph API's application permission `Files.Read.All` is able to read any file in the tenant using Microsoft Graph. In general, only an administrator or owner of an API's service principal can consent to application permissions exposed by that API.

### Comparison of delegated and application permissions

| Permission types | Delegated permissions | Application permissions |
| --- | --- | --- |
| Types of apps | Web / Mobile / single-page app (SPA) | Web / Daemon |
| Access context | Get access on behalf of a user | Get access without a user |
| Who can consent | - Users can consent for their data  - Admins can consent for all users | Only admin can consent |
| Consent methods | - Static: configured list on app registration  - Dynamic: request individual permissions at sign-in | - Static ONLY: configured list on app registration |
| Other names | - Scopes  - OAuth2 permission scopes | - App roles  - App-only permissions |
| Result of consent (specific to Microsoft Graph) | [OAuth2PermissionGrant](/en-us/graph/api/resources/oauth2permissiongrant) | [appRoleAssignment](/en-us/graph/api/resources/approleassignment) |

## Consent

One way that applications are granted permissions is through consent. Consent is a process where users or admins authorize an application to access a protected resource. For example, when a user attempts to sign into an application for the first time, the application can request permission to see the user's profile and read the contents of the user's mailbox. The user sees the list of permissions the app is requesting through a consent prompt. Other scenarios where users might see a consent prompt include:

- When previously granted consent is revoked.
- When the application is coded to specifically prompt for consent during sign-in.
- When the application uses dynamic consent to ask for new permissions as needed at run time.

The key details of a consent prompt are the list of permissions the application requires and the publisher information. For more information about the consent prompt and the consent experience for both admins and end users, see [application consent experience](application-consent-experience).

### User consent

User consent happens when a user attempts to sign into an application. The user provides their sign-in credentials, which are checked to determine if consent already is granted. If no previous record of user or admin consent for the required permissions exists, the user is shown a consent prompt, and asked to grant the application the requested permissions. An admin might be required to grant consent on behalf of the user.

### Administrator consent

Depending on the permissions they require, some applications might require an administrator to be the one who grants consent. For example, application permissions and many high-privilege delegated permissions can only be consented to by an administrator.

Administrators can grant consent for themselves or for the entire organization. For more information about user and admin consent, see [user and admin consent overview](../identity/enterprise-apps/user-admin-consent-overview).

Authentication requests are prompted for admin consent if consent wasn't granted and if one of those high-privilege permissions is requested.

Permission requests that contain custom application scopes aren't considered high-privilege and thus, they don't require admin consent.

### Preauthorization

Preauthorization enables a resource application owner to grant permissions to client apps without requiring users to see a consent prompt for the set of permissions that are preauthorized. For more information about preauthorization, see [Scopes and permissions](scopes-oidc#preauthorization).

## Other authorization systems

The consent framework is only one way an application or user can be authorized to access protected resources. Admins should be aware of other authorization systems that might grant access to sensitive information. Examples of various authorization systems at Microsoft include [Microsoft Entra built-in roles](/en-us/entra/identity/role-based-access-control/permissions-reference), [Azure RBAC](/en-us/azure/role-based-access-control/overview), [Exchange RBAC](/en-us/exchange/permissions-exo/application-rbac), and [Teams resource-specific consent](/en-us/microsoftteams/platform/graph-api/rsc/resource-specific-consent).
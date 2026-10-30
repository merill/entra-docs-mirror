---
layout: Conceptual
title: Authentication vs. authorization - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/authentication-vs-authorization
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Understand the fundamentals of authentication, authorization, and how the Microsoft identity platform simplifies these processes for developers.
manager: pmwongera
ms.custom: 
ms.date: 2025-03-21T00:00:00.0000000Z
ms.reviewer: jmprieur, sureshja, ludwignick
ms.topic: concept-article
locale: en-us
document_id: 6d1a08b2-74d4-6350-70c5-6661ef4f7ad1
document_version_independent_id: 52059965-3709-2520-0ed0-82c22648fea2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/authentication-vs-authorization.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/authentication-vs-authorization
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/authentication-vs-authorization.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: e61a0f51-7e17-cefa-ab77-8d62737dc021
---

# Authentication vs. authorization - Microsoft identity platform | Microsoft Learn

This article defines authentication and authorization. It also briefly covers multifactor authentication and how you can use the Microsoft identity platform to authenticate and authorize users in your web apps, web APIs, or apps that call protected web APIs. If you see a term you aren't familiar with, try our [glossary](developer-glossary) or our [Microsoft identity platform videos](identity-videos), which cover basic concepts.

## Authentication

*Authentication* is the process of proving that you are who you say you are. This is achieved by verification of the identity of a person or device. It's sometimes shortened to *AuthN*. The Microsoft identity platform uses the [OpenID Connect](https://openid.net/connect/) protocol for handling authentication.

## Authorization

*Authorization* is the act of granting an authenticated party permission to do something. It specifies what data you're allowed to access and what you can do with that data. Authorization is sometimes shortened to *AuthZ*. The Microsoft identity platform provides resource owners the ability to use the [OAuth 2.0](https://oauth.net/2/) protocol for handling authorization, but the Microsoft cloud also has other authorization systems such as [Microsoft Entra built-in roles](/en-us/entra/identity/role-based-access-control/permissions-reference), [Azure RBAC](/en-us/azure/role-based-access-control/overview), and [Exchange RBAC](/en-us/exchange/permissions-exo/application-rbac).

## Multifactor authentication

*Multifactor authentication* is the act of providing another factor of authentication to an account. This is often used to protect against brute force attacks. It's sometimes shortened to *MFA* or *2FA*. The [Microsoft Authenticator](https://support.microsoft.com/account-billing/set-up-the-microsoft-authenticator-app-as-your-verification-method-33452159-6af9-438f-8f82-63ce94cf3d29) can be used as an app for handling two-factor authentication. For more information, see [multifactor authentication](../identity/authentication/concept-mfa-howitworks).

## Authentication and authorization using the Microsoft identity platform

Creating apps that each maintain their own username and password information incurs a high administrative burden when adding or removing users across multiple apps. Instead, your apps can delegate that responsibility to a centralized identity provider.

Microsoft Entra ID is a centralized identity provider in the cloud. Delegating authentication and authorization to it enables scenarios such as:

- Conditional Access policies that require a user to be in a specific location.
- Multifactor authentication which requires a user to have a specific device.
- Enabling a user to sign in once and then be automatically signed in to all of the web apps that share the same centralized directory. This capability is called *single sign-on (SSO)*.

The Microsoft identity platform simplifies authorization and authentication for application developers by providing identity as a service. It supports industry-standard protocols and open-source libraries for different platforms to help you start coding quickly. It allows developers to build applications that sign in all Microsoft identities, get tokens to call [Microsoft Graph](https://developer.microsoft.com/graph/), access Microsoft APIs, or access other APIs that developers have built.

This video explains the Microsoft identity platform and the basics of modern authentication:

Here's a comparison of the protocols that the Microsoft identity platform uses:

- **OAuth versus OpenID Connect**: The platform uses OAuth for authorization and OpenID Connect (OIDC) for authentication. OpenID Connect is built on top of OAuth 2.0, so the terminology and flow are similar between the two. You can even both authenticate a user (through OpenID Connect) and get authorization to access a protected resource that the user owns (through OAuth 2.0) in one request. For more information, see [OAuth 2.0 and OpenID Connect protocols](v2-protocols) and [OpenID Connect protocol](v2-protocols-oidc).
- **OAuth versus SAML**: The platform uses OAuth 2.0 for authorization and SAML for authentication. For more information on how to use these protocols together to both authenticate a user and get authorization to access a protected resource, see [Microsoft identity platform and OAuth 2.0 SAML bearer assertion flow](scenario-token-exchange-saml-oauth).
- **OpenID Connect versus SAML**: The platform uses both OpenID Connect and SAML to authenticate a user and enable single sign-on. SAML authentication is commonly used with identity providers such as Active Directory Federation Services (AD FS) federated to Microsoft Entra ID, so it's often used in enterprise applications. OpenID Connect is commonly used for apps that are purely in the cloud, such as mobile apps, websites, and web APIs.
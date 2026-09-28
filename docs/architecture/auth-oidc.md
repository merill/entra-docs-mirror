---
layout: Conceptual
title: OpenID Connect authentication with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/auth-oidc
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Architectural guidance on achieving OpenID Connect authentication with Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2023-01-10T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: f2def5b5-18c6-0dff-7247-7784f9582cbf
document_version_independent_id: bf8a1c34-ea5e-b1d5-c9df-bdfc1e2a8c52
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/auth-oidc.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/auth-oidc
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/auth-oidc.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 0cbc9799-67fb-c5aa-0b97-ef0a87d94b4a
---

# OpenID Connect authentication with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

OpenID Connect (OIDC) is an authentication protocol based on the OAuth2 protocol (which is used for authorization). OIDC uses the standardized message flows from OAuth2 to provide identity services.

The design goal of OIDC is "making simple things simple and complicated things possible". OIDC lets developers authenticate their users across websites and apps without having to own and manage password files. This provides the app builder with a secure way to verify the identity of the person currently using the browser or native app that is connected to the application.

The authentication of the user must take place at an identity provider where the user's session or credentials will be checked. To do that, you need a trusted agent. Native apps usually launch the system browser for that purpose. Embedded views are considered not trusted since there's nothing to prevent the app from snooping on the user password.

In addition to authentication, the user can be asked for consent. Consent is the user's explicit permission to allow an application to access protected resources. Consent is different from authentication because consent only needs to be provided once for a resource. Consent remains valid until the user or admin manually revokes the grant.

## Use when

There is a need for user consent and for web sign in.

![Architectural diagram](media/authentication-patterns/oidc-auth.png)

## Components of system

- **User:** Requests a service from the application.
- **Trusted agent:** The component that the user interacts with. This trusted agent is usually a web browser.
- **Application:** The application, or Resource Server, is where the resource or data resides. It trusts the identity provider to securely authenticate and authorize the trusted agent.
- **Microsoft Entra ID:** The OIDC provider, also known as the identity provider, securely manages anything to do with the user's information, their access, and the trust relationships between parties in a flow. It authenticates the identity of the user, grants and revokes access to resources, and issues tokens.

## Implement OIDC with Microsoft Entra ID

- [Integrating applications with Microsoft Entra ID](../identity/saas-apps/tutorial-list)
- [Open Authorization (OAuth) 2.0 and OpenID Connect protocols on the Microsoft identity platform](../identity-platform/v2-protocols)
- [Microsoft identity platform and OpenID Connect protocol](../identity-platform/v2-protocols-oidc)
- [Web sign-in with OpenID Connect in Azure Active Directory B2C](/en-us/azure/active-directory-b2c/openid-connect)
- [Secure your application by using OpenID Connect and Microsoft Entra ID](../identity-platform/v2-protocols-oidc)
---
layout: Conceptual
title: OAuth 2.0 authorization with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/auth-oauth2
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Architectural guidance on achieving OAuth 2.0 authorization with Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2023-01-10T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 535cb7a2-f177-7ba0-bb06-25bc540d9055
document_version_independent_id: 5e79865e-3d8d-3f7f-cae4-2670b408870f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/auth-oauth2.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/auth-oauth2
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/auth-oauth2.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3f529bb3-d735-4345-29fe-034be0fb955d
---

# OAuth 2.0 authorization with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

The Open Authorization (OAuth) 2.0 is the industry protocol for authorization. It allows a user to grant limited access to its protected resources. Designed to work specifically with Hypertext Transfer Protocol (HTTP), OAuth separates the role of the client from the resource owner. The client requests access to the resources controlled by the resource owner and hosted by the resource server. The resource server issues access tokens with the approval of the resource owner. The client uses the access tokens to access the protected resources hosted by the resource server.

OAuth 2.0 is directly related to OpenID Connect (OIDC). Since OIDC is an authentication and authorization layer built on top of OAuth 2.0, it isn't backward compatible with OAuth 1.0. Microsoft Entra ID supports all OAuth 2.0 flows.

## Use for:

Rich client and modern app scenarios and RESTful web API access.

![Diagram of architecture](media/authentication-patterns/oauth.png)

## Components of system

- **User:** Requests a service from the web application (app). The user is typically the resource owner who owns the data and has the power to allow clients to access the data or resource.
- **Web browser:** The web browser that the user interacts with is the OAuth client.
- **Web app:** The web app, or resource server, is where the resource or data resides. It trusts the authorization server to securely authenticate and authorize the OAuth client.
- **Microsoft Entra ID:** Microsoft Entra ID is the authentication server, also known as the Identity Provider (IdP). It securely handles anything to do with the user's information, their access, and the trust relationship. It's responsible for issuing the tokens that grant and revoke access to resources.

## Implement OAuth 2.0 with Microsoft Entra ID

- [Integrating applications with Microsoft Entra ID](../identity/saas-apps/tutorial-list)
- [OAuth 2.0 and OpenID Connect protocols on the Microsoft identity platform](../identity-platform/v2-protocols)
- [Application types and OAuth2](../identity-platform/v2-app-types)
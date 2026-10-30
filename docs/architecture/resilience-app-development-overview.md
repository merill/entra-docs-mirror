---
layout: Conceptual
title: Increase the resilience of authentication and authorization applications you develop - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/resilience-app-development-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Resilience guidance for application development using Microsoft Entra ID and the Microsoft identity platform
ms.topic: how-to
ms.date: 2023-03-02T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: e64d9c46-2567-183b-384f-80141742f6a7
document_version_independent_id: 3e93082d-2ec5-14a7-ee76-1c6984c6db83
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/resilience-app-development-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/resilience-app-development-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/resilience-app-development-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d69b43ee-1b7e-2616-23f7-5caceb6c2e53
---

# Increase the resilience of authentication and authorization applications you develop - Microsoft Entra | Microsoft Learn

The [Microsoft identity platform](../identity-platform/v2-overview) helps you build applications your users and customers can sign in to using their Microsoft identities or social accounts. The Microsoft identity platform uses token-based authentication and authorization flows to communicate with applications. Client applications acquire tokens from an identity provider (IdP), Microsoft Entra and Azure AD B2C, to authenticate users and authorize applications to call protected APIs. A service validates tokens. For more information, see [Security tokens](../identity-platform/security-tokens).

A token is valid for a length of time, and then the app must acquire a new one. Rarely, a call to retrieve a token fails due to network or infrastructure issues or an authentication service outage. The [backup authentication system](backup-authentication-system) increases authentication resilience if there's an outage. This system transparently and automatically handles authentications for supported applications and services if the primary Microsoft Entra service is unavailable or degraded.

The following articles have guidance for client and service applications for a signed in user and daemon applications. They contain best practices for using tokens and calling resources.

- [Increase the resilience of authentication and authorization in client applications you develop](resilience-client-app)
- [Increase the resilience of authentication and authorization in daemon applications you develop](resilience-daemon-app)
- [Build resilience in your identity and access management infrastructure](resilience-in-infrastructure)
- [Build resilience in your customer identity and access management with Azure AD B2C](resilience-b2c)
- [Building application support for the backup authentication system](backup-authentication-system-apps)
- [Build services that are resilient to Microsoft Entra ID OpenID Connect metadata refresh](../identity-platform/howto-build-services-resilient-to-metadata-refresh)
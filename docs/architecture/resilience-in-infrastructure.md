---
layout: Conceptual
title: Build resilience in your IAM infrastructure with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/resilience-in-infrastructure
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: A guide for architects and IT administrators on building resilience to disruption of their IAM infrastructure.
ms.topic: concept-article
ms.date: 2022-11-16T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: d3667474-171e-2b00-c6e7-0e1411bb5adb
document_version_independent_id: 018a3e34-5e3d-743c-6dee-417439a49979
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/resilience-in-infrastructure.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/resilience-in-infrastructure
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/resilience-in-infrastructure.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 7579392e-dcc6-1a93-ac2d-7cfed64fba5d
---

# Build resilience in your IAM infrastructure with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

Microsoft Entra ID is a global cloud identity and access management system that provides critical services such as authentication and authorization to your organization's resources. This article provides you with guidance to understand, contain, and mitigate the risk of disruption of authentication or authorization services for resources that rely on Microsoft Entra ID.

The document set is designed for

- Identity Architects
- Identity Service Owners
- Identity Operations teams

Also see the documentation for [application developers](resilience-app-development-overview) and for [Azure AD B2C systems](resilience-b2c).

## What is resilience?

In the context of your identity infrastructure, resilience is the ability to endure disruption to services like authentication and authorization, or failure of other components, with minimal or no effect on your business, users, and operations. The effect of disruption can be severe and resilience requires diligent planning.

## Why worry about disruption?

Every call to the authentication system is subject to disruption if any component of the call fails. When authentication is disrupted, because of the underlying component failures, your users won't access their applications. Therefore, reducing the number of authentication calls and number of dependencies in those calls is important to your resilience. Application developers can assert some control over how often tokens are requested. For example, work with your developers to ensure they're using managed identities for Azure resources for their applications wherever possible.

In a token-based authentication system like Microsoft Entra ID, a user's application (client) must acquire a security token from the identity system before it can access an application or other resource. During the validity period, a client can present the same token multiple times to access the application.

When the token presented to the application expires, the application rejects the token, and the client must acquire a new token from Microsoft Entra ID. Acquiring a new token potentially requires user interaction, such as credential prompts or meeting other requirements of the authentication system. Reducing the frequency of authentication calls with longer-lived tokens decreases unnecessary interactions. However, you must balance token life with the risk created by fewer policy evaluations. For more information on managing token lifetimes, see this article on [optimizing reauthentication prompts](../identity/authentication/concepts-azure-multi-factor-authentication-prompts-session-lifetime).

## Ways to increase resilience

The following diagram shows six concrete ways you can increase resilience. Each method is explained in detail in the articles linked in the following Next steps portion of this article.

![Diagram showing overview of admin resilience](media/resilience-in-infrastructure/admin-resilience-overview.png)
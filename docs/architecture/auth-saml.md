---
layout: Conceptual
title: SAML authentication with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/auth-saml
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Architectural guidance on achieving SAML authentication with Microsoft Entra ID
ms.topic: concept-article
ms.date: 2024-02-26T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: ad11b236-1f86-c5e1-36ab-ede236b3d44a
document_version_independent_id: 832cabb7-8585-5d6f-e358-dda7b09cd6d2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/auth-saml.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/auth-saml
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/auth-saml.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c6f99e62-1cf6-4b71-af9b-649b05f80cce
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3f56b378-07a9-4fa1-afe8-9889fdc77628
platformId: e086f90f-2eb6-b0a0-d0bb-0e8edd44430c
---

# SAML authentication with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

Security Assertion Markup Language (SAML) is an open standard for exchanging authentication and authorization data between an identity provider (IdP) and a service provider. SAML is an XML-based markup language for security assertions, which are statements that service providers use to make access-control decisions.

The SAML specification defines three roles:

- The principal, generally a user
- The identity provider (IdP)
- The service provider (SP)

## Use when

There's a need to provide a single sign-on (SSO) experience for an enterprise SAML application.

While one of most important use cases that SAML addresses is SSO, especially by extending SSO across security domains, there are other use cases (called profiles) as well.

![architectural diagram for SAML](media/authentication-patterns/saml-auth.png)

## Components of system

- **User:** Requests a service from the application.
- **Web browser:** The component that the user interacts with.
- **Web app:** Enterprise application that supports SAML and uses Microsoft Entra ID as IdP.
- **Token:** A SAML assertion (also known as SAML tokens) that carries sets of claims made by the IdP about the principal (user). It contains authentication information, attributes, and authorization decision statements.
- **Microsoft Entra ID:** Enterprise cloud IdP that provides SSO and multifactor authentication for SAML apps. It synchronizes, maintains, and manages identity information for users while providing authentication services to relying applications.

## Implement SAML authentication with Microsoft Entra ID

- [Tutorials for integrating software as a service (SaaS) applications using Microsoft Entra ID](../identity/saas-apps/tutorial-list)
- [Configuring SAML-based single sign-on for non-gallery applications](../identity/enterprise-apps/add-application-portal)
- [How Microsoft Entra ID uses the SAML protocol](../identity-platform/saml-protocol-reference)
---
layout: Conceptual
title: Microsoft Entra authentication and synchronization protocol overview - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/auth-sync-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Architectural guidance on integrating Microsoft Entra ID with legacy authentication protocols and sync patterns
ms.topic: concept-article
ms.date: 2023-02-08T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 09c75885-77bc-f500-92af-a6a41e5ce127
document_version_independent_id: a1dfc93e-4982-351a-8cef-7440d0fcd49c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/auth-sync-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/auth-sync-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/auth-sync-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 010aabdc-9ca2-bedf-4b85-586d3d0f1046
---

# Microsoft Entra authentication and synchronization protocol overview - Microsoft Entra | Microsoft Learn

Microsoft Entra ID enables integration with many authentication protocols. The authentication integrations enable you to use Microsoft Entra ID and its security and management features with little or no changes to your applications that use legacy authentication methods.

## Legacy authentication protocols

The following table presents authentication Microsoft Entra integration with legacy authentication protocols and their capabilities. Select the name of an authentication protocol to see

- A detailed description
- When to use it
- Architectural diagram
- Explanation of system components
- Links for how to implement the integration

| Authentication protocol | Authentication | Authorization | Multifactor Authentication | Conditional Access |
| --- | --- | --- | --- | --- |
| [Header-based authentication](auth-header-based) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) |
| [LDAP authentication](auth-ldap) | ![check mark](media/authentication-patterns/check.png) |  |  |  |
| [Open Authorization (OAuth) 2.0 authentication](auth-oauth2) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) |
| [OIDC authentication](auth-oidc) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) |
| [Password-based single sign-on (SSO) authentication](auth-password-based-sso) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) |
| [RADIUS authentication](auth-radius) | ![check mark](media/authentication-patterns/check.png) |  | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) |
| [Remote Desktop Gateway services](auth-remote-desktop-gateway) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) |
| [Secure Shell (SSH)](auth-ssh) | ![check mark](media/authentication-patterns/check.png) |  | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) |
| [Security Assertion Markup Language (SAML) authentication](auth-saml) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) |
| [Windows Authentication - Kerberos Constrained Delegation](auth-kcd) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) | ![check mark](media/authentication-patterns/check.png) |
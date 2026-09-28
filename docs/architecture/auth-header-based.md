---
layout: Conceptual
title: Header-based authentication with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/auth-header-based
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Architectural guidance on achieving header-based authentication with Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2023-01-10T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 02edd845-f021-8fa2-4fdd-82899769a714
document_version_independent_id: 2a39e99f-8692-5cb5-cdfc-da72a5b787af
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/auth-header-based.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/auth-header-based
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/auth-header-based.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 6e3a484a-4dcb-5ee4-1fe6-d46e84db6bdc
---

# Header-based authentication with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

Legacy applications commonly use Header-based authentication. In this scenario, a user (or message originator) authenticates to an intermediary identity solution. The intermediary solution authenticates the user and propagates the required Hypertext Transfer Protocol (HTTP) headers to the destination web service. Microsoft Entra ID supports this pattern via its Application Proxy service, and integrations with other network controller solutions.

In our solution, Application Proxy provides remote access to the application, authenticates the user, and passes headers required by the application.

## Use when

Remote users need to securely single sign-on (SSO) into to on-premises applications that require header-based authentication.

![Architectural image header-based authentication](media/authentication-patterns/header-based-auth.png)

## Components of system

- **User:** Accesses legacy applications served by Application Proxy.
- **Web browser:** The component that the user interacts with to access the external URL of the application.
- **Microsoft Entra ID:** Authenticates the user.
- **Application Proxy service:** Acts as reverse proxy to send request from the user to the on-premises application. It resides in Microsoft Entra ID and can also enforce any Conditional Access policies.
- **Private network connector:** Installed on-premises on Windows servers to provide connectivity to the applications. It only uses outbound connections. Returns the response to Microsoft Entra ID.
- **Legacy applications:** Applications that receive user requests from Application Proxy. The legacy application receives the required HTTP headers to set up a session and return a response.

## Implement header-based authentication with Microsoft Entra ID

- [Add an on-premises application for remote access through Application Proxy in Microsoft Entra ID](../identity/app-proxy/application-proxy-add-on-premises-application)
- [Header-based authentication for single sign-on with Application Proxy and PingAccess](../identity/app-proxy/application-proxy-configure-single-sign-on-with-headers)
- [Secure legacy apps with app delivery controllers and networks](../identity/enterprise-apps/secure-hybrid-access)
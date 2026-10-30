---
layout: Conceptual
title: Kerberos constrained delegation with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/auth-kcd
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Architectural guidance on achieving Kerberos constrained delegation with Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2023-03-01T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 0ec4819b-b916-7589-3593-fc6e42984c1c
document_version_independent_id: 33f8235a-9178-9f7f-0eb4-9912577cf008
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/auth-kcd.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/auth-kcd
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/auth-kcd.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 9d954724-5105-0976-d1bd-71e2dc3327fe
---

# Kerberos constrained delegation with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

Based on service principal Names, Kerberos Constrained Delegation (KCD) provides constrained delegation between resources. It requires domain administrators to create the delegations and is limited to a single domain. You can use resource-based KCD to provide Kerberos authentication for a web application that has users in multiple domains within an Active Directory forest.

Microsoft Entra application proxy can provide single sign-on (SSO) and remote access to KCD-based applications that require a Kerberos ticket for access and Kerberos Constrained Delegation (KCD).

To enable SSO to your on-premises KCD applications that use integrated Windows authentication (IWA), give private network connectors permission to impersonate users in Active Directory. The private network connector uses this permission to send and receive tokens on the users' behalf.

## When to use KCD

Use KCD when there's a need to provide remote access, protect with pre-authentication, and provide SSO to on-premises IWA applications.

![Diagram of architecture](media/authentication-patterns/kcd-auth.png)

## Components of system

- **User:** Accesses legacy application that Application Proxy serves.
- **Web browser:** The component that the user interacts with to access the external URL of the application.
- **Microsoft Entra ID:** Authenticates the user.
- **Application Proxy service:** Acts as reverse proxy to send requests from the user to the on-premises application. It sits in Microsoft Entra ID. Application Proxy can enforce Conditional Access policies.
- **Private network connector:** Installed on Windows on-premises servers to provide connectivity to the application. Returns the response to Microsoft Entra ID. Performs KCD negotiation with Active Directory, impersonating the user to get a Kerberos token to the application.
- **Active Directory:** Sends the Kerberos token for the application to the private network connector.
- **Legacy applications:** Applications that receive user requests from Application Proxy. The legacy applications return the response to the private network connector.

## Implement Windows authentication (KCD) with Microsoft Entra ID

Explore the following resources to learn more about implementing Windows authentication (KCD) with Microsoft Entra ID.

- [Kerberos-based single sign-on (SSO) in Microsoft Entra ID with Application Proxy](../identity/app-proxy/how-to-configure-sso-with-kcd) describes prerequisites and configuration steps.
- The [Tutorial - Add an on-premises app - Application Proxy in Microsoft Entra ID](../identity/app-proxy/application-proxy-add-on-premises-application) helps you to prepare your environment for use with Application Proxy.
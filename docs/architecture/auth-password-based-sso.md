---
layout: Conceptual
title: Password-based authentication with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/auth-password-based-sso
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Architectural guidance on achieving password-based authentication with Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2023-01-10T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 654c42ee-24d4-6541-1dab-02b18020d9a3
document_version_independent_id: 51783a7b-db99-7420-cf15-0571bdcbc696
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/auth-password-based-sso.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/auth-password-based-sso
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/auth-password-based-sso.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: c8f2db25-d00f-a755-d5b6-a7f5524d37f8
---

# Password-based authentication with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

Password-based Single Sign-On (SSO) uses the existing authentication process for the application. When you enable password-based SSO, Microsoft Entra ID collects, encrypts, and securely stores user credentials in the directory. Microsoft Entra ID supplies the username and password to the application when the user attempts to sign in.

Choose password-based SSO when an application authenticates with a username and password instead of access tokens and headers. Password-based SSO supports any cloud-based application that has an HTML-based sign in page.

## Use when

You need to protect with pre-authentication and provide SSO through password vaulting to web apps.

![architectural diagram](media/authentication-patterns/password-based-sso-auth.png)

## Components of system

- **User:** Accesses formed-based application from either My Apps or by directly visiting the site.
- **Web browser:** The component that the user interacts with to access the external URL of the application. The user accesses the form-based application via the MyApps extension.
- **MyApps extension:** Identifies the configured password-based SSO application and supplies the credentials to the sign in form. The MyApps extension is installed on the web browser.
- **Microsoft Entra ID:** Authenticates the user.

## Implement password-based SSO with Microsoft Entra ID

- [What is password-based SSO](../identity/enterprise-apps/what-is-single-sign-on)
- [Configure password-based SSO for cloud applications](../identity/enterprise-apps/configure-password-single-sign-on-non-gallery-applications)
- [Configure password-based SSO for on-premises applications with Application Proxy](../identity/app-proxy/application-proxy-configure-single-sign-on-password-vaulting)
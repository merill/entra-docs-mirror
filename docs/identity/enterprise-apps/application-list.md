---
layout: Conceptual
title: Viewing apps using your tenant for identity management - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/application-list
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Understand how to view all applications using your Microsoft Entra tenant for identity management.
ms.topic: reference
ms.date: 2023-07-14T00:00:00.0000000Z
ms.reviewer: alamaral
ms.custom: enterprise-apps
locale: en-us
document_id: 650c8b12-78ca-ed93-fdc8-2be029910ae5
document_version_independent_id: b13db460-cf2c-bd71-bc94-d325ecd9f568
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/application-list.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/application-list
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/application-list.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: dc3bf9ad-8820-42fd-35f6-6489699a12b7
---

# Viewing apps using your tenant for identity management - Microsoft Entra ID | Microsoft Learn

The [Quickstart Series on Application Management](view-applications-portal) walks you the basics. In it, you learn how to view all of the apps using your Microsoft Entra tenant for identity management. This article dives a bit deeper into the types of apps you'll find.

## Why does a specific application appear in my all applications list?

When filtered to **All Applications**, the **All Applications** **List** shows every Service Principal object in your tenant. Service Principal objects can appear in this list in a various ways:

- When you add any application from the application gallery, including:

    - **Microsoft Entra ID - Enterprise applications** – Apps added to your tenant using the **Enterprise applications** option on the Microsoft Entra admin center. Usually apps integrated using the SAML standard.
    - **Microsoft Entra ID - App registrations** – Apps added to your tenant using the **App registrations** option on the Microsoft Entra admin center. Usually custom developed apps using the OpenID Connect and OAuth standards.
    - **Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally
- When signing up for, or signing in to, a third-party application integrated with Microsoft Entra ID. One example is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).
- Microsoft apps such as Microsoft 365.
- When you use managed identities for Azure resources. For more information, see [Managed identity types](../managed-identities-azure-resources/overview#managed-identity-types).
- When you add a new application registration by creating a custom-developed application using the [Application Registry](../../identity-platform/quickstart-register-app)
- When you add a new application registration by creating a custom-developed application using the [V2.0 Application Registration portal](../../identity-platform/quickstart-register-app)
- When you add an application, you’re developing using Visual Studio’s [ASP.NET authentication methods](/en-us/aspnet/core/security/authentication/identity?tabs=visual-studio) or [Connected Services](https://devblogs.microsoft.com/visualstudio/connecting-to-cloud-services/)
- When you create a service principal object using the [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/installation) module.
- When you [consent to an application](../../identity-platform/howto-convert-app-to-be-multi-tenant) as an administrator to use data in your tenant
- When a [user consents to an application](../../identity-platform/howto-convert-app-to-be-multi-tenant) to use data in your tenant
- When you enable certain services that store data in your tenant. One example is Password Reset, which is modeled as a service principal to store your password reset policy securely.

Learn more about how, and why, apps are added to your directory, see [How applications are added to Microsoft Entra ID](../../identity-platform/how-applications-are-added).
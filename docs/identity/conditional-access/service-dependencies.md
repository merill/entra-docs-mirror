---
layout: Conceptual
title: Conditional Access service dependencies - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/service-dependencies
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Learn about service dependencies in Microsoft Entra Conditional Access and how they affect policy enforcement.
ms.topic: concept-article
ms.date: 2026-05-12T00:00:00.0000000Z
ms.reviewer: kvenkit
locale: en-us
document_id: 7834fc25-6e4d-1a00-e9d3-949928ccb94b
document_version_independent_id: 23e71a83-28ea-da6f-0e3e-cda56a320358
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/service-dependencies.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/service-dependencies
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/service-dependencies.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 94155a5d-4715-2835-8229-a80a43875f03
---

# Conditional Access service dependencies - Microsoft Entra ID | Microsoft Learn

## Overview

With Conditional Access policies, you specify requirements to use websites and services. For example, your requirements can include requiring multifactor authentication (MFA) or [managed devices](concept-conditional-access-grant).

When you use a site or service directly, it's usually easy to see how a related policy affects you. For example, if you set a policy that requires multifactor authentication (MFA) for SharePoint Online, MFA is required for each sign-in to the SharePoint web portal. But sometimes it's hard to know how a policy affects you because some cloud apps depend on other cloud apps. For example, Microsoft Teams lets you use resources in SharePoint Online. So, when you use Microsoft Teams in this scenario, you're also subject to the SharePoint MFA policy.

Tip

Use the [Office 365](concept-conditional-access-cloud-apps#office-365) app to target all Office apps and avoid issues with service dependencies in the Office stack.

## Policy enforcement

If you have a service dependency configured, the policy can apply using early-bound or late-bound enforcement.

- **Early-bound policy enforcement** means a user must meet the dependent service policy before using the calling app. For example, a user must meet the SharePoint policy before signing in to Microsoft Teams.
- **Late-bound policy enforcement** happens after the user signs in to the calling app. Enforcement is deferred until the calling app requests a token for the downstream service. Examples include Microsoft Teams accessing Planner, and Office.com accessing SharePoint.

The following diagram shows Microsoft Teams service dependencies. Solid arrows indicate early-bound enforcement, and the dashed arrow for Planner indicates late-bound enforcement.

![A diagram showing Microsoft Teams service dependencies.](media/service-dependencies/01.png)

Set common policies across related apps and services whenever possible. A consistent security posture gives you the best user experience. For example, setting a common policy across Exchange Online, SharePoint Online, and Microsoft Teams reduces prompts that can come from different policies applied to downstream services.

To set a common policy for Microsoft 365 apps, use the [Office 365 app](concept-conditional-access-cloud-apps#office-365) instead of targeting individual applications.

The following table lists some more service dependencies, where the client apps must satisfy. This list isn't exhaustive.

| Client apps | Downstream service | Enforcement |
| --- | --- | --- |
| Azure Data Lake | Windows Azure Service Management API (portal and API) | Early-bound |
| Azure portal | Exchange | Early-bound |
|  | SharePoint | Early-bound |
|  | Microsoft 365 Reporting Service | Early-bound |
|  | Windows 365 | Early-bound |
| Microsoft Classroom | Exchange | Early-bound |
|  | SharePoint | Early-bound |
| Microsoft Intune Portal Extension | Microsoft Intune | Early-bound |
|  | Windows 365 | Early-bound |
| Microsoft Teams | Exchange | Early-bound |
|  | MS Planner | Late-bound |
|  | Microsoft Stream | Late-bound |
|  | SharePoint | Early-bound |
|  | Microsoft Whiteboard | Late-bound |
| Microsoft 365 portal | Exchange | Early-bound |
|  | SharePoint | Early-bound |
|  | Microsoft Teams Services | Early-bound |
|  | Microsoft 365 Reporting Service | Early-bound |
|  | Windows 365 | Early-bound |
| Outlook groups | Exchange | Early-bound |
|  | SharePoint | Early-bound |
| Power Apps | Windows Azure Service Management API (portal and API) | Early-bound |
|  | Windows Azure Active Directory | Early-bound |
|  | SharePoint | Early-bound |
|  | Exchange | Early-bound |
| Power Automate | Power Apps | Early-bound |
| Project | Dynamics CRM | Early-bound |
| Visual Studio | Windows Azure Service Management API (portal and API) | Early-bound |
| Microsoft Forms | Exchange | Early-bound |
|  | SharePoint | Early-bound |
| Microsoft To Do | Exchange | Early-bound |
| SharePoint | SharePoint Online Web Client Extensibility | Early-bound |
|  | SharePoint Online Web Client Extensibility Isolated | Early-bound |
|  | SharePoint Client Extensibility web application principal (where present) | Early-bound |

## Troubleshooting service dependencies

The Microsoft Entra sign-in log is a valuable source of information when you troubleshoot why and how a Conditional Access policy applies in your environment. The sign-in logs include helpful information like applications, resources, and audiences. For more information about troubleshooting unexpected sign-in outcomes related to Conditional Access, see the article [Troubleshooting sign-in problems with Conditional Access](troubleshoot-conditional-access#service-dependencies).
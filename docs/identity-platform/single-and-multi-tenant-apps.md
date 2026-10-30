---
layout: Conceptual
title: Single and multitenant apps in Microsoft Entra ID - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/single-and-multi-tenant-apps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn about the features and differences between single-tenant and multitenant apps in Microsoft Entra ID.
manager: pmwongera
ms.custom: 
ms.date: 2025-03-13T00:00:00.0000000Z
ms.reviewer: 
ms.topic: concept-article
locale: en-us
document_id: cc84ec3c-dcb4-b735-5c51-5e7b1417a341
document_version_independent_id: 39d44a1e-06e5-40d2-9c6c-d011377bdc13
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/single-and-multi-tenant-apps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/single-and-multi-tenant-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/single-and-multi-tenant-apps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 606bf965-ac3b-b7fe-1fd5-07e1e424ee7e
---

# Single and multitenant apps in Microsoft Entra ID - Microsoft identity platform | Microsoft Learn

Microsoft Entra ID organizes objects like users and apps into groups called *tenants*. Tenants allow an administrator to set policies on the users within the organization and the apps that the organization owns to meet their security and operational policies.

## Who can sign in to your app?

When it comes to developing apps, developers can choose to configure their app to be either single-tenant or multitenant during app registration.

- Single-tenant apps are only available in the tenant they were registered in, also known as their home tenant.
- Multitenant apps are available to users in both their home tenant and other tenants.

When you register an application, you can configure it to be single-tenant or multitenant by setting the audience as follows.

| Audience | Single/multi-tenant | Who can sign in |
| --- | --- | --- |
| Accounts in this directory only | Single tenant | All user and guest accounts in your directory can use your application or API.Use this option if your target audience is internal to your organization.  Use if building an app registration for a third party that instructs you to build your own app registration for their app. |
| Accounts in any Microsoft Entra directory | Multitenant | All users and guests with a work or school account from Microsoft can use your application or API. This includes schools and businesses that use Microsoft 365.Use this option if your target audience is business or educational customers. |
| Accounts in any Microsoft Entra directory and personal Microsoft accounts (such as Skype, Xbox, Outlook.com) | Multitenant | All users with a work or school, or personal Microsoft account can use your application or API. It includes schools and businesses that use Microsoft 365 as well as personal accounts that are used to sign in to services like Xbox and Skype.Use this option to target the widest set of Microsoft accounts. |

## Best practices for multitenant apps

Building great multitenant apps can be challenging because of the number of different policies that IT administrators can set in their tenants. If you choose to build a multitenant app, follow these best practices:

- Test your app in a tenant that has configured [Conditional Access policies](v2-conditional-access-dev-guide).
- Follow the principle of least user access to ensure that your app only requests permissions it actually needs.
- Provide appropriate names and descriptions for any permissions you expose as part of your app. This helps users and admins know what they're agreeing to when they attempt to use your app's APIs. For more information, see the best practices section in the [permissions guide](permissions-consent-overview).

Note

Multitenant applications can be deployed to the same national cloud instances, but not across [Azure National Clouds](authentication-national-cloud). Examples:

- A multitenant application created in a commercial tenant can be added to other commercial tenants.
- A multitenant application created in an Azure Government tenant can be added to other Azure Government tenants.
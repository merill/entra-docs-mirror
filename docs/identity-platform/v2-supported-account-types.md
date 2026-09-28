---
layout: Conceptual
title: Supported account types - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/v2-supported-account-types
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Conceptual documentation about audiences and supported account types in in the Microsoft identity platform
manager: pmwongera
ms.date: 2024-04-24T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.topic: concept-article
ms.custom: sfi-ropc-nochange
locale: en-us
document_id: dd4f98b7-3d87-6a84-8247-20a8893f7e98
document_version_independent_id: 01482485-7e2b-5621-897b-850618ef3f1e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/v2-supported-account-types.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/v2-supported-account-types
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/v2-supported-account-types.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 46bd5f13-7150-a158-82a0-6e1553ad8ba7
---

# Supported account types - Microsoft identity platform | Microsoft Learn

This article explains what account types (sometimes called *audiences*) are supported in the Microsoft identity platform applications.

## Account types in the public cloud

In the Microsoft Azure public cloud, most types of apps can sign in users with any audience:

- If you're writing a line-of-business (LOB) application, you can sign in users in your own organization. Such an application is sometimes called *single-tenant*.
- If you're an independent software vendor (ISV), you can write an application that signs in users:

    - In any organization. Such an application is called a *multitenant* web application. You'll sometimes read that it signs in users with their work or school accounts.
    - With their work or school or personal Microsoft accounts.
    - With only personal Microsoft accounts.
- If you're writing a business-to-consumer application, you can also sign in users with their social identities, by using Azure Active Directory B2C (Azure AD B2C). Effective May 1, 2025, Azure AD B2C will no longer be available to purchase for new customers. To learn more, please see [Is Azure AD B2C still available to purchase?](/en-us/azure/active-directory-b2c/faq?tabs=app-reg-ga#azure-ad-b2c-end-of-sale) in our FAQ.

## Account type support in authentication flows

Some account types can't be used with certain authentication flows. For instance, in desktop, Universal Windows Platform (UWP), or daemon applications:

- Daemon applications can be used only with Microsoft Entra organizations. It doesn't make sense to try to use daemon applications to manipulate Microsoft personal accounts. The admin consent will never be granted.
- You can use the integrated Windows authentication flow only with work or school accounts (in your organization or any organization). Integrated Windows authentication works with domain accounts, and it requires the machines to be domain-joined or Microsoft Entra joined. This flow doesn't make sense for personal Microsoft accounts.
- The [Resource Owner Password Credentials grant](v2-oauth-ropc) (username/password) can't be used with personal Microsoft accounts. Personal Microsoft accounts require that the user consents to accessing personal resources at each sign-in session. That's why this behavior isn't compatible with non-interactive flows.

## Account types in national clouds

Apps can also sign in users in [national clouds](authentication-national-cloud). However, Microsoft personal accounts aren't supported in these clouds. That's why the supported account types are reduced, for these clouds, to your organization (single tenant) or any organizations (multitenant applications).
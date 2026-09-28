---
layout: Conceptual
title: Use MSAL.js with Azure AD B2C - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/msal-b2c-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: The Microsoft Authentication Library for JavaScript (MSAL.js) enables applications to work with Azure AD B2C and acquire tokens to call secured web APIs. These web APIs can be Microsoft Graph, other Microsoft APIs, web APIs from others, or your own web API.
manager: pmwongera
ms.custom: 
ms.date: 2023-03-07T00:00:00.0000000Z
ms.reviewer: negoe
ms.topic: concept-article
locale: en-us
document_id: 5b24fece-c54c-519a-7d3a-13db520d776e
document_version_independent_id: 34749db8-8bda-c17d-c16e-17271223ddc1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/msal-b2c-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/msal-b2c-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/msal-b2c-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: a7538264-01b9-622e-7f5d-15726863d85e
---

# Use MSAL.js with Azure AD B2C - Microsoft identity platform | Microsoft Learn

Important

Effective May 1, 2025, Azure Active Directory B2C (Azure AD B2C) is no longer available for new customers to purchase. To learn more, see [Is Azure AD B2C still available to purchase?](/en-us/azure/active-directory-b2c/faq?tabs=app-reg-ga#azure-ad-b2c-end-of-sale) in our FAQ.

The [Microsoft Authentication Library for JavaScript (MSAL.js)](https://github.com/AzureAD/microsoft-authentication-library-for-js) enables JavaScript developers to authenticate users with social and local identities using [Azure Active Directory B2C](/en-us/azure/active-directory-b2c/overview) (Azure AD B2C).

By using Azure AD B2C as an identity management service, you can customize and control how your customers sign up, sign in, and manage their profiles when they use your applications.

Azure AD B2C also enables you to brand and customize the UI that your application displays during the authentication process.

## Supported app types and scenarios

MSAL.js enables [single-page applications](/en-us/azure/active-directory-b2c/application-types#single-page-applications) to sign-in users with Azure AD B2C using the [authorization code flow with PKCE](/en-us/azure/active-directory-b2c/authorization-code-flow) grant. With MSAL.js and Azure AD B2C:

- Users **can** authenticate with their social and local identities.
- Users **can** be authorized to access Azure AD B2C protected resources (but not Microsoft Entra protected resources).
- Users **cannot** obtain tokens for Microsoft APIs (for example, MS Graph API) using [delegated permissions](permissions-consent-overview#types-of-permissions).
- Users with administrator privileges **can** obtain tokens for Microsoft APIs (for example, MS Graph API) using [delegated permissions](permissions-consent-overview#types-of-permissions).

For more information, see: [Working with Azure AD B2C](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-browser/docs/working-with-b2c.md)
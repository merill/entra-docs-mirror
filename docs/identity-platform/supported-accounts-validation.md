---
layout: Conceptual
title: Validation differences by supported account types - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/supported-accounts-validation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn about the validation differences of various properties for different supported account types when registering your app with the Microsoft identity platform.
manager: pmwongera
ms.custom: 
ms.date: 2026-09-25T00:00:00.0000000Z
ms.reviewer: sureshja
ms.topic: reference
ai-usage: ai-assisted
locale: en-us
document_id: 9a96dee0-81a3-b66f-6051-d0aa59ca3bb9
document_version_independent_id: c7d5e3c7-2701-e003-bc2e-129a6bb24b9d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/supported-accounts-validation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/supported-accounts-validation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/supported-accounts-validation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 24b5926e-605e-5a1c-35eb-5ea085f78748
---

# Validation differences by supported account types - Microsoft identity platform | Microsoft Learn

When registering an application with the Microsoft identity platform for developers, you're asked to select which account types your application supports. You can refer to the **Help me choose** link under **Supported account types** during the registration process. The value you select for this property has implications on other app object properties.

After the application has been registered, you can check or change the account type that the application supports at any time. Under the **Manage** pane of your application, search for **Manifest** and find the `signInAudience` value. The different account types, and the corresponding `signInAudience` are shown in the following table:

| Supported account types (Register an application) | `signInAudience`(Manifest) |
| --- | --- |
| Accounts in this organizational directory only (Single tenant) | `AzureADMyOrg` |
| Accounts in any organizational directory (Any Microsoft Entra directory - Multitenant) | `AzureADMultipleOrgs` |
| Accounts in any organizational directory (Any Microsoft Entra directory - Multitenant) and personal Microsoft accounts (such as Skype, Xbox) | `AzureADandPersonalMicrosoftAccount` |
| Personal Microsoft accounts only | `PersonalMicrosoftAccount` |

If you change this property you may need to change other properties first.

## Validation differences

See the following table for the validation differences of various properties for different supported account types.

| Property | `AzureADMyOrg` | `AzureADMultipleOrgs` | `AzureADandPersonalMicrosoftAccount`and`PersonalMicrosoftAccount` |
| --- | --- | --- | --- |
| Application ID URI (`identifierURIs`) | Must be unique in the tenant `urn://` schemes are supported  Wildcards aren't supported  Query strings and fragments are supported  Maximum length of 255 characters  No limit\* on number of identifierURIs | Must be globally unique `urn://` schemes are supported  Wildcards aren't supported  Query strings and fragments are supported  Maximum length of 255 characters  No limit\* on number of identifierURIs | Must be globally unique `urn://` schemes aren't supported  Wildcards, fragments, and query strings aren't supported  Maximum length of 120 characters  Maximum of 50 identifierURIs |
| National clouds | Supported | Supported | Not supported |
| Certificates (`keyCredentials`) | Symmetric signing key | Symmetric signing key | Encryption and asymmetric signing key |
| Client secrets (`passwordCredentials`) | No limit\* | No limit\* | Maximum of two client secrets |
| Redirect URIs (`replyURLs`) | See [Redirect URI/reply URL restrictions and limitations](reply-url) for more info. |  |  |
| API permissions (`requiredResourceAccess`) | No more than 50 total APIs (resource apps), with no more than 10 APIs from other tenants. No more than 400 permissions total across all APIs. | No more than 50 total APIs (resource apps), with no more than 10 APIs from other tenants. No more than 400 permissions total across all APIs. | No more than 50 total APIs (resource apps), with no more than 10 APIs from other tenants. No more than 200 permissions total across all APIs. Maximum of 30 permissions per resource (for example, Microsoft Graph). |
| Scopes defined by this API (`oauth2Permissions`) | Maximum scope name length of 120 characters  Default limit of 700 permission definitions, shared with app roles. See [App role limits](howto-add-app-roles-in-apps#app-role-limits). | Maximum scope name length of 120 characters  Default limit of 700 permission definitions, shared with app roles. See [App role limits](howto-add-app-roles-in-apps#app-role-limits). | Maximum scope name length of 40 characters  Maximum of 100 scopes defined, also subject to the shared [app role limit](howto-add-app-roles-in-apps#app-role-limits). |
| Authorized client applications (`preAuthorizedApplications`) | No set limit\* | No set limit\* | Total maximum of 500  Maximum of 100 client apps defined  Maximum of 30 scopes defined per client |
| appRoles | Supported  Default limit of 700 permission definitions, shared with exposed delegated permission scopes. See [App role limits](howto-add-app-roles-in-apps#app-role-limits). | Supported  Default limit of 700 permission definitions, shared with exposed delegated permission scopes. See [App role limits](howto-add-app-roles-in-apps#app-role-limits). | `PersonalMicrosoftAccount`: Not supported `AzureADandPersonalMicrosoftAccount`: Supported, subject to the shared [app role limit](howto-add-app-roles-in-apps#app-role-limits).  App roles are not supported for consumer (MSA) users of the application at runtime |
| Front-channel logout URL | `https://localhost` is allowed `http` scheme isn't allowed  Maximum length of 255 characters | `https://localhost` is allowed `http` scheme isn't allowed  Maximum length of 255 characters | `https://localhost` is allowed, `http://localhost` fails `http` scheme isn't allowed  Maximum length of 255 characters |
| Display name | Maximum length of 120 characters | Maximum length of 120 characters | Maximum length of 90 characters |

\* There's an aggregate limit of 1,200 entries across the collection properties in the application manifest. Individual collection limits also apply. See [Manifest limits](reference-microsoft-graph-app-manifest#manifest-limits).
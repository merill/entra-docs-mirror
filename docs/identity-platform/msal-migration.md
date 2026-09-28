---
layout: Conceptual
title: Migrate to the Microsoft Authentication Library (MSAL) - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/msal-migration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn about the differences between the Microsoft Authentication Library (MSAL) and Azure AD Authentication Library (ADAL) and how to migrate to MSAL.
manager: dougeby
ms.custom: has-adal-ref
ms.date: 2025-02-27T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.topic: concept-article
locale: en-us
document_id: d686df6b-2d78-779b-d09c-d6c3e41e4adf
document_version_independent_id: 832e4900-0aeb-c414-be10-b93ee5c1a79d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/msal-migration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/msal-migration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/msal-migration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: 96a3c656-3c64-0f2a-951d-d30b9b3c49d2
---

# Migrate to the Microsoft Authentication Library (MSAL) - Microsoft identity platform | Microsoft Learn

If any of your applications use the Azure Active Directory Authentication Library (ADAL) for authentication and authorization capabilities, it's time to migrate them to the [Microsoft Authentication Library (MSAL)](/en-us/entra/msal).

- All Microsoft support and development for ADAL, including security fixes, ended on June 30, 2023.
- There were no ADAL feature releases or new platform version releases planned before the deprecation date.
- No new features have been added to ADAL since June 30, 2020.

Warning

Azure Active Directory Authentication Library (ADAL) has been deprecated. While existing apps that use ADAL will continue to work, Microsoft will no longer release security fixes on ADAL. Use the [Microsoft Authentication Library (MSAL)](/en-us/entra/msal/) to avoid putting your app's security at risk.

## Why switch to MSAL?

If you've developed apps using the Azure AD (v1.0) endpoint, you're likely using ADAL. Since Microsoft identity platform (v2.0) endpoint has changed significantly, the new library (MSAL) was entirely built for the new endpoint.

MSAL is designed to enable a secure solution without developers having to worry about the implementation details. It simplifies and manages acquiring, managing, caching, and refreshing tokens, and uses best practices for resilience. We recommend you use MSAL to [increase the resilience of authentication and authorization in client applications that you develop](../architecture/resilience-client-app?tabs=csharp#use-the-microsoft-authentication-library-msal).

MSAL provides multiple benefits over ADAL, including the following features:

| Features | MSAL | ADAL |
| --- | --- | --- |
| **Security** |  |  |
| Security fixes beyond June 2023 | ![Security fixes beyond June 2023 - MSAL provides the feature](media/common/yes.png) | ![Security fixes beyond June 2023 - ADAL doesn't provide the feature](media/common/no.png) |
| Proactively refresh and revoke tokens based on policy or critical events for Microsoft Graph and other APIs that support [Continuous Access Evaluation (CAE)](app-resilience-continuous-access-evaluation). | ![Proactively refresh and revoke tokens based on policy or critical events for Microsoft Graph and other APIs that support Continuous Access Evaluation (CAE) - MSAL provides the feature](media/common/yes.png) | ![Proactively refresh and revoke tokens based on policy or critical events for Microsoft Graph and other APIs that support Continuous Access Evaluation (CAE) - ADAL doesn't provide the feature](media/common/no.png) |
| Standards compliant with OAuth v2.0 and OpenID Connect (OIDC) | ![Standards compliant with OAuth v2.0 and OpenID Connect (OIDC) - MSAL provides the feature](media/common/yes.png) | ![Standards compliant with OAuth v2.0 and OpenID Connect (OIDC) - ADAL doesn't provide the feature](media/common/no.png) |
| **User accounts and experiences** |  |  |
| Microsoft Entra accounts | ![Microsoft Entra accounts - MSAL provides the feature](media/common/yes.png) | ![Microsoft Entra accounts - ADAL provides the feature](media/common/yes.png) |
| Microsoft account (MSA) | ![Microsoft account (MSA) - MSAL provides the feature](media/common/yes.png) | ![Microsoft account (MSA) - ADAL doesn't provide the feature](media/common/no.png) |
| Azure AD B2C accounts | ![Azure AD B2C accounts - MSAL provides the feature](media/common/yes.png) | ![Azure AD B2C accounts - ADAL doesn't provide the feature](media/common/no.png) |
| Best single sign-on experience | ![Best single sign-on experience - MSAL provides the feature](media/common/yes.png) | ![Best single sign-on experience - ADAL doesn't provide the feature](media/common/no.png) |
| **Authentication experiences** |  |  |
| Continuous access evaluation through proactive token refresh | ![Proactive token renewal - MSAL provides the feature](media/common/yes.png) | ![Proactive token renewal - ADAL doesn't provide the feature](media/common/no.png) |
| Throttling | ![Throttling - MSAL provides the feature](media/common/yes.png) | ![Throttling - ADAL doesn't provide the feature](media/common/no.png) |
| Auth broker support | ![Device-based Conditional Access policy - MSAL has the feature built-in](media/common/yes.png) | ![Device-based Conditional Access policy - ADAL doesn't provide the feature](media/common/no.png) |
| Token protection | ![Token protection - MSAL provides the feature](media/common/yes.png) | ![Token protection - ADAL doesn't provide the feature](media/common/no.png) |

## Additional capabilities of MSAL over ADAL

- Proof of possession tokens
- Microsoft Entra certificate-based authentication (CBA) on mobile
- System browsers on mobile devices
- Where ADAL had only authentication context class, MSAL exposes the notion of a collection of client apps (public client and confidential client).

## Active Directory Federation Services (AD FS) support in MSAL

You can use MSAL.NET, MSAL Java, MSAL.js, and MSAL Python to get tokens from Active Directory Federation Services (AD FS) 2019 or later. Earlier versions of AD FS, including AD FS 2016, are unsupported by MSAL.

If you need to continue using AD FS, you should upgrade to AD FS 2019 or later before you update your applications from ADAL to MSAL.

## How to migrate to MSAL

Before you start the migration, you need to identify which of your apps are using ADAL for authentication. Follow the steps in this article to get a list by using the Azure portal:

- [How to: Get a complete list of apps using ADAL in your tenant](howto-get-list-of-all-auth-library-apps)

After identifying applications that use ADAL, migrate them to MSAL depending on your app type:

**Single-page app (SPA)**

- [ADAL.js to MSAL.js](msal-compare-msal-js-and-adal-js)

**Web app**

- [ADAL Node to MSAL Node](msal-node-migration)
- [ADAL.NET to MSAL.NET](/en-us/entra/msal/dotnet/how-to/msal-net-migration)

**Web API**

- [ADAL Java to MSAL Java](/en-us/entra/msal/java/advanced/migrate-adal-msal-java)
- [ADAL Python to MSAL Python](/en-us/entra/msal/python/advanced/migrate-python-adal-msal)
- [ADAL.NET to MSAL.NET](/en-us/entra/msal/dotnet/how-to/msal-net-migration)

**Desktop app**

- [ADAL Java to MSAL Java](/en-us/entra/msal/java/advanced/migrate-adal-msal-java)
- [ADAL Python to MSAL Python](/en-us/entra/msal/python/advanced/migrate-python-adal-msal)
- [ADAL.NET to MSAL.NET](/en-us/entra/msal/dotnet/how-to/msal-net-migration)

**Mobile app**

- [ADAL.Android to MSAL.Android](migrate-android-adal-msal)
- [ADAL.iOS to MSAL.iOS](/en-us/entra/msal/objc/migrate-objc-adal-msal)

**Service / daemon app**

- [ADAL Python to MSAL Python](/en-us/entra/msal/python/advanced/migrate-python-adal-msal)
- [ADAL.NET to MSAL.NET](/en-us/entra/msal/dotnet/how-to/msal-net-migration)
- [ADAL Node to MSAL Node](msal-node-migration)
- [ADAL Java to MSAL Java](/en-us/entra/msal/java/advanced/migrate-adal-msal-java)

MSAL Supports a wide range of application types and scenarios. Refer to [Microsoft Authentication Library support for several application types](reference-v2-libraries#single-page-application-spa).

ADAL to MSAL migration guide for different platforms are available in the following links:

- [Migrate to MSAL iOS and macOS](/en-us/entra/msal/objc/migrate-objc-adal-msal)
- [Migrate to MSAL Java](/en-us/entra/msal/java/advanced/migrate-adal-msal-java)
- [Migrate to MSAL.js](msal-compare-msal-js-and-adal-js)
- [Migrate to MSAL .NET](/en-us/entra/msal/dotnet/how-to/msal-net-migration)
- [Migrate to MSAL Node](msal-node-migration)
- [Migrate to MSAL Python](/en-us/entra/msal/python/advanced/migrate-python-adal-msal)

## Migration help

If you have questions about migrating your app from ADAL to MSAL, here are some options:

- Post your question on [Microsoft Q&A](/en-us/answers/topics/azure-ad-adal-deprecation.html) and tag it with `[azure-ad-adal-deprecation]`.
- Open an issue in the library's GitHub repository. See the [Languages and frameworks](msal-overview#msal-languages-and-frameworks) section of the MSAL overview article for links to each library's repo.

If you partnered with an Independent Software Vendor (ISV) in the development of your application, we recommend that you contact them directly to understand their migration journey to MSAL.
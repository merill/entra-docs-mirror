---
layout: Conceptual
title: App manifest (Azure AD Graph format) deprecation - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/azure-active-directory-graph-app-manifest-deprecation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Describes the deprecation of the app manifest (Azure AD Graph format) and attribute differences in the new format.
manager: pmwongera
ms.topic: concept-article
ms.date: 2024-09-18T00:00:00.0000000Z
ms.custom: 
ms.reviewer: 
locale: en-us
document_id: a510a48b-cb79-bcb3-7a04-323b18ebbdf9
document_version_independent_id: a510a48b-cb79-bcb3-7a04-323b18ebbdf9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/azure-active-directory-graph-app-manifest-deprecation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/azure-active-directory-graph-app-manifest-deprecation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/azure-active-directory-graph-app-manifest-deprecation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 0c0848e7-d20e-5b87-2e17-9db8426a4295
---

# App manifest (Azure AD Graph format) deprecation - Microsoft identity platform | Microsoft Learn

Following the Azure AD Graph deprecation, the Azure AD Graph format of application manifests is deprecated and the Microsoft Entra admin center displays app manifests in Microsoft Graph format. Read this article to learn more about how the app manifest migration impacts your user experience.

Important

Apps registered with your personal Microsoft account (MSA account) are not in scope for this deprecation. Apps registered with your personal MSA account will continue to manage app manifests in the Azure AD Graph format in the Microsoft Entra admin center until further notice.

## Migration date

From June 13 to September 16 2024, the **App registrations** manifest page in the Microsoft Entra admin center launched a new tabbed experience that allows you to view, edit, upload, download the app manifest in both Azure AD Graph format and Microsoft Graph format.

Important

The new tabbed experience is rolling out to Microsoft Entra users in batches to ensure the quality of your experience. You may not see the new experience immediately.

Starting January 7 2025, you won't be able to view, save, upload, or download the Azure AD Graph app manifest in the **App registrations** manifest page in the Microsoft Entra admin center.

## How does app manifest migration impact your user experience?

If you don't view, edit, or save app manifests, this migration doesn't impact your workflow.

If you view or edit app manifests, you notice the attribute differences between Azure AD Graph format and Microsoft Graph format. We recommend that you start viewing and editing app manifests following the [Microsoft Graph format reference](reference-microsoft-graph-app-manifest).

If your workflow requires you to save the manifests in your source repository for use later, you need to convert an app manifest in Azure AD Graph format to Microsoft Graph format.

## Attribute differences between Azure AD Graph and Microsoft Graph formats

Most Azure AD Graph app manifest attributes stay the same. However, the following Azure AD Graph app manifest attributes have been deprecated, renamed, or relocated in the Microsoft Graph manifest.

| Azure AD manifest attribute | Microsoft Graph manifest |
| --- | --- |
| `acceptMappedClaims` | Relocated as `acceptMappedClaims` property of the `api` attribute |
| `accessTokenAcceptedVersion` | Relocated and renamed as `requestedAccessTokenVersion` property of the `api` attribute |
| `allowPublicClient` | Renamed as `isFallbackPublicClient` |
| `errorUrl` | Deprecated/no longer support |
| `informationalUrls` | Renamed as `info` |
| `knownClientApplications` | Relocated as a property of the `api` attribute |
| `logoUrl` | Relocated as a property of the `info` attribute |
| `logoutUrl` | Relocated as property `logoutUrl` of the `web` attribute |
| `name` | `displayName` |
| `oauth2AllowIdTokenImplicitFlow` | Relocated and renamed as property `enableIdTokenIssuance` of the `implicitGrantSettings` property in the `web` attribute |
| `oauth2AllowImplicitFlow` | Relocated and renamed as property `enableAccessTokenIssuance` of property `implicitGrantSettings` in the `web` attribute |
| `oauth2Permissions` | Relocated and renamed as `oauth2PermissionScopes` property of the `api` attribute |
| `preAuthorizedApplications` | Relocated as `preAuthorizedApplications` property of the `api` attribute |
| `replyUrlsWithType` | Renamed as property `redirectUris` in multiple attributes: `web` attribute, `spa` attribute, `publicClient` attribute |
| `signInUrl` | Relocated and renamed as property `homePageUrl` of the `web` attribute |
| `trustedCertificateSubjects` | This is a Microsoft internal property. The portal shows v1.0 version of MS Graph app manifest while this property is only present in beta version of MS Graph app manifest. Continue to edit this property using Azure AD Graph app manifest in Microsoft Entra admin center. We will expose MS Graph app manifest beta version in Microsoft Entra admin center before deprecating Azure AD Graph app manifest |

## How do I tell the format of my app manifest?

You can tell whether an app manifest is an Azure AD Graph format or Microsoft Graph format by the attributes it contains. For example,

- If an app manifest has the attribute `replyUrlsWithType`, then it is in Azure AD Graph format.
- If an app manifest has the attribute `implicitGrantSettings`, it is in Microsoft Graph format.

## Convert an app manifest in Azure AD Graph format to Microsoft Graph format

If you have stored an app manifest in Azure AD Graph format and want to convert it to Microsoft Graph format:

Between June 13 2024 and January 7 2025, you can follow the steps below and use the portal to convert an app manifest in Azure AD Graph format to Microsoft format:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) as at least an [Application Developer](/en-us/entra/identity/role-based-access-control/permissions-reference#application-developer).
2. Browse to **Entra ID** &gt; **App registrations**.
3. Select **New registration** and create a new app registration.
4. In the **Manifest** page for that application, select **Azure AD Graph app manifest** tab.
5. Upload the app manifest in Azure AD Graph format that you have.
6. Select the **Microsoft Graph app manifest** tab.
7. Select **download**.

Starting January 7 2025, the Microsoft Entra admin center will no longer support app manifests in Azure AD Graph format. However, you can perform the conversion manually.

1. Browse to **Entra ID** &gt; **App registrations**.
2. Select **New registration** and create a new app registration.
3. An app manifest is created in the new format with default values.
4. Go through each attribute in Azure AD Graph formatted app manifest one by one and edit the corresponding attribute in the Microsoft Graph formatted app manifest to match its value.

    1. If the attribute is listed in Attribute differences between Azure AD Graph manifest and Microsoft Graph manifest, you need to understand the syntax and semantics of old and new attributes so that you can successfully edit the new attribute's value in Microsoft Graph app manifest.
    2. If the attribute isn't listed in Attribute differences between Azure AD Graph manifest and Microsoft Graph manifest but you can't find a corresponding attribute in Microsoft Graph app manifest, this attribute is likely to have been deprecated and you can discard this attribute.
    3. For all other attributes, you can copy the value of the attribute in Azure AD Graph app manifest and paste it into the value of the attribute in Microsoft Graph app manifest.
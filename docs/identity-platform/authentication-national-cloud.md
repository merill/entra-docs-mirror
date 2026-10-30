---
layout: Conceptual
title: Microsoft Entra authentication & national clouds - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/authentication-national-cloud
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn about app registration and authentication endpoints for national clouds.
manager: pmwongera
ms.custom: references_regions
ms.date: 2025-01-15T00:00:00.0000000Z
ms.reviewer: negoe
ms.topic: concept-article
locale: en-us
document_id: 36ad8cf5-067f-6715-eabf-f0254d6ed7c8
document_version_independent_id: 8a4ff617-6d6b-d6ef-1691-82c9477a73e4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/authentication-national-cloud.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/authentication-national-cloud
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/authentication-national-cloud.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 65c28425-c0b6-ab42-cfb0-2723587cd08a
---

# Microsoft Entra authentication & national clouds - Microsoft identity platform | Microsoft Learn

National clouds are physically isolated instances of Azure. These regions of Azure are designed to make sure that data residency, sovereignty, and compliance requirements are honored within geographical boundaries.

Including the global Azure cloud, Microsoft Entra ID is deployed in the following national clouds:

- Azure Government
- Microsoft Azure operated by 21Vianet
- Azure Germany ([Closed on October 29, 2021](https://www.microsoft.com/cloud-platform/germany-cloud-regions)). Learn more about Azure Germany migration.

The individual national clouds and the global Azure cloud are cloud *instances*. Each cloud instance is separate from the others and has its own environment and *endpoints*. Cloud-specific endpoints include OAuth 2.0 access token and OpenID Connect ID token request endpoints, and URLs for app management and deployment.

As you develop your apps, use the endpoints for the cloud instance where you'll deploy the application.

## App registration endpoints

There's a separate Azure portal for each one of the national clouds. To integrate applications with the Microsoft identity platform in a national cloud, you're required to register your application separately in each Azure portal that's specific to the environment.

Note

Users with a Microsoft Entra guest account from another national cloud can’t access Cost management + Billing features to manage EA enrollments. The following table lists the base URLs for the Microsoft Entra endpoints used to register an application for each national cloud.

| National cloud | Azure portal endpoint |
| --- | --- |
| Azure portal for US Government | `https://portal.azure.us` |
| Azure portal China operated by 21Vianet | `https://portal.azure.cn` |
| Azure portal (global service) | `https://portal.azure.com` |

## Application endpoints

You can find the authentication endpoints for your application.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **App registrations**.
3. Select **Endpoints** in the top menu.

    The **Endpoints** page is displayed showing the authentication endpoints for the application.

    Use the endpoint that matches the authentication protocol you're using in conjunction with the **Application (client) ID** to craft the authentication request specific to your application.

## Microsoft Entra authentication endpoints

All the national clouds authenticate users separately in each environment and have separate authentication endpoints.

The following table lists the base URLs for the Microsoft Entra endpoints used to acquire tokens for each national cloud.

| National cloud | Microsoft Entra authentication endpoint |
| --- | --- |
| Microsoft Entra ID for US Government | `https://login.microsoftonline.us` |
| Microsoft Entra China operated by 21Vianet | `https://login.partner.microsoftonline.cn` |
| Microsoft Entra ID (global service) | `https://login.microsoftonline.com` |

You can form requests to the Microsoft Entra authorization or token endpoints by using the appropriate region-specific base URL. For example, for global Azure:

- Authorization common endpoint is `https://login.microsoftonline.com/common/oauth2/v2.0/authorize`.
- Token common endpoint is `https://login.microsoftonline.com/common/oauth2/v2.0/token`.

For single-tenant applications, replace "common" in the previous URLs with your tenant ID or name. An example is `https://login.microsoftonline.com/contoso.com`.

## Azure Germany (Microsoft Cloud Deutschland)

If you haven't migrated your application from Azure Germany, follow [Microsoft Entra information for the migration from Azure Germany](/en-us/microsoft-365/enterprise/ms-cloud-germany-transition-azure-ad) to get started.

## Microsoft Graph API

To learn how to call the Microsoft Graph APIs in a national cloud environment, go to [Microsoft Graph in national cloud deployments](/en-us/graph/deployments).

Some services and features in the global Azure cloud might be unavailable in other cloud instances like the national clouds.

To find out which services and features are available in a given cloud instance, see [Products available by region](https://azure.microsoft.com/global-infrastructure/services/?products=all&amp;regions=usgov-non-regional,us-dod-central,us-dod-east,usgov-arizona,usgov-iowa,usgov-texas,usgov-virginia,china-non-regional,china-east,china-east-2,china-north,china-north-2,germany-non-regional,germany-central,germany-northeast).

To learn how to build an application by using the Microsoft identity platform, follow the [Single-page application (SPA) using auth code flow tutorial](tutorial-v2-angular-auth-code). Specifically, this app will sign in a user and get an access token to call the Microsoft Graph API.
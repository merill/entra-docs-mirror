---
layout: Conceptual
title: Build resilience in external user authentication with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/resilience-b2b-authentication
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: A guide for IT admins and architects to building resilient authentication for external users
ms.topic: concept-article
ms.date: 2022-11-16T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 126351bd-99c0-0e07-cf40-572b138c05f4
document_version_independent_id: c2e0acce-466b-b8e0-bafe-50d6f97d8a25
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/resilience-b2b-authentication.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/resilience-b2b-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/resilience-b2b-authentication.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 8cd52cf0-51d7-830e-bf08-aa0bcebea4c2
---

# Build resilience in external user authentication with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

[Microsoft Entra B2B collaboration](../external-id/what-is-b2b) (Microsoft Entra B2B) is a feature of [External Identities](../external-id/external-collaboration-settings-configure) that enables collaboration with other organizations and individuals. It enables the secure onboarding of guest users into your Microsoft Entra tenant without having to manage their credentials. External users bring their identity and credentials with them from an external identity provider (IdP) so they don't have to remember a new credential.

## Ways to authenticate external users

You can choose the methods of external user authentication to your directory. You can use Microsoft IdPs or other IdPs.

With every external IdP, you take a dependency on the availability of that IdP. With some methods of connecting to IdPs, there are things you can do to increase your resilience.

Note

Microsoft Entra B2B has the built-in ability to authenticate any user from any [Microsoft Entra ID](../) tenant or with a personal [Microsoft Account](https://account.microsoft.com/account). You do not have to do any configuration with these built-in options.

### Considerations for resilience with other IdPs

When you use external IdPs for guest user authentication, there are configurations that you must maintain to prevent disruptions.

| Authentication Method | Resilience considerations |
| --- | --- |
| Federation with social IDPs like [Facebook](../external-id/facebook-federation) or [Google](../external-id/google-federation). | You must maintain your account with the IdP and configure your Client ID and Client Secret. |
| [SAML/WS-Fed identity provider (IdP) federation](../external-id/direct-federation) | You must collaborate with the IdP owner for access to their endpoints upon which you're dependent. You must maintain the metadata that contain the certificates and endpoints. |
| [Email one-time passcode](../external-id/one-time-passcode) | You're dependent on Microsoft's email system, the user's email system, and the user's email client. |

## Self-service sign-up

As an alternative to sending invitations or links, you can enable [Self-service sign-up](../external-id/self-service-sign-up-overview). This method allows external users to request access to an application. You must create an [API connector](../external-id/self-service-sign-up-add-api-connector) and associate it with a user flow. You associate user flows that define the user experience with one or more applications.

It's possible to use [API connectors](../external-id/api-connectors-overview) to integrate your self-service sign-up user flow with external systems' APIs. This API integration can be used for [custom approval workflows](../external-id/self-service-sign-up-add-approvals), [performing identity verification](../external-id/code-samples-self-service-sign-up), and other tasks such as overwriting user attributes. Using APIs requires that you manage the following dependencies.

- **API Connector Authentication**: Setting up a connector requires an endpoint URL, a username, and a password. Set up a process by which these credentials are maintained, and work with the API owner to ensure you know any expiration schedule.
- **API Connector Response**: Design API Connectors in the sign-up flow to fail gracefully if the API isn't available. Examine and provide to your API developers these [example API responses](../external-id/self-service-sign-up-add-api-connector) and the [best practices for troubleshooting](../external-id/self-service-sign-up-add-api-connector). Work with the API development team to test all possible response scenarios, including continuation, validation-error, and blocking responses.
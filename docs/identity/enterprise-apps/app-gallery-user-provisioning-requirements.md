---
layout: Conceptual
title: User provisioning requirements for Microsoft Entra App Gallery - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/app-gallery-user-provisioning-requirements
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: HildaK-pm
ms.author: hkinyunyu
ms.service: entra-id
ms.subservice: enterprise-apps
manager: msteele
description: Review the SCIM requirements for publishing a user provisioning integration in Microsoft Entra App Gallery.
ms.topic: concept-article
ms.date: 2026-08-26T00:00:00.0000000Z
ms.reviewer: hkinyunyu
ms.custom: enterprise-apps-article, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 84ccdc4a-d381-1241-be44-44afcb3f75dd
document_version_independent_id: 84ccdc4a-d381-1241-be44-44afcb3f75dd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/app-gallery-user-provisioning-requirements.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/app-gallery-user-provisioning-requirements
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/app-gallery-user-provisioning-requirements.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 96bff3e8-6c9e-230e-15a5-d46352e2eec6
---

# User provisioning requirements for Microsoft Entra App Gallery - Microsoft Entra ID | Microsoft Learn

Review these requirements before you validate and publish an application that supports user provisioning in Microsoft Entra App Gallery. For requirements that apply to every submission, see [Prerequisites to validate and publish your app](v2-howto-app-gallery-listing).

If your application also supports SSO, see [SSO requirements for Microsoft Entra App Gallery](app-gallery-sso-requirements).

## SCIM API requirements

Your System for Cross-Domain Identity Management (SCIM) API must meet the following requirements:

- Support a SCIM 2.0 user and group endpoint. User provisioning is required. Group provisioning is recommended. (Required)
- Support at least 25 requests per second per tenant so that users and groups are provisioned and deprovisioned without delay. (Required)
- Validate and test user and group provisioning by using a [non-gallery application](../app-provisioning/use-scim-to-provision-users-and-groups#getting-started). (Required)
- Validate client credentials authentication or another supported authentication method by using a [non-gallery application](../app-provisioning/use-scim-to-provision-users-and-groups#getting-started). (Required)
- Support soft delete or hard delete for users. You can support both methods. (Required)
- Return a successful response with zero results when a query doesn't match a user. Don't return a bad request. (Required)
- Support schema discovery on the SCIM endpoint. (Required)
- Support updating multiple group memberships with a single `PATCH` request. (Recommended)
- Support SCIM bulk APIs to improve connector performance. (Recommended)

## SCIM authentication requirements

Use OAuth 2.0 client credentials or workload identity federation to authenticate the Microsoft Entra provisioning service to your SCIM endpoint. Microsoft doesn't onboard SCIM provisioning applications that use basic authentication, long-lived bearer tokens, or the authorization code grant flow.

### OAuth 2.0 client credentials

If you use OAuth 2.0 client credentials, meet these requirements:

- Provide customers with a client ID, client secret, token endpoint, and SCIM endpoint. (Required)
- Set the client secret to expire after one to three years. Don't issue an access token when the credentials are expired. (Required)
- Enable smooth secret rotation by allowing multiple active secrets and deletion of old secrets. Alternatively, let customers create a new client ID and client secret. (Required)
- Set access tokens to expire between 60 minutes and six hours after issuance. (Required)

For implementation guidance, see [OAuth 2.0 client credentials grant flow](../app-provisioning/use-scim-to-provision-users-and-groups#oauth-20-client-credentials-grant-flow).

### Workload identity federation

Workload identity federation lets the Microsoft Entra provisioning service authenticate to your SCIM endpoint without storing a long-lived secret. Microsoft Entra ID presents a signed JSON Web Token (JWT) assertion to your token endpoint by using the OAuth 2.0 JWT bearer profile in [RFC 7523](https://datatracker.ietf.org/doc/html/rfc7523). Your token endpoint validates the assertion and returns a short-lived access token for the SCIM endpoint.

To support workload identity federation, validate Microsoft Entra-issued JWTs against Microsoft's published JSON Web Key Set and issue access tokens scoped to your SCIM endpoint. For the configuration flow, token claims, and implementation requirements, see [Workload identity federation for SCIM provisioning](https://github.com/AzureAD/SCIMReferenceCode/blob/master/Workload-Identity-Federation-for-SCIM-Provisioning.md). (Recommended)

## ISV requirements

As an independent software vendor (ISV), you must meet these requirements:

- Establish engineering and support contacts for App Gallery onboarding, post-onboarding support, and future communication from Microsoft. (Required)
- Publish documentation for your SCIM endpoint. (Required)
- Deploy your SCIM provisioning integration to at least 100 mutual customers by using the Microsoft Entra non-gallery approach.
- Meet the compliance requirements for each cloud where you plan to list the application, such as Azure Government or Microsoft Azure operated by 21Vianet. (Required)

## Known limitations

Review [Known issues for application provisioning](../app-provisioning/known-issues?pivots=app-provisioning) before submitting your integration.

## Validate your integration

After your SCIM endpoint meets these requirements, validate it against the Microsoft Entra provisioning service and submit the results with your gallery submission. For instructions, see [Validate user provisioning for Microsoft Entra App Gallery](validate-user-provisioning-app-gallery).

## Prepare customer documentation

Publish documentation that includes at least the following information:

- An introduction to your provisioning functionality.
- Licensing requirements.
- Roles required to configure provisioning.
- Your SCIM endpoint and supported resources and attributes.
- Authentication setup and credential rotation instructions.
- Testing steps for pilot users.
- Troubleshooting information, including error codes and messages.
- Support options.
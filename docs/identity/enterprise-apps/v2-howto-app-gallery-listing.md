---
layout: Conceptual
title: Prerequisites to validate and publish your app - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/v2-howto-app-gallery-listing
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Review the shared prerequisites for validating and publishing an application in Microsoft Entra App Gallery.
ms.topic: how-to
ms.date: 2026-09-02T00:00:00.0000000Z
ms.reviewer: hkinyunyu
ms.custom: kr2b-contr-experiment, enterprise-apps-article
ai-usage: ai-assisted
locale: en-us
document_id: bc9add8e-9cd4-1f17-0429-a95ac85f4c37
document_version_independent_id: b5bf54e4-54cd-2c94-123a-ed046c3e0a9d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/v2-howto-app-gallery-listing.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/v2-howto-app-gallery-listing
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/v2-howto-app-gallery-listing.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 9446f192-2ba6-d25a-2b37-b0a31ad17886
---

# Prerequisites to validate and publish your app - Microsoft Entra ID | Microsoft Learn

Microsoft Entra App Gallery is a catalog of thousands of applications. When Microsoft publishes your application in the gallery, customers can discover it and add it to their tenants. For more information, see [Overview of Microsoft Entra App Gallery](overview-application-gallery).

Before you validate your application, review the shared prerequisites and the requirements for each capability that you plan to publish.

## Choose the capabilities to publish

Review the requirements that apply to your application:

- For Security Assertion Markup Language (SAML) or OpenID Connect (OIDC) integration, see [SSO requirements for Microsoft Entra App Gallery](app-gallery-sso-requirements).
- For System for Cross-Domain Identity Management (SCIM) integration, see [User provisioning requirements for Microsoft Entra App Gallery](app-gallery-user-provisioning-requirements).

If your application supports both SSO and user provisioning, complete the requirements and validation for both capabilities.

## Shared prerequisites

Before you submit an application, complete these prerequisites:

- Read and agree to the [Microsoft Entra App Gallery terms and conditions](https://azure.microsoft.com/support/legal/active-directory-app-gallery-terms/).
- Prepare a production-ready application that customers can access.
- Establish engineering and support contacts for onboarding and post-onboarding support.
- Prepare public customer documentation for each capability that you plan to publish.
- Create a test tenant and test accounts. You can join the [Microsoft 365 Developer Program](/en-us/office/developer-program/microsoft-365-developer-program) to get a renewable development subscription with Microsoft Entra features.
- Associate your organization with the [Microsoft AI Cloud Partner Program](https://partner.microsoft.com/partnership).
- Provide a **Partner One ID (formerly Microsoft Partner Network (MPN) ID)** associated with your organization. This identifier is used during the Microsoft Entra App Gallery onboarding and publishing process.

## Partner One ID

A Partner One ID identifies your organization in the Microsoft AI Cloud Partner Program. Provide the Partner One ID associated with the organization that will be listed as the application's publisher in Microsoft Entra App Gallery.

Note

If you don't know your Partner One ID, contact your organization's Microsoft AI Cloud Partner Program administrator. For information about Partner One IDs and partner accounts, see [Partner Center documentation](/en-us/partner-center/).

## Prepare customer documentation

Clear documentation helps customers configure and support your integration. Include the following information:

- Supported capabilities, protocols, versions, and SKUs.
- Licensing requirements.
- Roles required to configure the integration.
- Configuration and testing steps.
- Troubleshooting information, including error codes and messages.
- Support options.

The SSO and user provisioning requirement articles describe the capability-specific information to include.

## Publish your application

After your application meets the applicable requirements and passes validation, see [Publish your app to Microsoft Entra App Gallery](publish-app-gallery).
---
layout: Conceptual
title: How the Microsoft identity platform uses the SAML protocol - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/saml-protocol-reference
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: This article provides an overview of the single sign-on and Single Sign-Out SAML profiles in Microsoft Entra ID.
manager: pmwongera
ms.custom: 
ms.date: 2022-11-04T00:00:00.0000000Z
ms.reviewer: 
ms.topic: reference
locale: en-us
document_id: 45c0a575-9221-fa7c-b24f-4168bba5ff93
document_version_independent_id: 63f035d2-beff-b005-df3e-42b8b72c6285
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/saml-protocol-reference.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/saml-protocol-reference
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/saml-protocol-reference.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 26e8a47a-56d2-819c-8a4a-779893429e6f
---

# How the Microsoft identity platform uses the SAML protocol - Microsoft identity platform | Microsoft Learn

The Microsoft identity platform uses the SAML 2.0 and other protocols to enable applications to provide a single sign-on (SSO) experience to their users. The [SSO](single-sign-on-saml-protocol) and [Single Sign-Out](single-sign-out-saml-protocol) SAML profiles of Microsoft Entra ID explain how SAML assertions, protocols, and bindings are used in the identity provider service.

The SAML protocol requires the identity provider (Microsoft identity platform) and the service provider (the application) to exchange information about themselves.

When an application is registered with Microsoft Entra ID, the app developer registers federation-related information with Microsoft Entra ID. This information includes the **Redirect URI** and **Metadata URI** of the application.

The Microsoft identity platform uses the cloud service's **Metadata URI** to retrieve the signing key and the logout URI. This way the Microsoft identity platform can send the response to the correct URL. In the [Microsoft Entra admin center](https://entra.microsoft.com/);

- Open the app in **Microsoft Entra ID** and select **App registrations**
- Under **Manage**, select **Authentication**. From there you can update the Logout URL.

Microsoft Entra ID exposes tenant-specific and common (tenant-independent) SSO and single sign-out endpoints. These URLs represent addressable locations, and aren't only identifiers. You can then go to the endpoint to read the metadata.

- The tenant-specific endpoint is located at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`. The *&lt;TenantDomainName&gt;* placeholder represents a registered domain name or TenantID GUID of a Microsoft Entra tenant. For example, the federation metadata of the `contoso.com` tenant is at: `https://login.microsoftonline.com/contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`
- The tenant-independent endpoint is located at `https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml`. In this endpoint address, *common* appears instead of a tenant domain name or ID.
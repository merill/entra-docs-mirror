---
layout: Conceptual
title: SSO requirements for Microsoft Entra App Gallery - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/app-gallery-sso-requirements
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: HildaK-pm
ms.author: hkinyunyu
ms.service: entra-id
ms.subservice: enterprise-apps
manager: msteele
description: Review the SAML and OpenID Connect requirements for publishing an application in Microsoft Entra App Gallery.
ms.topic: concept-article
ms.date: 2026-08-26T00:00:00.0000000Z
ms.reviewer: hkinyunyu
ms.custom: enterprise-apps-article, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 358e4453-0d34-c361-c875-26fd8ca87c12
document_version_independent_id: 358e4453-0d34-c361-c875-26fd8ca87c12
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/app-gallery-sso-requirements.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/app-gallery-sso-requirements
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/app-gallery-sso-requirements.md
platformId: 66e122fa-ff98-8d92-8cac-60bce46d3905
---

# SSO requirements for Microsoft Entra App Gallery - Microsoft Entra ID | Microsoft Learn

Review these requirements before you validate and publish an application that supports single sign-on (SSO) in Microsoft Entra App Gallery. For requirements that apply to every submission, see [Prerequisites to validate and publish your app](v2-howto-app-gallery-listing).

If your application also supports user provisioning, see [User provisioning requirements for Microsoft Entra App Gallery](app-gallery-user-provisioning-requirements).

## SAML SSO requirements

These requirements apply to applications that use Security Assertion Markup Language (SAML) 2.0 for SSO.

Your application must meet the following authentication requirements:

- Support the SAML 2.0 protocol in service provider-initiated mode, identity provider-initiated mode, or both. (Required)
- Validate the SAML token certificate key, certificate validity, issuer, audience, and other required user claims. (Required)
- Test your SAML integration with Microsoft Entra ID by using a non-gallery application. (Required)
- Support [SAML Single Logout](../../identity-platform/single-sign-out-saml-protocol). (Recommended)
- Retrieve the identity provider SAML federation metadata from the URL that Microsoft Entra ID provides. This approach reduces customer configuration and supports certificate rotation. For more information, see [Certificate rotation guidance](tutorial-manage-certificates-for-federated-single-sign-on#guidance-and-best-practices-for-isvs-on-rotating-certificates). (Recommended)
- Provide a user interface and APIs that customers can use to configure SSO for their application instance. (Recommended)
- Provide a way to enforce SSO for the entire tenant. You can support other authentication options or bypass mechanisms for administrators and emergency access scenarios. (Recommended)

As an independent software vendor (ISV), you must also meet these requirements:

- Publish the application as software as a service (SaaS) in the cloud or distribute it to customers for installation so that customers can own and configure it. (Required)
- Establish engineering and support contacts for App Gallery onboarding and post-onboarding support. (Required)
- Publish documentation for configuring SAML SSO. (Required)
- Meet the compliance requirements for each cloud where you plan to list the application, such as Azure Government or Microsoft Azure operated by 21Vianet. (Required)

## Multitenant OIDC SSO requirements

These requirements apply to applications that use OpenID Connect (OIDC) for SSO.

Your application must meet the following authentication requirements:

- Support OpenID Connect. Use the [OAuth 2.0 authorization code flow](../../identity-platform/v2-oauth2-auth-code-flow). Don't use the [resource owner password credentials flow](../../identity-platform/v2-oauth-ropc). Use the [device authorization grant flow](../../identity-platform/v2-oauth2-device-code) only when your scenario requires it. (Required)
- Use a [multitenant application](../../identity-platform/howto-convert-app-to-be-multi-tenant) for a cloud SaaS application. A [single-tenant application](../../identity-platform/single-and-multi-tenant-apps) is acceptable when you deploy a separate application instance for each customer by using an infrastructure as a service (IaaS) or platform as a service (PaaS) architecture. (Required)
- Use the Microsoft identity platform v2.0 endpoint for authentication. (Required)
- Request the [least-privileged Microsoft Graph permissions](/en-us/graph/permissions-overview?tabs=http#best-practices-for-using-microsoft-graph-permissions) for your scenarios. (Required when using Microsoft Graph)
- Use [delegated permissions](/en-us/security/zero-trust/develop/developer-strategy-delegated-permission) so that a user or administrator can grant consent. Avoid [application permissions](/en-us/security/zero-trust/develop/developer-strategy-application-permissions) unless your scenario requires them. (Required when using Microsoft Graph)
- Use a certificate instead of a client secret when the application uses the client credentials flow. (Required)
- For single-page applications, use the authorization code flow instead of the OAuth 2.0 implicit grant flow. For more information, see [Security concerns with implicit grant flow](../../identity-platform/v2-oauth2-implicit-grant-flow#security-concerns-with-implicit-grant-flow). (Recommended)

As an ISV, you must also meet these requirements:

- Publish the application as SaaS in the cloud or distribute it to customers for installation so that customers can own and configure it. (Required)
- Add a **Sign in with Microsoft** button to the sign-in page and follow the [application branding guidelines](../../identity-platform/howto-add-branding-in-apps). (Recommended)
- Complete publisher verification by using your Microsoft AI Cloud Partner Program ID. (Required)
- Establish engineering and support contacts for post-onboarding support. (Required)
- Publish documentation for configuring OIDC and OAuth SSO. (Required)
- Meet the compliance requirements for each cloud where you plan to list the application, such as Azure Government or Microsoft Azure operated by 21Vianet. (Required)
- Use a confidential client application. Microsoft Entra App Gallery doesn't onboard public client applications.

## Prepare customer documentation

Publish documentation that includes at least the following information:

- An introduction to your SSO functionality, including supported protocols, versions, SKUs, and identity providers.
- Licensing requirements.
- Roles required to configure SSO.
- SAML configuration steps, including expected values and service provider information.
- OIDC and OAuth permissions with business justifications.
- Testing steps for pilot users.
- Troubleshooting information, including error codes and messages.
- Support options.
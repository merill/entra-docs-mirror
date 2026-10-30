---
layout: Conceptual
title: Microsoft identity platform token exchange scenario with SAML and OIDC/OAuth in Microsoft Entra ID - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/scenario-token-exchange-saml-oauth
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn about common token exchange scenarios when working with SAML and OIDC/OAuth in Microsoft Entra ID.
manager: pmwongera
ms.date: 2025-05-14T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.topic: how-to
locale: en-us
document_id: 0426f50b-e03b-4e77-4a8a-390b0ae08c62
document_version_independent_id: 0039b994-8481-1214-b42a-c2113b07fafc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/scenario-token-exchange-saml-oauth.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/scenario-token-exchange-saml-oauth
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/scenario-token-exchange-saml-oauth.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 184f0872-84ab-3fd5-e452-eb2ef5d683f2
---

# Microsoft identity platform token exchange scenario with SAML and OIDC/OAuth in Microsoft Entra ID - Microsoft identity platform | Microsoft Learn

SAML and OpenID Connect (OIDC) / OAuth are popular protocols used to implement single sign-on (SSO). Some apps might only implement SAML and others might only implement OIDC/OAuth. Both protocols use tokens to communicate secrets. To learn more about SAML, see [single sign-on SAML protocol](single-sign-on-saml-protocol). To learn more about OIDC/OAuth, see [OAuth 2.0 and OpenID Connect protocols on Microsoft identity platform](v2-protocols).

This article outlines a common scenario where an app implements SAML but calls the Graph API, which uses OIDC/OAuth. Basic guidance is provided for people working with this scenario.

## Scenario: You have a SAML token and want to call the Graph API

Many apps are implemented with SAML. However, the Graph API uses the OIDC/OAuth protocols. It's possible, though not trivial, to add OIDC/OAuth functionality to a SAML app. Once OAuth functionality is available in an app, the Graph API can be used.

The general strategy is to add the OIDC/OAuth stack to your app. With your app that implements both standards you can use a session cookie. You aren't exchanging a token explicitly. You're logging a user in with SAML, which generates a session cookie. When the Graph API invokes an OAuth flow, you use the session cookie to authenticate. This strategy assumes the Conditional Access checks pass and the user is authorized.

Note

The recommended library for adding OIDC/OAuth behavior to your applications is the [Microsoft Authentication Library (MSAL)](/en-us/entra/msal/).
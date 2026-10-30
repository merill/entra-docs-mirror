---
layout: Conceptual
title: 'SAML versus OpenID Connect: Choose the right SSO protocol - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/saml-vs-oidc-decision-guide
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Compare SAML 2.0 and OpenID Connect (OIDC) protocols to choose the right approach for your application's SSO integration with Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2026-06-22T00:00:00.0000000Z
ms.reviewer: hkinyunyu
ms.custom: enterprise-apps-article, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: a65a4f09-5b61-0ec0-d9c3-c323afbe4446
document_version_independent_id: a65a4f09-5b61-0ec0-d9c3-c323afbe4446
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/saml-vs-oidc-decision-guide.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/saml-vs-oidc-decision-guide
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/saml-vs-oidc-decision-guide.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: af8dde00-a822-58c8-b2c2-848a79eac777
---

# SAML versus OpenID Connect: Choose the right SSO protocol - Microsoft Entra ID | Microsoft Learn

To set up single sign-on (SSO) with Microsoft Entra ID, you choose between two protocols: Security Assertion Markup Language (SAML) 2.0 and OpenID Connect (OIDC). This article explains how the two protocols differ, when to use each, and how to choose for your app.

## Why your protocol choice matters

Your protocol choice shapes how you build the app, how hard it is to integrate, and how well it fits your customers' environments. Microsoft Entra ID fully supports both protocols, but each one suits different needs.

The choice affects two roles:

- **Independent software vendor (ISV) application developers**: It drives development effort, framework support, and how easily you meet varied customer requirements.
- **IT administrators**: It affects how well an app fits your identity infrastructure and security policies.

## What is SAML 2.0?

SAML 2.0 is a mature federation protocol based on XML. Enterprises have used it widely for over a decade. SAML safely shares sign-in and access data between identity providers and apps.

SAML uses XML messages and assertions to carry sign-in data. It maps user attributes in detail. It also supports complex enterprise needs, such as signed XML assertions and detailed attribute statements.

## What is OpenID Connect (OIDC)?

OpenID Connect (OIDC) is a modern sign-in protocol built on OAuth 2.0. It uses JSON tokens called JSON Web Tokens (JWTs) and REST APIs. OIDC signs users in, and OAuth 2.0 handles access.

OIDC is simpler and more developer-friendly. It fits modern app designs, including single-page applications, mobile apps, and microservices.

## Comparing SAML and OIDC

The following table compares SAML 2.0 and OpenID Connect across the factors that matter most for SSO integration.

| Aspect | SAML 2.0 | OpenID Connect |
| --- | --- | --- |
| **Message format** | XML-based | JSON-based |
| **Token type** | XML assertions | JWT tokens |
| **Enterprise adoption** | Widely established | Growing rapidly |
| **Developer experience** | Complex, requires XML handling | Simpler, REST-based |
| **Development complexity** | Higher, XML processing required | Lower, REST/JSON based |
| **Modern frameworks** | Limited native support | Excellent support |
| **Mobile/SPA support** | Challenging | Native support |
| **Validation alignment** | Good, established patterns | Excellent, modern standards |
| **Multi-tenant SaaS suitability** | Adequate with complexity | Native, optimal |
| **Customer onboarding effort** | More complex, manual setup | Simpler, automated discovery |
| **Long-term maintainability** | Higher overhead | Lower maintenance |
| **Attribute handling** | Rich XML attribute statements | JSON claims |
| **Security features** | XML signatures, complex controls | JWT signatures, OAuth scopes |

## Decision summary

Both protocols are secure, and Microsoft Entra ID fully supports each one. The preceding table compares them aspect by aspect, so use it for the detailed differences. This summary highlights why an ISV picks each protocol: OIDC suits new, cloud-native SaaS and customers with modern identity, while SAML is a requirement-driven choice for enterprise customers, compliance or procurement mandates, or legacy identity providers that support only SAML. Support both protocols when your customer base spans both worlds.

**Choose OpenID Connect (OIDC) if you:**

- Build new SaaS or cloud-native apps
- Build single-page applications (SPAs) or mobile apps
- Want development speed and modern integration
- Serve customers with modern identity systems
- Plan for multitenant, scalable distribution

**Choose SAML if you:**

- Have enterprise customers that require SAML
- Work with legacy identity providers that lack OIDC
- Must meet compliance or procurement rules that mandate SAML
- Already have a working SAML implementation

**Support both protocols if you:**

- Serve mixed customer environments that need both
- Want the widest compatibility across organizations

**If unsure, default to OIDC for new SaaS development.** OIDC fits modern apps, Microsoft Entra validation, and today's enterprise trends.
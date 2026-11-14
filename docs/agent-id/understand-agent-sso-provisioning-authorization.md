---
layout: Conceptual
title: Understand agent SSO, provisioning, and authorization - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/understand-agent-sso-provisioning-authorization
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Understand how agent SSO, provisioning, and ID-JAG support identity and access to third-party applications.
ms.date: 2026-11-13T00:00:00.0000000Z
ms.topic: concept-article
ai-usage: ai-assisted
locale: en-us
document_id: 0c4c58e3-2cac-260c-841d-89c813845482
document_version_independent_id: 0c4c58e3-2cac-260c-841d-89c813845482
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/understand-agent-sso-provisioning-authorization.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/understand-agent-sso-provisioning-authorization
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/understand-agent-sso-provisioning-authorization.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: a81c6c1b-e9cd-1114-946e-2eae0c9c4e88
---

# Understand agent SSO, provisioning, and authorization - Microsoft Entra Agent ID | Microsoft Learn

AI agents increasingly need to access third-party applications and services. Applications use different approaches to authenticate agents, represent agent identities, provision permissions, and authorize access.

Microsoft Entra Agent ID helps organizations manage, govern, and protect AI agent identities. **Identity Assertion JWT Authorization Grant (ID-JAG)** enables delegated authorization across applications. We'd like to understand how your application supports agent identity and access today and what you plan to support in the future.

If you're familiar with these capabilities, go directly to the [Identity Assertion JWT Authorization Grant (ID-JAG) | Partner and Customer Interest](https://forms.cloud.microsoft/r/HWqN80MaeS) form.

## How agent identity and access work

| Capability | What it does |
| --- | --- |
| **Microsoft Entra Agent ID** | Manages the agent's identity in Microsoft Entra. |
| **Agent SSO and authentication** | Authenticates the agent to your application. |
| **Agent provisioning** | Creates and manages the agent's identity and permissions in your application, when required. |
| **ID-JAG** | Enables the agent to obtain delegated access to your application. |

## Microsoft Entra Agent ID

Microsoft Entra Agent ID provides identity, security, and governance capabilities for AI agents. Creating an agent identity in Microsoft Entra doesn't automatically create a corresponding identity in your application.

For more information, see [Microsoft Entra Agent ID documentation](./).

## Agent SSO and authentication

Authentication establishes the identity of an agent accessing your application or API. The authentication methods you support depend on your application's identity architecture.

## Agent provisioning

Some applications require an agent to have an identity in their system before access can be granted. For these applications, provisioning creates and manages the agent's identity and permissions.

Provisioning can use SCIM, application-specific APIs, or other mechanisms.

Important

Provisioning here refers to how the agent is represented and managed in your application, not to creating the agent identity in Microsoft Entra Agent ID.

## ID-JAG

ID-JAG provides delegated authorization to your application. The target application's authorization server validates the grant, applies its authorization policies, and issues an appropriately scoped access token.

## Tell us what your application supports

**Help shape future Microsoft Entra integrations for AI agents.** Tell us how your application supports agent identity and access today, and what you plan to support in the future.

Complete the [Identity Assertion JWT Authorization Grant (ID-JAG) | Partner and Customer Interest](https://forms.cloud.microsoft/r/HWqN80MaeS) form to share your application's:

- Agent authentication and SSO capabilities
- Provisioning approach
- ID-JAG readiness and plans

We ask about provisioning and ID-JAG separately because they serve different purposes. Provisioning creates and manages an agent's identity and permissions in your application when required. ID-JAG enables delegated authorization to your application. Your application can support either capability without supporting the other.

Note

Sharing this information doesn't commit you to supporting ID-JAG and doesn't mean Microsoft has validated your implementation. Your input helps Microsoft understand partner readiness and inform future integration and testing plans.
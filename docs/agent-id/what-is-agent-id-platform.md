---
layout: Conceptual
title: What is the Microsoft agent identity platform - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/what-is-agent-id-platform
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn about the Microsoft Agent Identity Platform, a comprehensive identity, and authorization framework designed specifically for AI agents. Key concepts include agent registry, authentication protocols, tokens, claims, and agent discovery capabilities.
ms.date: 2025-10-24T00:00:00.0000000Z
ms.topic: concept-article
ms.reviewer: dastrock
locale: en-us
document_id: 59f05eb2-9dc7-1064-6932-744183b901b8
document_version_independent_id: 59f05eb2-9dc7-1064-6932-744183b901b8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/what-is-agent-id-platform.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/what-is-agent-id-platform
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/what-is-agent-id-platform.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/96407ebd-b9e6-40db-9488-063e1af76a01
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/302444b9-4a43-4841-8014-3d9e4251ff15
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8af61fb5-33c5-4523-b00a-7a42d7bbe9cd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/bebd8809-dac1-4c22-83e2-66d98af8a94d
platformId: a3910e74-c80b-d8bf-1dbb-a67cf4cd36a9
---

# What is the Microsoft agent identity platform - Microsoft Entra Agent ID | Microsoft Learn

The Microsoft agent identity platform is an identity and authorization framework built to address the unique authentication, authorization, and governance challenges posed by AI agents operating in enterprise environments.

Unlike nonagentic application identities designed for web services or user identities designed for humans, the Microsoft agent identity platform is purpose-built for AI agents. The platform provides specialized components that enable AI agents to authenticate securely and access resources appropriately. It also enables agents to discover other agents and operate within enterprise-grade governance frameworks.

This overview introduces the core components of the Microsoft agent identity platform. It focuses on the identity constructs, authentication mechanisms, token systems, and discovery capabilities that form the foundation of agent identity management in enterprise environments.

## How to get started

Microsoft Entra Agent ID is a product within Microsoft Entra that provides the platform for creating and managing agent identities and agent identity blueprints. Agent ID is available for all Microsoft Entra customers.

[Microsoft Agent 365](/en-us/microsoft-agent-365/overview) enables agents to operate across Microsoft 365 services and enterprise workflows, which requires a **Microsoft Agent 365** license for each user. For pricing details, see [Microsoft Agent 365 plans and pricing](https://www.microsoft.com/microsoft-agent-365#plans-and-pricing).

Extending Microsoft Entra security features to agents requires Microsoft Agent 365. Agent 365 is included with Microsoft 365 E7 and is available as an add-on to Microsoft E5/A5/Business Premium (or Microsoft Defender Suite + Microsoft Purview Suite). See our latest [Agent 365 product terms for more details](https://www.microsoft.com/licensing/terms/productoffering/Agent365/EAEAS#clause-2755-h3-1).

## Platform architecture overview

The Microsoft agent identity platform is built on several foundational technical components that work together to provide a complete identity and authorization solution for AI agents:

- **Authentication service**: An OAuth 2.0 and OpenID Connect (OIDC) standard-compliant authentication service that enables secure, standards-based authentication for agents. This service issues tokens that agents use to authenticate to resources and APIs, supporting both application-only and delegated access scenarios. There are three objects that form the core identity constructs in the platform: agent identity blueprint, agent identity, and agent's user account.
- **SDKs**: Software development kits that enable developers to integrate with the Microsoft agent identity platform. SDKs abstract the complexity of token acquisition and protocol handling, making it straightforward for platforms that build agents to incorporate identity management into their applications. Microsoft agent identity platform includes two SDKs: Microsoft Identity Web (.NET) and the Microsoft Entra ID Auth SDK (sidecar).
- **Agent management**: A comprehensive agent metadata store and administrative interface within the Microsoft Entra admin center that enables administrators to discover, view, configure, and manage agents. The platform provides the agent registry that is a centralized repository for registering and managing agents across an organization.

These technical components work together with the identity constructs described in the following section to provide complete platform functionality.

## Authentication and authorization

The Microsoft agent identity platform uses OAuth for authorization and OpenID Connect (OIDC) for authentication.

- **OpenID Connect (OIDC)** enables agents to authenticate and verify the identity of other entities they communicate with, establishing secure trust relationships.
- **OAuth 2.0** allows agents to request access tokens that authorize them to access resources on behalf of themselves or users, supporting both application-only and delegated access scenarios.

For more information, see [OAuth protocols](agent-oauth-protocols).

Tokens are the fundamental security mechanism enabling secure communication and authorization in the Microsoft agent identity platform. The platform supports multiple token flow patterns designed for specific operational scenarios. For more information, see [tokens in Microsoft agent identity platform](agent-tokens)

## Integration and interoperability

The Microsoft agent identity platform is designed to work seamlessly across the Microsoft ecosystem and beyond. It integrates with:

- **Microsoft Entra ID**: The platform extends Microsoft Entra ID capabilities to support agent scenarios, using existing identity infrastructure and policies.
- **Platforms and services that create agents**: Platforms that create and manage agents can integrate with the Microsoft agent identity platform to secure agents. This includes Microsoft-owned platforms like Copilot Studio and non-Microsoft platforms such as Amazon Web Services (AWS) Bedrock, n8n, and other agent frameworks that support OAuth 2.0 and OpenID Connect. Organizations can onboard agents from these platforms by using the [Microsoft Entra ID Auth SDK (sidecar)](authentication-with-auth-sdk-sidecar) or [workload identity federation](/en-us/entra/workload-id/workload-identity-federation), with no platform-specific credential management required.
- **Extended Microsoft identity and security products**: Integration with Conditional Access, identity protection, identity governance, Global Secure Access, and other security services enable comprehensive agent security.

This interoperability ensures that organizations can build, deploy, and manage agent identities consistently regardless of where agents are created or deployed. For step-by-step guidance on integrating non-Microsoft agents, see [Integrate third-party agents with Microsoft Entra Agent ID](configure-third-party-agents).
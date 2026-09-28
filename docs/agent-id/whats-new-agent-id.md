---
layout: Conceptual
title: What's new in Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/whats-new-agent-id
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn about new features and updates in Microsoft Entra Agent ID at general availability, including non-Microsoft integrations, migration guides, and enterprise governance.
ms.topic: whats-new
ms.date: 2026-05-01T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: d98524e2-fd85-c6d8-25e0-46d1fd7599e7
document_version_independent_id: d98524e2-fd85-c6d8-25e0-46d1fd7599e7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/whats-new-agent-id.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/whats-new-agent-id
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/whats-new-agent-id.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 8b6af3ef-35a6-0bbb-5a57-176059ca2f58
---

# What's new in Microsoft Entra Agent ID | Microsoft Learn

Microsoft Entra Agent ID is now generally available. This release brings first-class identity and access management to AI agents, enabling organizations to authenticate, authorize, govern, and protect agent identities at enterprise scale. Microsoft Entra Agent ID extends Zero Trust principles to AI workloads with purpose-built identity constructs, specialized OAuth flows, and comprehensive security controls.

This article summarizes the key capabilities and documentation currently available.

## Manage AI agents at scale

Microsoft Entra Agent ID introduces new identity constructs and authentication protocols designed specifically for AI agents. Notable updates include:

- [Key concepts](key-concepts) - New concepts added to further define core agent identity concepts and their relationships.
- [Administrative relationships](agent-owners-sponsors-managers) - Deeper definitions and clarified differences between owners, sponsors, and managers of agent identities, blueprints, and agents' user accounts.
- [Design patterns](concept-agent-id-design-patterns) (New) - Common architectural patterns for agent identity deployments.
- [Best practices](best-practices-agent-id) (New) - Recommended approaches for agent identity management.
- [Plan your agent identity architecture](how-to-plan-agent-identity-architecture) (New) - Guidance for planning agent identity deployment at scale.
- [Create an agent identity blueprint](create-blueprint) and [Create an agent identity](create-delete-agent-identities) (Preview) - Use the new "wizard" to create agent identity blueprints and agent identities in the Microsoft Entra admin center.
- [AI-guided setup](agent-id-ai-guided-setup) (New) - Automate onboarding with an AI coding agent that walks you through blueprint creation, credential configuration, and agent identity provisioning.
- [Agent identity deletion](concept-agent-identity-deletion) (New) - Learn about the automated cascade cleanup process and soft-delete functionality for agent identities.
- [Authentication with the Auth SDK (sidecar)](authentication-with-auth-sdk-sidecar) (New) - Overview of the sidecar pattern for agent authentication.
- [Configure Microsoft Entra ID Auth SDK (sidecar) for agent identities](microsoft-entra-sdk-for-agent-identities) - SDK configuration for token acquisition.
- [Run the sidecar for local development](sidecar-local-development) (New) - Local development setup for the Auth SDK.
- [Validate agent tokens in a downstream API](how-to-validate-agent-tokens-downstream-api) (New) - Token validation guidance for APIs that receive agent tokens.
- [Configure non-Microsoft agents with Agent ID](configure-third-party-agents) (New) - Integration patterns (sidecar and federation) for platforms like AWS, GCP, and n8n.
- [Secure an Amazon Bedrock agent](integrate-aws-bedrock-agent) (New) - Step-by-step guide for securing Bedrock agents with Agent ID.
- [Secure an n8n agent](integrate-n8n-agent) (New) - Deploy n8n on Azure with Agent ID integration.
- [Migrate custom app registrations](migrate-custom-app-registrations-to-agent-id) (New) - Move agents using standard app registrations to Agent ID.
- [Migrate Copilot Studio agents](migrate-copilot-studio-agents-to-agent-id) (New) - Move Microsoft Copilot Studio agents to Agent ID.

To simplify agent management across the enterprise, agent registry experiences are converging under [Microsoft Agent 365](/en-us/microsoft-365/admin/manage/agent-registry). This change gives customers one place to discover and manage all agents, while Microsoft Entra continues to provide the identity foundation through Agent ID. For more information, see [Agent Registry convergence with Microsoft Agent 365](agent-registry-convergence).

## Govern agent identities and lifecycle

Microsoft Entra ID Governance extends lifecycle and access management capabilities to agent identities:

- [Governing agent identities overview](../id-governance/agent-id-governance-overview) - Overview of how Microsoft Entra governs agent identity lifecycle and access.
- [Access packages for agent identities](agent-access-packages) - Govern agent access through policy-based access packages and permission assignment for both on-behalf-of (OBO) and autonomous (non-OBO) scenarios.
- [Sponsor lifecycle workflows](../id-governance/agent-sponsor-tasks) (New) - Automate sponsor maintenance and reassignment for agent blueprints and agent identities.
- [Manage your agent identities](manage-agent-identities-end-user) (New) - View and control agent identities you own or sponsor.
- [Agent identity sponsor templates](../id-governance/lifecycle-workflow-templates) (New) - Two new lifecycle workflow templates for notifying managers and cosponsors, and automatically transfer sponsorship when an agent identity sponsor changes roles or leaves the organization, to prevent orphaned agents.

## Protect agent access to resources

Conditional Access and ID Protection features extend Microsoft Entra Agent ID to help secure agent identities and their access to resources:

- [Conditional Access for agents](/en-us/entra/identity/conditional-access/agent-id) (Updated)- Improved guidance and detailed scenarios for Conditional Access policies, plus new templates for agent-specific policies.
- [Block access for high-risk agent identities](../identity/conditional-access/policy-agent-block-high-risk) (New) - Conditional Access template to block sign-ins from risky agent identities.
- [Autonomous agent access policy](../identity/conditional-access/policy-autonomous-agents) (New) - Conditional Access template for autonomous agents without user context.
- [On behalf of agent access policy](../identity/conditional-access/policy-on-behalf-of-agents) (New) - Conditional Access template for agents acting on behalf of users.
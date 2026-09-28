---
layout: Conceptual
title: Authentication protocols in agents - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/agent-oauth-protocols
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn about OAuth 2.0 protocols and token exchange patterns for agents in Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2025-11-04T00:00:00.0000000Z
ms.reviewer: jmprieur
locale: en-us
document_id: 83be56cb-cbba-3b11-bdc8-bd8bbbac6baa
document_version_independent_id: 83be56cb-cbba-3b11-bdc8-bd8bbbac6baa
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/agent-oauth-protocols.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/agent-oauth-protocols
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/agent-oauth-protocols.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 28eecd4d-8b79-f5b7-126f-3872887f9bb5
---

# Authentication protocols in agents - Microsoft Entra Agent ID | Microsoft Learn

Agents use OAuth 2.0 protocols with specialized token exchange patterns enabled by Federated Identity Credentials (FIC). All agent auth flows involve multi-stage token exchanges where the agent identity blueprint impersonates the agent identity to perform operations. This article explains the authentication protocols and token flows used by agents. It covers delegation scenarios, autonomous operations, and federated identity credential patterns. Microsoft recommends that you use our SDKs like [Microsoft Entra ID Auth SDK (sidecar)](https://aka.ms/entra/sdk/agentid) since implementing these protocol steps isn't easy.

All agent entities are confidential clients that can also serve as APIs for On-Behalf-Of scenarios. Interactive flows aren't supported for any agent entity type, ensuring that all authentication occurs through programmatic token exchanges rather than user interaction flows.

Warning

Microsoft recommends using the approved SDKs like Microsoft.Identity.Web and Microsoft Entra ID Auth SDK (sidecar) libraries to implement these protocols. Manual implementation of these protocols is complex and error-prone, and using the SDKs helps ensure security and compliance with best practices.

## Prerequisites

If you aren't familiar already, go through the following protocol docs.

- [Microsoft identity platform and OAuth 2.0 On-Behalf-Of flow](/en-us/entra/identity-platform/v2-oauth2-on-behalf-of-flow)
- [Microsoft identity platform and the OAuth 2.0 client credentials flow](/en-us/entra/identity-platform/v2-oauth2-client-creds-grant-flow)

## Supported grant types

The following are the supported grant types for agent applications.

### Agent identity blueprint

Agent identity blueprints support `client_credentials` enabling secure token acquisition for impersonation scenarios. The `jwt-bearer` grant type facilitates token exchanges in [On-Behalf Of scenarios](/en-us/entra/identity-platform/v2-oauth2-on-behalf-of-flow), allowing for delegation patterns. `refresh_token` grants enable background operations with user context, supporting long-running processes that maintain user authorization.

### Agent identity

Agent identities use `client_credentials` for app-only autonomous operations, enabling independent functionality without user context, and impersonation for a user agent identity. The `jwt-bearer` grant type supports both [client credential flow](/en-us/entra/identity-platform/v2-oauth2-client-creds-grant-flow) and [On-Behalf Of (OBO) flow](/en-us/entra/identity-platform/v2-oauth2-on-behalf-of-flow) providing flexibility in delegation patterns.`refresh_token` grants facilitate background user-delegated operations, allowing agent identities to maintain user context across extended operations.

### Unsupported flows

- The agent application model explicitly excludes certain authentication patterns to maintain security boundaries. Agents aren't supported for interactive (`/authorize`) flows, ensuring all authentication occurs programmatically.
- Public client capabilities aren't available, requiring all agents to operate as confidential clients.
- A web redirect URI can be configured on a blueprint for consent flows only (`response_type=none`), but can't be used for interactive token acquisition. Full redirect URI functionality is configured on the client application.

## Core protocol patterns

Agents can operate in three primary modes:

- Agents operating on behalf of regular users in Microsoft Entra ID (interactive agents). This is a regular on-behalf-of flow.
- Agents operating on their own behalf using service principals created for agents (autonomous).
- Agents operating on their own behalf using user principals created specifically for that agent (for instance agents having their own mailbox).

## Managed identities integration

Managed identities are the preferred credential type. In this configuration, the managed identity token serves as the credential for the parent agent identity blueprint, while standard MSI protocols apply for credential acquisition. This integration allows the agent ID to receive the full benefits of MSI security and management, including automatic credential rotation and secure storage.

Warning

Client secrets shouldn't be used as client credentials in production environments for agent identity blueprints due to security risks. Instead, use more secure authentication methods such as [federated identity credentials (FIC) with managed identities](/en-us/entra/workload-id/workload-identity-federation-config-app-trust-managed-identity) or client certificates. These methods provide enhanced security by eliminating the need to store sensitive secrets directly within your application configuration.

## Oauth protocols

There are three agent oauth flows:

[![Diagram showing the illustration of oauth flow for agents.](media/agent-oauth-protocols/agent-flows.png)](media/agent-oauth-protocols/agent-flows.png#lightbox)

- [Agent on-behalf of flow](agent-on-behalf-of-oauth-flow): Agents operating on behalf of regular users (interactive agents).
- [Autonomous app flow](agent-autonomous-app-oauth-flow): App-only operations enable agent identities to act autonomously without user context.
- [Agent's user account flow](agent-user-oauth-flow): Agents operating on their own behalf using user principals created specifically for agents.
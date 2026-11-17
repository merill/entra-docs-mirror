---
layout: Conceptual
title: Choose an authentication protocol for an agent - Microsoft Entra Agent ID | Microsoft Learn
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
description: Choose an OAuth protocol for a local, hosted, delegated, or autonomous agent in Microsoft Entra Agent ID.
ms.topic: concept-article
ms.date: 2026-11-03T00:00:00.0000000Z
ms.reviewer: jmprieur
ai-usage: ai-assisted
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
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 28eecd4d-8b79-f5b7-126f-3872887f9bb5
---

# Choose an authentication protocol for an agent - Microsoft Entra Agent ID | Microsoft Learn

The right authentication protocol depends on where the agent runs and whose identity it uses to access a resource. Start with these questions:

1. Does the agent run on a user's device or in a hosted service?
2. Does the agent act for a signed-in user, as itself, or as a dedicated agent user account?
3. If it acts for a signed-in user, does the agent initiate sign-in or receive a user access token from another application?

Use Microsoft Authentication Library (MSAL) or another supported authentication library instead of constructing protocol requests directly.

Warning

Microsoft recommends using the approved SDKs like Microsoft.Identity.Web and Microsoft Entra ID Auth SDK (sidecar) libraries to implement these protocols. Manual implementation of these protocols is complex and error-prone, and using the SDKs helps ensure security and compliance with best practices.

## Choose a protocol

| Use case | Recommended protocol | Access type | Client type |
| --- | --- | --- | --- |
| A local agent runs on an endpoint device and signs in the user | Authorization code flow with Proof Key for Code Exchange (PKCE) | Delegated | Public |
| A hosted agent receives a user access token from a client application and calls another service for that user | On-Behalf-Of (OBO) flow | Delegated | Confidential |
| A hosted agent runs without a user and accesses resources as itself | Client credentials flow; blueprint impersonation for multi-instance Agent IDs | Application | Confidential |
| An autonomous agent needs a mailbox or another resource available only to a user | Agent's user account impersonation | Delegated permissions assigned to the agent's user account | Confidential |

If more than one row applies, use a separate token acquisition path for each operating mode. For example, a hosted agent might use OBO for requests initiated by a user and app-only access for scheduled work that doesn't have user context.

The blueprint's [instance mode](agent-blueprint#instance-modes-preview) also affects token acquisition. A single-instance Agent ID (preview) uses the shared blueprint client ID directly for authorization code, refresh, client credentials, and OBO requests. It doesn't acquire an intermediate blueprint impersonation token. Single-instance mode isn't limited to local or public clients. For an overview and links to the consent and SDK walkthroughs, see [Authentication for a single-instance agent identity](authenticate-single-instance-agent). To start with a platform-specific walkthrough, see [Choose an integration path for an agent](choose-agent-integration-path).

## Local agent that signs in a user

Choose the authorization code flow with PKCE when the agent:

- Runs on a desktop, mobile device, or other endpoint.
- Can open a browser for interactive sign-in.
- Accesses protected services for the signed-in user.
- Can't securely store a client secret, certificate, or federated identity credential.

The local agent is a public client. It sends the user to the Microsoft identity platform `/authorize` endpoint, receives an authorization code at its registered redirect URI, and redeems the code by using a PKCE verifier. It doesn't present a client credential.

A registered public-client Agent ID must use [single-instance mode](agent-blueprint#instance-modes-preview). Every installation uses the same client ID; don't create an Agent ID for each device. A local agent can alternatively use a [Client ID Metadata Document (CIMD)](client-id-metadata-documents) URL as its client ID.

Don't use this flow for a hosted agent that receives a user access token from another application. Use OBO instead.

For implementation and protocol details, see:

- [Authenticate a local agent with Microsoft Entra ID](authenticate-local-agent)
- [OAuth 2.0 authorization code grant](agent-authorization-code-oauth-flow)
- [Microsoft identity platform and OAuth 2.0 authorization code flow](/en-us/entra/identity-platform/v2-oauth2-auth-code-flow)
- [Public client and confidential client applications](/en-us/entra/identity-platform/msal-client-applications)

## Hosted agent that acts for a signed-in user

Choose the OBO flow when:

- A client application signs in the user.
- The client calls the hosted agent or its API with a user access token.
- The agent must call a downstream API with the user's identity and delegated permissions.

The hosted agent is a confidential client. It doesn't start another interactive sign-in. Instead, it exchanges the incoming user access token for a token to the downstream resource. The incoming token must be intended for the agent's blueprint; don't relay a token issued for another resource.

For a multi-instance Agent ID, configure the required delegated permissions as inheritable permissions on the blueprint and obtain administrator consent.

Don't use OBO when no signed-in user initiated the operation. Use app-only access for autonomous work.

For implementation and protocol details, see:

- [Agent OAuth flows: On behalf of flow](agent-on-behalf-of-oauth-flow)
- [Microsoft identity platform and OAuth 2.0 On-Behalf-Of flow](/en-us/entra/identity-platform/v2-oauth2-on-behalf-of-flow)
- [Configure inheritable permissions for agent identity blueprints](configure-inheritable-permissions-blueprints)

## Hosted agent that acts as itself

Choose the client credentials flow with Agent ID impersonation when the agent:

- Runs in a hosted service that can protect a credential.
- Performs scheduled, event-driven, or other autonomous work.
- Accesses a resource as the Agent ID rather than as a user.

For a multi-instance Agent ID, the blueprint first authenticates and obtains a token-exchange token for its child Agent ID. The Agent ID then uses that token as a client assertion in the client credentials flow. A single-instance Agent ID instead authenticates directly with the shared client ID and a credential on the blueprint. The resource token contains application permissions granted by an administrator and identifies the Agent ID as the actor.

Use a managed identity and federated identity credential when the hosting environment supports them. Avoid client secrets.

## Managed identities integration

For Azure-hosted agents, prefer a managed identity when the hosting service provides one. Its token authenticates the parent blueprint through a configured federated identity credential; configuring the managed identity alone doesn't grant API access to the agent. A local developer's Azure CLI sign-in isn't a managed identity. For hosting requirements and local credential alternatives, see [Configure blueprint credentials](create-blueprint#configure-credentials-for-the-agent-identity-blueprint).

Warning

Client secrets shouldn't be used as client credentials in production environments for agent identity blueprints due to security risks. Instead, use more secure authentication methods such as [federated identity credentials (FIC) with managed identities](/en-us/entra/workload-id/workload-identity-federation-config-app-trust-managed-identity) or client certificates. These methods provide enhanced security by eliminating the need to store sensitive secrets directly within your application configuration.

Don't use application permissions when the resource should apply a signed-in user's permissions or consent. Use authorization code with PKCE or OBO instead.

For implementation and protocol details, see:

- [Agent autonomous app OAuth flow](agent-autonomous-app-oauth-flow)
- [Microsoft identity platform and the OAuth 2.0 client credentials flow](/en-us/entra/identity-platform/v2-oauth2-client-creds-grant-flow)
- [Workload identity federation](/en-us/entra/workload-id/workload-identity-federation)

## Autonomous agent that acts as a dedicated user

Choose agent's user account impersonation only when an autonomous agent needs capabilities that are available to a user but not to an application identity. For example, an agent might need its own mailbox.

An [agent's user account](agent-users) is a dedicated user identity for the agent, not the account of the person using the agent. The Agent ID impersonates this account through an agent-specific token exchange. Access is limited by the permissions assigned to the Agent ID and the agent's user account.

Don't create an agent's user account only to run unattended work. If the resource supports application permissions, prefer app-only access so the workload doesn't depend on a user identity.

For implementation details, see:

- [Agent's user account impersonation protocol](agent-user-oauth-flow)
- [Agent's user accounts](agent-users)

## Related authentication concepts

The following settings affect authentication but don't replace the protocol choice:

- **Public or confidential client** describes whether the agent can securely hold a credential. For more information, see [Public client and confidential client applications](/en-us/entra/identity-platform/msal-client-applications).
- **Managed identity, certificate, secret, or federated identity credential** describes how a confidential client proves its identity. Prefer managed identities and federated identity credentials when possible.
- **CIMD or registered client ID** describes how a public client is identified. Both options can use authorization code flow with PKCE.
- **Refresh token** lets a client obtain new access tokens without repeating the original authorization. It continues an existing delegated session; it isn't a separate operating model.
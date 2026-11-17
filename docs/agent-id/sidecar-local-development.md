---
layout: Conceptual
title: Run the Microsoft Entra ID Auth SDK sidecar locally - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/sidecar-local-development
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Run the Auth SDK sidecar and sample agent locally before deploying them to a hosted environment.
ms.topic: how-to
ms.date: 2026-11-06T00:00:00.0000000Z
ai-usage: ai-assisted
ms.reviewer: dastrock
locale: en-us
document_id: 7c97b53e-03e2-ba82-a423-3ab2f2e8031f
document_version_independent_id: 7c97b53e-03e2-ba82-a423-3ab2f2e8031f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/sidecar-local-development.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/sidecar-local-development
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/sidecar-local-development.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: 1eba242e-a5e8-280e-ee54-6e4ac2cd4bb8
---

# Run the Microsoft Entra ID Auth SDK sidecar locally - Microsoft Entra Agent ID | Microsoft Learn

Use the official sidecar sample to test Agent ID authentication without placing Microsoft Entra credentials in the agent process. The sample includes an agent, the Auth SDK sidecar, and a protected weather API.

## Prerequisites

- Docker Desktop or another Docker Compose environment.
- A Microsoft Entra tenant.
- Completion of [Create an identity for your agent](create-single-instance-agent), including tenant enablement, administrator approvals, and the recorded client and object IDs.
- A development credential on the blueprint.

Use a client secret only for local testing. Use managed identity federation for hosted deployments.

## Get the sample

Clone the [Microsoft Entra Agent ID samples](https://github.com/microsoft/entra-agentid-samples) repository and open the `sidecar/dev` directory.

Use the sample's container layout with the [cloud-agent sidecar configuration](microsoft-entra-sdk-for-agent-identities). Set the client ID recorded during setup and the blueprint credential, and keep identity overrides disabled. Don't use sample flows with `AgentIdentity` or `AgentUserId` overrides. Don't commit the environment file or client secret.

## Start the sample

Start the containers by following the [`sidecar/dev` sample instructions](https://github.com/microsoft/entra-agentid-samples/tree/dev/sidecar/dev).

The agent must call the sidecar through `localhost` in a shared network namespace. Use the [Docker Compose configuration](microsoft-entra-sdk-for-agent-identities#add-the-sidecar-container), not separate containers communicating through a `sidecar` DNS name. Don't expose the sidecar port publicly.

Before testing, verify the sidecar with the [health check](microsoft-entra-sdk-for-agent-identities#verify-the-sidecar). It confirms the sidecar is accepting requests, not that credentials, consent, or API access are configured correctly.

## Understand the token flow

For app-only calls, the sidecar uses the configured Agent ID and API profile to acquire a token for the downstream resource. For delegated calls, the agent sends the signed-in user's access token to the sidecar, which exchanges it for a downstream token by using the OAuth on-behalf-of flow. The agent can request an authorization header or have the sidecar proxy the downstream API call.

## Test API access

Test these operations separately:

- **App-only:** The agent calls `AuthorizationHeaderUnauthenticated` for a named API without an `AgentIdentity` query parameter.
- **User-delegated:** The sample client signs in a user and passes the access token to the agent. The agent forwards it to the authenticated sidecar endpoint for OBO.
- **Token validation:** The protected API validates the access token's signature, issuer, audience, expiry, and Agent ID claims.

Verify that app-only tokens have application permissions and delegated tokens contain the expected user and scope claims.

## Move to a hosted environment

Before deployment:

- Replace the development secret with a managed identity federated credential.
- Keep sidecar traffic on loopback in the shared network namespace.
- Configure production redirect URIs and API audiences.
- Remove development-only ports and sample credentials.
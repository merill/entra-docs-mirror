---
layout: Conceptual
title: Authentication with Microsoft Entra ID Auth SDK sidecar - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/authentication-with-auth-sdk-sidecar
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Understand when and how to use the Microsoft Entra ID Auth SDK sidecar with agents built in frameworks other than ASP.NET Core.
ms.topic: concept-article
ms.date: 2026-11-05T00:00:00.0000000Z
ai-usage: ai-assisted
ms.reviewer: dastrock
locale: en-us
document_id: 72318d5b-7543-0b3a-53ae-52bb6786aff2
document_version_independent_id: 72318d5b-7543-0b3a-53ae-52bb6786aff2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/authentication-with-auth-sdk-sidecar.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/authentication-with-auth-sdk-sidecar
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/authentication-with-auth-sdk-sidecar.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/d452572f-6212-498f-9050-ca4a9e50a425
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/a12e40b7-59a2-4437-96e2-166ce622b864
platformId: a81799e4-e453-fb65-0b87-f2c2b537ae41
---

# Authentication with Microsoft Entra ID Auth SDK sidecar - Microsoft Entra Agent ID | Microsoft Learn

Use the Microsoft Entra ID Auth SDK sidecar when your cloud agent isn't built with ASP.NET Core and Microsoft.Identity.Web. The sidecar runs next to the agent, holds the blueprint credential, acquires and caches tokens, and returns authorization headers or calls downstream APIs.

The agent communicates with the sidecar through `localhost` in a shared network namespace. Don't expose the sidecar endpoint publicly.

## Choose this integration

Use the sidecar when the agent needs to:

- Call an API as its Agent ID.
- Call an API as a signed-in user through On-Behalf-Of (OBO).
- Validate an incoming user token and read its claims.
- Change credential sources without changing agent code.

For ASP.NET Core agents, use the integrated Microsoft.Identity.Web guidance in this documentation instead.

## How the sidecar works

| Component | Responsibility |
| --- | --- |
| Upstream client | Signs in a user and sends an access token to the agent when user context is required. |
| Agent | Applies business logic and requests an authorization header or downstream call. |
| Sidecar | Validates inbound tokens, authenticates with the configured shared client ID and blueprint credential, and caches tokens. |
| Protected API | Validates the resulting access token and authorizes the request. |

For a cloud agent, the sidecar supports two token acquisition patterns:

- **App-only Agent ID:** The agent requests a token without an inbound user token.
- **Agent acting for a signed-in user:** The agent forwards the inbound user token and the sidecar performs OBO.

If you're building a platform that hosts separate agents for teams or customers, or your scenario needs an agent's dedicated user account, follow the [agent fleet tutorial](sidecar-fleet-provision-agent-identities).

The following diagram shows an agent and sidecar running in the same private environment. The agent requests an authorization header from the sidecar, which gets an access token from Microsoft Entra.

[![Diagram that shows an agent requesting an authorization header from a sidecar, which obtains an access token from Microsoft Entra ID.](media/configure-third-party-agents/sidecar-pattern-architecture.png)](media/configure-third-party-agents/sidecar-pattern-architecture.png#lightbox)

## Security boundary

Run the sidecar in the same network namespace as the agent, such as the same pod or container app. Production builds restrict callers to loopback; separate containers on a private bridge aren't sufficient. For Docker Compose, follow the [shared-network configuration](microsoft-entra-sdk-for-agent-identities#add-the-sidecar-container). Only trusted agent code should be able to call it. Use a managed identity and federated identity credential for hosted deployments. Use client secrets only for local development.
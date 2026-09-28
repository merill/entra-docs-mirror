---
layout: Conceptual
title: Grant agents access to Microsoft 365 resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/grant-agent-access-microsoft-365
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how to grant access to agents through consent, manual authorization, and other authorization systems for Microsoft 365 resources.
ms.topic: how-to
ms.date: 2026-05-01T00:00:00.0000000Z
ms.reviewer: ergreenl
locale: en-us
document_id: 206d3b06-6dbd-8e1c-f007-fee7c8e37131
document_version_independent_id: 206d3b06-6dbd-8e1c-f007-fee7c8e37131
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/grant-agent-access-microsoft-365.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/grant-agent-access-microsoft-365
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/grant-agent-access-microsoft-365.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: cc4c86a7-7c91-3c51-5077-bb02e266e351
---

# Grant agents access to Microsoft 365 resources | Microsoft Learn

This article provides guidance on how to grant access to agents through consent, manual authorization, and other authorization systems. Learn about the different methods available for authorizing agents to access Microsoft 365 resources and when to use each approach.

## Prerequisites

- An agent identity blueprint and at least one agent identity created from it.
- An agent identity blueprint with a valid redirect URI.

## How to request consent (delegated or application permissions)

Users or administrators can grant agents access to data by consenting to API permissions during the OAuth flow. This section explains how to request consent for delegated and application permissions for your agents.

### When to use delegated or application permissions

The type of permissions you request depends on how your agent operates and what resources it needs to access.

Use delegated permissions when your interactive agent needs to act on behalf of a signed-in user. For example, read that user's mail, calendar, or files. Delegated access is carried in the token's scp claim.

Use application permissions when your autonomous agent runs without a user present and requires app-only access. For example, to read all users' profiles. App permissions appear in the token's roles claim.

For more information, see [permissions and consent overview](../identity-platform/permissions-consent-overview)

### How consent works

For delegated permissions, when you redirect the user to the Microsoft identity platform `/authorize` endpoint, they review scopes such as `User.Read` and `Mail.Read`. If consent is granted, Microsoft Entra ID records an OAuth2PermissionGrant from your agent (client) to the resource such as Microsoft Graph. Future delegated tokens for that resource include the approved scopes in `scp` without reprompting unless consent changes. If your app requests consent for admin restricted permissions, your users get an error. An admin requests these permissions directly. For more information, see [admin-restricted permissions](/en-us/entra/identity-platform/scopes-oidc#admin-restricted-permissions).

### Building the consent URL

When building your consent URL, the client ID should be your agent identity's ID.

For more information, see requesting permissions through consent. Some permissions require consent from an administrator before they can be granted within a tenant. For more information, see [admin consent on the Microsoft identity platform](/en-us/entra/identity-platform/v2-admin-consent)

## How to manually grant authorization (delegated or application)

You can create the underlying authorization objects directly. It's useful for situations where you want to automate authorization or when you want to avoid interactive prompts.

- [Manually grant delegated permissions](/en-us/graph/api/oauth2permissiongrant-post). Set your client ID as the agent identity ID.
- [Manually grant application permissions (app role assignment)](/en-us/graph/api/serviceprincipal-post-approleassignments). Set your principal ID as the agent identity ID.

## How to manage access through access packages

Using access packages, you can enable standardized access for many AI Agents with the same access needs. The access package can include Entra roles, OAuth2 delegated and application permission grants and security group memberships. Agents can then request an access package, or a sponsor or admin can request for them, and once approved, the agent identity or agent's user account receives the access rights until the assignment is revoked or expires. For more information, see [access packages for agent identities](agent-access-packages).

## Other authorization systems

Agents can be authorized in several ways beyond app-role assignments, group memberships and OAuth2 permission grants. These alternative systems offer flexibility for assigning access tailored to different platforms, services, and security requirements. The following sections summarize some of the many methods for agent authorization.

### Azure role-based access control (Azure RBAC)

Assign Azure roles to the agent identity at the narrowest scope (resource, resource group, subscription). For example, you can grant the Key Vault Reader role on a single vault so the agent can read secrets without needing broad directory or tenant permissions. For more information and step-by-step guidance, see [Azure RBAC documentation](/en-us/azure/role-based-access-control/built-in-roles).

### Microsoft Entra roles

Some low-privilege directory roles might be assignable to agents for metadata or read scenarios. High-privilege roles are blocked for agents by platform policy. To learn more about Microsoft Entra roles and PIM, see [Microsoft Entra roles](/en-us/entra/identity/role-based-access-control/permissions-reference).

### Exchange RBAC

Exchange RBAC (Role-Based Access Control) lets administrators delegate permissions to Exchange resources. It ensures agents can get granular authorization, such as autonomous access to one mailbox or a few mailboxes. For information, see [Role Based Access Control for Applications in Exchange Online](/en-us/exchange/permissions-exo/application-rbac)

### Teams Resource-Specific Consent (RSC)

Teams Resource-Specific Consent (RSC) enables granular permission assignments for agents within Microsoft Teams. RSC allows you to grant permissions to an app or agent on a per-team basis, rather than at the tenant level. This approach is especially useful when you want to limit access to only the resources and data within specific teams. Such data includes channels, messages, or roster information, without granting broader organizational permissions. For more information, see [Resource-specific consent for your Teams app](/en-us/microsoftteams/platform/graph-api/rsc/resource-specific-consent).

### Permissions for agent communication across Microsoft 365 channels

An agent with its own identity (Agent ID) can communicate across Microsoft 365 surfaces, including sending and receiving Outlook email, receiving and responding to comments in OneDrive and SharePoint files, and sending and receiving messages from Teams chats and channels. Each surface the agent communicates in requires specific permissions, which you declare in the agent identity blueprint's required resource access, and which a tenant admin must consent to before the agent can send or receive anything there.

| Channel | Displayed as | Inbound (channel → agent)Receiving events | Outbound (agent → channel)Sending responses |
| --- | --- | --- | --- |
| `email` | Outlook | `Mail.Read` or `Mail.ReadWrite` | `Mail.Send` or `Mail.ReadWrite` |
| `spo.files.comments` | OneDrive and SharePoint | `Files.Read.All` or `Files.ReadWrite.All` | `Files.ReadWrite.All` |
| `teams-chat` | Teams chats | `Chat.Read` or `Chat.ReadWrite` | `Chat.ReadWrite` or `ChatMessage.Send` |
| `teams-channel` | Teams channels | `ChannelMessage.Read.All` | `ChannelMessage.Send` |

### Custom (third‑party) APIs

Agents can call other OAuth‑protected APIs. Ensure the resource application and its service principal exist in the tenant, define required scopes/app roles, and follow the same delegated or app‑permission flows. For more information, see Microsoft's guide to permissions and consent in the Microsoft identity platform.
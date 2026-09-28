---
layout: Conceptual
title: Learn how agent identity deletion works - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/concept-agent-identity-deletion
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how deleting an agent identity blueprint triggers automatic cleanup of child agent identities in Microsoft Entra, and how to restore deleted objects.
ms.topic: concept-article
ms.date: 2026-05-15T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: aca16107-491d-e28c-abcd-ff65cfc7abed
document_version_independent_id: aca16107-491d-e28c-abcd-ff65cfc7abed
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/concept-agent-identity-deletion.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/concept-agent-identity-deletion
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/concept-agent-identity-deletion.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 72f1f42f-3021-a0d3-63bf-2e56f400f6f0
---

# Learn how agent identity deletion works - Microsoft Entra Agent ID | Microsoft Learn

When you delete an agent identity blueprint or its principal, Microsoft Entra automatically cleans up all child agent identities and agents' user accounts with a *cascade cleanup* process. You don't need to manually query and delete each one. Understanding when and how this cascade cleanup happens helps you plan for restoration if needed.

Agent identity blueprints and their associated objects follow the same soft deletion and hard deletion behavior as other app registrations and service principals in Microsoft Entra. For a full overview of that process, see [Deleting and recovering applications FAQ](../identity/enterprise-apps/delete-recover-faq). This article focuses on what's unique to agent identity deletion.

## Object relationships

The following objects are involved in the agent identity deletion lifecycle. The cascade cleanup process is based on these relationships.

| Object | Directory object type | Relationship |
| --- | --- | --- |
| Agent identity blueprint | Application | Parent of the blueprint principal |
| Agent identity blueprint principal | Service principal | The principal for the blueprint |
| Agent identity | Service principal | Child of the blueprint principal |
| Agent's user account | User | Paired 1:1 with an agent identity |

## Disable versus delete

Before deleting a blueprint, consider whether disabling is the right action instead.

- **Disable**: Prevents the blueprint principal or its agent identities from authenticating, but leaves all objects in place. Use this when you want to temporarily stop agent activity, investigate an issue, or decommission agents gradually. Objects remain in the directory and count toward quota.
- **Delete**: Removes the agent identity blueprint or its agent identity blueprint principal from the directory and triggers cascade cleanup of child agent identities. Use this when you're permanently retiring a blueprint and all agents created from it. Deletion can't be undone after the 30-day soft-deletion window expires.

For information on disabling agent identities, see [Disable agent identities](disable-agent-identities).

## Cascade cleanup

When you delete an agent identity blueprint or its agent identity blueprint principal, Microsoft Entra automatically soft deletes all associated child agent identities and agents' user accounts. This cleanup is asynchronous.

The cascade process works as follows:

1. **You delete the agent identity blueprint or agent identity blueprint principal**: The object is soft deleted and moves to the recycle bin.
2. **Microsoft Entra triggers automatic cleanup**: A background task soft deletes all child agent identities and agents' user accounts associated with the deleted blueprint.
3. **Objects are restorable for 30 days**: Soft-deleted objects can be restored within 30 days. After that, they're permanently deleted.

Important

If you restore the agent identity blueprint principal before the background cleanup runs, child agent identities aren't affected. After the cleanup runs, each child identity must be restored individually. Restoring the agent identity blueprint principal doesn't reverse cascade deletions that already occurred.

### Cascade cleanup in audit logs

When the background cleanup task deletes agent identities, the deletions appear in your tenant's [Microsoft Entra audit logs](../identity/monitoring-health/concept-audit-logs). These entries have the following characteristics:

| Audit log field | Value |
| --- | --- |
| **Activity** | Delete service principal |
| **Initiated by (actor)** | Application: *Delete Agent Identities Task* |
| **Actor App ID** | (blank) |

The actor is shown as an application named **Delete Agent Identities Task** with no app ID. This is expected because the cleanup is performed by an internal Microsoft Entra background process, not by an external application or user.

Note

The cascade cleanup runs asynchronously after the blueprint is deleted. It might not run immediately — there can be a delay of hours or days between the blueprint deletion and the cleanup of child agent identities. Each child identity deletion appears as a separate audit log entry.

## Orphaned objects and quota considerations

When an agent identity blueprint principal is permanently deleted, any associated agent identities and agents' user accounts that weren't deleted become **orphaned objects** and become soft-deleted. Orphaned objects can't authenticate but continue to count toward directory quota until they're permanently deleted after the 30-day retention period expires.

Agent identity deletion follows the same quota rules as other Microsoft Entra objects. Soft-deleted objects continue to count toward quota limits until permanently deleted. For general quota information, see [Microsoft Entra service limits and restrictions](../identity/users/directory-service-limits-restrictions).

One consideration specific to agent identities: if you're using app-only permissions and are at the 250 agent identity limit for a blueprint, deleting an agent identity doesn't free up space until it's permanently deleted. By default, permanent deletion happens automatically after the 30-day retention period expires. If you need to free up quota immediately, you can force permanent deletion of soft-deleted agent identities. For steps, see [Permanently delete agent identity objects](howto-delete-agent-identity#permanently-delete-agent-identity-objects). Agent identity blueprints also follow this 250 limit when using app-only permissions.
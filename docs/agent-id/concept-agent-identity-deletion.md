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
description: Learn what Microsoft Graph documents about deleting agent identity objects and which related-object behavior requires confirmation.
ms.topic: concept-article
ms.date: 2026-11-06T00:00:00.0000000Z
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
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 72f1f42f-3021-a0d3-63bf-2e56f400f6f0
---

# Learn how agent identity deletion works - Microsoft Entra Agent ID | Microsoft Learn

Microsoft Graph documents soft deletion and recovery for agent identity and application objects. Its public delete API references don't specify whether deleting an agent identity blueprint or blueprint principal also deletes child agent identities or associated agent user accounts. Don't rely on a cascade unless Microsoft confirms the behavior for your scenario.

For general application soft-deletion behavior, see [Deleting and recovering applications FAQ](../identity/enterprise-apps/delete-recover-faq). This article separates the behavior documented for individual Graph objects from related-object behavior that isn't specified in those API references.

## Object relationships

| Object | Directory object type | Documented relationship or operation |
| --- | --- | --- |
| Agent identity blueprint | Application | Delete the application object by using the Graph application delete API. |
| Agent identity blueprint principal | Service principal | Delete the service principal by using the Graph servicePrincipal delete API. |
| Agent identity | `agentIdentity` service principal | The `agentIdentityBlueprintId` property identifies its blueprint. Delete an agent identity by using the Graph agentIdentity delete API. |
| Agent user | `agentUser`, a specialized user subtype | The [agentUser resource](/en-us/graph/api/resources/agentuser?view=graph-rest-beta&amp;preserve-view=true) has a one-to-one relationship with a parent agent identity. The agentIdentity delete API doesn't specify what happens to the associated agent user. Check that object separately. |

## Disable versus delete

Before deleting a blueprint, consider whether disabling is the right action instead.

- **Disable**: Prevents the blueprint principal or its agent identities from authenticating, but leaves objects in place. Use this when you want to temporarily stop agent activity or investigate an issue. For more information, see [Disable agent identities](disable-agent-identities).
- **Delete**: Sends a delete request for the specific Graph object addressed. The [application delete API](/en-us/graph/api/application-delete) documents a 30-day recovery period for deleted applications. The [agentIdentity delete API](/en-us/graph/api/agentidentity-delete?view=graph-rest-beta&amp;preserve-view=true) documents the same period for deleted agent identities.

## Related-object cleanup and restoration

Use the API that matches the object you intend to delete:

- Delete a blueprint application with `DELETE /applications/{applicationObjectId}`.
- Delete a blueprint principal with `DELETE /servicePrincipals/{servicePrincipalId}`.
- Delete one agent identity with `DELETE /servicePrincipals/{id}/microsoft.graph.agentIdentity`.

The public Graph API references describe deletion of the addressed object. They don't specify whether deleting a blueprint application or principal triggers cleanup of child agent identities or associated agent users. The [Graph restore API](/en-us/graph/api/directory-deleteditems-restore) specifies that restoring an application doesn't automatically restore its associated service principal; restore that principal separately. The API references don't specify cleanup timing, an internal cleanup actor, or whether restoring a parent restores or reverses changes to child objects.

Before deletion, record the object IDs you might need to recover. After the operation, check each related object independently. If an object was soft deleted, restore that object by its own ID; don't assume that restoring a blueprint or its principal restores related objects.

For restore steps, see [Delete and restore agent identity objects](howto-delete-agent-identity).

## Audit logs

Review the tenant's [Microsoft Entra audit logs](../identity/monitoring-health/concept-audit-logs) to investigate recorded directory operations. The Graph delete API references don't specify a particular internal cleanup actor or audit sequence for related objects.

## Quota considerations

The public Graph API references document soft deletion and a 30-day recovery period for agent identities and applications. They don't specify an agent identity-specific quota, a maximum number of agent identities per blueprint, a maximum number of inheritable resource apps, or when quota becomes available after deletion. Check current Microsoft Entra service limits and confirm Agent ID-specific limits before capacity planning. Don't assume that soft deletion immediately frees quota.

For general directory limits, see [Microsoft Entra service limits and restrictions](../identity/users/directory-service-limits-restrictions).
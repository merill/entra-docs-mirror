---
layout: Conceptual
title: Delete and restore agent identity objects - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/howto-delete-agent-identity
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how to delete an agent identity blueprint and restore soft-deleted agent identity objects in Microsoft Entra.
ms.topic: how-to
ms.date: 2026-11-06T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 06aac48f-ef7f-1dcc-728a-0c0d529e3bdb
document_version_independent_id: 06aac48f-ef7f-1dcc-728a-0c0d529e3bdb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/howto-delete-agent-identity.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/howto-delete-agent-identity
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/howto-delete-agent-identity.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/5cf46315-b33f-4e99-8224-a1592697eff9
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/715d24c3-3683-4219-82c5-1e3c813fb7fc
platformId: 295a8c0a-11cf-92a7-7b19-6ee3098323ce
---

# Delete and restore agent identity objects - Microsoft Entra Agent ID | Microsoft Learn

Microsoft Graph documents soft deletion and recovery for application and agent identity objects. Its public delete API references don't specify whether deleting a blueprint or blueprint principal also deletes child agent identities or associated agent user accounts. Don't rely on a cascade unless Microsoft confirms the behavior for your scenario.

For details on documented behavior and unresolved related-object behavior, see [Agent identity deletion](concept-agent-identity-deletion).

## Prerequisites

To delete and restore agent identity objects, you need:

- [Agent ID Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#agent-id-administrator) to view and manage agent identity objects.
- [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) to delete the blueprint application and its service principal.
- The `Application.ReadWrite.All` permission for Microsoft Graph operations on blueprint applications and service principals.
- The `AgentIdentity.DeleteRestore.All` permission for Microsoft Graph delete and restore operations on agent identities.
- The `AgentIdentity.ReadWrite.All` permission for permanent deletion of soft-deleted agent identities, or `AgentIdentityBlueprintPrincipal.ReadWrite.All` to permanently delete a soft-deleted blueprint principal.
- The `AgentIdentityBlueprintPrincipal.DeleteRestore.All` permission to restore a soft-deleted blueprint principal.
- The `AgentIdUser.ReadWrite.IdentityParentedBy` permission to delete or restore an associated agent user.

## Delete a blueprint

Deleting agent identity objects isn't supported in the Microsoft Entra admin center. Use Microsoft Graph API or Microsoft Entra PowerShell to delete blueprints and agent identities.

The blueprint application and blueprint principal are separate directory objects with separate delete endpoints. Use the endpoint for the object you intend to delete, then check the other object and related agent identities independently.

Note

Deleting an application moves it to the deleted items container, where it can be restored within 30 days. The [agentIdentity delete API](/en-us/graph/api/agentidentity-delete?view=graph-rest-beta&amp;preserve-view=true) documents the same recovery period for an agent identity. The Graph delete API references don't specify whether deleting a blueprint application or principal also deletes child agent identities or associated agent user accounts.

# [Microsoft Graph API](#tab/microsoft-graph-api)
To delete the blueprint application:

```http
DELETE https://graph.microsoft.com/v1.0/applications/{blueprint-app-object-id}
```

To delete the blueprint principal:

```http
DELETE https://graph.microsoft.com/v1.0/servicePrincipals/{blueprint-principal-object-id}
```

Note

For permissions and current behavior, see the Microsoft Graph [delete application](/en-us/graph/api/application-delete) and [delete servicePrincipal](/en-us/graph/api/serviceprincipal-delete) references.

# [Microsoft Entra PowerShell](#tab/microsoft-entra-powershell)
To delete the blueprint application:

```powershell
Connect-Entra -Scopes 'Application.ReadWrite.All'
Remove-EntraApplication -ObjectId '<blueprint-app-object-id>'
```

To delete only the blueprint principal:

```powershell
Connect-Entra -Scopes 'Application.ReadWrite.All'
Remove-EntraServicePrincipal -ObjectId '<blueprint-principal-object-id>'
```

---

The public Graph API references describe deletion of the addressed object, but don't specify cascade behavior for child agent identities or associated agent user accounts. Record their object IDs before deletion and check their states independently afterward. For more information, see [Agent identity deletion](concept-agent-identity-deletion).

Important

Don't assume that restoring a blueprint application or principal restores related objects. If a child agent identity or associated user account was soft deleted, restore or manage that object separately.

## Delete an agent identity

Use the agentIdentity-specific Graph operation to delete one agent identity. The API moves the object to a temporary container, where it can be restored within 30 days.

```http
DELETE https://graph.microsoft.com/beta/servicePrincipals/{agent-identity-object-id}/microsoft.graph.agentIdentity
```

For the API's permissions and current behavior, see [Delete agentIdentity](/en-us/graph/api/agentidentity-delete?view=graph-rest-beta&amp;preserve-view=true).

## Restore a blueprint principal

You can restore a soft-deleted blueprint principal within 30 days. Restoring an application doesn't automatically restore its associated service principal, so restore the blueprint principal separately. Restoring agent identity objects isn't supported in the Microsoft Entra admin center. Use Microsoft Graph API or Microsoft Entra PowerShell. For details, see [Restore deleted items](/en-us/graph/api/directory-deleteditems-restore).

# [Microsoft Graph API](#tab/microsoft-graph-api)
```http
POST https://graph.microsoft.com/v1.0/directory/deletedItems/{blueprint-principal-object-id}/restore
```

# [Microsoft Entra PowerShell](#tab/microsoft-entra-powershell)
```powershell
Connect-Entra -Scopes 'AgentIdentityBlueprintPrincipal.DeleteRestore.All'
Restore-EntraDeletedDirectoryObject -Id '<blueprint-principal-object-id>'
```

---

## Restore child agent identities

If an agent identity is soft deleted, restore it by its own object ID.

Note

The Microsoft Graph `/directory/deletedItems` endpoint doesn't support filtering by agent identity type. Query for deleted service principals and filter results on the client side using known object IDs, app IDs, or display names to identify the correct agent identities.

# [Microsoft Graph API](#tab/microsoft-graph-api)
1. List soft-deleted service principals to find affected agent identities:

    ```http
    GET https://graph.microsoft.com/v1.0/directory/deletedItems/microsoft.graph.servicePrincipal
    ```
2. Filter the results on the client side to identify agent identities linked to your blueprint, then restore each one:

    ```http
    POST https://graph.microsoft.com/v1.0/directory/deletedItems/{agent-identity-object-id}/restore
    ```

# [Microsoft Entra PowerShell](#tab/microsoft-entra-powershell)
```powershell
Connect-Entra -Scopes 'Application.ReadWrite.All'

# List deleted service principals and identify agent identities
Get-EntraDeletedServicePrincipal

# Restore each agent identity individually
Restore-EntraDeletedDirectoryObject -Id '<agent-identity-object-id>'
```

---

## Permanently delete agent identity objects

The Graph API references don't specify an agent identity-specific quota or when quota becomes available after deletion. Check current Microsoft Entra service limits before capacity planning.

Caution

Permanently deleted objects can't be restored. Only permanently delete objects when you're certain they're no longer needed.

# [Microsoft Graph API](#tab/microsoft-graph-api)
Permanently delete a soft-deleted agent identity:

```http
DELETE https://graph.microsoft.com/v1.0/directory/deletedItems/{agent-identity-object-id}
```

Permanently delete a soft-deleted blueprint principal:

```http
DELETE https://graph.microsoft.com/v1.0/directory/deletedItems/{blueprint-principal-object-id}
```

Permanently delete a soft-deleted blueprint application:

```http
DELETE https://graph.microsoft.com/v1.0/directory/deletedItems/{blueprint-app-object-id}
```

# [Microsoft Entra PowerShell](#tab/microsoft-entra-powershell)
Permanently delete a soft-deleted agent identity:

```powershell
Connect-Entra -Scopes 'AgentIdentity.ReadWrite.All'
Remove-EntraDeletedDirectoryObject -DirectoryObjectId '<agent-identity-object-id>'
```

Permanently delete a soft-deleted blueprint principal:

```powershell
Connect-Entra -Scopes 'AgentIdentityBlueprintPrincipal.ReadWrite.All'
Remove-EntraDeletedDirectoryObject -DirectoryObjectId '<blueprint-principal-object-id>'
```

Permanently delete a soft-deleted blueprint application:

```powershell
Connect-Entra -Scopes 'Application.ReadWrite.All'
Remove-EntraDeletedDirectoryObject -DirectoryObjectId '<blueprint-app-object-id>'
```

---

## Agents' user accounts

The agentIdentity delete API doesn't specify what happens to an associated agent user's account. Check the user object independently. If you confirm that the account is no longer needed, delete it separately:

# [Microsoft Graph API](#tab/microsoft-graph-api)
```http
DELETE https://graph.microsoft.com/beta/users/microsoft.graph.agentUser/{agent-user-object-id}
```

For the API's permissions and current behavior, see [Delete agentUser](/en-us/graph/api/agentuser-delete?view=graph-rest-beta&amp;preserve-view=true).

# [Microsoft Entra PowerShell](#tab/microsoft-entra-powershell)
```powershell
Connect-Entra -Scopes 'AgentIdUser.ReadWrite.IdentityParentedBy'
Remove-EntraUser -UserId '<agent-user-object-id>'
```

---
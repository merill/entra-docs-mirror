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
ms.date: 2026-04-29T00:00:00.0000000Z
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
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 295a8c0a-11cf-92a7-7b19-6ee3098323ce
---

# Delete and restore agent identity objects - Microsoft Entra Agent ID | Microsoft Learn

When you delete an agent identity blueprint, Microsoft Entra automatically cleans up all associated child agent identities and agents' user accounts. All deletions are soft deletions — deleted objects move to the recycle bin and can be restored within 30 days.

For a conceptual overview of how cascade cleanup works and quota considerations, see [Agent identity deletion works](concept-agent-identity-deletion).

## Prerequisites

To delete and restore agent identity objects, you need:

- [Agent ID Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#agent-id-administrator) to view and manage agent identity objects.
- [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) to delete the blueprint application and its service principal.
- The `Application.ReadWrite.All` permission for Microsoft Graph API or Microsoft Entra PowerShell operations.
- The `AgentIdentity.ReadWrite.All` permission to permanently delete soft-deleted agent identities.
- Owners of an agent identity blueprint can delete agent identity objects associated with that blueprint without these roles.

## Delete a blueprint

Deleting agent identity objects isn't supported in the Microsoft Entra admin center. Use Microsoft Graph API or Microsoft Entra PowerShell to delete blueprints and agent identities.

You can delete the agent identity blueprint and blueprint principal separately. Deleting the app registration also deletes the principal. Deleting only the principal leaves the app registration in place.

Note

Standard deletion is always soft deletion. Objects are moved to the recycle bin, but not immediately removed. Permanent deletion happens automatically after 30 days, or you can force it using the standard hard-delete process described in [Deleting and recovering applications FAQ](../identity/enterprise-apps/delete-recover-faq).

# [Microsoft Graph API](#tab/microsoft-graph-api)
To delete the blueprint application (which also deletes the principal):

```http
DELETE https://graph.microsoft.com/v1.0/applications/{blueprint-app-object-id}
```

To delete only the blueprint principal:

```http
DELETE https://graph.microsoft.com/v1.0/servicePrincipals/{blueprint-principal-object-id}
```

Note

Explicit hard deletion of a blueprint principal (`permanentDelete`) is blocked. Use the standard delete endpoint shown above.

# [Microsoft Entra PowerShell](#tab/microsoft-entra-powershell)
To delete the blueprint application (which also deletes the principal):

```powershell
Connect-Entra -Scopes 'Application.ReadWrite.All'
Remove-EntraApplication -ObjectId <blueprint-app-object-id>
```

To delete only the blueprint principal:

```powershell
Connect-Entra -Scopes 'Application.ReadWrite.All'
Remove-EntraServicePrincipal -ObjectId <blueprint-principal-object-id>
```

---

After you delete the blueprint or its principal, Microsoft Entra automatically soft deletes all associated child agent identities and agents' user accounts. For more information on this process, see [Agent identity deletion](concept-agent-identity-deletion).

Important

If you restore the blueprint principal before the cascade cleanup runs, child agent identities aren't affected. After the cleanup runs, each child identity must be restored individually. Restoring the blueprint principal doesn't reverse cascade deletions that already occurred.

## Restore a blueprint principal

You can restore a soft-deleted blueprint principal within 30 days. Restoring agent identity objects isn't supported in the Microsoft Entra admin center. Use Microsoft Graph API or Microsoft Entra PowerShell.

# [Microsoft Graph API](#tab/microsoft-graph-api)
```http
POST https://graph.microsoft.com/v1.0/directory/deletedItems/{blueprint-principal-object-id}/restore
```

# [Microsoft Entra PowerShell](#tab/microsoft-entra-powershell)
```powershell
Connect-Entra -Scopes 'Application.ReadWrite.All'
Restore-EntraDeletedDirectoryObject -Id <blueprint-principal-object-id>
```

---

## Restore child agent identities

If the cascade cleanup already ran and child agent identities were soft deleted, restore each one individually.

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
Restore-EntraDeletedDirectoryObject -Id <agent-identity-object-id>
```

---

## Permanently delete agent identity objects

Soft-deleted objects continue to count toward [directory quota](../identity/users/directory-service-limits-restrictions) until they're permanently deleted. If you're at the 250 agent identity limit for a blueprint using app-only permissions, you might need to force permanent deletion to free up quota immediately rather than waiting for the 30-day retention period to expire. Permanent deletion of an agent identity blueprint principal is blocked. To permanently free quota used by a blueprint principal, wait for the 30-day retention period to expire.

Caution

Permanently deleted objects can't be restored. Only permanently delete objects when you're certain they're no longer needed.

# [Microsoft Graph API](#tab/microsoft-graph-api)
Permanently delete a soft-deleted agent identity:

```http
DELETE https://graph.microsoft.com/v1.0/directory/deletedItems/{agent-identity-object-id}
```

Permanently delete a soft-deleted blueprint application:

```http
DELETE https://graph.microsoft.com/v1.0/directory/deletedItems/{blueprint-app-object-id}
```

# [Microsoft Entra PowerShell](#tab/microsoft-entra-powershell)
Permanently delete a soft-deleted agent identity:

```powershell
Connect-Entra -Scopes 'AgentIdentity.ReadWrite.All'
Remove-EntraDeletedDirectoryObject -DirectoryObjectId <agent-identity-object-id>
```

Permanently delete a soft-deleted blueprint application:

```powershell
Connect-Entra -Scopes 'Application.ReadWrite.All'
Remove-EntraDeletedDirectoryObject -DirectoryObjectId <blueprint-app-object-id>
```

---

## Agents' user accounts

Agents' user accounts are paired 1:1 with agent identities. If agents' user accounts aren't automatically cleaned up as part of cascade deletion, delete them manually.

# [Microsoft Graph API](#tab/microsoft-graph-api)
```http
DELETE https://graph.microsoft.com/v1.0/users/{agent-user-object-id}
```

# [Microsoft Entra PowerShell](#tab/microsoft-entra-powershell)
```powershell
Connect-Entra -Scopes 'User.ReadWrite.All'
Remove-EntraUser -UserId <agent-user-object-id>
```

---
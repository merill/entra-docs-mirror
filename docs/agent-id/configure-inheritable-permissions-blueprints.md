---
layout: Conceptual
title: Configure inheritable permissions for agent identity blueprints | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/configure-inheritable-permissions-blueprints
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how to configure delegated permission scope inheritance for agent identity blueprints by using the Microsoft Graph beta API.
ms.topic: how-to
ms.date: 2026-11-06T00:00:00.0000000Z
ms.reviewer: ergreenl
ai-usage: ai-assisted
locale: en-us
document_id: 39610f42-4c35-c50f-a1cd-f8cf07b0525d
document_version_independent_id: 39610f42-4c35-c50f-a1cd-f8cf07b0525d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/configure-inheritable-permissions-blueprints.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/configure-inheritable-permissions-blueprints
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/configure-inheritable-permissions-blueprints.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: b5aa0f1e-d1c8-6d4f-cf74-9839dff92f6e
---

# Configure inheritable permissions for agent identity blueprints | Microsoft Learn

Configure inheritable permissions on an agent identity blueprint to specify which delegated scopes can be inherited by agent identities. A scope is eligible for inheritance only when the resource app is configured as inheritable and the scope is granted to the blueprint principal.

For conceptual background on how inheritable permissions relate to required resource access and direct permission grants, see [Inheritable permissions and required resource access](concept-inheritable-permissions).

## Prerequisites

- An existing agent identity blueprint.
- For Microsoft Graph requests, the `AgentIdentityBlueprint.Create` permission to add an entry and `AgentIdentityBlueprint.ReadWrite.All` to update or delete an entry.
- For delegated requests by a nonowner, the Agent ID Administrator role. Blueprint owners can manage their own blueprints.

## How inheritable permissions work

The public Microsoft Graph beta `inheritablePermission` resource documents delegated scope inheritance through `inheritableScopes`. The broader Agent ID permission model also describes application-role inheritance, but the public Graph reference doesn't define an application-role property or payload. Confirm the supported Graph API contract before relying on application-role inheritance.

For inheritance conditions and the distinction between declarations and grants, see [Inheritable permissions and required resource access](concept-inheritable-permissions) and the [Microsoft Graph `inheritablePermission` resource](/en-us/graph/api/resources/inheritablepermission?view=graph-rest-beta&amp;preserve-view=true).

## Inheritance patterns

The Graph beta API supports these patterns for delegated permission scopes:

| Pattern | Graph type | Description |
| --- | --- | --- |
| All allowed scopes | `allAllowedScopes` | Make all delegated scopes published by the resource app eligible for inheritance. |
| Enumerated scopes | `enumeratedScopes` | Make only the listed delegated scopes eligible for inheritance. |
| No scopes | `noScopes` | Disable delegated scope inheritance for the resource app. |

## Inheritable permissions limitations

The public Microsoft Graph reference doesn't specify a maximum number of resource apps or `inheritablePermissions` entries for a blueprint. Don't rely on a numeric limit unless Microsoft publishes or confirms it.

The public Graph reference also doesn't document how application roles are configured for inheritance. The API examples in this article are limited to delegated scopes.

Regularly review the scopes configured on each blueprint and the grants on its blueprint principal. Remove permissions that are no longer needed.

## Configure scope inheritance (using Microsoft Graph)

These examples use the Microsoft Graph beta API. Beta APIs are subject to change and aren't supported for production applications. For details, see the Microsoft Graph [create](/en-us/graph/api/agentidentityblueprint-post-inheritablepermissions?view=graph-rest-beta&amp;preserve-view=true), [update](/en-us/graph/api/inheritablepermission-update?view=graph-rest-beta&amp;preserve-view=true), and [delete](/en-us/graph/api/agentidentityblueprint-delete-inheritablepermissions?view=graph-rest-beta&amp;preserve-view=true) operations.

Use the `inheritablePermissions` navigation property on the `agentIdentityBlueprint` application resource. Each entry specifies scope inheritance for one resource app. When specifying `resourceAppId`, use the resource app's application ID in GUID format.

### Add all delegated scopes for Microsoft Graph

```http
POST https://graph.microsoft.com/beta/applications/bc057821-f236-49d6-9f2c-1ebf43e9437a/microsoft.graph.agentIdentityBlueprint/inheritablePermissions
Content-Type: application/json

{
  "resourceAppId": "00000003-0000-0000-c000-000000000000",
  "inheritableScopes": {
    "@odata.type": "microsoft.graph.allAllowedScopes"
  }
}
```

The request returns `201 Created`. The response includes the configured resource app and inheritance pattern:

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "resourceAppId": "00000003-0000-0000-c000-000000000000",
  "inheritableScopes": {
    "@odata.type": "microsoft.graph.allAllowedScopes",
    "kind": "allAllowed"
  }
}
```

### Add enumerated scopes for a resource app

To allow only selected delegated scopes, use the `enumeratedScopes` pattern:

```http
POST https://graph.microsoft.com/beta/applications/bc057821-f236-49d6-9f2c-1ebf43e9437a/microsoft.graph.agentIdentityBlueprint/inheritablePermissions
Content-Type: application/json

{
  "resourceAppId": "00000003-0000-0000-c000-000000000000",
  "inheritableScopes": {
    "@odata.type": "microsoft.graph.enumeratedScopes",
    "scopes": [
      "User.Read",
      "Mail.Read"
    ]
  }
}
```

### Add scopes for multiple resource apps

Create a separate entry for each resource app, using its application ID as `resourceAppId`. For example, change the ID to the SharePoint Online resource app ID for a separate request:

```http
POST https://graph.microsoft.com/beta/applications/bc057821-f236-49d6-9f2c-1ebf43e9437a/microsoft.graph.agentIdentityBlueprint/inheritablePermissions
Content-Type: application/json

{
  "resourceAppId": "00000003-0000-0ff1-ce00-000000000000",
  "inheritableScopes": {
    "@odata.type": "microsoft.graph.allAllowedScopes"
  }
}
```

### Disable scope inheritance

Use `PATCH` to update an existing entry. This example disables delegated scope inheritance for Microsoft Graph:

```http
PATCH https://graph.microsoft.com/beta/applications/bc057821-f236-49d6-9f2c-1ebf43e9437a/microsoft.graph.agentIdentityBlueprint/inheritablePermissions/00000003-0000-0000-c000-000000000000
Content-Type: application/json

{
  "inheritableScopes": {
    "@odata.type": "microsoft.graph.noScopes"
  }
}
```

The update operation returns `204 No Content` when successful. To remove an entry, use `DELETE`:

```http
DELETE https://graph.microsoft.com/beta/applications/bc057821-f236-49d6-9f2c-1ebf43e9437a/microsoft.graph.agentIdentityBlueprint/inheritablePermissions/00000003-0000-0000-c000-000000000000
```
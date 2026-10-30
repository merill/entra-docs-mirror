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
description: Learn how to configure inheritable permissions for agent identity blueprints to automatically grant OAuth 2.0 delegated permission scopes and application roles to agent identities.
ms.topic: how-to
ms.date: 2026-05-21T00:00:00.0000000Z
ms.reviewer: ergreenl
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
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: b5aa0f1e-d1c8-6d4f-cf74-9839dff92f6e
---

# Configure inheritable permissions for agent identity blueprints | Microsoft Learn

Configure inheritable permissions on an agent identity blueprint to preauthorize a base set of delegated scopes and application roles. Agent identities created from the blueprint automatically inherit those permissions without interactive consent prompts.

For conceptual background on how inheritable permissions relate to required resource access and direct permission grants, see [Inheritable permissions and required resource access](concept-inheritable-permissions).

## Prerequisites

- An existing agent identity blueprint already created and configured
- Either of the following permissions:
    - Agent ID Developer role for managing agent identity blueprints owned by the user
    - Agent ID Administrator role for managing agent identity blueprints

## How inheritable permissions work

During token issuance for an agent identity, the platform merges eligible inherited scopes with the agent's requested delegated scopes. Inherited scopes appear in the access token's **scp** claim and inherited roles appear in the **roles** claim. For details on inheritance conditions and the relationship between declarations, grants, and effective permissions, see [Inheritable permissions and required resource access](concept-inheritable-permissions).

## Inheritance patterns

The concept article describes inheritance patterns at a high level. The following table shows the specific `kind` values used in the API when you configure inheritance per resource app:

| Inheritance | Kind | Description |
| --- | --- | --- |
| All Allowed | `allAllowed` | Inherit all available delegated scopes or application roles for the specified resource app. Newly granted scopes or roles on the agent identity blueprint principal are automatically included. |
| None | `none` | Inherit no scopes or roles for the specified resource app. Use this to explicitly disable inheritance for scopes (`noScopes`) or roles (`noRoles`) independently. |

You can configure scopes and roles independently on the same resource. For example, you can inherit all scopes while inheriting no roles, or vice versa.

## Inheritable permissions limitations

- Maximum of 50 resource apps per agent identity blueprint (for example, up to 50 entries in the *inheritablePermissions* collection). If you exceed this limit, reduce the number of resource apps to stay within the supported boundary.

Regularly review and monitor your inheritable permissions configuration. Reevaluate inherited scopes and roles to ensure they remain appropriate for your use case. Audit which inherited scopes and roles are being used by agents and remove any unused permissions from both the agent identity blueprint principal and the inheritable permissions list to maintain security hygiene.

## Configure inheritable permissions (using Microsoft Graph)

To configure inheritable permissions, use the inheritablePermissions navigation property on the `agentIdentityBlueprint` application resource. Each entry specifies the scopes and roles inheritance configuration for a single resource app. Document your configuration decisions by tracking why each scope or role is inheritable and who approved it for audit purposes.

When specifying the `resourceAppId` in your requests, ensure you provide a valid GUID format. Invalid GUIDs result in 400 Bad Request errors.

### Add all scopes and roles inheritance for Microsoft Graph

**Request**

```http
POST https://graph.microsoft.com/v1.0/applications/microsoft.graph.agentIdentityBlueprint/bc057821-f236-49d6-9f2c-1ebf43e9437a/inheritablePermissions
Content-Type: application/json
OData-Version: 4.0

{
  "resourceAppId": "00000003-0000-0000-c000-000000000000",
  "inheritableScopes": {
    "@odata.type": "#microsoft.graph.allAllowedScopes",
    "kind": "allAllowed"
  },
  "inheritableRoles": {
    "@odata.type": "#microsoft.graph.allAllowedRoles",
    "kind": "allAllowed"
  }
}
```

**Response**

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#applications('bc057821-f236-49d6-9f2c-1ebf43e9437a')/inheritablePermissions/$entity",
  "resourceAppId": "00000003-0000-0000-c000-000000000000",
  "inheritableScopes": {
    "@odata.type": "microsoft.graph.allAllowedScopes",
    "kind": "allAllowed"
  },
  "inheritableRoles": {
    "@odata.type": "microsoft.graph.allAllowedRoles",
    "kind": "allAllowed"
  }
}
```

### Add all scopes and roles inheritance for multiple resources

You can configure inheritable permissions for multiple resource apps on the same blueprint. Each resource requires a separate POST request. The following example adds inheritance for both Microsoft Graph and SharePoint Online.

**Request (Microsoft Graph)**

```http
POST https://graph.microsoft.com/v1.0/applications/microsoft.graph.agentIdentityBlueprint/bc057821-f236-49d6-9f2c-1ebf43e9437a/inheritablePermissions
Content-Type: application/json
OData-Version: 4.0

{
  "resourceAppId": "00000003-0000-0000-c000-000000000000",
  "inheritableScopes": {
    "@odata.type": "#microsoft.graph.allAllowedScopes",
    "kind": "allAllowed"
  },
  "inheritableRoles": {
    "@odata.type": "#microsoft.graph.allAllowedRoles",
    "kind": "allAllowed"
  }
}
```

**Response**

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#applications('bc057821-f236-49d6-9f2c-1ebf43e9437a')/inheritablePermissions/$entity",
  "resourceAppId": "00000003-0000-0000-c000-000000000000",
  "inheritableScopes": {
    "@odata.type": "microsoft.graph.allAllowedScopes",
    "kind": "allAllowed"
  },
  "inheritableRoles": {
    "@odata.type": "microsoft.graph.allAllowedRoles",
    "kind": "allAllowed"
  }
}
```

**Request (SharePoint Online)**

```http
POST https://graph.microsoft.com/v1.0/applications/microsoft.graph.agentIdentityBlueprint/bc057821-f236-49d6-9f2c-1ebf43e9437a/inheritablePermissions
Content-Type: application/json
OData-Version: 4.0

{
  "resourceAppId": "00000003-0000-0ff1-ce00-000000000000",
  "inheritableScopes": {
    "@odata.type": "#microsoft.graph.allAllowedScopes",
    "kind": "allAllowed"
  },
  "inheritableRoles": {
    "@odata.type": "#microsoft.graph.allAllowedRoles",
    "kind": "allAllowed"
  }
}
```

**Response**

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#applications('bc057821-f236-49d6-9f2c-1ebf43e9437a')/inheritablePermissions/$entity",
  "resourceAppId": "00000003-0000-0ff1-ce00-000000000000",
  "inheritableScopes": {
    "@odata.type": "microsoft.graph.allAllowedScopes",
    "kind": "allAllowed"
  },
  "inheritableRoles": {
    "@odata.type": "microsoft.graph.allAllowedRoles",
    "kind": "allAllowed"
  }
}
```

### Add scopes inheritance only (no roles)

To inherit delegated scopes but not application roles, set `inheritableRoles` to `noRoles`.

**Request**

```http
POST https://graph.microsoft.com/v1.0/applications/microsoft.graph.agentIdentityBlueprint/bc057821-f236-49d6-9f2c-1ebf43e9437a/inheritablePermissions
Content-Type: application/json
OData-Version: 4.0

{
  "resourceAppId": "00000003-0000-0000-c000-000000000000",
  "inheritableScopes": {
    "@odata.type": "#microsoft.graph.allAllowedScopes",
    "kind": "allAllowed"
  },
  "inheritableRoles": {
    "@odata.type": "#microsoft.graph.noRoles",
    "kind": "none"
  }
}
```

**Response**

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#applications('bc057821-f236-49d6-9f2c-1ebf43e9437a')/inheritablePermissions/$entity",
  "resourceAppId": "00000003-0000-0000-c000-000000000000",
  "inheritableScopes": {
    "@odata.type": "microsoft.graph.allAllowedScopes",
    "kind": "allAllowed"
  },
  "inheritableRoles": {
    "@odata.type": "microsoft.graph.noRoles",
    "kind": "none"
  }
}
```

### Add roles inheritance only (no scopes)

To inherit application roles but not delegated scopes, set `inheritableScopes` to `noScopes`.

**Request**

```http
POST https://graph.microsoft.com/v1.0/applications/microsoft.graph.agentIdentityBlueprint/bc057821-f236-49d6-9f2c-1ebf43e9437a/inheritablePermissions
Content-Type: application/json
OData-Version: 4.0

{
  "resourceAppId": "00000003-0000-0000-c000-000000000000",
  "inheritableScopes": {
    "@odata.type": "#microsoft.graph.noScopes",
    "kind": "none"
  },
  "inheritableRoles": {
    "@odata.type": "#microsoft.graph.allAllowedRoles",
    "kind": "allAllowed"
  }
}
```

**Response**

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#applications('bc057821-f236-49d6-9f2c-1ebf43e9437a')/inheritablePermissions/$entity",
  "resourceAppId": "00000003-0000-0000-c000-000000000000",
  "inheritableScopes": {
    "@odata.type": "microsoft.graph.noScopes",
    "kind": "none"
  },
  "inheritableRoles": {
    "@odata.type": "microsoft.graph.allAllowedRoles",
    "kind": "allAllowed"
  }
}
```

### Update to disable roles inheritance

If an entry already exists for a resourceAppId, use PATCH to update it rather than attempting to create a duplicate entry, which would result in a 409 Conflict error. The following example disables role inheritance while keeping scope inheritance enabled.

**Request**

```http
PATCH https://graph.microsoft.com/v1.0/applications/microsoft.graph.agentIdentityBlueprint/bc057821-f236-49d6-9f2c-1ebf43e9437a/inheritablePermissions/00000003-0000-0000-c000-000000000000
Content-Type: application/json
OData-Version: 4.0

{
  "inheritableRoles": {
    "@odata.type": "#microsoft.graph.noRoles",
    "kind": "none"
  }
}
```

**Response**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#applications('bc057821-f236-49d6-9f2c-1ebf43e9437a')/inheritablePermissions/$entity",
  "resourceAppId": "00000003-0000-0000-c000-000000000000",
  "inheritableScopes": {
    "@odata.type": "microsoft.graph.allAllowedScopes",
    "kind": "allAllowed"
  },
  "inheritableRoles": {
    "@odata.type": "microsoft.graph.noRoles",
    "kind": "none"
  }
}
```

### Update to disable scopes inheritance

The following example disables scope inheritance while keeping role inheritance enabled.

**Request**

```http
PATCH https://graph.microsoft.com/v1.0/applications/microsoft.graph.agentIdentityBlueprint/bc057821-f236-49d6-9f2c-1ebf43e9437a/inheritablePermissions/00000003-0000-0000-c000-000000000000
Content-Type: application/json
OData-Version: 4.0

{
  "inheritableScopes": {
    "@odata.type": "#microsoft.graph.noScopes",
    "kind": "none"
  }
}
```

**Response**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#applications('bc057821-f236-49d6-9f2c-1ebf43e9437a')/inheritablePermissions/$entity",
  "resourceAppId": "00000003-0000-0000-c000-000000000000",
  "inheritableScopes": {
    "@odata.type": "microsoft.graph.noScopes",
    "kind": "none"
  },
  "inheritableRoles": {
    "@odata.type": "microsoft.graph.allAllowedRoles",
    "kind": "allAllowed"
  }
}
```

### Delete existing inheritable permissions

**Request**

```http
DELETE https://graph.microsoft.com/v1.0/applications/microsoft.graph.agentIdentityBlueprint/bc057821-f236-49d6-9f2c-1ebf43e9437a/inheritablePermissions/00000003-0000-0000-c000-000000000000
OData-Version: 4.0
```

**Response**

```http
HTTP/1.1 204 No Content
```
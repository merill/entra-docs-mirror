---
layout: Conceptual
title: Microsoft Entra Agent ID logs | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/sign-in-audit-logs-agents
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how audit and sign-in activities associated with agent identities are logged in Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2026-04-28T00:00:00.0000000Z
ms.reviewer: egreenberg14
locale: en-us
document_id: 4341dc75-ef36-5ba3-0387-11511d9dfd54
document_version_independent_id: 4341dc75-ef36-5ba3-0387-11511d9dfd54
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/sign-in-audit-logs-agents.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/sign-in-audit-logs-agents
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/sign-in-audit-logs-agents.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 61d3c02b-765a-14a2-f668-bbfbaa958c59
---

# Microsoft Entra Agent ID logs | Microsoft Learn

As the usage, capabilities, and scope of AI agents grow, it's important to understand how activities associated with agent identities are logged in Microsoft Entra ID. As an IT admin, you need to know what information is available in the audit and sign-in logs and how to use that information to monitor agent activity. The audit and sign-in logs are helpful when you need to investigate the following types of scenarios:

- Sign-in logs for agents or agent related traffic
- Audit logs for when an agent identity or agent's user account is either the initiator or performer of an operation in my tenant

This article describes how agent identity activities are logged in Microsoft Entra ID and how to access those logs using the Microsoft Entra admin center and Microsoft Graph.

## Audit logs

Agent activity is logged under the base identity type from where the activity originates. There are currently three agent identity types that appear in the audit logs, each correlating to an existing identity type in Microsoft Entra ID.

- **Agent identity blueprint** activities appear as *application events* (for example, "Add application" or "Delete application").
- **Agent identity** activities appear as *service principal events* (for example, "Add service principal" or "Update service principal").
- **Agent's user account** activities appear as *user events* (for example, "Add user").

To identify whether an audit event involves an agent identity, check the `agentType` property on the `initiatedBy`, `performedBy`, and `targetResources` fields. An agent identity and an agent's user account can both be represented in the `initiatedBy` and `performedBy` events. A value other than `notAgentic` indicates agent involvement.

### agentType

The `agentType` value further clarifies agent identity actions. The `agentType` property indicates whether the identity involved in an audit event is an agent identity, agent identity blueprint, or an agent's user account.

The `agentType` property appears on the following resources:

- `auditAppIdentity`
- `auditUserIdentity`
- `targetResource`
- `auditActivityPerformer`

| Value | Description |
| --- | --- |
| `notAgentic` | The identity isn't an agent. This is a standard app, user, or service principal. |
| `agenticApp` | An agent identity blueprint, which is the template or definition for an agent. Analogous to an app registration. |
| `agenticAppInstance` | An agent identity, which is a specific running instance of an agent. Analogous to a service principal. |
| `agentIdentityBlueprintPrincipal` | The blueprint principal itself, which is the service principal that represents the blueprint. |
| `agentIDuser` | An agent's user account. This identity lets an agent act as a user with user-delegated permissions. |
| `unknownFutureValue` | Evolvable enumeration sentinel value. Don't use. |

The following table summarizes how these agent activities and values map together and appear in the audit logs:

| Agent action | Audit activity | agentType value |
| --- | --- | --- |
| Create an agent identity blueprint | Add application | `agenticApp` |
| Create an agent identity | Add service principal | `agenticAppInstance` |
| Create an agent's user account | Add user | `agentIDuser` |
| Update an agent identity blueprint | Update application | `agenticApp` |
| Update an agent identity | Update service principal | `agenticAppInstance` |
| Delete an agent identity blueprint | Delete application | `agenticApp` |
| Delete an agent identity | Delete service principal | `agenticAppInstance` |

Tip

To receive `agentIdentityBlueprintPrincipal` and `agentIDuser` values in Microsoft Graph responses, include the `Prefer: include-unknown-enum-members` request header. These values are part of an [evolvable enumeration](/en-us/graph/best-practices-concept#handling-future-members-in-evolvable-enumerations).

### blueprintId

The `blueprintId` property is the object ID of the [agentIdentityBlueprint](/en-us/graph/api/resources/agentidentityblueprint?view=graph-rest-beta&amp;preserve-view=true) associated with the agent. Use this property to correlate an agent identity (instance) back to its blueprint (template). This property appears on `auditAppIdentity`, [targetResource](/en-us/graph/api/resources/targetresource?view=graph-rest-beta&amp;preserve-view=true), and `auditActivityPerformer`.

The relationship between `blueprintId` and the agent identity is similar to the relationship between an app registration and its service principal. Multiple agent identities can share the same blueprint.

### What changed in the audit log schema

The following changes to the audit log schema enable agent identity tracking:

- The `initiatedBy.app` property now uses the `auditAppIdentity` resource type, which includes `agentType` and `blueprintId` alongside the existing `appId`, `displayName`, `servicePrincipalId`, and `servicePrincipalName` properties.
- The [targetResource](/en-us/graph/api/resources/targetresource?view=graph-rest-beta&amp;preserve-view=true) resource type now includes `agentType` and `blueprintId` properties.
- The [auditUserIdentity](/en-us/graph/api/resources/audituseridentity?view=graph-rest-beta&amp;preserve-view=true) resource type now includes an `agentType` property.
- A new `auditActivityPerformer` resource type provides `agentType`, `appId`, and `blueprintId` for the actor of an audit event.

## Sign-in logs

The `agentSignIn` sign-in event type contains properties about the agent, such as if the agent is an app or an instance of an app. Because agents can sign in with either user-delegated or app-only permissions, their sign-ins might appear across each of the four sign-in log types.

The `agentSignIn` sign-in event type is available in the Microsoft Entra admin center and the Microsoft Graph API.

# [Microsoft Entra admin center](#tab/microsoft-entra-admin-center)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../identity/role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Sign-in logs**.
3. Use the following filter options to view agent sign-ins:
    - **Agent type**: Choose from **Agent ID user**, **Agent Identity**, **Agent Identity Blueprint** or **Not Agentic**
    - **Is Agent**: Choose from **No** or **Yes**

# [Microsoft Graph](#tab/microsoft-graph)
Microsoft Entra Agent ID logs can be viewed and managed using Microsoft Graph on the `/beta` endpoint.

To get started, follow these instructions to work with recommendations using Microsoft Graph in Graph Explorer.

1. Sign in to [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).
2. Select **GET** as the HTTP method from the dropdown.
3. Set the API version to **beta**.

### Retrieve agent identity sign-in events

To retrieve only sign-in events where Microsoft Entra Agent ID was involved, you need to find events initiated by a service principal where the agent type is `AgentIdentity`. Use the following Microsoft Graph request:

```http
GET https://graph.microsoft.com/beta/auditLogs/signIns?$filter=signInEventTypes/any(t: t eq 'servicePrincipal') and agent/agentType eq 'AgentIdentity'
```

---
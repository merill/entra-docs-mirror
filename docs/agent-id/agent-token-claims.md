---
layout: Conceptual
title: Token claims reference for agent IDs - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/agent-token-claims
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn about specialized token claims used by agent applications in Microsoft Entra to identify entity types, relationships, and roles during authentication and authorization flows.
ms.topic: reference
ms.date: 2025-11-04T00:00:00.0000000Z
ms.reviewer: jmprieur
locale: en-us
document_id: fe6f3d42-6075-795d-ec73-039d66fc6cec
document_version_independent_id: fe6f3d42-6075-795d-ec73-039d66fc6cec
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/agent-token-claims.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/agent-token-claims
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/agent-token-claims.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 1baa76e1-810b-0c73-dd9e-8d506241a4dd
---

# Token claims reference for agent IDs - Microsoft Entra Agent ID | Microsoft Learn

Agents use specialized token claims to identify different entity types and their relationships during authentication and authorization flows. These claims enable proper attribution, policy evaluation, and audit trails for agent operations. This article outlines the token claims for agent applications, detailing how tokens identify agent entities and their roles in authentication flows.

Clients using agent identities are expected to treat the access tokens issued to them to use at resource servers as opaque, and not try to parse them. However, resource servers that receive access tokens issued to agents need to parse the tokens to validate them and extract claims for authorization purposes.

## Core token claim types

Tokens issued for identities used for resource access include claims that you'd normally expect to see in access tokens that Microsoft Entra issues. For more information, see [access token claim reference](/en-us/entra/identity-platform/access-token-claims-reference). The following example shows a sample access token issued to an agent acting autonomously.

```json
{
  "aud": "00001111-aaaa-2222-bbbb-3333cccc4444",
  "iss": "https://sts.windows.net/00000001-0000-0ff1-ce00-000000000000/",
  "iat": 1753392285,
  "nbf": 1753392285,
  "exp": 1753421385,
  "aio": "Y2JgYGhn1nzmErKqi0vc4Fr6H22/C5/4FP+xZbZYpik8nRkp+gEA",
  "appid": "11112222-bbbb-3333-cccc-4444dddd5555",
  "appidacr": "2",
  "idp": "https://sts.windows.net/00000001-0000-0ff1-ce00-000000000000/",
  "idtyp": "app",
  "oid": "aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb",
  "rh": "1.AAAAAQAAAAAA8Q_OAAAAAAAAADQNUfLKjbhKoLyq7E06PjYAAAAAAA.",
  "sub": "bbbbbbbb-1111-2222-3333-cccccccccccc",
  "tid": "aaaabbbb-0000-cccc-1111-dddd2222eeee",
  "uti": "m5RaaRnoFUyp2TbSCAAAAA",
  "ver": "1.0",
  "xms_act_fct": "3 9 11",
  "xms_ftd": "Z5DrW4HFOkR_Lz0M5qETa260d2-fO6seMZJ_tOwRNuc",
  "xms_idrel": "7 10",
  "xms_sub_fct": "9 3 11",
  "xms_tnt_fct": "3 9",
  "xms_par_app_azp": "30cf4c22-9985-4ef7-8756-91cc888176bd"
}
```

In v2 tokens, you see `azp` instead of `appid`. They both refer to the application ID of the agent identity.

You'd notice that the token includes a few claims that aren't previously seen in access tokens issued to applications. The following optional claims are also supported to identify that the tokens are for agent identities. They also provide more context in which the agent identity is acting.

- `xms_tnt_fct`
- `xms_sub_fct`
- `xms_act_fct`
- `xms_par_app_azp`

| Claim Name | Description |
| --- | --- |
| `tid` | Tenant ID of the customer tenant where the agent identity is registered. It's the tenant where the token is valid. |
| `sub` | Subject (the user, service principal, or agent identity being authenticated) |
| `oid` | Object ID of the subject. User object ID for user delegation scenarios. Agent ID service principal OID for app-only scenarios. Agent's user account OID for user impersonation scenarios. |
| `idtyp` | Type of entity the subject is. Values are `user`, `app`. |
| `xms_idrel` | Relationship between the subject and the resource tenant. Learn more. |
| `aud` | Audience (the API that the agent is trying to access) |
| `azp` or `appid` | Authorized party / actor. The application ID of the agent identity. Enables proper client attribution in audit logs. |
| `scp` | Scope. Delegated permissions for user-context tokens. Only present in user delegation and agent's user account scenarios. Empty or `/` for app-only scenarios |
| `xms_act_fct` | Actor facets claim. Learn more. |
| `xms_sub_fct` | Subject facets claim. Learn more . |
| `xms_tnt_fct` | Tenant facets claim. Learn more . |
| `xms_par_app_azp` | Parent application of the authorized party. Learn more . |

## idtyp claim values by scenario

The `idtyp` claim identifies the type of entity the token subject represents. The value depends on which agent flow issued the token:

| Agent scenario | `idtyp`value | Subject (`sub`/`oid`) |
| --- | --- | --- |
| On-behalf-of flow (interactive agent) | `user` | The human user the agent acts on behalf of |
| Autonomous app flow (app-only) | `app` | The agent identity service principal |
| Agent's user account flow | `user` | The agent's own user account |

Note

The `idtyp` value alone doesn't distinguish a human user from an agent's user account. Use the `xms_sub_fct` claim (value `13` = agent's user account) to differentiate these scenarios.

## xms\_idrel

The `xms_idrel` claim indicates the identity relationship between the entity for which the token is issued and the resource tenant.

Here are the possible values for the `xms_idrel` claim. It's a multivalued claim, meaning it can have multiple values, separated by spaces. The values are represented as integers. The valid values are always odd numbers starting from 1.

| Claim Value | Description |
| --- | --- |
| `1` | Member user |
| `3` | MSA member user |
| `5` | Guest user |
| `7` | Service principal |
| `9` | Device principal |
| `11` | GDAP user |
| `13` | SPLess application |
| `15` | Passthrough |
| `17` | Native identity user with profile |
| `19` | Native identity user |
| `21` | Native identity Teams meeting participant |
| `23` | Passthrough authenticated Teams meeting participant |
| `25` | Native identity content sharing user |
| `27` | Fully synced MTO member |
| `29` | Weak MTO user |
| `31` | DAP user |
| `33` | Federated managed identity |

## xms\_tnt\_fct, xms\_sub\_fct, and xms\_act\_fct claims

The `xms_tnt_fct` claim describes the tenant (identified by the `tid` claim). The `xms_sub_fct` and `xms_act_fct` claims are used to describe facts about the subject (`sub`) and the actor (`azp` or `appid`) of the token, respectively. These claims provide more context about the agent's identity and the actions it's performing.

Here are the relevant values for these claims. These claims are multivalued, meaning they can have multiple values, separated by spaces. The valid values are always odd numbers starting from 1.

| Claim Value | Description |
| --- | --- |
| `11` | AgentIdentity |
| `13` | AgentIDUser |

You should ignore any values that aren't relevant to your scenario or validation logic. Ignore the values that aren't relevant to your application. Don't assume any order of the values in these claims.

## xms\_par\_app\_azp

The `xms_par_app_azp` claim is used to identify the parent application of the authorized party (`azp` or `appid`). It's a GUID, when included. You can use the claim to determine the parent

Log the parent application ID for auditing purposes. Microsoft Entra ID sign-in logs always includes the parent ID if available, so resource server should do the same. It isn't recommended to use the parent application ID for authorization decisions, as it would result in widespread access by many agents.

## Scenario-wise examples

The following section outlines some auth scenarios and the relevant claims for each one of them.

### Agent identity acting on behalf of a human user

In this scenario, the agent identity is acting on behalf of a human user. The access token includes the following claims:

| Claim Name | Description |
| --- | --- |
| `tid ` | Tenant ID of the customer tenant |
| `idtyp ` | `user` (indicating the subject is a user) |
| `xms_idrel` | `1` (indicating a member user; others possible too) |
| `azp` / `appid` | Application ID of the agent identity |
| `scp` | Delegated permissions granted to the agent identity |
| `oid` | Object ID of the user |
| `aud` | Resource audience for the token |
| `xms_act_fct` | `11` (AgentIdentity) |

### Agent identity acting autonomously

In this scenario, the agent identity acts using its own identity. The access token includes the following claims:

| Claim Name | Description |
| --- | --- |
| `tid` | Tenant ID of the customer tenant |
| `idtyp` | `app` (indicating the subject is an application) |
| `xms_idrel` | `7` (indicating a service principal) |
| `azp` / `appid` | Application ID of the agent identity |
| `roles` | Permissions granted to the agent identity |
| `oid` | Object ID of the agent identity |
| `xms_act_fct` | `11` (AgentIdentity) |
| `xms_sub_fct` | `11` (AgentIdentity) |
| `aud` | Resource audience for the token |
| `scp` | Empty or `/` (unscoped). |

### Agent identity acts autonomously via agent's user account

In this scenario, the agent obtains a token using the agent's user account associated with its agent identity. The access token includes the following claims:

| Claim Name | Description |
| --- | --- |
| `tid` | Tenant ID of the customer tenant |
| `idtyp` | `user` (indicating the subject is a user) |
| `xms_idrel` | `1` (indicating a member user; others possible too) |
| `azp` / `appid` | Application ID of the agent identity |
| `scp` | Delegated permissions granted to the agent identity |
| `oid` | Object ID of the agent's user account |
| `xms_act_fct` | `11` (Agent identity) |
| `xms_sub_fct` | `13` (Agent's user account) |
| `aud` | Resource audience for the token |
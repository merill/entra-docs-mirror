---
layout: Conceptual
title: Microsoft agent identity platform error codes | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/error-codes
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn about the Agent ID, Agent Blueprint, and Agent Identity error codes.
ms.date: 2025-12-02T00:00:00.0000000Z
ms.reviewer: ryankabir
ms.topic: error-reference
locale: en-us
document_id: faf6e85a-197b-38c9-619c-be49d94e35b1
document_version_independent_id: faf6e85a-197b-38c9-619c-be49d94e35b1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/error-codes.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/error-codes
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/error-codes.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/96407ebd-b9e6-40db-9488-063e1af76a01
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8af61fb5-33c5-4523-b00a-7a42d7bbe9cd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 354cd03e-87e8-ea32-3c48-366df092a8c3
---

# Microsoft agent identity platform error codes | Microsoft Learn

This article provides a comprehensive reference for error codes you might encounter when working with the Microsoft agent identity platform.

## Handling error codes in your application

The [OAuth2.0 spec](https://tools.ietf.org/html/rfc6749#section-5.2) provides guidance on how to handle errors during authentication using the `error` portion of the error response. For more information on handling error code and the possible `error` field values, see the [Microsoft identity platform and OAuth 2.0 error codes documentation](/en-us/entra/identity-platform/reference-error-codes#handling-error-codes-in-your-application).

## Quota and limit errors

These errors occur when you exceed the tenant quota or the maximum number of agent identity blueprints or agent identities.

| Error code | Description |
| --- | --- |
| `Agent_Directory_QuotaExceeded` | Agent identity blueprints and/or agent identities have exceeded 95% of the tenant resource quota. To create more, you must permanently delete unneeded blueprints or identities. |
| `AgentBlueprint_LimitExceeded` | You've reached the maximum number of agent identity blueprints allowed including active and soft-deleted items. To create more, you must permanently delete unneeded blueprints. |
| `AgentIdentity_LimitExceeded` | You've reached the maximum number of agent identities allowed including active and soft-deleted entries. To add more, you must permanently delete unneeded agent identities. |

## Agent identity blueprint errors

These errors occur when a request includes properties or API versions that agent identity blueprints don't support.

| Error code | Description |
| --- | --- |
| `AgentBlueprint_IncompatibleProperty` | A property specified in the request is incompatible with agent identity blueprints and can't be set. |
| `AgentBlueprint_IncompatibleProperty_NullPropertyName` | A property in the request is incompatible with agent identity blueprints and can't be set. |
| `AgentBlueprint_NotSupportedOnApiVersion` | Agent identity blueprints aren't supported on the API version used in this request. |

## Agent identity blueprint principal errors

These errors occur when a request includes properties, API versions, or parent resources that agent identity blueprint principals don't support.

| Error code | Description |
| --- | --- |
| `AgentBlueprintPrincipal_AgentIdentity_IncompatibleProperty` | A property specified in the request is incompatible with agent identity and can't be set. |
| `AgentBlueprintPrincipal_IncompatibleProperty` | A property specified in the request is incompatible with agent identity blueprint principals and can't be set. |
| `AgentBlueprintPrincipal_NotSupportedOnApiVersion` | Agent identity blueprint principals aren't supported on the API version used in this request. |
| `AgentBlueprintPrincipal_RequireAgentBlueprint` | Agent identity blueprint principals can only be created for Agent Blueprints. |

## Agent identity errors

These errors occur when a request references a missing blueprint principal, an incompatible parent type, or unsupported credentials or API versions for agent identities.

| Error code | Description |
| --- | --- |
| `AgentIdentity_AgentBlueprintPrincipalDoesNotExist` | The required agent identity blueprint principal doesn't exist for the specified agent identity blueprint ID. |
| `AgentIdentity_CredentialsNotSupported` | Credentials are not supported for agent identities. All credentials must be added to the agent identity blueprint. |
| `AgentIdentity_IncompatibleParentType` | The specified Application (AppId) isn't an Agent Blueprint. The *AgentIdentityBlueprintId* must be set to the *AppId* of a valid agent identity blueprint. |
| `AgentIdentity_NotSupportedOnApiVersion` | Agent identities aren't supported on the API version used in this request. |

## Agent identity creation errors

These errors occur when the calling principal isn't allowed to create the requested agent identity.

| Error code | Description |
| --- | --- |
| `Error_AgentBlueprintCannotCreateAssociatedIdentity` | Agent identity blueprints can't create agent identities that are associated with another agent identity blueprint. To create this agent identity, either use the agent identity blueprint that's associated with the agent identity, or perform the operation with a different principal that has the required roles/permissions to create agent identities. |
| `Error_AgentIdentitiesCreatingAgentIdentitiesNotAllowed` | Agent identities can't create other agent identities. To create an agent identity, use the associated agent identity blueprint principal or nonagent blueprint service principal with the required permissions. |
| `Error_AgentIdentitySelfCreateRequired` | Applications can only create agent identities under themselves. The provided *AgentIdentityBlueprintId* doesn't match the calling application's *AppId*. |

## Get help

If you have a question or can't find what you're looking for, see [Support and help options for developers](/en-us/entra/identity-platform/developer-support-help-options) to learn about other ways you can get help.
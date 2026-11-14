---
layout: Conceptual
title: Supported Microsoft Entra resource policy resources and actions (preview) - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/resource-policy-supported-resources
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Review the resource types, actions, and operation categories that Microsoft Entra resource policies can target.
ms.topic: reference
ms.date: 2026-11-11T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: 4c3dde27-129a-1cbb-8606-191af374dc7f
document_version_independent_id: 4c3dde27-129a-1cbb-8606-191af374dc7f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/resource-policy-supported-resources.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/resource-policy-supported-resources
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/resource-policy-supported-resources.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 772cf813-566d-3dda-ec3d-40a84198dad9
---

# Supported Microsoft Entra resource policy resources and actions (preview) - Microsoft Entra ID Governance | Microsoft Learn

A custom policy's `__metadata__.selector` identifies its target resource type or action and operations. Use supported targets rather than assuming that every Microsoft Graph endpoint participates in resource policy evaluation.

This reference lists policy targets, not the available built-in policies. Use the linked Microsoft Graph references to review resource properties, methods, request formats, and API versions.

## Resource types

Policies can target the following resource types. Resource selectors include supported derived types by default. Set `includeDerivedTypes` to `false` to target only the named type.

| Resource type | Resource |
| --- | --- |
| [`microsoft.graph.user`](/en-us/graph/api/resources/user?view=graph-rest-beta&amp;preserve-view=true) | Users. |
| [`microsoft.graph.group`](/en-us/graph/api/resources/group?view=graph-rest-beta&amp;preserve-view=true) | Groups. |
| [`microsoft.graph.application`](/en-us/graph/api/resources/application?view=graph-rest-beta&amp;preserve-view=true) | Application registrations. |
| [`microsoft.graph.federatedIdentityCredential`](/en-us/graph/api/resources/federatedidentitycredential?view=graph-rest-beta&amp;preserve-view=true) | Federated identity credentials. |
| [`microsoft.graph.servicePrincipal`](/en-us/graph/api/resources/serviceprincipal?view=graph-rest-beta&amp;preserve-view=true) | Service principals. |
| [`microsoft.graph.appRoleAssignment`](/en-us/graph/api/resources/approleassignment?view=graph-rest-beta&amp;preserve-view=true) | App role assignments. |
| [`microsoft.graph.oAuth2PermissionGrant`](/en-us/graph/api/resources/oauth2permissiongrant?view=graph-rest-beta&amp;preserve-view=true) | Delegated permission grants. |
| [`microsoft.graph.administrativeUnit`](/en-us/graph/api/resources/administrativeunit?view=graph-rest-beta&amp;preserve-view=true) | Administrative units. |
| [`microsoft.graph.scopedRoleMembership`](/en-us/graph/api/resources/scopedrolemembership?view=graph-rest-beta&amp;preserve-view=true) | Scoped role memberships. |
| [`microsoft.graph.device`](/en-us/graph/api/resources/device?view=graph-rest-beta&amp;preserve-view=true) | Devices. |
| [`microsoft.graph.directoryRole`](/en-us/graph/api/resources/directoryrole?view=graph-rest-beta&amp;preserve-view=true) | Directory roles. |
| [`microsoft.graph.unifiedRoleDefinition`](/en-us/graph/api/resources/unifiedroledefinition?view=graph-rest-beta&amp;preserve-view=true) | Unified role definitions. |
| [`microsoft.graph.unifiedRoleAssignment`](/en-us/graph/api/resources/unifiedroleassignment?view=graph-rest-beta&amp;preserve-view=true) | Unified role assignments. |
| [`microsoft.graph.invitation`](/en-us/graph/api/resources/invitation?view=graph-rest-beta&amp;preserve-view=true) | Invitations. |
| [`microsoft.graph.authorizationPolicy`](/en-us/graph/api/resources/authorizationpolicy?view=graph-rest-beta&amp;preserve-view=true) | Authorization policies. |
| [`microsoft.graph.crossTenantAccessPolicy`](/en-us/graph/api/resources/crosstenantaccesspolicy?view=graph-rest-beta&amp;preserve-view=true) | Cross-tenant access policies. |
| [`microsoft.graph.crossTenantAccessPolicyConfigurationDefault`](/en-us/graph/api/resources/crosstenantaccesspolicyconfigurationdefault?view=graph-rest-beta&amp;preserve-view=true) | Cross-tenant access default configurations. |
| [`microsoft.graph.crossTenantAccessPolicyConfigurationPartner`](/en-us/graph/api/resources/crosstenantaccesspolicyconfigurationpartner?view=graph-rest-beta&amp;preserve-view=true) | Cross-tenant access partner configurations. |
| [`microsoft.graph.crossTenantIdentitySyncPolicyPartner`](/en-us/graph/api/resources/crosstenantidentitysyncpolicypartner?view=graph-rest-beta&amp;preserve-view=true) | Cross-tenant identity synchronization partner policies. |
| [`microsoft.graph.conditionalAccessPolicy`](/en-us/graph/api/resources/conditionalaccesspolicy?view=graph-rest-beta&amp;preserve-view=true) | Conditional Access policies. |
| [`microsoft.graph.countryNamedLocation`](/en-us/graph/api/resources/countrynamedlocation?view=graph-rest-beta&amp;preserve-view=true) | Country/region named locations. |
| [`microsoft.graph.ipNamedLocation`](/en-us/graph/api/resources/ipnamedlocation?view=graph-rest-beta&amp;preserve-view=true) | IP named locations. |
| [`microsoft.graph.privilegedAccessGroupAssignmentScheduleRequest`](/en-us/graph/api/resources/privilegedaccessgroupassignmentschedulerequest?view=graph-rest-beta&amp;preserve-view=true) | Privileged access group assignment schedule requests. |
| [`microsoft.graph.privilegedAccessGroupEligibilityScheduleRequest`](/en-us/graph/api/resources/privilegedaccessgroupeligibilityschedulerequest?view=graph-rest-beta&amp;preserve-view=true) | Privileged access group eligibility schedule requests. |
| [`microsoft.graph.agentUser`](/en-us/graph/api/resources/agentuser?view=graph-rest-beta&amp;preserve-view=true) | Agent users. |
| [`microsoft.graph.agentIdentity`](/en-us/graph/api/resources/agentidentity?view=graph-rest-beta&amp;preserve-view=true) | Agent identities. |
| [`microsoft.graph.agentIdentityBlueprint`](/en-us/graph/api/resources/agentidentityblueprint?view=graph-rest-beta&amp;preserve-view=true) | Agent identity blueprints. |
| [`microsoft.graph.agentIdentityBlueprintPrincipal`](/en-us/graph/api/resources/agentidentityblueprintprincipal?view=graph-rest-beta&amp;preserve-view=true) | Agent identity blueprint principals. |

## Actions

Specify an action target as the binding type followed by its fully qualified action name.

| Target | Binding types |
| --- | --- |
| [`microsoft.graph.addPassword`](/en-us/graph/api/application-addpassword?view=graph-rest-beta&amp;preserve-view=true) | [`microsoft.graph.application`](/en-us/graph/api/resources/application?view=graph-rest-beta&amp;preserve-view=true). |
| [`microsoft.graph.addPassword`](/en-us/graph/api/serviceprincipal-addpassword?view=graph-rest-beta&amp;preserve-view=true) | [`microsoft.graph.servicePrincipal`](/en-us/graph/api/resources/serviceprincipal?view=graph-rest-beta&amp;preserve-view=true). |
| [`microsoft.graph.removePassword`](/en-us/graph/api/application-removepassword?view=graph-rest-beta&amp;preserve-view=true) | [`microsoft.graph.application`](/en-us/graph/api/resources/application?view=graph-rest-beta&amp;preserve-view=true). |
| [`microsoft.graph.removePassword`](/en-us/graph/api/serviceprincipal-removepassword?view=graph-rest-beta&amp;preserve-view=true) | [`microsoft.graph.servicePrincipal`](/en-us/graph/api/resources/serviceprincipal?view=graph-rest-beta&amp;preserve-view=true). |
| [`microsoft.graph.addKey`](/en-us/graph/api/application-addkey?view=graph-rest-beta&amp;preserve-view=true) | [`microsoft.graph.application`](/en-us/graph/api/resources/application?view=graph-rest-beta&amp;preserve-view=true). |
| [`microsoft.graph.addKey`](/en-us/graph/api/serviceprincipal-addkey?view=graph-rest-beta&amp;preserve-view=true) | [`microsoft.graph.servicePrincipal`](/en-us/graph/api/resources/serviceprincipal?view=graph-rest-beta&amp;preserve-view=true). |
| [`microsoft.graph.removeKey`](/en-us/graph/api/application-removekey?view=graph-rest-beta&amp;preserve-view=true) | [`microsoft.graph.application`](/en-us/graph/api/resources/application?view=graph-rest-beta&amp;preserve-view=true). |
| [`microsoft.graph.removeKey`](/en-us/graph/api/serviceprincipal-removekey?view=graph-rest-beta&amp;preserve-view=true) | [`microsoft.graph.servicePrincipal`](/en-us/graph/api/resources/serviceprincipal?view=graph-rest-beta&amp;preserve-view=true). |
| [`microsoft.graph.addTokenSigningCertificate`](/en-us/graph/api/serviceprincipal-addtokensigningcertificate?view=graph-rest-beta&amp;preserve-view=true) | [`microsoft.graph.servicePrincipal`](/en-us/graph/api/resources/serviceprincipal?view=graph-rest-beta&amp;preserve-view=true). |
| [`microsoft.graph.assignLicense`](/en-us/graph/api/user-assignlicense?view=graph-rest-beta&amp;preserve-view=true) | [`microsoft.graph.user`](/en-us/graph/api/resources/user?view=graph-rest-beta&amp;preserve-view=true). |
| [`microsoft.graph.assignLicense`](/en-us/graph/api/group-assignlicense?view=graph-rest-beta&amp;preserve-view=true) | [`microsoft.graph.group`](/en-us/graph/api/resources/group?view=graph-rest-beta&amp;preserve-view=true). |
| [`microsoft.graph.instantiate`](/en-us/graph/api/applicationtemplate-instantiate?view=graph-rest-beta&amp;preserve-view=true) | [`microsoft.graph.applicationTemplate`](/en-us/graph/api/resources/applicationtemplate?view=graph-rest-beta&amp;preserve-view=true). |

For example, the application key action uses the target [`microsoft.graph.application/microsoft.graph.addKey`](/en-us/graph/api/application-addkey?view=graph-rest-beta&amp;preserve-view=true).

Action selectors use the operation `invokeAction` and omit `includeDerivedTypes`.

## Operations

The policy contract uses `create`, `updateOrUpsert`, `delete`, and `invokeAction`. Listing a resource type doesn't establish that every operation or endpoint shape for that type is supported.

Use explicit operation metadata and test the intended request shape, including alternate keys, reference requests, or partial updates where relevant.
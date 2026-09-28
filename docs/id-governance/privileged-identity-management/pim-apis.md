---
layout: Conceptual
title: API concepts in Privileged Identity Management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-apis
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Information for understanding the APIs in Microsoft Entra Privileged Identity Management (PIM).
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: shaunliu
ms.custom: pim
locale: en-us
document_id: c8c28716-3b7f-2064-4c79-72d46f09f886
document_version_independent_id: fd636801-4b0a-b825-78f6-55373797b3dd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-apis.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-apis
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-apis.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: c8e53bc8-9b71-2c1c-e314-9a800910a4ec
---

# API concepts in Privileged Identity Management - Microsoft Entra ID Governance | Microsoft Learn

## Overview

Privileged Identity Management (PIM), part of Microsoft Entra, includes three providers:

- PIM for Microsoft Entra roles.
- PIM for Azure resources.
- PIM for Groups.

You can manage assignments in PIM for Microsoft Entra roles and PIM for Groups using Microsoft Graph. You can manage assignments in PIM for Azure Resources using Azure Resource Manager APIs. This article describes important concepts for using the APIs for Privileged Identity Management.

Find more details about APIs that allow you to manage assignments in the documentation:

- [PIM for Microsoft Entra roles API reference](/en-us/graph/api/resources/privilegedidentitymanagementv3-overview)
- [PIM for Azure resource roles API reference](/en-us/rest/api/authorization/privileged-role-eligibility-rest-sample)
- [PIM for Groups API reference](/en-us/graph/api/resources/privilegedidentitymanagement-for-groups-api-overview)
- [PIM Alerts for Microsoft Entra roles API reference](/en-us/graph/api/resources/privilegedidentitymanagementv3-overview?view=graph-rest-beta&amp;preserve-view=true#building-blocks-of-the-pim-alerts-apis)
- [PIM Alerts for Azure Resources API reference](/en-us/rest/api/authorization/role-management-alert-rest-sample)

## PIM API history

There have been several iterations of the PIM APIs over the past few years. There are some overlaps in functionality, but they don't represent a linear progression of versions.

### Iteration 1 – Retired

Under the `/beta/privilegedRoles` endpoint, Microsoft had a classic version of the PIM API, which only supported Microsoft Entra roles. This API was retired in June 2021.

### Iteration 2 – Deprecated

Under the `/beta/privilegedAccess` endpoint, Microsoft supported both `/aadRoles` and `/azureResources` segments for managing Microsoft Entra roles and Azure resource roles, respectively. This endpoint is deprecated and will stop returning data on October 28, 2026. Microsoft recommends against starting any new development with these APIs.

Additionally, we are currently in the process of migrating the UI to Iteration 3 APIs.

### Iteration 3 (Current) – PIM for Microsoft Entra roles, groups in Microsoft Graph API, and for Azure resources in Azure Resource Manager API

This is the final iteration of the PIM API. It includes:

- PIM for Microsoft Entra roles in Microsoft Graph API - Generally available.
- PIM for Azure resources in Azure Resource Manager API - Generally available.
- PIM for groups in Microsoft Graph API - Generally available.
- PIM alerts for Microsoft Entra roles in Microsoft Graph API - Preview.
- PIM alerts for Azure Resources in ARM API - Preview.

Note

The roleAssignmentApprovals APIs are only available in /beta.

Having PIM for Microsoft Entra roles in Microsoft Graph API and PIM for Azure Resources in ARM API provides a few benefits including:

- Alignment of the PIM APIs for regular role assignment for both Microsoft Entra roles and Azure Resource roles.
- Reducing the need to call other PIM APIs to onboard a resource, get a resource, or get a role definition.
- Supporting app-only permissions.
- New features such as approval and email notification configuration.

### Overview of PIM API iteration 3

PIM APIs across providers (both Microsoft Graph APIs and Azure Resource Manager APIs) follow the same principles.

#### Assignments management

To create assignment (active or eligible), renew, extend, or update assignment (active or eligible), activate eligible assignment, deactivate eligible assignment, use resources **\*AssignmentScheduleRequest** and **\*EligibilityScheduleRequest**:

- For Microsoft Entra roles: [unifiedRoleAssignmentScheduleRequest](/en-us/graph/api/resources/unifiedroleassignmentschedulerequest), [unifiedRoleEligibilityScheduleRequest](/en-us/graph/api/resources/unifiedroleeligibilityschedulerequest);
- For Azure resources: [Role Assignment Schedule Request](/en-us/rest/api/authorization/role-assignment-schedule-requests), [Role Eligibility Schedule Request](/en-us/rest/api/authorization/role-eligibility-schedule-requests);
- For Groups: [privilegedAccessGroupAssignmentScheduleRequest](/en-us/graph/api/resources/privilegedaccessgroupassignmentschedulerequest), [privilegedAccessGroupEligibilityScheduleRequest](/en-us/graph/api/resources/privilegedaccessgroupeligibilityschedulerequest).

Creation of **\*AssignmentScheduleRequest** or **\*EligibilityScheduleRequest** objects may lead to creation of read-only **\*AssignmentSchedule**, **\*EligibilitySchedule**, **\*AssignmentScheduleInstance**, and **\*EligibilityScheduleInstance** objects.

- **\*AssignmentSchedule** and **\*EligibilitySchedule** objects show current assignments and requests for assignments to be created in the future.
- **\*AssignmentScheduleInstance** and **\*EligibilityScheduleInstance** objects show current assignments only.

When an eligible assignment is activated (**Create** **\*AssignmentScheduleRequest** was called), the **\*EligibilityScheduleInstance** continues to exist, new **\*AssignmentSchedule** and a **\*AssignmentScheduleInstance** objects are created for that activated duration.

For more information about assignment and activation APIs, see [PIM API for managing role assignments and eligibilities](/en-us/graph/api/resources/privilegedidentitymanagementv3-overview#pim-api-for-managing-role-assignment).

#### PIM policies (role settings)

To manage the PIM policies, use **\*roleManagementPolicy** and **\*roleManagementPolicyAssignment** entities:

- For PIM for Microsoft Entra roles, PIM for Groups: [unifiedroleManagementPolicy](/en-us/graph/api/resources/unifiedrolemanagementpolicy), [unifiedroleManagementPolicyAssignment](/en-us/graph/api/resources/unifiedrolemanagementpolicyassignment)
- For PIM for Azure resources: [Role Management Policies](/en-us/rest/api/authorization/role-management-policies), [Role Management Policy Assignments](/en-us/rest/api/authorization/role-management-policy-assignments)

The **\*roleManagementPolicy** resource includes rules that constitute PIM policy: approval requirements, maximum activation duration, notification settings.

The **\*roleManagementPolicyAssignment** object attaches the policy to a specific role.

For more information about the policy settings APIs, see [role settings and PIM](/en-us/graph/api/resources/privilegedidentitymanagementv3-overview#role-settings-and-pim).

## Permissions

### PIM for Microsoft Entra roles

For Microsoft Graph permissions required for PIM for Microsoft Entra roles, see the corresponding REST API reference pages.

### PIM for Azure resources

The PIM APIs for Azure resource roles is developed on top of the Azure Resource Manager framework. You need to consent to Azure Resource Management but don’t need any Microsoft Graph permissions. You also need to make sure the user or the service principal calling the API has at least the Owner or User Access Administrator role on the resource you're trying to administer.

### PIM for Groups

For Microsoft Graph permissions required for PIM for Groups, see the corresponding REST API reference pages.

## Relationship between PIM entities and role assignment entities

The only link between the PIM entity and the role assignment entity for persistent (active) assignment for either Microsoft Entra roles or Azure roles is the `*AssignmentScheduleInstance`. There's a one-to-one mapping between the two entities. That mapping means `roleAssignment` and `*AssignmentScheduleInstance` would both include:

- Persistent (active) assignments made outside of PIM.
- Persistent (active) assignments with a schedule made inside PIM.
- Activated eligible assignments.

PIM-specific properties (such as end time) will be available only through **\*AssignmentScheduleInstance** object.
---
layout: Conceptual
title: Update and retire Microsoft Entra resource policies (preview) - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/resource-policy-lifecycle
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Publish a new policy version, try it alongside an enforced version, switch enforcement, roll back, and delete or restore resource policies.
ms.topic: how-to
ms.date: 2026-11-11T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: dafb28b9-6b33-1e6e-d4c8-f88ab81332b4
document_version_independent_id: dafb28b9-6b33-1e6e-d4c8-f88ab81332b4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/resource-policy-lifecycle.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/resource-policy-lifecycle
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/resource-policy-lifecycle.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d0a46c79-d69b-1c66-c2c7-af84b518594b
---

# Update and retire Microsoft Entra resource policies (preview) - Microsoft Entra ID Governance | Microsoft Learn

Use this article to update an assigned policy, roll back, or delete and restore policies. Assess a new version through a separate report-only assignment while the existing version stays enforced.

For your first policy assignment, testing, and enforcement readiness, see [Safely deploy resource policy assignments](resource-policy-safe-deployment). For parameter-value changes, see [Edit an assignment](resource-policy-manage-portal#edit-an-existing-assignment) and [Parameter update behavior](resource-policy-parameters#assignment-update-behavior).

Use [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) to call the linked Microsoft Graph APIs for these procedures. For portal assignment controls, see [Manage policies in the Microsoft Entra admin center](resource-policy-manage-portal).

## Prerequisites

- A work or school account in the target tenant with active [Resource Policy Administrator](resource-policy-concepts#roles-and-api-permissions) and [Reports Reader](../../identity/role-based-access-control/permissions-reference#reports-reader) roles. Use Resource Policy Administrator for policy management and evaluation, and Reports Reader for evaluation audit events.
- [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer), signed in to that tenant with the same account, with admin consent for the delegated permissions listed below. Request only the permissions for the procedures you follow.
- A Microsoft Entra ID Governance service plan for publishing or updating policies, creating or updating assignments, and restoring deleted items. See [licensing requirements and exceptions](licensing#resource-policy-preview).
- A policy or assignment to update, retire, or restore. For the parallel rollout below, the existing assignment must be enabled and enforced.
- A saved copy of the current policy and assignment settings, including parameter values.
- For policies that use `fetchAsPolicy()`, a [configured privileged-read application](resource-policy-privileged-read-app) with application permissions for the Microsoft Graph reads used by the policy.

Activate any eligible roles through Privileged Identity Management (PIM) before signing in to Graph Explorer.

| Delegated permission for Graph Explorer | When needed |
| --- | --- |
| `ResourcePolicyDefinition.ReadWrite.All` | Publish, delete, or restore custom definitions, or manage their versions. Not needed for assignment-only changes to built-in policies. |
| `ResourcePolicyAssignment.ReadWrite.All` | Read, create, update, delete, or restore assignments. |
| `ResourcePolicyEvaluation.Read.All` | Test policy changes. |
| `AuditLog.Read.All` | Review evaluation audit events. |

## Publish a new custom policy version

For a built-in policy, select an available newer version and go directly to Roll out the new version. Don't edit built-in definitions.

1. Update your Rego policy and increase its version number. Update any parameter reference or import to match the new package version. For example, change `1.0.0` to `1.1.0` in the package declaration:

    ```rego
    package graph.application_name_prefix["1.1.0"]
    ```
2. [Test the revised policy](resource-policy-test-troubleshoot) with the intended parameter values and requests that should pass and fail. Check that unchanged requirements still behave as expected.
3. [Update the custom definition](/en-us/graph/api/resourcepolicydefinition-update?view=graph-rest-beta&amp;preserve-view=true) with the revised Rego, following the API reference's update requirements.
4. Confirm that both versions are available. Keep your existing assignment unchanged.

A parameter schema change requires a higher major version, such as `2.0.0`, and compatible parameter values. Keep the target resource type unchanged. See [Author policies with Rego](resource-policy-rego).

## Roll out the new version

Use two assignments: one enforces the old version, and the other evaluates the new version in report-only mode.

Each version can have only one live assignment in a tenant, including a disabled assignment. Choose a new version that isn't already assigned; don't repoint the existing assignment to it.

1. [Create a new assignment](/en-us/graph/api/resourcepolicyassignment-create?view=graph-rest-beta&amp;preserve-view=true) with a different name, the new policy version, and its intended parameter values. Set it to enabled (`isEnabled: true`) and report-only (`enforcementMode: doNotEnforce`). Leave the existing enforced assignment on.
2. Wait for [assignment changes to take effect](resource-policy-evaluation#assignment-propagation).
3. Confirm that evaluation audit events include both assignment names and their expected policy versions.
4. [Review the new assignment's impact](resource-policy-logs#assess-assignment-impact-from-evaluation-events), agree on remediation or supported temporary exceptions, and complete the [checks before enforcement](resource-policy-safe-deployment#6-enable-enforcement).
5. [Update the new assignment](/en-us/graph/api/resourcepolicyassignment-update?view=graph-rest-beta&amp;preserve-view=true) to **Enforce** (`enforcementMode: enforce`). Keep the old assignment enforced while the change takes effect.
6. Verify the new assignment's enforced results in evaluation audit events, and test compliant and noncompliant requests.
7. Once the new version is enforcing as expected, turn the old assignment **Off** (`isEnabled: false`). Keep that assignment and its policy version available for rollback.

Review each assignment's results separately. The old version can still block requests that the new one would allow. While both versions enforce, either can block.

## Roll back to the previous version

To return to the old version, use the assignment you retained:

1. Check that the old assignment still references the tested version and has its original parameter values.
2. Turn the old assignment **On** with **Enforcement** set to **Enforce**.
3. Wait for [assignment changes to take effect](resource-policy-evaluation#assignment-propagation).
4. Verify the old assignment's enforced results in evaluation audit events and test requests.
5. Turn the new assignment **Off** after the old assignment is enforcing again.

This order keeps enforcement in place. Don't create another assignment for a version that already has one.

Rollback doesn't undo resource changes that were already allowed.

## Retire an old version

Keep the old version and assignment until you no longer need them for recovery.

1. Confirm that the replacement works and the policy owner approves retirement.
2. [Delete the old assignment](/en-us/graph/api/resourcepolicyassignment-delete?view=graph-rest-beta&amp;preserve-view=true). A disabled assignment still prevents you from deleting its policy version.
3. For a custom policy, [delete the unused previous version](/en-us/graph/api/resourcepolicydefinitionversion-delete?view=graph-rest-beta&amp;preserve-view=true). Don't delete Microsoft-managed built-in versions.

Warning

Deleting a previous version is permanent. It can't be restored.

Keep custom policy source in your own repository. See [Version-history limits](resource-policy-service-limits#version-history-and-deleted-items).

## Delete a custom policy

To remove a custom policy you no longer need:

1. Save its Rego and assignment settings if you might need them later.
2. Delete all assignments that reference the definition, including disabled assignments.
3. [Delete the custom definition](/en-us/graph/api/resourcepolicydefinition-delete?view=graph-rest-beta&amp;preserve-view=true).

Deleted definitions and assignments can be restored for 30 days. Permanent deletion or expiration removes this recovery option.

## Restore a deleted policy or assignment

Restore the policy before an assignment that uses it:

1. [Restore the custom definition](/en-us/graph/api/resourcepolicydefinition-restore?view=graph-rest-beta&amp;preserve-view=true) if it was deleted, and confirm that the required version is available.
2. Review the deleted assignment's version, parameters, and enablement and enforcement settings.
3. Confirm that the version has no other live assignment, including a disabled assignment.
4. [Restore the assignment](/en-us/graph/api/resourcepolicyassignment-restore?view=graph-rest-beta&amp;preserve-view=true).
5. Allow the restored settings to take effect, then verify request behavior and evaluation audit events.

Restore the deleted assignment rather than reusing its reserved name.
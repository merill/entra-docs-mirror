---
layout: Conceptual
title: How Microsoft Entra resource policy evaluation works (preview) - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/resource-policy-evaluation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Understand request matching, Rego evaluation, enforcement modes, multiple assignments, and propagation of resource policy changes.
ms.topic: concept-article
ms.date: 2026-11-11T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: c184518f-6e5c-24ae-f668-d09ebc9750ad
document_version_independent_id: c184518f-6e5c-24ae-f668-d09ebc9750ad
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/resource-policy-evaluation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/resource-policy-evaluation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/resource-policy-evaluation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 3b318792-3de5-e3a9-050a-65596e18df18
---

# How Microsoft Entra resource policy evaluation works (preview) - Microsoft Entra ID Governance | Microsoft Learn

Microsoft Entra resource policy evaluates matching Microsoft Graph requests before the requested resource operation proceeds. Evaluation combines assignment settings with the assigned policy's applicability and compliance rules.

## Request-time evaluation

Evaluation has three stages.

1. **Match assignments.** The service finds enabled assignments whose scope, target resource or action, and operations match the incoming request. If none match, resource policy doesn't evaluate Rego for the request.
2. **Check applicability.** If the assigned policy has an `applicable` rule, the service evaluates it. A false result excludes the request from that policy's compliance evaluation.
3. **Evaluate compliance.** The service evaluates each applicable policy's `deny` rule. A true result identifies noncompliance; a false result identifies compliance.

The service combines the results with assignment enforcement modes to determine whether resource policy blocks the request.

## Multiple policies and enforcement modes

An assignment's `enforcementMode` doesn't change the policy's compliance result. It changes how the service applies that result.

| Results | Request-time behavior |
| --- | --- |
| At least one applicable policy returns a noncompliant result through an `enforce` assignment. | Resource policy blocks the request. |
| Noncompliant results occur only through `doNotEnforce` assignments. | Those assignments don't block the request, and evaluation results are recorded. |
| All applicable policies evaluate successfully and are compliant. | Resource policy doesn't block the request. |

An excluded or compliant result from one policy doesn't override a different enforced policy's noncompliant result.

Note

Passing policy evaluation doesn't guarantee that the underlying operation succeeds. Microsoft Graph permissions, resource validation, and other service controls still apply.

## Disabled assignments and exceptions

A disabled assignment doesn't evaluate requests. An enabled assignment in `doNotEnforce` mode evaluates without enforcing its result.

An exception expressed in a policy's applicability logic affects only that policy. It doesn't grant Microsoft Graph permissions or bypass other assignments.

## Simulated evaluation

Use evaluation actions to test policy behavior without performing the simulated resource operation.

| Action | What it evaluates |
| --- | --- |
| `evaluatePolicy` | Rego supplied directly in the evaluation request, with any supplied parameter values. |
| `evaluateAssignedPolicies` | Assigned policies that match the simulated request. |

Inspect policy results and errors even when the evaluation returns HTTP success. Success alone doesn't prove compliance.

Both actions return `appliedPoliciesEffects` and `isBlocked`. A noncompliant result can have `appliedPoliciesEffects: "deny"` and `isBlocked: false` when it isn't enforced. For `evaluatePolicy`, supply `enforcementMode` to test the intended behavior; its default is `doNotEnforce`. For `evaluateAssignedPolicies`, the assignments supply their enforcement modes.

Request detailed results with `isResultDetailed: true` to inspect policy-provided violation reasons separately from evaluation errors.

For testing guidance, see [Test and troubleshoot a resource policy](resource-policy-test-troubleshoot).

## Assignment propagation

Assignment creation, updates, and deletion can take up to 10 minutes to affect incoming requests. The evaluation actions and policy management APIs reflect saved assignment changes without that propagation delay.

Account for propagation when testing enablement, enforcement-mode changes, version changes, or rollback. An immediate management response doesn't prove that every incoming request uses the updated assignment.

## Errors and diagnostics

Distinguish a noncompliant policy result from a loading or evaluation failure. Failures can arise from invalid Rego, unexpected input, unavailable policy versions, or unsuccessful additional reads.

Review per-policy results and available error details. Don't assume that an evaluation error is equivalent to a deny result.

| Condition | Request-time behavior |
| --- | --- |
| An applicable policy's `deny` evaluation fails or returns an undefined result. | An `enforce` assignment blocks the request. A `doNotEnforce` assignment records the error without blocking through that assignment. |
| An optional `applicable` rule fails or returns an invalid result. | That policy doesn't proceed to `deny` evaluation. Other matching policies can still block the request. |
| The request payload exceeds the policy evaluation input-size limit. | Policy evaluation is skipped. A matching enforced deny assignment blocks the request; assignments in `doNotEnforce` don't block through this size check. |
| An unexpected service error prevents policy evaluation from completing. | The request can continue without completed policy evaluation. A successful write isn't proof that all policies evaluated successfully. |

For additional reads, the policy must inspect the `fetchAsPolicy()` response code. A failed read isn't automatically a noncompliant result; the policy's handling of that response determines whether it returns a result or encounters an evaluation error.

Use [evaluation audit logs](resource-policy-logs) to investigate real requests. Inspect the assignment and version in each event: a request's overall decision can differ from an individual assignment's result. These logs don't assess preexisting resource configuration.
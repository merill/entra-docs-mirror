---
layout: Conceptual
title: Test and troubleshoot a Microsoft Entra resource policy (preview) - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/resource-policy-test-troubleshoot
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Validate custom and assigned resource policies, inspect normalized request input, and troubleshoot unexpected evaluation and enforcement results.
ms.topic: how-to
ms.date: 2026-11-11T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: f13fb72b-3f33-9914-3250-603e608b97a4
document_version_independent_id: f13fb72b-3f33-9914-3250-603e608b97a4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/resource-policy-test-troubleshoot.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/resource-policy-test-troubleshoot
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/resource-policy-test-troubleshoot.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: a8135566-49c6-dc63-4c65-1a7cad09ad77
---

# Test and troubleshoot a Microsoft Entra resource policy (preview) - Microsoft Entra ID Governance | Microsoft Learn

Test custom Rego or assigned policies with simulated requests, then investigate unexpected results. Evaluation actions don't perform the requested resource change.

## Choose your task

| Task | Start here |
| --- | --- |
| Test custom policy logic in isolation. | Evaluate custom policy logic. |
| Test or reproduce a decision from assigned policies. | Evaluate assigned policies. |
| Check the configured application's live read access. | [Validate a live privileged read](resource-policy-privileged-read-app#validate-a-live-privileged-read). |
| Investigate unexpected evaluation or enforcement results. | Troubleshoot unexpected results. |

## Prerequisites

- A work or school account in the target tenant with an active [Resource Policy Evaluator](resource-policy-concepts#roles-and-api-permissions) or [Resource Policy Administrator](resource-policy-concepts#roles-and-api-permissions) role. Activate an eligible role through Privileged Identity Management (PIM) before signing in.
- [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer), signed in to that tenant with this account, with admin consent for the delegated `ResourcePolicyEvaluation.Read.All` permission for the HTTP examples.

These requirements cover simulated requests. Additional requirements for real reads and resource operations are listed with those procedures. Evaluation permissions don't grant policy management or target-resource write access.

## Build a test matrix

1. Prepare requests that should pass and fail. Record the URI, method, body, parameters, and expected applicability and compliance.
2. Include relevant missing, null, empty, and boundary values, partial updates, excluded requests, and additional-read success and failure cases.
3. Save the inputs, expected and actual results, and errors. Rerun these cases after changing policy logic or parameters.

## Evaluate custom policy logic

1. Prepare the Rego and test input. Replace the placeholders below, and add JSON `params` if needed. For parameterized Rego, check the [qualified reference or import alias](resource-policy-rego#parameters-and-defaults).
2. In Graph Explorer, select **POST** and **beta**, and submit the following URL and JSON body to `evaluatePolicy`:

    ```http
    POST https://graph.microsoft.com/beta/admin/resourcePolicy/evaluatePolicy
    Content-Type: application/json
    ```

    ```json
    {
      "policy": "<complete Rego policy serialized as a JSON string>",
      "resourceUri": "/v1.0/applications",
      "httpMethod": "post",
      "resourceBody": {
        "displayName": "Contoso-Inventory",
        "signInAudience": "AzureADMyOrg"
      },
      "enforcementMode": "doNotEnforce",
      "isResultDetailed": true,
      "includeNormalizedRequestInput": true
    }
    ```
3. Select **Run query**.
4. In **Response preview**, compare the policy results and errors with your expectations. Use normalized request input to investigate unexpected outcomes.

This action doesn't create a definition or assignment.

## Evaluate assigned policies

1. Prepare the proposed request input without an inline `policy` property.
2. In Graph Explorer, select **POST** and **beta**, and submit it to `evaluateAssignedPolicies`:

    ```http
    POST https://graph.microsoft.com/beta/admin/resourcePolicy/evaluateAssignedPolicies
    Content-Type: application/json
    ```

    ```json
    {
      "resourceUri": "/v1.0/applications",
      "httpMethod": "post",
      "resourceBody": {
        "displayName": "Inventory",
        "signInAudience": "AzureADMyOrg"
      },
      "scope": "/",
      "isResultDetailed": true,
      "includeNormalizedRequestInput": true
    }
    ```
3. Select **Run query**.
4. In **Response preview**, inspect each assignment's results and errors, version, and parameters. Check whether another assignment affects the overall result.

An evaluation action doesn't prove that a recent assignment change has reached request-time evaluation.

## Interpret evaluation results

Use these fields for both evaluation actions:

| Field | Use |
| --- | --- |
| `appliedPoliciesEffects` | Check the combined effect, `deny` or `compliant`, alongside errors. |
| `isBlocked` | Check whether the proposed request would be blocked under the enforcement settings and error behavior. |
| `details` | Review policy outcomes, violation `reasons`, and errors. Request `isResultDetailed: true` to include these details. |

For `evaluatePolicy`, a violation returns `appliedPoliciesEffects: "deny"` in both modes: `isBlocked` is `true` with `enforce` and `false` with `doNotEnforce`. Omitting the mode uses `doNotEnforce`.

Inspect errors and skipped evaluations too. A payload-size error can block without a completed compliance evaluation.

## Test additional reads with simulated responses

1. Add `fetchResponses` to the `evaluatePolicy` request to test read handling without real additional reads. Supply a response for every read path the policy executes, matching `relativePathUri` and its query string exactly:

    ```json
    {
      "fetchResponses": [
        {
          "relativePathUri": "/v1.0/applications/00000000-0000-0000-0000-000000000001?$select=id,displayName",
          "code": 200,
          "data": {
            "id": "00000000-0000-0000-0000-000000000001",
            "displayName": "Contoso-Inventory"
          }
        }
      ]
    }
    ```
2. Run the tests with successful and failed read responses. An unmatched read produces an error, not a real request; an empty array permits no additional reads. Read URI validation still applies.
3. Before deployment, meet the requirements in Validate a live privileged read, then omit `fetchResponses` or set it to `null` to test real reads.

Simulated responses need only evaluation permissions, but don't prove the configured app can read the resource.

### Validate a live privileged read

For real `fetchAsPolicy()` reads during `evaluatePolicy` in Graph Explorer, use an active [Resource Policy Administrator](resource-policy-concepts#roles-and-api-permissions) role and obtain admin consent for the additional delegated `ResourcePolicyDefinition.ReadWrite.All` permission. A [configured privileged-read app](resource-policy-privileged-read-app) supplies the application permissions for the reads your policy makes.

Use the [live-read PowerShell walkthrough](resource-policy-privileged-read-app#validate-a-live-privileged-read) to verify application-read access after configuration or consent changes. Its PowerShell permissions are separate from Graph Explorer's grants.

## Verify real request behavior

For the operation you test, grant Graph Explorer the delegated permissions and use the user authorization specified by its Microsoft Graph API reference. For application creation, use the [tutorial prerequisites](resource-policy-tutorial-portal#prerequisites). If you need to create or change an assignment, also meet the [portal management prerequisites](resource-policy-manage-portal#prerequisites).

To query evaluation audit events, use an active [Reports Reader](../../identity/role-based-access-control/permissions-reference#reports-reader) role and obtain admin consent for Graph Explorer's delegated `AuditLog.Read.All` permission.

After the request-input tests pass:

1. Use an enabled report-only assignment. For a version update, keep existing enforcement and use a [separate assignment for the new version](resource-policy-lifecycle#roll-out-the-new-version).
2. Wait for [assignment propagation](resource-policy-evaluation#assignment-propagation).
3. Perform an approved test operation with a caller that has the target-resource permissions.
4. [Retrieve its evaluation event](resource-policy-logs#retrieve-evaluation-audit-events) by request ID. Check the intended assignment and version, and separate violations from errors.

A real operation can create or modify resources. Use an approved test environment, and follow [safe deployment](resource-policy-safe-deployment) for enforcement and recovery.

## Troubleshoot unexpected results

| Symptom | Checks |
| --- | --- |
| The policy isn't evaluated. | Check assignment enablement, scope, resource type, operation, and policy applicability. |
| A noncompliant request isn't blocked. | Check enforcement mode, propagation, and whether the result came from an evaluation action or an actual resource request. |
| A request is blocked despite a `doNotEnforce` assignment. | Inspect other enforced assignments and other Microsoft Graph controls. |
| A rule reports compliance unexpectedly. | Inspect normalized input, missing properties, parameter values, and the assigned policy version. Check that the [parameter reference or import](resource-policy-rego#parameters-and-defaults) matches the definition name and version. |
| An assignment update is rejected. | Check the current ETag, the referenced version's parameter schema, and whether that version already has a live assignment, including a disabled assignment. Include `params` when changing the assigned version. |
| No privileged-read app is configured. | [Configure the application](resource-policy-privileged-read-app) before testing real `fetchAsPolicy()` reads. |
| The privileged-read configuration update fails validation. | Confirm tenant ownership, single-tenant registration, and exact federated credential values. See [Create the federated identity credential](resource-policy-privileged-read-app#create-the-federated-identity-credential). |
| An additional read fails after successful configuration. | Check whether the app, service principal, consent, or federated credential changed. [Validate a live privileged read](resource-policy-privileged-read-app#validate-a-live-privileged-read), including the evaluation client's permission and role requirements. |
| Only some additional reads fail. | Check the least-privileged permission and consent required for each failing API. |
| An evaluation action succeeds but the resource operation fails. | Check the real caller's permissions, resource validation, propagation, and request differences. |

## Inspect Rego logic locally

You can use an approved local Rego evaluator to investigate individual rules with sanitized normalized input. Validate an optional `applicable` rule separately from `deny`.

Don't upload tenant data, policy source, or authentication context to an external playground without authorization. Local tests don't verify service-specific functions, permissions, or enforcement. Rerun service tests after every policy change.
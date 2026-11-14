---
layout: Conceptual
title: Author Microsoft Entra resource policies with Rego (preview) - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/resource-policy-rego
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn the Rego structure, normalized request input, applicability rules, parameters, and Microsoft Graph read functions used by resource policies.
ms.topic: concept-article
ms.date: 2026-11-11T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: 3932a5c8-2c57-a6c2-dad2-7c2848812c60
document_version_independent_id: 3932a5c8-2c57-a6c2-dad2-7c2848812c60
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/resource-policy-rego.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/resource-policy-rego
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/resource-policy-rego.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 9905f387-4885-3b66-9fde-b4282f1dfcc6
---

# Author Microsoft Entra resource policies with Rego (preview) - Microsoft Entra ID Governance | Microsoft Learn

Use Rego to author a custom Microsoft Entra resource policy when a built-in policy doesn't meet your requirements. Rego evaluates structured data against declarative rules. Resource policy uses those rules to identify noncompliant Microsoft Graph requests.

You don't need to author Rego to [assign a built-in policy](resource-policy-quickstart-portal).

## Required policy structure

A custom policy contains these elements.

| Element | Purpose |
| --- | --- |
| `package graph.<uniqueName>["X.Y.Z"]` | Identifies the policy and its semantic version. The name after `graph.` must match the definition's `uniqueName`. |
| `__metadata__` | Defines descriptive metadata, the required selector, and any parameter schema. |
| `__metadata__.selector` | Identifies the target resource type or action and applicable operations. |
| `deny` | Reports whether the request is noncompliant. |

An optional `applicable` rule can exclude requests that match the selector. Without it, matching requests continue to `deny` evaluation.

Start a new custom definition at version `1.0.0`. Declare later versions in the package name when you update the definition. The version uses three nonnegative integers separated by periods.

Choose a definition `uniqueName` that matches `[A-Za-z][A-Za-z0-9_]{0,127}`: an ASCII letter followed by up to 127 ASCII letters, digits, or underscores. The prefixes `microsoft` and `ms`, including `msft`, and the exact names `utils` and `input` are reserved regardless of case. For example, use `contosoApplicationNaming`.

Use the same name in the Rego package, the JSON `uniqueName` property when supplied, URL keys, and an assignment's `assignedPolicy.policyUniqueName`. URL encoding doesn't make an invalid name valid.

An assignment's own `uniqueName` is a separate identifier. It uses the same character and length rules and reserved prefixes, but the definition-specific reserved names `utils` and `input` don't apply to assignment names.

The optional metadata `category` accepts `notSpecified`, `workloadIdentity`, `identityAndTenant`, `privilegedAccess`, `zeroTrust`, `agenticIdentity`, or `networkAccess`.

Resource policy supports a restricted set of native Rego built-ins. Check [Disabled Rego built-in functions](resource-policy-service-limits#disabled-rego-built-in-functions) before using a function from the broader Rego language.

For general language guidance, see the [Open Policy Agent policy language documentation](https://www.openpolicyagent.org/docs/policy-language).

## Applicability metadata

In `__metadata__.selector`, set `resourceName` to a [supported resource type or action](resource-policy-supported-resources). Set `operations` to a nonempty array of the operations that the policy evaluates. Use the exact casing shown for resource names and operations.

| Operation | Use |
| --- | --- |
| `create` | Evaluate resource creation. |
| `updateOrUpsert` | Evaluate resource updates or upserts. |
| `delete` | Evaluate resource deletion. |
| `invokeAction` | Evaluate an action invocation. |

Specify operations explicitly so readers and reviewers can see the policy's intended coverage.

For resource targets, `includeDerivedTypes` defaults to `true`. Set it to `false` to match only the named resource type. For action targets, specify the binding type and action name in `resourceName`, and omit `includeDerivedTypes`.

## Example custom policy

This custom policy requires new application display names to start with `Contoso-`. It isn't the quickstart's built-in naming policy.

```rego
package graph.application_name_prefix["1.0.0"]

__metadata__ := {
    "title": "Application name prefix",
    "description": "Requires new application display names to start with Contoso-.",
    "category": "workloadIdentity",
    "selector": {
        "resourceName": "microsoft.graph.application",
        "operations": ["create"]
    }
}

default deny := {"result": false, "reasons": []}

deny := {
    "result": true,
    "reasons": ["Use an application display name that starts with Contoso-."]
} if {
    resource := object.get(input, "resource", {})
    name := object.get(resource, "displayName", "")
    not startswith(name, "Contoso-")
}
```

The default result is compliant. The rule returns a noncompliant result and an actionable explanation when the prefix is missing.

This policy targets creation only. An update payload can omit unchanged properties, so don't apply the same check to updates without accounting for partial request bodies and, when necessary, existing resource state.

## Format policy source

Keep each line within 1,024 characters. Longer lines return `line exceeds maximum column width of 1024`, even when the policy is within the [definition-size limit](resource-policy-service-limits#definitions-assignments-and-content).

Split objects, arrays, and rule bodies across lines. For a long description, use a raw multiline string enclosed in backticks, as in this metadata fragment:

```rego
__metadata__ := {
    "description": `Requires application display names to start with Contoso-.
Evaluate this requirement when an application is created.`
}
```

Line breaks and indentation inside the backticks are part of the description and count toward its 1,024-character limit. Reformatting doesn't increase the metadata or total policy-size limits.

## Submit and retrieve policy source

Definition create and update requests accept `Content-Type: text/plain`. Send the complete Rego policy as the request body, including the versioned package declaration and metadata. On creation, the service derives the definition's name from that package.

Alternatively, send JSON with the source in `rule.policy`. In either format, Rego supplies the definition's version, display name, description, category, parameter schema, and selector.

To retrieve custom policy source, use `Accept: text/plain` when reading a current definition, a soft-deleted definition, or an individual previous version. Use the JSON representation when you need the surrounding definition metadata. ETags and update preconditions still apply.

## Deny results and enforcement

The `deny` rule can return a Boolean or an object with a Boolean `result` and a `reasons` array.

- A false result identifies a compliant request.
- A true result identifies a noncompliant request.

The rule doesn't determine whether the request is blocked. The assignment's `enforcementMode` controls that behavior. See [How resource policy evaluation works](resource-policy-evaluation).

Write reasons that explain how to correct the request. Don't include sensitive resource data or credentials in reason text.

## Normalized request input

The service normalizes the request into an `input` object before evaluation.

| Input element | Contents |
| --- | --- |
| `input.request.apiVersion` | The Microsoft Graph version of the evaluated request. |
| `input.request.authContext` | Selected authentication context, including the caller application, tenant, and available subject information. |
| `input.request.authContext.isAgenticSession` | Present with the value `true` for an agentic session. Its absence doesn't represent an explicit `false` value. |
| `input.request.uriSegments` | URI segments with resource types and keys when present. |
| `input.request.resourceKeys` | Keys of the target resource, when the request identifies an existing resource. |
| `input.resource` | The normalized request body, when the request has a body. |

For example, a normalized request body for application creation can include:

```json
{
  "resource": {
    "displayName": "Contoso-Inventory",
    "signInAudience": "AzureADMyOrg"
  }
}
```

This fragment illustrates `input.resource`; it isn't a complete normalized input document.

Properties can be absent. For example, the request might not have a body or a target resource key. Don't treat an absent property as proof of a particular identity type. `input.request.authContext.isAppOnly` is a Boolean.

Use the evaluation action's `includeNormalizedRequestInput` option to inspect the service-generated input. See [Test and troubleshoot a resource policy](resource-policy-test-troubleshoot).

## Parameters and defaults

Define typed parameters in `__metadata__.paramsSchema`. Supply assignment-specific values through the assignment's JSON `params` property.

Read values through `data.graph.<definitionUniqueName>["<version>"].params`, matching the package name and version. An import alias lets you use `params.<name>`:

```rego
package graph.application_name_prefix_parameterized["1.0.0"]

import data.graph.application_name_prefix_parameterized["1.0.0"].params as params
```

For example, use `params.required_prefix` after this import. Update the import when you change the package version, and don't declare your own `params` rule.

Rego `default` declarations must use constant expressions. Don't put references to `input`, other rules, or function calls in a default declaration.

For schema and assignment-value examples, see [Resource policy parameters](resource-policy-parameters).

## Read additional Microsoft Graph data

Some requirements need information that isn't in the request body. Use `fetchAsPolicy()` for additional read-only Microsoft Graph requests. It uses a configured, customer-owned privileged-read application independently of the request caller's permissions.

Configure the [privileged-read application](resource-policy-privileged-read-app) before creating or updating a definition that uses this function.

The function takes a request object containing `relativePathUri`, including the Microsoft Graph API version. The result contains an HTTP response `code` and response `data`.

The following fragment checks that an existing application's display name starts with `Contoso-` after an update. Use it as the `deny` logic for an application policy whose selector sets `operations` to `["updateOrUpsert"]`. It uses the proposed name when the update supplies `displayName`, or the existing name from the read response when the update omits it:

```rego
default deny := true

deny := false if {
    response := fetchAsPolicy({
        "relativePathUri": sprintf(
            "/%s/applications/%s?$select=displayName",
            [input.request.apiVersion, input.request.resourceKeys.id]
        )
    })
    response.code == 200
    name_after_update := object.get(
        object.get(input, "resource", {}),
        "displayName",
        response.data.displayName
    )
    is_string(name_after_update)
    startswith(name_after_update, "Contoso-")
}
```

Use this pattern only when normalized input contains the required resource key. The example reports noncompliance if the read fails, required data is missing, or the name check fails. The assignment's enforcement mode determines whether that result blocks the request.

Additional reads increase latency and consume Microsoft Graph request capacity. Request only the properties you need, prefer a specific resource to a collection, and don't rely on paging. Keep calls within the [additional-read limits](resource-policy-service-limits#additional-read-limits).

## Test before assignment

Build tests for compliant, noncompliant, missing-property, and excluded requests. Validate applicability separately from the `deny` result.

Use service evaluation before deployment. A locally valid policy isn't evidence that the service accepts it or that its assignments behave as intended.
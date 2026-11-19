---
layout: Conceptual
title: What is Microsoft Entra resource policy (preview)? - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/resource-policy-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how Microsoft Entra resource policy evaluates Microsoft Graph requests to help prevent noncompliant resource configuration changes.
ms.topic: overview
ms.date: 2026-11-11T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: a9295e9a-fb61-143b-bfd9-a981270fbca2
document_version_independent_id: a9295e9a-fb61-143b-bfd9-a981270fbca2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/resource-policy-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/resource-policy-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/resource-policy-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: cfca5f79-6bd8-23d3-d412-951a4f2ce194
---

# What is Microsoft Entra resource policy (preview)? - Microsoft Entra ID Governance | Microsoft Learn

Microsoft Entra resource policy helps you prevent configuration changes that don't meet your organization's requirements. You assign policies in your tenant, and the service evaluates matching Microsoft Graph requests before the requested changes occur.

Resource policy is a feature of Microsoft Entra Tenant Governance. You can adopt it in an individual tenant without enabling related tenant discovery or establishing a governance relationship.

## Prevent noncompliant changes

Use resource policy to express configuration requirements for [supported resource types and actions](resource-policy-supported-resources). For example, a policy can evaluate a resource name or restrict a configuration value.

A policy assignment controls how the service handles a noncompliant request:

- In `doNotEnforce` mode, the policy evaluates the request and records the result without blocking it.
- In `enforce` mode, a noncompliant result can block the request and return a policy-specific explanation.

Another assignment in `enforce` mode can still block a request evaluated in `doNotEnforce` mode.

Resource policy evaluates matching requests. Assigning a policy doesn't automatically scan or remediate preexisting resources, and it doesn't replace the permissions required to perform a Microsoft Graph operation.

## Start with a built-in policy

Built-in policies let you apply predefined requirements without writing policy code. Select a policy, supply its required parameters, and assign it in your tenant.

Start with the [built-in policy quickstart](resource-policy-quickstart-portal) to assign and test a policy with simulated requests. Then follow the [tutorial to observe and enforce the policy](resource-policy-tutorial-portal) with real requests. Assess its impact in `doNotEnforce` mode before you enforce it.

## Author a custom policy

If a built-in policy doesn't meet your needs, author a custom policy in [Rego](https://www.openpolicyagent.org/docs/policy-language), the declarative policy language used by Open Policy Agent. Define which requests the policy evaluates and the requirements they must meet.

The policy's `deny` rule identifies noncompliance. The assignment's enforcement mode determines whether that result blocks the request.

Learn about [resource policy parameters](resource-policy-parameters), [authoring with Rego](resource-policy-rego), and [managing policy versions](resource-policy-lifecycle).

## Choose a management method

Use the management method that fits your workflow.

| Method | Use |
| --- | --- |
| Microsoft Entra admin center | Discover policies and manage definitions and assignments through the [admin center experience](resource-policy-manage-portal). |
| Microsoft Graph REST APIs | Integrate policy management, simulated evaluation, and evaluation audit-log retrieval with your tools. |

Keep Rego, tests, and assignment configuration in source control for review and repeatable API-based management.

## Assess impact before enforcement

Use simulated evaluations to test policy behavior without performing the requested write. Then use `doNotEnforce` assignments and the Microsoft Graph policy evaluation audit-log API to understand the impact on real requests. Inspect per-assignment results to identify noncompliance, affected applications and operations, and evaluation errors.

The preview provides evaluation audit events, not service-generated aggregated impact reports. Diagnostic settings aren't required to retrieve events through Microsoft Graph. For the assessment workflow and optional custom analysis, see [Analyze resource policy evaluation audit logs](resource-policy-logs).

Follow [safe assignment deployment practices](resource-policy-safe-deployment) before enabling enforcement.

## Compare Tenant Governance features

Tenant Governance features address different parts of your governance workflow.

| Feature | Purpose |
| --- | --- |
| Related tenants | Discover tenants with observable relationships to your tenant. |
| Governance relationships | Establish approved cross-tenant administrative access. |
| Configuration management | Compare existing resource configuration with a baseline and report drift. |
| Resource policy | Evaluate matching requests and help prevent noncompliant configuration changes. |
| Secure tenant creation | Create add-on tenants with governance and recovery capabilities. |

Use [configuration management](configuration-management) to detect configuration drift and resource policy to help prevent supported changes that would introduce noncompliance. Their supported resources and permissions aren't necessarily the same.

## Licensing and availability

Most resource policy operations during preview require a Microsoft Entra ID Governance service plan. See [Tenant Governance licensing](licensing#resource-policy-preview) for requirements and exceptions.
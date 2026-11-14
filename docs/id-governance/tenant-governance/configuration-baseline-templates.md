---
layout: Conceptual
title: Configuration baseline templates (Preview) - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/configuration-baseline-templates
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how configuration baseline templates standardize configuration definitions across monitors and deployments in Microsoft Entra Tenant Governance.
ms.topic: concept-article
ms.date: 2026-11-12T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: 8c32d2ae-daf7-9cc2-2afe-b4224cf30c25
document_version_independent_id: 8c32d2ae-daf7-9cc2-2afe-b4224cf30c25
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/configuration-baseline-templates.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/configuration-baseline-templates
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/configuration-baseline-templates.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 80e6763a-5aa6-8e22-10c2-aa26ae1318de
---

# Configuration baseline templates (Preview) - Microsoft Entra ID Governance | Microsoft Learn

A configuration baseline template is a reusable baseline definition in Microsoft Entra Tenant Governance. Use Configuration baseline templates to standardize baseline definitions across monitors and deployments.

Configuration management supports operations in the home tenant and in other tenants that are connected through governance relationships. A shared template helps you use the same approved configuration standard for those targets.

The **Templates** page separates configuration baseline templates from governance policy templates and shows each baseline template's version.

[![Screenshot of configuration baseline templates with descriptions and version numbers.](../media/tenant-governance-configuration-management/configuration-baseline-templates.png)](../media/tenant-governance-configuration-management/configuration-baseline-templates.png#lightbox)

## Templates, baselines, and snapshots

A baseline is the JSON definition of resources and their expected property values. A snapshot captures actual resource settings at a point in time. A template lets you reuse a reviewed baseline when you create monitors or deployments.

Use the following workflow:

1. Capture current settings in a snapshot or author baseline JSON.
2. Review the settings and remove or adjust values that shouldn't become part of your standard.
3. Save the approved baseline as a template.
4. Use the template to create a monitor or deployment for a selected tenant.

A template doesn't grant permissions or apply settings by itself. A monitor evaluates the baseline; a deployment applies it.

Note

Configuration baseline templates are different from [governance policy templates](governance-policy-templates). Governance policy templates define access through governance relationships, not the desired configuration of workload resources.

## Reuse across tenants

Before using a template in another tenant, review tenant-specific resource identifiers, dependencies, and workload availability. A baseline captured in one tenant isn't automatically suitable for every target tenant.

The operation that uses the template must have the required permissions in its target tenant. Monitoring requires read access. Deployments require permissions to change the affected settings.

## Manage versions and approvals

Treat approved template revisions as controlled configuration changes:

- Include a version or revision in your naming convention.
- Record the owner, approval date, and intended environments.
- Store reviewed baseline JSON in version control.
- Validate a revision with a limited target scope before broader use.
- Review existing monitors and deployments explicitly when adopting a revised template; don't rely on editing a template to update existing operations.

The service creates a new version when you save a template edit. Existing monitors continue using their selected version until you explicitly update them. For a template-linked monitor, use **Apply latest**, when available, to adopt the latest version and review its parameter values.

The service limits the number of versions retained for a template. When the limit prevents a save, the editor attempts to delete the oldest version that no monitor references and retry. If all earlier versions are still referenced, update or delete those monitors before trying again. Keep reviewed baseline JSON in version control for durable change history.
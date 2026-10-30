---
layout: Conceptual
title: PowerShell samples for dynamic membership processing - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-dynamic-membership-powershell-samples
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Use these PowerShell samples to pause and resume dynamic membership rule processing for Microsoft Entra groups and administrative units during incident response.
ms.topic: sample
ms.date: 2026-06-11T00:00:00.0000000Z
ms.reviewer: mbhargava
ai-usage: ai-assisted
locale: en-us
document_id: 1a7297b0-3ed3-83d4-3d9c-e6f2ed6e77c5
document_version_independent_id: 1a7297b0-3ed3-83d4-3d9c-e6f2ed6e77c5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-dynamic-membership-powershell-samples.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-dynamic-membership-powershell-samples
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-dynamic-membership-powershell-samples.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 7d090cf9-3102-ecfe-9adf-4721a4ac819b
---

# PowerShell samples for dynamic membership processing - Microsoft Entra ID | Microsoft Learn

When dynamic membership rules cause unintended changes or processing delays in your Microsoft Entra tenant, you can pause rule processing to contain the issue and resume it in a controlled order during recovery. These samples cover both dynamic groups and dynamic administrative units.

## Overview

These PowerShell samples help you pause and resume dynamic membership rule processing for groups and administrative units in your Microsoft Entra tenant when you need to mitigate ongoing membership update issues or unintended rule changes. Pausing stops rule evaluation; resuming restores it. Each script runs in two phases: groups first, then administrative units. At the start of each phase, the script asks for confirmation; enter `yes` to run that phase or anything else to skip it. This lets you target only groups, only administrative units, or both in a single run.

These samples use the [Microsoft Graph PowerShell module](/en-us/powershell/microsoftgraph/installation).

## Prerequisites

- PowerShell 5.1 (x64) or later.
- The Microsoft Graph PowerShell module:

    ```powershell
    Install-Module Microsoft.Graph -Scope CurrentUser
    ```
- A signed-in account that can manage the collections you target. The groups phase needs the [Groups Administrator](../role-based-access-control/permissions-reference#groups-administrator) Microsoft Entra role and the `Group.ReadWrite.All` Microsoft Graph scope. The administrative units phase needs the [Privileged Role Administrator](../role-based-access-control/permissions-reference#privileged-role-administrator) Microsoft Entra role and the `AdministrativeUnit.ReadWrite.All` scope. Each script requests only the scopes for the phases you run.

Important

Verify all steps in a test environment before you run any of these scripts in production.

Note

In large tenants, these scripts might trigger Microsoft Graph throttling. They include built-in retry handling, so expect a longer runtime rather than a failure. Don't cancel a running script unless you see an explicit error.

## Pause dynamic membership processing

| Sample | Description |
| --- | --- |
| [Pause all groups and administrative units with dynamic membership](scripts/powershell-pause-all-dynamic-membership) | Pauses every group and administrative unit that has dynamic membership rules in your tenant. Use this sample when you suspect a tenant-wide unintended change or widespread membership processing delays. |
| [Pause specific groups and administrative units with dynamic membership](scripts/powershell-pause-specific-dynamic-membership) | Pauses only the groups and administrative units whose IDs you supply. Use this sample when you need to halt processing for a known subset of collections. |
| [Pause all groups and administrative units with dynamic membership except specified](scripts/powershell-pause-all-except-dynamic-membership) | Pauses every group and administrative unit with dynamic membership except the IDs you exclude. Use this sample to keep critical collections running while halting everything else. |

## Resume dynamic membership processing

| Sample | Description |
| --- | --- |
| [Resume specific critical groups and administrative units with dynamic membership](scripts/powershell-resume-specific-critical-dynamic-membership) | Resumes processing for the critical groups and administrative units you specify. Run this sample first when recovering from a pause. |
| [Resume noncritical groups and administrative units with dynamic membership in batches](scripts/powershell-resume-noncritical-dynamic-membership) | Resumes processing for paused noncritical groups and administrative units, up to 100 of each per run. Run this sample after critical collections are restored and at least 12 hours have passed since pausing. |
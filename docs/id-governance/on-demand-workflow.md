---
layout: Conceptual
title: Run a workflow on-demand - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/on-demand-workflow
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This article guides a user to running a workflow on demand using Lifecycle Workflows.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
ms.custom: template-how-to
locale: en-us
document_id: c50196f3-8fb3-149b-1259-bf42b128e22d
document_version_independent_id: d0e57771-79ac-8984-70a7-40b59bec8282
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/on-demand-workflow.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/on-demand-workflow
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/on-demand-workflow.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 4adaff3b-ebc1-dd48-0753-42cfd7474d61
---

# Run a workflow on-demand - Microsoft Entra ID Governance | Microsoft Learn

Scheduled workflows by default run every 3 hours, but can also run on-demand so that they can be applied to specific users whenever you see fit. A workflow can be run on demand for any user, and doesn't take into account whether or not a user meets the workflow's execution conditions. Running a workflow on-demand allows you to test workflows before their scheduled run. This testing, on a set of users up to 10 at a time, allows you to see how a workflow will run before it processes a larger set of users. Testing your workflows before their scheduled runs helps you proactively solve potential lifecycle issues more quickly.

## Run a workflow on-demand in the Microsoft Entra admin center

Use the following steps to run a workflow on-demand:

Note

To be run on demand, the workflow must be enabled.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **workflows**.
3. On the workflow screen, select the specific workflow you want to run.

    ![Screenshot of a list of Lifecycle Workflows workflows to run on-demand.](media/on-demand-workflow/on-demand-list.png)
4. Select **Run on demand**.
5. On the **select users** tab, select **add users**.
6. On the add users screen, select the users you want to run the on-demand workflow for.

    ![Screenshot of add users for on-demand workflow.](media/on-demand-workflow/on-demand-add-users.png)
7. Select **Add**.
8. Confirm your choices and select **Run workflow**.

    ![Screenshot of a workflow being run on-demand.](media/on-demand-workflow/on-demand-run.png)

## Run a workflow on-demand using Microsoft Graph

To run a workflow on-demand using API via Microsoft Graph, see: [workflow: activate (run a workflow on-demand)](/en-us/graph/api/identitygovernance-workflow-activate).
---
layout: Conceptual
title: Simulate workflow execution using the What-if tool - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/simulate-workflow-execution
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to use the What-if tool in Lifecycle Workflows to simulate workflow execution and preview results without impacting actual users.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
ms.custom: template-how-to
ai-usage: ai-assisted
locale: en-us
document_id: d8bf04a6-ef3d-98bb-a777-52d1e0a51b1e
document_version_independent_id: d8bf04a6-ef3d-98bb-a777-52d1e0a51b1e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/simulate-workflow-execution.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/simulate-workflow-execution
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/simulate-workflow-execution.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f7c66b65-1f64-eaae-1741-b07a7e783006
---

# Simulate workflow execution using the What-if tool - Microsoft Entra ID Governance | Microsoft Learn

The What-if tool in Lifecycle Workflows lets you evaluate workflow execution before it runs for your users. Using the What-if tool, you can:

- View which users are currently in the execution scope of a workflow.
- Preview which workflow tasks might fail based on the current configuration.
- Simulate workflow execution for up to 10 users and review results without impacting actual users.

The primary goal of the What-if tool is to help you identify and resolve misconfigurations and prevent accidental workflow executions before processing begins.

Note

Workflows with change-based trigger types, such as attribute changes and group membership changes, aren't currently supported.

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Access the What-if tool

To access the What-if tool for a workflow:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Workflows**.
3. Select the workflow you want to evaluate.

    Note

    Workflows that use attribute changes or group membership changes as trigger types aren't currently supported by the What-if tool.
4. On the workflow overview page, select **What if** from the command bar. ![Screenshot of the What if tool on a workflow overview page.](media/simulate-workflow-execution/what-if-tool.png)

### Review users in scope

Within the What-if tool, select the **Users in Scope** tab to see the list of users that would be included in the current execution scope for the selected workflow. This list reflects the users who meet the workflow's execution conditions at the time the tool is run.

### Review potential task failures

Within the What-if tool, you can also review the tasks listed on the What-if page to see which workflow tasks might fail based on the current configuration. ![Screenshot of potential task failures within the what if tool.](media/simulate-workflow-execution/potential-task-failures.png)

## Run a workflow execution simulation

To simulate workflow execution and preview results for specific users:

1. On the What-if page, select the **Users in Scope** tab.
2. Select up to 10 users from the list.

    Note

    The **Simulate Workflow Execution** button is disabled if more than 10 users are selected.
3. Select **Simulate Workflow Execution** from the command bar.
4. The simulation starts automatically. Results appear on the **Execution Simulation Results** tab once they're available. ![Screenshot of the execution simulation results.](media/simulate-workflow-execution/execution-simulation-results.png)

    Note

    Depending on the workflow tasks, results might take a few seconds up to a couple of minutes to appear. If no results appear after a brief period, select **Refresh** to check for updated results. The **Execution Simulation Results** tab appears only after you run a simulation for the first time. Results are cleared when you run another simulation.
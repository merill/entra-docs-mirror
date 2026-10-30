---
layout: Conceptual
title: Manage lifecycle workflows with Microsoft Security Copilot | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/security-copilot/entra-lifecycle-workflows
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: cilwerner
ms.author: cwerner
manager: pmwongera
description: Use Microsoft Security Copilot in the Microsoft Entra admin center to create lifecycle workflows for Joiner, Mover, and Leaver scenarios. Execute workflows on-demand and use workflow insights to monitor execution and troubleshoot as needed.
ms.reviewer: ptyagi
ms.date: 2025-09-23T00:00:00.0000000Z
ms.update-cycle: 180-days
ms.topic: how-to
ms.service: entra
ms.custom: security-copilot
ms.collection: msec-ai-copilot
locale: en-us
document_id: 0485f690-285e-dd0b-525c-14cfb4e45d18
document_version_independent_id: 0485f690-285e-dd0b-525c-14cfb4e45d18
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/security-copilot/entra-lifecycle-workflows.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-copilot/entra-lifecycle-workflows
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/security-copilot/entra-lifecycle-workflows.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
platformId: f492a4dc-611a-fd60-33ad-afe239ca30b4
---

# Manage lifecycle workflows with Microsoft Security Copilot | Microsoft Learn

Microsoft Entra ID Governance applies the capabilities of [Microsoft Security Copilot](/en-us/security-copilot/microsoft-security-copilot) to save identity administrators time and effort when configuring custom workflows to manage the lifecycle of users across JML scenarios. It also helps you to customize workflows more efficiently using natural language to configure workflow information including custom tasks, execute workflows, and get workflow insights.

This article describes how to work with lifecycle workflows using Security Copilot in the Microsoft Entra admin center for the following use cases:

- Create step-by-step guidance for a new lifecycle workflow
- Explore available workflow configurations
- Analyze the active workflow list
- Troubleshoot the processing results of workflows
- Compare versions of a lifecycle workflow

## Prerequisites

- A tenant with Security Copilot enabled. Refer to [Get started with Microsoft Security Copilot](/en-us/copilot/security/get-started-security-copilot#option-2-provision-capacity-in-azure) for more information.
- A [Microsoft Entra ID Governance license](/en-us/entra/id-governance/identity-governance-overview#license-requirements).
- The assigned role of [Lifecycle Workflow Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#lifecycle-workflow-administrator)

## Launch Security Copilot in Microsoft Entra

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with the appropriate administrative role(s) for your scenario based off the specific use cases.
2. Launch Security Copilot from the **Copilot** button in the Microsoft Entra admin center.

    ![Screenshot that shows Security Copilot in the Microsoft Entra admin center.](media/copilot-security-entra/security-copilot-entra-admin-center.png)
3. Refer to the following use cases and prompts to retrieve information or perform actions using natural language queries.

Note

If an action is blocked by insufficient permissions, a recommended role is displayed. You can use the following prompt in the Security Copilot chat to activate the required role. This is dependent on having an eligible role assignment that provides the necessary access.

- *Activate the {required role} so that I can perform {the desired task}.*

## Create step-by-step guidance for a new lifecycle workflow

Security Copilot can give you the steps to guide you in creating a new lifecycle workflow. Provide a prompt with actions to take when the workflow is triggered and conditions that define which users (scope) this workflow should run against, and when (trigger) the workflow should run. For example:

*Create a lifecycle workflow for new hires in the Marketing department that sends a welcome email and a TAP and adds them to the "All Users in My Tenant" group. Also, provide the option to enable the schedule of the workflow.*

Review the returned results to see what the workflow includes and then follow the steps to [create a new workflow](/en-us/entra/id-governance/create-lifecycle-workflow) in the Microsoft Entra admin center. After the workflow is created, you can perform verification testing before enabling the schedule.

## Explore available workflow configurations

Using Microsoft Security Copilot, you can efficiently manage various lifecycle workflows. Here are some common tasks you can accomplish with Security Copilot:

For example:

- *List all lifecycle workflows in my tenant*
- *List all the supported workflow templates for creating a new workflow*
- *What are my lifecycle workflow settings?*
- *Which leaver tasks can I automate with lifecycle workflows?*
- *What templates can be used for creating a mover workflow?*

## Analyze active workflow list

With Microsoft Security Copilot, you can easily analyze and manage your active workflow list and retrieve specific workflow information.

For example:

- *Get my lifecycle workflows with the name {workflow name}.*
- *List all mover workflows in my tenant.*
- *List all the deleted lifecycle workflows in my tenant.*
- *List all disabled lifecycle workflows in my tenant.*
- *Show me the details of disabled workflow {workflow}.*

## Troubleshoot a Lifecycle Workflow run

You can use Security Copilot to help troubleshoot a workflow run. Security Copilot uses the information provided to generate and return a rich summary of the workflow history over the given time period for the specified workflow.

Explore workflow processing results of a specific workflow:

- *Summarize the runs for {workflow} in the last 7 days.*
- *How many times did the workflow run in the last 24 hours.*
- *Which users failed to be processed by this workflow in the last 7 days?*
- *Which tasks failed for {workflow} in the last 7 days?*
- *Show me the user processing results summary for {workflow} in the last 7 days.*

Explore workflow processing results across workflows:

- *How many workflows were processed in the last 7 days?*
- *How many users were successfully processed by workflows in the last 14 days?*
- *Which workflows have been run the most in the last 7 days?*
- *Which tasks failed the most in the last 30 days?*
- *Which workflows failed the most in the last 7 days?*
- *How many mover workflows were executed in the last 30 days?*

## Compare versions of a lifecycle workflow

You can use Security Copilot to compare workflow versions. Security Copilot uses the information provided to generate and return a rich summary of the content of two versions of the specified workflow as well as the core differences between the workflow versions including tasks and execution conditions.

For example:

- *List all workflow versions for {workflow}.*
- *Show me who last modified {workflow} and when.*
- *Show me the details of {version #} for this workflow.*
- *What changed in the last version of this workflow?*
- *Compare the last two versions of this workflow.*
- *Compare {version #} and {version #} of this workflow.*
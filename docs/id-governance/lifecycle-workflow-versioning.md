---
layout: Conceptual
title: Workflow Versioning - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/lifecycle-workflow-versioning
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: An article discussing Lifecycle workflow versioning and history
ms.subservice: lifecycle-workflows
ms.topic: concept-article
ms.date: 2026-03-12T00:00:00.0000000Z
ms.custom: template-concept, sfi-image-nochange
locale: en-us
document_id: e3f63875-570b-1fa3-9964-073a64a45e2d
document_version_independent_id: 810ba499-79ad-7e10-fa7e-3807e8b84ecc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/lifecycle-workflow-versioning.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/lifecycle-workflow-versioning
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/lifecycle-workflow-versioning.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 9e741176-59a9-ed4e-d5b5-553cd27bae30
---

# Workflow Versioning - Microsoft Entra ID Governance | Microsoft Learn

Workflows created using Lifecycle Workflows can be updated as needed to satisfy organizational requirements in terms of auditing the lifecycle of users in your organization. To manage updates in workflows, Lifecycle Workflows introduce the concept of workflow versioning. Workflow versions are new versions of existing workflows, triggered by updating execution conditions or their tasks. Workflow versions can change the actions or even scope of an existing workflow. Understanding how workflow versioning is handled during the workflow update process allows you to strategically set up workflows so that workflows tasks, and conditions, are always relevant for users processed by a workflow.

## Versioning benefits

Versioning with Lifecycle Workflows provides many benefits over the alternative of creating a new workflow for each use case. These benefits show up in its ability to improve the reporting process for both troubleshooting, and record keeping, capabilities in the following ways:

- **Long-term retention**- Versioning allows for longer retention of workflow information than by only using the audit logs. While the audit logs only store information from the previous 30 days, with versioning you're able to keep track of workflow details from creation.
- **Traceability**- Allows tracking of which specific version of a workflow processed a user.

## Workflow properties and versions

While updates to workflows can trigger the creation of a new version, this isn't always the case. There are parameters of workflows known as basic properties, that's changeable without creating a new version of the workflow. The list of these parameters is as follows:

- displayName
- description
- isEnabled
- IsSchedulingEnabled
- task name
- task description

You'll find these corresponding parameters in the Microsoft Entra admin center under the **Properties** section of the workflow you're updating. [![Screenshot of updated basic properties LCW](media/lifecycle-workflow-versioning/basic-updateable-properties.png)](media/lifecycle-workflow-versioning/basic-updateable-properties.png#lightbox)

For a step by step guide on updating these properties using both the Microsoft Entra admin center and the API via Microsoft Graph, see: [Manage workflow properties](manage-workflow-properties).

Properties that trigger the creation of a new version are as follows:

- tasks
- executionConditions

While new versions of these workflows are made as soon as you make the updates in the Microsoft Entra admin center, creating a new version of a workflow using the API with Microsoft Graph requires running the createNewVersion method. For a step by step guide for updating either tasks, or execution conditions, see: [Manage Workflow Versions](manage-workflow-tasks).

Note

If the workflow is on-demand, the configure information associated with execution conditions isn't present.

## What details are contained in workflow version history

Unlike with changing basic properties of a workflow, newly created workflow versions can be vastly different from previous versions. Tasks can be added or removed, and who the workflow runs for can be different. Due to the vast changes that can happen to a workflow between versions, version details are also there to give detailed information about not only the current version of the workflow, but also its previous iterations.

Details contained in version information as shown in the Microsoft Entra admin center:

![Screenshot of workflow versioning information.](media/lifecycle-workflow-versioning/workflow-version-information.png)

Detailed **Version information** is as follows:

| parameter | description |
| --- | --- |
| Version Number | An integer denoting which version of the workflow the information is for. Sequentially goes up with each new workflow version. |
| Last modified date | The last time the workflow was updated. For previous versions of workflows, the last modified date will always be the time the next version was created. |
| Last modified by | Who last modified this workflow version. |
| Created date | The date and time for when a workflow version was created. |
| Created by | Who created this specific version of the workflow. |
| Name | Name of the workflow at this version. |
| Description | Description of the workflow at this version. |
| Category | Category of the workflow. |
| Execution Conditions | Defines for who and when the workflow runs in this version. |
| Tasks | The tasks present in this workflow version. If viewing through the API, you're also able to see task arguments. For specific task definitions, see: [Lifecycle Workflow tasks and definitions](lifecycle-workflow-tasks) |
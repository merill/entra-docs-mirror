---
layout: Conceptual
title: Agent identity sponsor tasks in Lifecycle Workflows - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/agent-sponsor-tasks
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This article describes workflow tasks that involve sponsors of agent identities.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2025-10-25T00:00:00.0000000Z
locale: en-us
document_id: 2b1b5792-eadf-0d18-c395-912ac4a43c5a
document_version_independent_id: 2b1b5792-eadf-0d18-c395-912ac4a43c5a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/agent-sponsor-tasks.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/agent-sponsor-tasks
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/agent-sponsor-tasks.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/302444b9-4a43-4841-8014-3d9e4251ff15
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/bebd8809-dac1-4c22-83e2-66d98af8a94d
platformId: 4f858779-caee-4eeb-5557-11aba541a9dd
---

# Agent identity sponsor tasks in Lifecycle Workflows - Microsoft Entra ID Governance | Microsoft Learn

Governing agent identities sponsors is a critical aspect of maintaining lifecycle governance and access control in your organization. Agent identity sponsors are responsible for overseeing the lifecycle and access decisions of agent identities. Keeping sponsor information up to date helps with effective governance and compliance. For an overview of agent identity governance including access packages and sponsor responsibilities, see [Governing Agent Identities](agent-id-governance-overview).

Lifecycle Workflows currently contain the following tasks that involve the governing of sponsors of agent identities:

- [Send email to manager about sponsorship changes](lifecycle-workflow-tasks#send-email-to-manager-about-sponsorship-changes)
- [Send email to cosponsors about sponsor changes](lifecycle-workflow-tasks#send-email-to-co-sponsors-about-sponsor-changes)
- [Transfer agent identity sponsorships to manager](lifecycle-workflow-tasks#transfer-agent-identity-sponsorships-to-manager)

These tasks ensure continuity of sponsorship when an agent's sponsor changes roles or leaves the organization. All three tasks are classified as **mover and leaver** tasks and are available only under mover or leaver workflow templates.

This article explains how to configure Lifecycle Workflows to streamline agent identity sponsor governance.

## License Requirements

Using [Microsoft Entra ID Governance](licensing-fundamentals) for agent identities requires one of the following license plans:

- **Microsoft 365 E7**, which includes Agent 365 and Microsoft Entra Suite, to provide governance of user and agent identities.
- **Microsoft Agent 365** license paired with at least Microsoft Entra P1 or Microsoft 365 E3.

For more information, see [Microsoft Agent 365 plans and pricing](https://www.microsoft.com/microsoft-agent-365#plans-and-pricing). For the full list of agent-specific capabilities, refer to the **Microsoft Agent 365** column in the [Microsoft Entra ID Governance licensing table](licensing-fundamentals).

## Create a sponsor workflow using the Microsoft Entra Admin Center

To create a workflow that notifies the manager or cosponsors of an existing agent identity sponsor's move, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **workflows**.
3. On the workflow screen, select the specific mover or leaver workflow template you want to add the sponsorship email tasks to, or create a new workflow based on a template.

    Note

    The **Send email to manager about sponsorship changes**, **Send email to co-sponsors about sponsor changes**, and **Transfer agent identity sponsorships to manager** are mover and leaver tasks, and are only available as selectable tasks under workflow templates of the same category.
4. On the **Basics** tab, after entering a unique display name and description for the workflow, select your trigger and select **Next**.
5. On the **Configure scope** screen, select the scope of the workflow and select **Next**.
6. On the **Tasks** page, select which sponsor related tasks you want to include and select **Next**. ![Screenshot of the sponsor workflow tasks.](media/manage-agent-sponsors/sponsor-workflow-tasks.png)
7. Review the created workflow, and then select **Create**.
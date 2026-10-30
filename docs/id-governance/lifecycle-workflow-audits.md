---
layout: Conceptual
title: Auditing Lifecycle Workflows - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/lifecycle-workflow-audits
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Information about audit logs with Lifecycle Workflows
ms.subservice: lifecycle-workflows
ms.topic: concept-article
ms.date: 2026-03-12T00:00:00.0000000Z
ms.custom: template-concept, sfi-image-nochange
locale: en-us
document_id: 3e52a046-29aa-a2a4-52e7-83e806c70179
document_version_independent_id: a44276d3-fc93-9ede-e091-0876d3439eda
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/lifecycle-workflow-audits.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/lifecycle-workflow-audits
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/lifecycle-workflow-audits.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
platformId: ee6a3591-ea7d-cc85-b538-edb9083fd42e
---

# Auditing Lifecycle Workflows - Microsoft Entra ID Governance | Microsoft Learn

Workflows created using Lifecycle Workflows allow for the automation of lifecycle tasks for users no matter where they fall in the Joiner-Mover-Leaver (JML) model of their identity lifecycle in your organization. Making sure workflows are processed correctly is an important part of an organization's lifecycle management process. Workflows that aren't processed correctly can lead to many issues in terms of security and compliance. With audit logs, every action that Lifecycle Workflows completes within a timeframe of up to 30 days is recorded.

## Audit Logs

Every time a workflow is processed, an event is logged. These events are stored in the **Audit Logs** section, and can be used to gain information about workflows for historical, and auditing, purposes. Audit log services, categories, and activities might change frequently.

![Screenshot of a workflow audit log.](media/lifecycle-workflow-audits/audit-logs-concept.png)

On the **Audit Log** page, you're presented with a sequential list, by date, of every action Lifecycle Workflows has taken. From this information, you can filter based on the following parameters:

| Filter | Description |
| --- | --- |
| Date | You can filter a specific range for the audit logs from as short as 24 hours up to 30 days. |
| Date option | You can filter by your tenant's local time, or by UTC. |
| Service | The Lifecycle Workflow service. |
| Category | Categories of the event being logged. Separated into: **Other**- Events related to custom tasks.**TaskManagement**- Task related events logged by Lifecycle Workflows. **WorkflowManagement**- Events dealing with the workflow itself. |
| Activity | You can filter based on specific activities, which are based on categories. |

After filtering this information, you're also able to see other information in the log such as:

- **Status**: Whether or not the logged event was successful.
- **Status Reason**: If the event failed, a reason is given why.
- **Target(s)**: Who the logged event ran for. Information given as their Microsoft Entra object ID.
- **Initiated by (actor)**: Who did the event being logged. Information given as the user name.
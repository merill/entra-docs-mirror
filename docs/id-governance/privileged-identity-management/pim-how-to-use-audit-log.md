---
layout: Conceptual
title: View audit log report for Microsoft Entra roles in Microsoft Entra PIM - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-how-to-use-audit-log
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Learn how to view the audit log history for Microsoft Entra roles in Microsoft Entra Privileged Identity Management (PIM).
ms.topic: how-to
ms.date: 2026-08-03T00:00:00.0000000Z
ms.reviewer: ilyalushnikov
ai-usage: ai-assisted
ms.custom: pim
locale: en-us
document_id: 80e649ea-1dc1-5fbc-2de5-41ac1424bcfc
document_version_independent_id: b8207854-8285-4685-d1e8-33152bfe44ca
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-how-to-use-audit-log.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-how-to-use-audit-log
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-how-to-use-audit-log.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 66af8a94-1ef9-e6d3-37ea-195bba01cf9d
---

# View audit log report for Microsoft Entra roles in Microsoft Entra PIM - Microsoft Entra ID Governance | Microsoft Learn

## Overview

You can use the Microsoft Entra Privileged Identity Management (PIM) Resource audit logs to see role assignment changes, role activations, and PIM Policy changes. Data is available for the past 30 days.

The PIM Resource audit log is a subset of Microsoft Entra audit logs. Use [Microsoft Entra security and activity reports](../../identity/monitoring-health/overview-monitoring-health) to view the full audit history of Microsoft Entra ID activity including administrator, end user, and synchronization activity.

If you want to retain audit data for longer than the default retention period, you can use Diagnostic Settings in Azure Monitor to route it to an Azure storage account or Log Analytics. For more information, see [Integrate Microsoft Entra logs with Azure Monitor logs](../../identity/monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs).

Follow these steps to view the audit history for Microsoft Entra roles.

## View resource audit history

Use the **Resource audit** blade to view all activity associated with your Microsoft Entra role assignment and PIM policy management in PIM.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a Global Administrator, Global Reader, Privileged Role Administrator, Security Administrator, or Security Reader.
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **Microsoft Entra roles**.
3. Select **Resource audit**.
4. Filter the history using a predefined date or custom range.

    ![Screenshot showing the Microsoft Entra role audit list with filters.](media/pim-how-use-audit-log/resource-audit.png)

## View my audit

Use the **My audit** blade to view your role activity for Microsoft Entra role assignment and PIM policy management.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **Microsoft Entra roles**.
3. Select **My audit**.
4. Filter the history using a predefined date or custom range.

    ![Screenshot showing the Audit list page for the current user.](media/pim-how-use-audit-log/my-audit.png)

## Correlating events related to the same activation cycle

`CorrelationId` is generally used to correlate audit log events related to one request. With PIM, multiple asynchronously processed operations can be part of one activation/deactivation cycle. As a result, some events related to the same activation/deactivation cycle will have different `CorrelationId`s.

During role activation, the following operations may be processed asynchronously, resulting in multiple `CorrelationId`s being generated:

- **Scheduled activation** in PIM allows eligible users to request role activation to begin at a specified future time. Once scheduled, the system tracks the activation request and automatically creates a role assignment at the designated start time — without requiring further user input. Because this operation is asynchronous, a new `CorrelationId` is generated at the time of actual activation, which may differ from the original request's `CorrelationId`. This makes direct correlation using `CorrelationId` challenging across the request and activation phases.
- **Approval-gated activation**: When PIM Policy requires approval for role activation, the activation request follows a two-step process: the request is created by an eligible user, then approval is provided by a designated approver. Once approved, the system proceeds with role assignment — this may happen immediately or later if the user chose a scheduled start. Due to the asynchronous nature of this flow, the `CorrelationId` may differ across stages.
- In rare cases, `CorrelationId` may change during the role activation flow due to the way requests are processed between systems.

Use `roleAssignmentRequestId` to correlate events related to one activation request in all of the examples above. `roleAssignmentRequestId` remains the same during the asynchronous processing of operations such as scheduled activation or approval.

Use the following example Log Analytics query to get audit log entries related to role activation:

```Kusto
AuditLogs
| where OperationName has "Add member to role"
```

Use the output of this query to get the `roleAssignmentRequestId` for the event you need to analyze.

Use the following example Log Analytics query to get audit log entries related to the same role activation:

```Kusto
let roleAssignmentRequestId = "{roleAssignmentRequestId}";
AuditLogs
| where AdditionalDetails has roleAssignmentRequestId
```

`CorrelationId` logged during the deactivation process depends on how deactivation was triggered:

- When deactivation is triggered automatically based on the expiration of an activated role assignment, `CorrelationId` of deactivation events matches the latest `CorrelationId` used during the activation.
- When deactivation is triggered by the assignee (user selected **Deactivate** on the portal), `CorrelationId` will be different from the one used in the activation flow.

In both cases, `roleAssignmentRequestId` of the original activation request is logged under **Additional details** for audit log events of deactivation.

Use the following example Log Analytics query to get audit log entries related to the full activation/deactivation cycle:

```Kusto
let roleAssignmentRequestId = "{roleAssignmentRequestId}";
let relatedCorrelationIds = AuditLogs
   | where AdditionalDetails has roleAssignmentRequestId
   | summarize makeset(CorrelationId);
AuditLogs
| where AdditionalDetails has roleAssignmentRequestId
  or CorrelationId in (relatedCorrelationIds)
```
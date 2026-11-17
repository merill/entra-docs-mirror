---
layout: Conceptual
title: View audit report for Azure resource roles in Privileged Identity Management (PIM) - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/azure-pim-resource-rbac
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: tamimsangrar
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: View activity and audit history for Azure resource roles in Privileged Identity Management (PIM).
ms.topic: how-to
ms.date: 2026-11-17T00:00:00.0000000Z
ms.reviewer: ilyal
ms.custom: sfi-image-nochange, msecd-doc-authoring-1032
ai-usage: ai-assisted
locale: en-us
document_id: b9dcb3c8-7a2a-098a-41bb-937483596a92
document_version_independent_id: 577311fd-9d22-0270-d39e-0047ca63fb11
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/azure-pim-resource-rbac.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/azure-pim-resource-rbac
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/azure-pim-resource-rbac.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7c01134-b8f3-438c-822d-13471e513908
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/82fff6b2-939d-4e9a-8f9c-d1c41a59749b
platformId: 159cca87-da89-1b4f-b977-22810c82654f
---

# View audit report for Azure resource roles in Privileged Identity Management (PIM) - Microsoft Entra ID Governance | Microsoft Learn

## Overview

Privileged Identity Management (PIM) in Microsoft Entra ID enables you to view activity, activations, and audit history for Azure resource roles within your organization. This includes subscriptions, resource groups, and even virtual machines. Any resource within the Microsoft Entra admin center that uses the Azure role-based access control functionality can take advantage of the security and lifecycle management capabilities in Privileged Identity Management. If you want to keep audit data for longer than the default retention period, you can use Azure Monitor to route it to an Azure storage account. For more information, see [Archive Microsoft Entra logs to an Azure storage account](../../identity/monitoring-health/howto-archive-logs-to-storage-account).

Note

If your organization has outsourced management functions to a service provider who uses [Azure Lighthouse](/en-us/azure/lighthouse/overview), role assignments authorized by that service provider won't be shown here.

## View activity and activations

To see the actions a specific user took in various resources, view the Azure resource activity associated with their activation period.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **Azure resources**.
3. Select the resource you want to view activity and activations for.
4. Select **Roles** or **Members**.
5. Select a user.

    You see a summary of the user's actions in Azure resources by date. It also shows the recent role activations over that same time period.

    ![Screenshot of user details with resource activity summary and role activations.](media/azure-pim-resource-rbac/rbac-user-details.png)
6. Select a specific role activation to see details and corresponding Azure resource activity that occurred while that user was active.

    ![Screenshot of role activation selected and activity details.](media/azure-pim-resource-rbac/export-membership.png)

## Export role assignments with children

You might have a compliance requirement where you must provide a complete list of role assignments to auditors. Privileged Identity Management enables you to query role assignments at a specific resource, which includes role assignments for all child resources. Previously, it was difficult for administrators to get a complete list of role assignments for a subscription and they had to export role assignments for each specific resource. Using Privileged Identity Management, you can query for all active and eligible role assignments in a subscription including role assignments for all resource groups and resources.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **Azure resources**.
3. Select the resource you want to export role assignments for, such as a subscription.
4. Select **Assignments**.
5. Select **Export** to open the Export membership pane.

    ![Screenshot showing the export membership pane to export all members.](media/azure-pim-resource-rbac/export-membership.png)
6. Select **Export all members** to export all role assignments in a CSV file.

    ![Screenshot showing exported role assignments in CSV file as displayed in Excel.](media/azure-pim-resource-rbac/export-csv.png)

## View resource audit history

Resource audit gives you a view of all role activity for a resource.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **Azure resources**.
3. Select the resource you want to view audit history for.
4. Select **Resource audit**.
5. Filter the history using a predefined date or custom range.

    ![Screenshot showing resource audit list with filters.](media/azure-pim-resource-rbac/rbac-resource-audit.png)
6. For **Audit type**, select **Activate (Assigned + Activated)**.

    ![Screenshot showing the resource audit list filtered by Activate audit type.](media/azure-pim-resource-rbac/rbac-audit-activity.png)
7. Under **Action**, select **(activity)** for a user to see that user's activity detail in Azure resources.

    ![Screenshot showing user activity details for a particular action.](media/azure-pim-resource-rbac/rbac-audit-activity-details.png)

## View my audit

My audit enables you to view your personal role activity.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **Azure resources**.
3. Select the resource you want to view audit history for.
4. Select **My audit**.
5. Filter the history using a predefined date or custom range.

    ![Screenshot showing an audit list for the current user.](media/azure-pim-resource-rbac/my-audit-time.png)

Note

Access to audit history requires at least the Privileged Role Administrator role.

## Get reason, approver, and ticket number for approval events

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Audit logs**.
3. Use the **Service** filter to display only audit events for the Privileged Identity Management service. On the **Audit logs** page, you can:

    - See the reason for an audit event in the **Status reason** column.
    - See the approver in the **Initiated by (actor)** column for the "add member to role request approved" event.

    ![Screenshot showing filtering the audit log for the PIM service.](media/azure-pim-resource-rbac/filter-audit-logs.png)
4. Select an audit log event to see the ticket number on the **Activity** tab of the **Details** pane.

    ![Screenshot showing the ticket number for the audit event.](media/azure-pim-resource-rbac/audit-event-ticket-number.png)
5. You can view the requester (person activating the role) on the **Targets** tab of the **Details** pane for an audit event. There are three target types for Azure resource roles:

    - The role (**Type** = Role)
    - The requester (**Type** = Other)
    - The approver (**Type** = User)

    ![Screenshot showing how to check the target type.](media/azure-pim-resource-rbac/audit-event-target-type.png)

Typically, the log event immediately above the approval event is an event for **Add member to role completed** where the **Initiated by (actor)** is the requester. In most cases, you won't need to find the requester in the approval request from an auditing perspective.

## View session activity (preview)

Use Session Analytics to view an identity's PIM role lifecycle and Azure Bastion connection activity for a selected Azure subscription or resource group. The view covers role activation, Bastion access to an Azure Virtual Machine, and role deactivation or expiration. It doesn't show Azure resource operations, such as creating a resource group, or commands run inside a virtual machine.

For graphical recordings, use Session Recordings. Recordings have separate setup and viewing requirements.

### Session Analytics prerequisites

Microsoft Entra ID Governance licensing is required for Session Analytics in preview. See [Microsoft Entra ID Governance licensing fundamentals](../licensing-fundamentals).

Configure diagnostic settings on each Azure Bastion host you want to monitor to send `BastionAuditLogs` to a Log Analytics workspace. Use a workspace in the same tenant. Only Azure Bastion audit logs need this routing for Session Analytics. You don't need to route additional PIM log sources to the workspace.

Complete Set up Azure Bastion audit-log collection with the setup roles, then verify Bastion log collection. Use the separate roles listed in View Session Analytics to view the results.

### Set up Azure Bastion audit-log collection

Configure the destination for each host before viewing its Bastion connection activity. If log collection is already configured, continue to Verify Bastion log collection.

For setup with an existing Log Analytics workspace, use these recommended roles:

| Resource | Recommended role | Role assignment scope |
| --- | --- | --- |
| Azure Bastion host | **Monitoring Contributor** | The Azure Bastion resource. |
| Existing Log Analytics workspace | **Monitoring Contributor** | The Log Analytics workspace. |

These are sufficient built-in setup recommendations, not minimum permissions. Custom roles can grant narrower permissions. See [Monitoring Contributor permissions](/en-us/azure/azure-monitor/fundamentals/roles-permissions-security#monitoring-contributor) and [Log Analytics workspace permissions](/en-us/azure/azure-monitor/logs/manage-access#azure-rbac).

1. Create or reuse a Log Analytics workspace in the same tenant. Follow [Create a Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace) for creation steps and permissions.
2. For each Azure Bastion host you want to monitor, follow [Diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/data-collection/diagnostic-settings) to configure a setting, for example, `SendToLogAnalytics`, that sends `BastionAuditLogs` to the workspace. For the log category and `MicrosoftAzureBastionAuditLogs` table, see [Azure Bastion resource logs](/en-us/azure/bastion/monitor-bastion-reference#resource-logs).
3. Before viewing Bastion activity in PIM, verify the host's connection records in the destination workspace.

### Verify Bastion log collection

Use the **Log Analytics Reader** role on the destination Log Analytics workspace to check for Bastion connection records before viewing Bastion activity in PIM.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. After a user connects through a monitored Bastion host, check for that connection's records in the workspace's `MicrosoftAzureBastionAuditLogs` table. Use `_ResourceId` to identify the Bastion host, `TargetResourceId` to identify the virtual machine, and `SessionStartTime` to check the connection time. For column details, see [MicrosoftAzureBastionAuditLogs](/en-us/azure/azure-monitor/reference/tables/microsoftazurebastionauditlogs).

    If the expected record isn't present, verify the host's diagnostic settings, the destination workspace, and the time range you're checking before viewing Bastion activity in PIM.

After verifying log collection, continue to View Session Analytics.

### View Session Analytics

To view Session Analytics, you need both of the following:

- At least the **Reports Reader** role in Microsoft Entra ID.
- The **Azure resource and Log Analytics workspace viewing roles**.

If your directory role assignment is eligible, activate it before viewing Session Analytics. See [Microsoft Entra activity-log prerequisites](../../identity/monitoring-health/howto-access-activity-logs#prerequisites).

The following Azure resource and workspace viewing roles apply at the listed resource scopes. These are separate from the setup roles.

| Resource | Role | Role assignment scope |
| --- | --- | --- |
| Log Analytics workspace | **Log Analytics Reader** | The Log Analytics workspace. |
| Azure Bastion host | **Reader** | The Azure Bastion resource. |
| Azure Virtual Machine | **Reader** | The Azure Virtual Machine resource. |
| Network interface | **Reader** | The Azure Virtual Machine's network interface. |
| Virtual network | **Reader** | The relevant virtual network, including a peered virtual network where applicable. |

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Open **Privileged Identity Management**, select **Azure resources**, and select the Azure subscription or resource group whose activity you want to view.
3. Under **Activity**, select **Session Analytics (Preview)**.
4. Use **Date range** or search by identity, role, or scope to find the activity you want to view.

    [![Screenshot of Session Analytics showing a role activation with its scope, start and end times, and filtering controls.](media/azure-pim-resource-rbac/session-analytics-activity.png)](media/azure-pim-resource-rbac/session-analytics-activity.png#lightbox)
5. View the identity, activated role, scope, scope type, and start and end times. Select **Refresh** to reload the results.

## View Azure Bastion session recordings (preview)

Use Session Recordings to find recording-enabled Azure Bastion hosts in the selected scope and open their graphical recordings.

### Session Recordings prerequisites

- Microsoft Entra ID Governance licensing is required for the PIM Session Recordings view in preview. See [Microsoft Entra ID Governance licensing fundamentals](../licensing-fundamentals).
- Azure Bastion must use the **Premium** SKU with session recording and storage configured. Follow [Record Bastion sessions](/en-us/azure/bastion/session-recording) for setup and storage requirements.
- To view or list recordings in Azure Bastion, you need the **Storage Blob Data Reader** role. Follow the [Bastion recording guide](/en-us/azure/bastion/session-recording#prerequisites) for the viewing requirements.

### Azure Bastion recording support

A recording-enabled Azure Bastion Premium host records RDP and SSH connections through that host. It records all connections through the host, not just connections initiated from My Access. The following table summarizes supported and unsupported connection combinations for graphical recording:

| Protocol | Authentication | Client | Graphical recording |
| --- | --- | --- | --- |
| **SSH** | Microsoft Entra ID or other supported SSH authentication. | Azure portal (browser). | Supported. |
| **RDP** | Supported authentication other than Microsoft Entra ID. | Azure portal (browser). | Supported. |
| **RDP** | Microsoft Entra ID. | Azure portal (browser). | Not supported concurrently with Microsoft Entra ID RDP. |
| **RDP or SSH** | Any authentication method. | Native client. | Not supported. |

Use this table when selecting a connection method for a recording requirement. For recording setup and considerations, see [Record Bastion sessions](/en-us/azure/bastion/session-recording). For Microsoft Entra connection requirements, see [Configure Microsoft Entra ID authentication for Azure Bastion](/en-us/azure/bastion/bastion-entra-id-authentication).

### Session Recordings (Preview)

After recording setup is complete, use the PIM view to locate the host and open its recordings.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Open **Privileged Identity Management** and select **Azure resources**. Use the scope selector to select the **subscription or resource group that contains the Azure Bastion host** whose recordings you want to view.
3. Under **Activity**, select **Session Recordings (Preview)**.

    [![Screenshot of Session Recordings listing Azure Bastion hosts with recording enabled.](media/azure-pim-resource-rbac/session-recordings-hosts.png)](media/azure-pim-resource-rbac/session-recordings-hosts.png#lightbox)
4. Select a Bastion host to open its recordings in the Bastion experience.
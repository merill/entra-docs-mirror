---
layout: Conceptual
title: View audit report for Azure resource roles in Privileged Identity Management (PIM) - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/azure-pim-resource-rbac
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: View activity and audit history for Azure resource roles in Privileged Identity Management (PIM).
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: shaunliu
ms.custom: sfi-image-nochange
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
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
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
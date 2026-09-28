---
layout: Conceptual
title: Cross-tenant access activity workbook - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/workbook-cross-tenant-access-activity
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how to use the cross-tenant access activity workbook in Microsoft Entra ID to monitor the resources your external users are accessing.
ms.topic: how-to
ms.date: 2024-11-04T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 23ca952c-2b85-0179-1441-6746922458e6
document_version_independent_id: eee8625a-3d34-be0e-fd7c-9b08ec17664b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/workbook-cross-tenant-access-activity.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/workbook-cross-tenant-access-activity
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/workbook-cross-tenant-access-activity.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 2ac615c2-ba1e-7dcd-72da-cd8bbdc9f503
---

# Cross-tenant access activity workbook - Microsoft Entra ID | Microsoft Learn

As an IT administrator, you want insights into how your users are collaborating with other organizations. The cross-tenant access activity workbook helps you understand which external users are accessing resources in your organization, and which organizations’ resources your users are accessing. This workbook combines all your organization’s inbound and outbound collaboration into a single view.

This article provides you with an overview of the **Cross-tenant access activity** workbook.

## Prerequisites

To use Azure Workbooks for Microsoft Entra ID, you need:

- A Microsoft Entra tenant with a [Premium P1 license](../../fundamentals/get-started-premium)
- A Log Analytics workspace *and* access to that workspace
- The appropriate roles for Azure Monitor *and* Microsoft Entra ID

### Log Analytics workspace

You must create a [Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace)*before* you can use Microsoft Entra Workbooks. several factors determine access to Log Analytics workspaces. You need the right roles for the workspace *and* the resources sending the data.

For more information, see [Manage access to Log Analytics workspaces](/en-us/azure/azure-monitor/logs/manage-access).

### Azure Monitor roles

Azure Monitor provides [two built-in roles](/en-us/azure/azure-monitor/roles-permissions-security#monitoring-reader) for viewing monitoring data and editing monitoring settings. Azure role-based access control (RBAC) also provides two Log Analytics built-in roles that grant similar access.

- **View**:

    - Monitoring Reader
    - Log Analytics Reader
- **View and modify settings**:

    - Monitoring Contributor
    - Log Analytics Contributor

### Microsoft Entra roles

Read only access allows you to view Microsoft Entra ID log data inside a workbook, query data from Log Analytics, or read logs in the Microsoft Entra admin center. Update access adds the ability to create and edit diagnostic settings to send Microsoft Entra data to a Log Analytics workspace.

- **Read**:

    - Reports Reader
    - Security Reader
    - Global Reader
- **Update**:

    - Security Administrator

For more information on Microsoft Entra built-in roles, see [Microsoft Entra built-in roles](../role-based-access-control/permissions-reference).

For more information on the Log Analytics RBAC roles, see [Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles#log-analytics-contributor).

## Description

![Image showing this workbook is found under the Usage category](media/workbook-cross-tenant-access-activity/workbook-category.png)

Tenant administrators who are making changes to policies governing cross-tenant access can use this workbook to visualize and review existing access activity patterns before making policy changes. For example, you can identify the applications your users are accessing in external organizations so that you don't inadvertently block critical business processes. Understanding how external users access resources in your tenant (inbound access) and how users in your tenant access resources in external tenants (outbound access) help ensure you have the right cross-tenant policies in place.

For more information, see the [Microsoft Entra External ID documentation](../../external-id/).

## How to access the workbook

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) using the appropriate combination of roles.
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Workbooks**.
3. Select the **Cross-tenant access activity** workbook from the **Usage** section.

## Workbook sections

This workbook has four sections:

- All inbound and outbound activity by tenant ID
- Sign-in status summary by tenant ID for inbound and outbound collaboration
- Applications accessed for inbound and outbound collaboration by tenant ID
- Individual users for inbound and outbound collaboration by tenant ID

The total number of external tenants that had cross-tenant access activity with your tenant is shown at the top of the workbook.

![Screenshot of the first section of the workbook.](media/workbook-cross-tenant-access-activity/cross-tenant-activity-top.png)

The **External Tenant** list shows all the tenants that had inbound or outbound activity with your tenant. When you select an external tenant in the table, the sections after the table display information about outbound and inbound activity for that tenant.

![Screenshot of the external tenant list.](media/workbook-cross-tenant-access-activity/cross-tenant-activity-external-tenant-list.png)

When you select an external tenant from the list with outbound activity, associated details appear in the **Outbound activity** table. The same applies when you select an external tenant with inbound activity. Select the **Inbound activity** tab to view the details of an external tenant with inbound activity.

![Screenshot of the outbound and inbound activity, with the outbound and inbound options highlighted.](media/workbook-cross-tenant-access-activity/cross-tenant-activity-outbound-inbound-activity.png)

When you're viewing external tenants with outbound activity, the subsequent two tables display details for the application, and user activity appear. When you're viewing external tenants with inbound activity, the same tables show inbound application and user activity. These tables are dynamic and based on what was previously selected, so make sure you're viewing the correct tenant and activity.

## Filters

This workbook supports multiple filters:

- Time range (up to 90 days)
- External tenant ID
- User principal name
- Application
- Status of the sign-in (success or failure)

![Screenshot showing workbook filters](media/workbook-cross-tenant-access-activity/workbook-filters.png)

## Best practices

Use this workbook to:

- Get the information you need to manage your cross-tenant access settings effectively, without breaking legitimate collaborations
- Identify all inbound sign-ins from external Microsoft Entra organizations
- Identify all outbound sign-ins by your users to external Microsoft Entra organizations
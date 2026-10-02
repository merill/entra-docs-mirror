---
layout: Conceptual
title: Microsoft Graph PowerShell monitoring and health cmdlets - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/reference-powershell-reporting
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Reference information for Microsoft Graph PowerShell cmdlets for Microsoft Entra monitoring and health.
ms.topic: reference
ms.date: 2024-02-06T00:00:00.0000000Z
ms.reviewer: dhanyahk
locale: en-us
document_id: 2a01fec2-4745-40f5-ac28-3e278e08e9f5
document_version_independent_id: e34e1b92-a59a-b215-12c4-8d5613f3da2c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/reference-powershell-reporting.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/reference-powershell-reporting
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/reference-powershell-reporting.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/5cf46315-b33f-4e99-8224-a1592697eff9
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/715d24c3-3683-4219-82c5-1e3c813fb7fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 6aa40777-d02c-0438-17fc-31deac6f15f0
---

# Microsoft Graph PowerShell monitoring and health cmdlets - Microsoft Entra ID | Microsoft Learn

With Microsoft Entra monitoring and health, you can get details on activities around all the write operations in your directory (audit logs) and authentication data (sign-in logs). Although the information is available by using the Microsoft Graph API, now you can retrieve the same data by using the Microsoft Graph PowerShell cmdlets for Identity monitoring and health.

This article gives you an overview of the Microsoft Graph PowerShell cmdlets to use for audit logs and sign-in logs. [Get started with Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/get-started).

## Audit logs

[Audit logs](concept-audit-logs) provide traceability through logs for all changes done by various features within Microsoft Entra ID. Examples of audit logs include changes made to any resources within Microsoft Entra ID like adding or removing users, apps, groups, roles, and policies.

You get access to the audit logs using the `Get-MgAuditLogDirectoryAudit` cmdlet.

| Scenario | PowerShell command |
| --- | --- |
| Application Display Name | `Get-MgAuditLogDirectoryAudit -Filter "initiatedBy/app/displayName eq 'Azure AD Cloud Sync'"` |
| Category | `Get-MgAuditLogDirectoryAudit -Filter "category eq 'ApplicationManagement'"` |
| Activity Date Time | `Get-MgAuditLogDirectoryAudit -Filter "activityDateTime gt 2019-04-18"` |
| All of the above | `Get-MgAuditLogDirectoryAudit -Filter "initiatedBy/app/displayName eq 'Azure AD Cloud Sync' and category eq 'ApplicationManagement' and activityDateTime gt 2019-04-18"` |

## Sign-in logs

The [sign-ins](concept-sign-ins) logs provide information about the usage of managed applications and user sign-in activities.

You get access to the sign-in logs using the `Get-MgAuditLogSignIn` cmdlet. Use the following table for more scenarios.

| Scenario | Microsoft Graph PowerShell command |
| --- | --- |
| User Display Name | `Get-MgAuditLogSignIn -Filter "userDisplayName eq 'Timothy Perkins'"` |
| Create Date Time | `Get-MgAuditLogSignIn -Filter "createdDateTime gt 2023-04-18T17:30:00.0Z"` (Everything since 5:30 pm on 4/18) |
| Status | `Get-MgAuditLogSignIn -Filter "status/errorCode eq 50105"` |
| Application Display Name | `Get-MgAuditLogSignIn -Filter "appDisplayName eq 'StoreFrontStudio [wsfed enabled]'"` |
| All of the above | `Get-MgAuditLogSignIn -Filter "userDisplayName eq 'Timothy Perkins' and status/errorCode ne 0 and appDisplayName eq 'StoreFrontStudio [wsfed enabled]'"` |
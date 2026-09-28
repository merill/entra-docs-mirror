---
layout: Conceptual
title: Backup, difference report, and recovery model in Microsoft Entra Backup and Recovery - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/backup/backup-difference-report-recovery-model
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id
manager: dougeby
description: Understand how Microsoft Entra Backup and Recovery creates backups, generates difference reports, and recovers tenant objects to a previous state
ms.date: 2026-08-25T00:00:00.0000000Z
ms.topic: concept-article
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1023
locale: en-us
document_id: c8de0803-3665-8d68-e778-09848f7b0312
document_version_independent_id: c8de0803-3665-8d68-e778-09848f7b0312
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/backup/backup-difference-report-recovery-model.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: backup/backup-difference-report-recovery-model
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/backup/backup-difference-report-recovery-model.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 06b86416-4fef-c871-11a8-b32a07581c1d
---

# Backup, difference report, and recovery model in Microsoft Entra Backup and Recovery - Microsoft Entra | Microsoft Learn

Microsoft Entra Backup and Recovery automatically backs up supported tenant objects so you can compare changes and recover to a previous state. Supported objects include:

- Users, including agents' user accounts
- Groups
- Applications, including agent identity blueprints
- Service principals, including agent identities and agent identity blueprint principals
- Conditional access policies
- Named location policies
- Authentication method policy
- Authorization policy
- Organization

For a full list of supported attributes, see [Supported objects and attributes](scope-supported-objects-limitations).

Backups are created automatically once per day. Select from retained backups when you create a difference report or start recovery.

## Difference reports

Create a difference report to compare the current state of your tenant with a selected backup. Only changed objects appear in the report, with changed attributes and links shown for review. Apply filters to view changes for a specific object type or a specific object. If you don't apply a filter, all changed objects are included in the difference report.

Changes for users and groups synchronized from on-premises Active Directory appear in the difference report to help you track changed objects. However, you can't recover on-premises synced objects through Backup and Recovery, because the source of authority for these objects is on-premises Active Directory.

### First-time difference report generation

The first time you create a difference report, you might experience a delay as backup data loads before the difference calculation starts. Check the progress of report generation in the **Difference Reports** section.

| Tenant size | Estimated data loading time for first-time report generation |
| --- | --- |
| 1-50,000 objects | Up to 1 hour |
| 50,000-300,000 objects | Up to 1 hour 30 minutes |
| 300,000-1,000,000 objects | Up to 2 hours |
| More than 1,000,000 objects | Up to 2 hours and 30 minutes |

The second time you create a difference report against the same backup, the report doesn't need the data loading step, so it finishes faster.

Difference calculation depends on the changes that have happened between the backup state and the current state. For 100,000 object and/or link changes, full report generation could take approximately 45 minutes to complete.

Note

Time estimates are approximate and provided for general planning purposes only. Actual performance might differ significantly based on concurrent network activities, resource availability, and tenant size.

## Recovery

When you recover your tenant, apply filters to control which objects to recover:

- **By object type**: Recover only objects of a certain type, such as users, groups, applications, service principals, or Conditional Access policies.
- **By object ID**: Supply the object type and object ID to recover a specific object.
- **All changes**: Recover all changed objects to the state captured in the selected backup.

Recovery performance depends on the number of changes to be recovered. Recovering 500,000 changes can take up to 30 hours.

Note

Time estimates are approximate and provided for general planning purposes only. Actual performance might differ significantly based on concurrent network activities, resource availability, and tenant size.

Important

Only one job can run at a time, including difference reports and recovery jobs. For example, if a difference report is running in your tenant, you can't start a recovery job. Wait until the current job finishes before starting a new one.

## Recovery model

The type of change from the backup state determines the recovery action:

| Change since backup | Recovery action |
| --- | --- |
| Object was added | Backup and Recovery soft-deletes the object |
| Object was updated | Backup and Recovery updates the object to the backup value |
| Object was soft-deleted | Backup and Recovery restores the object |
| Object was restored | Backup and Recovery soft-deletes the object |

Backup and Recovery doesn't create new objects or hard-delete objects from your tenant.

Warning

Hard-deleted objects can't be recovered. Configure [protected actions](/en-us/entra/identity/role-based-access-control/protected-actions-overview) to prevent unwanted hard deletions.

For soft-deleted users, Microsoft 365 Groups, cloud security groups, application registrations, and service principals, you can also use [soft deletion](soft-deletion) within the 30-day retention window.

On-premises synchronized objects can't be recovered through Backup and Recovery, because the source of authority is on-premises Active Directory. Recover these objects in on-premises Active Directory instead. Changes to synced objects still appear in difference reports.

Microsoft Entra Backup and Recovery is available for workforce tenants only. Microsoft Entra External ID tenants and Azure AD B2C tenants aren't supported.

Microsoft Entra Backup and Recovery backs up and recovers Microsoft Entra directory objects. Microsoft 365 resources, such as mailboxes, OneDrive, or SharePoint sites, and Azure resources aren't backed up by Microsoft Entra Backup and Recovery.
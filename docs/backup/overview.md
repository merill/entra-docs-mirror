---
layout: Conceptual
title: Microsoft Entra Backup and Recovery overview - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/backup/overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id
manager: dougeby
description: Learn how Microsoft Entra Backup and Recovery helps you recover from malicious attacks or accidental changes to tenant objects
ms.date: 2026-03-02T00:00:00.0000000Z
ms.topic: overview
ai-usage: ai-assisted
locale: en-us
document_id: adb10229-e9b1-33ea-9f06-834e1d0059cd
document_version_independent_id: adb10229-e9b1-33ea-9f06-834e1d0059cd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/backup/overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: backup/overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/backup/overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ff24cfdf-fe4e-fb2f-515c-c36da847b809
---

# Microsoft Entra Backup and Recovery overview - Microsoft Entra | Microsoft Learn

Microsoft Entra Backup and Recovery is a built-in backup and recovery solution that lets you recover critical Microsoft Entra directory objects to a previously known good state after accidental changes or security compromises. Supported objects include users, groups, apps, service principals, Conditional Access policies, named locations, authentication method policy, and authorization policy (selected properties). The solution also supports Agent ID because it consists of user and service principal objects with distinct types and characteristics.

## How backups work

Microsoft Entra Backup and Recovery takes backups of supported objects automatically, once a day, retaining up to seven days of backup history. The solution helps restore your tenant to a productive and secure state. Microsoft regularly improves and expands the solution to support more directory objects and more attributes.

Microsoft creates backups automatically and makes them available to administrators with sufficient permissions. No signed-in user or application, even with the highest admin privileges, can turn off, delete, or modify backups in the tenant. Backup data resides securely in the same [geo-location as the Microsoft Entra tenant](/en-us/entra/fundamentals/data-residency), determined during tenant creation.

## Key capabilities

Microsoft Entra Backup and Recovery lets you:

- **View available backups**: See a list of backups available in your Microsoft Entra tenant.
- **Create difference reports**: Before recovering objects to a previous state, compare the current state of your tenant with a backup and review changed attributes and links.
- **Recover objects**: Recover all supported objects, selected object types, or specific object IDs.
- **Review recovery history**: View completed and in-progress recovery operations for your tenant.

Tip

To ensure you recover to the right backup, always run a difference report, review the changes, and then decide what to recover. The time to recover mostly depends on the number of changes in the recovery job.

## Get started

To get started, browse to the [Microsoft Entra admin center](https://entra.microsoft.com) and select **Backup and recovery** in the left navigation pane. These pages are available:

- **Overview**: View a summary of the backup and recovery feature.
- **Backups**: Browse available backups from the last seven days.
- **Difference Reports**: Create and review reports that compare a backup with the current tenant state.
- **Recovery History**: View completed and in-progress recovery operations for your tenant.

## Prerequisites

To use Microsoft Entra Backup and Recovery, your tenant must meet these requirements:

- The tenant is a **workforce tenant**. External ID and Azure AD B2C tenants aren't supported.
- The tenant has **Microsoft Entra ID P1 or P2** licenses.
- You're signed in with one of these roles:
    - **Microsoft Entra Backup Reader**: Can view backups, view comparisons of changed objects between the backup state and the current state, and review recovery history.
    - **Microsoft Entra Backup Administrator**: Has all the permissions of Microsoft Entra Backup Reader, plus can initiate difference reports and trigger recovery for changed objects. All the permissions of Microsoft Entra Backup Administrator are included in the Global Administrator role.

## Hybrid identity and broader recoverability

Organizations that use hybrid identity with Microsoft Entra ID can create difference reports to identify changes to objects synchronized from Active Directory Domain Services (AD DS). For certain object types, such as groups, you can move the source of authority from AD DS to the cloud. This makes all Microsoft Entra Backup and Recovery functionality available for those converted objects. Use an alternative solution to back up and recover objects managed in AD DS.

Soft-deleted users, Microsoft 365 Groups, cloud security groups, application registrations, and service principals can be restored for 30 days. For more information about how soft deletion relates to Backup and Recovery, see [Soft deletion in Microsoft Entra Backup and Recovery](soft-deletion). Backup and Recovery restores supported properties and links from retained backups and complements soft-delete recovery.

Microsoft Entra Backup and Recovery doesn't support the recovery or re-creation of hard-deleted objects.

Use Microsoft Entra Backup and Recovery as part of a broader approach to recoverability that helps your organization be more resilient. For more information about limitations, hybrid scenarios, and recoverability best practices, see [Supported objects and recoverable properties](scope-supported-objects-limitations).
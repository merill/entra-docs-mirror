---
layout: Conceptual
title: Event enrichment in Microsoft 365 enriched logs - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/reference-event-enrichment-logs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Global Secure Access includes Microsoft Entra Private Access and Microsoft Entra Internet Access. This article references event enrichment in Microsoft 365 enriched logs.
ms.topic: reference
ms.date: 2026-03-13T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 6a938491-fbec-991d-389c-0cb45c523768
document_version_independent_id: 6a938491-fbec-991d-389c-0cb45c523768
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/reference-event-enrichment-logs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/reference-event-enrichment-logs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/reference-event-enrichment-logs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
- https://authoring-docs-microsoft.poolparty.biz/devrel/7428317a-e6c2-4461-ad3e-8a8ad3608734
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
- https://authoring-docs-microsoft.poolparty.biz/devrel/e4f59707-f107-48f2-8d75-0afd91868cd7
platformId: 312241bf-3543-1b46-1d62-29ac06a5ad27
---

# Event enrichment in Microsoft 365 enriched logs - Global Secure Access | Microsoft Learn

## Overview

Event enrichment uses Microsoft 365 enriched logs to bring events across different workloads into sharper focus. The result is nuanced insights that are essential for improved security and improved efficiency. Events are carefully chosen and several factors are used to select them. These factors include priority ranking, relevance to security landscapes, and how useful these events are for Sentinel or Defender.

In the future, event coverage is set to broaden, increasing the scope of the security narrative.

## SharePoint Online (preview)

| # | Workload | Operation |
| --- | --- | --- |
| 1 | OneDrive | `FileDeleted` |
| 2 | SharePoint | `FileDeleted` |
| 3 | SharePoint | `FileDeletedFirstStageRecycleBin` |
| 4 | OneDrive | `FileDeletedFirstStageRecycleBin` |
| 5 | OneDrive | `FileDownloaded` |
| 6 | SharePoint | `FileDownloaded` |
| 7 | SharePoint | `FileRecycled` |
| 8 | OneDrive | `FileRecycled` |
| 9 | OneDrive | `FileUploaded` |
| 10 | SharePoint | `FileUploaded` |
| 11 | OneDrive | `ListItemDeleted` |
| 12 | SharePoint | `ListItemRecycled` |

## Teams (limited preview)

| # | Workload | Operation |
| --- | --- | --- |
| 1 | Teams | `AppInstalled` |
| 2 | Teams | `BotAddedToTeam` |
| 3 | Teams | `MemberAdded` |
| 4 | Teams | `MemberRemoved` |
| 5 | Teams | `MemberRoleChanged` |
| 6 | Teams | `TeamDeleted` |
| 7 | Teams | `TeamsAdminAction` |

## Exchange (limited preview)

| # | Workload | Operation |
| --- | --- | --- |
| 1 | Exchange | `New-InboxRule` |
| 2 | Exchange | `New-ManagementRoleAssignment` |
| 3 | Exchange | `New-TransportRule` |
| 4 | Exchange | `Set-AdminAuditLogConfig` |
| 5 | Exchange | `Set-AtpPolicyForO365` |
| 6 | Exchange | `Set-CrossTenantAccessPolicy` |
| 7 | Exchange | `Set-OrganizationConfig` |
| 8 | Exchange | `Set-SharingPolicy` |
| 9 | Exchange | `Set-TransportRule` |

Note

This preview showcases a number of events pivotal to improving security postures and operational capabilities. While the coverage herein is preliminary, it is subject to change without notice as we continue to refine and expand our event enrichment repertoire for Microsoft 365 enriched logs.
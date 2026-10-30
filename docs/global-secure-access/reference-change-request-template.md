---
layout: Conceptual
title: Global Secure Access change request template - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/reference-change-request-template
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Template for documenting and tracking configuration changes to Microsoft Entra Global Secure Access.
ms.topic: reference
ms.date: 2026-05-04T00:00:00.0000000Z
ms.reviewer: tdetzner
ai-usage: ai-assisted
locale: en-us
document_id: efcc9cd2-8648-821a-9d95-a71d714ea148
document_version_independent_id: efcc9cd2-8648-821a-9d95-a71d714ea148
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/reference-change-request-template.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/reference-change-request-template
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/reference-change-request-template.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 96f1f74b-87eb-70d1-86a8-0b2cf392dea6
---

# Global Secure Access change request template - Global Secure Access | Microsoft Learn

Use this template for all **normal** and **major** changes to Global Secure Access configuration. For change categories and the execution process, see the [Common operations guide](how-to-operations-common#change-management).

## Change request details

| Field | Value |
| --- | --- |
| **Change ID** | *(your IT service management (ITSM) ticket number or sequential ID)* |
| **Date submitted** |  |
| **Requested by** |  |
| **Change category** | Standard / Normal / Emergency / Major |
| **Priority** | Low / Medium / High / Critical |
| **Target date** |  |
| **Maintenance window required** | Yes / No |

## Description

**What is being changed?**

*(Describe the specific configuration change in detail. Include the Global Secure Access capability affected: Private Access, Internet Access, Remote Networks, or Microsoft Traffic.)*

**Why is this change needed?**

*(Business justification, user request, security requirement, or compliance need.)*

## Scope and impact

**Affected Global Secure Access capability:**

- Private Access
- Internet Access
- Remote Networks
- Microsoft Traffic
- Common / Cross-cutting

**Affected components:**

*(List specific components: connector groups, application segments, web filtering policies, traffic forwarding rules, tunnels, etc.)*

**Affected users / sites:**

*(Estimate the number of users or sites impacted. List specific groups or locations if known.)*

**Expected user impact during change:**

- No user impact
- Brief reconnection (&lt; 1 minute)
- Service interruption during maintenance window
- Extended impact—communication plan required

## Risk assessment

| Risk factor | Assessment |
| --- | --- |
| **Risk level** | Low / Medium / High |
| **Potential for service disruption** | None / Minimal / Moderate / High |
| **Reversibility** | Fully reversible / Partially reversible / Irreversible |

**What could go wrong?**

*(Describe the worst-case scenario if the change fails.)*

## Testing

**Tested in non-production?** Yes / No / Not applicable

**Test results:**

*(Describe testing performed and outcomes. If not tested, explain why.)*

## Prechange checklist

- Configuration backup completed (see capability guide for export scripts)
- Change approved by Service Owner or Change Advisory Board
- Communication sent to affected users and support teams (if necessary)
- Rollback plan documented (see Rollback plan)
- Maintenance window scheduled (if necessary)
- On-call engineer confirmed for maintenance window

## Rollback plan

**How to roll back if the change fails:**

*(Step-by-step procedure to restore the previous configuration. Reference the backup file created in the prechange checklist.)*

**Maximum time to decide on rollback:**

*(How long to wait before deciding the change failed and needs to be rolled back.)*

## Execution

| Step | Action | Completed | Notes |
| --- | --- | --- | --- |
| 1 | Back up current configuration | [ ] |  |
| 2 | *(Add change steps)* | [ ] |  |
| 3 | *(Add change steps)* | [ ] |  |
| 4 | Verify change—check traffic logs, alerts, and user connectivity | [ ] |  |
| 5 | Confirm rollback isn't needed | [ ] |  |

## Post-change verification

- Traffic logs show expected behavior
- No new alerts triggered
- User access confirmed for affected applications / sites
- Change documented in ITSM system

## Approvals

| Role | Name | Approved | Date |
| --- | --- | --- | --- |
| Service Owner |  | Yes / No |  |
| Network Security Engineer |  | Yes / No |  |
| Change Advisory Board (if major) |  | Yes / No |  |

**Post-change notes:**
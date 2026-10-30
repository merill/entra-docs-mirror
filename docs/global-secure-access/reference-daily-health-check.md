---
layout: Conceptual
title: Global Secure Access daily health check - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/reference-daily-health-check
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Consolidated daily health check checklist for all Microsoft Entra Global Secure Access capabilities.
ms.topic: reference
ms.date: 2026-05-04T00:00:00.0000000Z
ms.reviewer: tdetzner
ai-usage: ai-assisted
locale: en-us
document_id: 7a8b9346-9169-d6af-0b00-9d0a7fe8197c
document_version_independent_id: 7a8b9346-9169-d6af-0b00-9d0a7fe8197c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/reference-daily-health-check.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/reference-daily-health-check
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/reference-daily-health-check.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: d5150446-bc3c-15b1-45a0-a17a483acae5
---

# Global Secure Access daily health check - Global Secure Access | Microsoft Learn

Use this checklist every business day. Record results and escalate any failed checks per the "What to do" column.

**Date:** \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ **Completed by:** \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

## Private Access

| # | Check | Status | What to do if it fails |
| --- | --- | --- | --- |
| 1 | All connectors show **Active** in Microsoft Entra admin center &gt; Global Secure Access &gt; Connect &gt; Connectors | Pass / Fail | Restart the connector service. If unresolved, check network connectivity and Windows Event Logs on the connector host. |
| 2 | No unassigned P1/P2 Private Access alerts in Sentinel | Pass / Fail | Assign and investigate. Escalate alerts older than 4 hours. |
| 3 | Audit logs reviewed—no unauthorized configuration changes | Pass / Fail | Flag unrecognized changes. Verify each change maps to an approved change request. |

## Internet Access

| # | Check | Status | What to do if it fails |
| --- | --- | --- | --- |
| 4 | Internet Access traffic forwarding profile is enabled | Pass / Fail | Re-enable the profile. Check audit logs for who disabled it. |
| 5 | No unassigned P1/P2 Internet Access alerts in Sentinel | Pass / Fail | Assign and investigate. Escalate alerts older than 4 hours. |
| 6 | Spot-check top 10 blocked URLs—verify they should be blocked | Pass / Fail | Adjust policies or add exceptions for legitimate business sites. |

## Remote Networks

| # | Check | Status | What to do if it fails |
| --- | --- | --- | --- |
| 7 | All tunnels show **Connected** in Microsoft Entra admin center &gt; Global Secure Access &gt; Connect &gt; Remote networks | Pass / Fail | Check the customer premises equipment (CPE) device status and internet service provider (ISP) connectivity at the affected branch. |
| 8 | No unassigned P1/P2 Remote Networks alerts in Sentinel | Pass / Fail | Assign and investigate. Escalate alerts older than 4 hours. |
| 9 | Traffic volumes for major sites are within baseline range | Pass / Fail | Investigate significant drops (possible outage) or spikes (possible anomaly). |

## Microsoft Traffic

| # | Check | Status | What to do if it fails |
| --- | --- | --- | --- |
| 10 | Microsoft traffic forwarding profile is enabled | Pass / Fail | Re-enable the profile. Check audit logs for who disabled it. |
| 11 | No user-reported Microsoft 365 performance issues in the help desk queue | Pass / Fail | If reported, compare Global Secure Access traffic logs with the Microsoft 365 service health dashboard. |
| 12 | Spot-check sign-in logs for compliant network enrichment | Pass / Fail | Verify the Global Secure Access client is running on affected devices and the compliant network check is configured. |

## Cross-cutting

| # | Check | Status | What to do if it fails |
| --- | --- | --- | --- |
| 13 | Azure Service Health and Microsoft 365 service health—no reported Global Secure Access service issues | Pass / Fail | If Microsoft reports an issue, communicate it to your operations team and follow the published mitigation guidance. |
| 14 | All scheduled automation jobs (backups, reports) ran without errors | Pass / Fail | Troubleshoot the failed job. Run the backup or report manually if needed. |

**Notes / issues observed:**
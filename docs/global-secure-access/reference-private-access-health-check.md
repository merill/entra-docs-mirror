---
layout: Conceptual
title: Private Access health check checklist - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/reference-private-access-health-check
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Daily, weekly, and monthly health check checklist for Microsoft Entra Private Access operations.
ms.topic: reference
ms.date: 2026-05-04T00:00:00.0000000Z
ms.reviewer: tdetzner
ai-usage: ai-assisted
locale: en-us
document_id: 59b87d5c-096a-b0d7-30d3-41d7d27ec2d1
document_version_independent_id: 59b87d5c-096a-b0d7-30d3-41d7d27ec2d1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/reference-private-access-health-check.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/reference-private-access-health-check
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/reference-private-access-health-check.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 6918f410-2417-57fd-0925-d08f958a5ff7
---

# Private Access health check checklist - Global Secure Access | Microsoft Learn

Use this checklist to maintain the health of your Microsoft Entra Private Access environment. For the consolidated daily health check covering all Global Secure Access (GSA) capabilities, see the [daily health check template](reference-daily-health-check). Cross-references in this checklist link to Kusto Query Language (KQL) queries in the Private Access operations guide.

## Daily checks

**Date:** \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ **Completed by:** \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

| # | Check | How | Status | What to do if it fails |
| --- | --- | --- | --- | --- |
| 1 | All connectors **Active** | Microsoft Entra admin center &gt; **Global Secure Access** &gt; **Connect** &gt; **Connectors** | Pass / Fail | Restart the `Microsoft Entra private network connector` service. Check outbound connectivity to `*.msappproxy.net:443`. Review Windows Event Logs on the connector host. |
| 2 | Connector resource utilization normal | Check CPU and memory on each connector host via your monitoring tool | Pass / Fail | If CPU &gt; 80% or memory &gt; 85%, investigate high-traffic applications and consider adding a connector to the group. |
| 3 | No unassigned P1/P2 alerts | Review Private Access alerts in Sentinel or your security information and event management (SIEM) platform from the last 24 hours | Pass / Fail | Assign and begin investigation. Escalate alerts unassigned for more than 4 hours. |
| 4 | Audit log—no unauthorized changes | Run the [audit log KQL query](how-to-operate-private-access#kql-queries-for-private-access-monitoring) for the last 24 hours | Pass / Fail | Verify each change maps to an approved change request. Flag unrecognized changes and investigate. |
| 5 | Application access success rate normal | Spot-check `NetworkAccessTraffic` for Private Access denials in the last 24 hours | Pass / Fail | Identify affected users and apps. Determine if the denials are policy-related (adjust policy) or security-related (escalate to SOC). |
| 6 | Quick Access and per-app segments reachable | Verify key applications are accessible (manual test or synthetic monitoring) | Pass / Fail | Check the application segment configuration. Test DNS resolution and connectivity from the connector host to the backend server. |

**Daily notes:**

## Weekly checks

**Week of:** \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ **Completed by:** \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

| # | Check | How | Status | What to do if it fails |
| --- | --- | --- | --- | --- |
| 1 | Connector group load distribution | Run the [connector group load KQL query](how-to-operate-private-access#kql-queries-for-private-access-monitoring)—look for hot connectors | Pass / Fail | If one connector handles more traffic, check connector group assignments and consider rebalancing. |
| 2 | Policy efficacy review | Review top denied applications and users in the Sentinel workbook | Pass / Fail | Adjust policies for persistent false positives (legitimate traffic blocked). Investigate repeated unauthorized access attempts. |
| 3 | Configuration backup completed | Verify the [weekly configuration export](how-to-operate-private-access#export-private-access-configuration-via-graph-api) ran successfully and output is stored | Pass / Fail | Run the export manually. Troubleshoot the automation runbook. |
| 4 | Application segment inventory | Compare active segments (both Quick Access and per-app) against your application inventory | Pass / Fail | Add segments for newly onboarded apps. Flag stale segments for decommissioned apps (review before removing). |
| 5 | Cross-correlation review | Run the [cross-correlation KQL query](how-to-operate-private-access#kql-queries-for-private-access-monitoring)—denied connections + identity risk | Pass / Fail | Investigate users with both denied connections and elevated risk. Escalate confirmed threats to SOC. |
| 6 | Connector host OS health | Check for pending OS patches, disk space, and certificate expiration on connector hosts | Pass / Fail | Schedule patching during maintenance windows. Patch one connector at a time per group. Free disk space or extend storage. |

**Weekly notes:**

## Monthly checks

**Month:** \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ **Completed by:** \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

| # | Check | How | Status | What to do if it fails |
| --- | --- | --- | --- | --- |
| 1 | Connector software version | Compare installed version on each host against the [latest available version](/en-us/entra/global-secure-access/concept-connectors) | Pass / Fail | Schedule connector updates during a maintenance window. Update one connector at a time per group. |
| 2 | Failover validation | Follow the [failover validation procedure](how-to-operate-private-access#failover-validation) during a scheduled maintenance window | Pass / Fail | Investigate connector group assignment and network routing. Don't run in production without a maintenance window. |
| 3 | Role-based access control (RBAC) review | Review accounts with Global Secure Access Administrator or related roles in the Microsoft Entra admin center | Pass / Fail | Remove access for accounts that no longer require it. Verify all admin accounts use phishing-resistant MFA. |
| 4 | Capacity assessment | Review 30-day trend of concurrent sessions and bandwidth per connector group against [capacity thresholds](how-to-operate-private-access#capacity-thresholds) | Pass / Fail | If any group is consistently above 70%, plan to add connectors. Use the [Private Access Sizing Planner](https://github.com/FranckhDev/GSA-Private-Access-Sizing-Planner). |
| 5 | Stale segment cleanup | Identify application segments with zero traffic in the last 90 days using [automation playbook #6](how-to-operate-private-access#automation-playbooks) | Pass / Fail | Review with application owners before removing. Document removed segments. |
| 6 | Performance baseline comparison | Compare current month's traffic patterns against the [30-day baseline](how-to-operate-private-access#kql-queries-for-private-access-monitoring) | Pass / Fail | Investigate significant deviations. Update baseline if traffic growth is expected (for example, new user populations onboarded). |
| 7 | DR/fallback plan review | Confirm your fallback connectivity plan is documented and contacts are current | Pass / Fail | Update the plan. If no plan exists, create one per [maintenance and health checks](how-to-operate-private-access#maintenance-and-health-checks). |

**Monthly notes:**
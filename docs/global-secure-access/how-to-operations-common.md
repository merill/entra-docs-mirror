---
layout: Conceptual
title: Common operations for Microsoft Entra Global Secure Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-operations-common
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Shared operational guidance for Global Secure Access covering roles, change management, metrics and reporting, and continuous improvement.
ms.topic: how-to
ms.date: 2026-05-04T00:00:00.0000000Z
ms.reviewer: jricketts
ai-usage: ai-assisted
locale: en-us
document_id: c3466b76-f4cc-2681-7fbe-a23e63ce4cca
document_version_independent_id: c3466b76-f4cc-2681-7fbe-a23e63ce4cca
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-operations-common.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-operations-common
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-operations-common.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 6d395d5a-6b1c-3d83-a8c7-942a67ae0156
---

# Common operations for Microsoft Entra Global Secure Access - Global Secure Access | Microsoft Learn

This guide is the operational foundation for running Microsoft Entra Global Secure Access (GSA). Start here to establish the team structure, change management process, metrics framework, and reporting cadence that every capability guide builds on. The capability guides assume you have these cross-cutting practices in place.

For capability-specific operations, see the individual guides:

- [Private Access operations](how-to-operate-private-access)
- [Internet Access operations](how-to-operate-internet-access)
- [Remote Networks operations](how-to-operate-remote-networks)
- [Microsoft Traffic operations](how-to-operate-microsoft-traffic)

For initial deployment and configuration, see the [Global Secure Access deployment guide](/en-us/entra/architecture/gsa-deployment-guide-intro). For identity-layer security investigations and incident response, see the [Microsoft Entra Security Operations Guide](https://aka.ms/AzureADSecOps).

## Roles and responsibilities

The following section lists the roles that operate GSA and presents a Responsible / Accountable / Consulted / Informed (RACI) matrix that maps each operational activity to the role that owns it.

### RACI matrix

Assign clear ownership for GSA operations. The following RACI matrix defines who is **R**esponsible, **A**ccountable, **C**onsulted, and **I**nformed for key operational activities.

| Activity | Service Owner | Network Security Engineer | Identity Engineer | SOC Analyst | IT Support / Help desk | Platform Ops / Monitoring |
| --- | --- | --- | --- | --- | --- | --- |
| Approve policy changes | A | R | C | C | I | I |
| Configure access policies | I | R | C | C | — | I |
| Manage Conditional Access policies for GSA | I | C | R | C | — | I |
| Manage GSA service principals and enterprise apps | I | C | R | — | — | I |
| Troubleshoot authentication and sign-in failures | I | C | R | C | C | I |
| Monitor alerts and health | I | C | C | R | — | R |
| Respond to connector/tunnel alerts | A | R | I | I | I | R |
| Investigate security incidents | I | C | C | R | — | C |
| Handle user access issues (Tier 1) | — | C | C | — | R | — |
| Manage configuration backups | A | R | C | — | — | R |
| Conduct change reviews | A | R | C | C | I | C |
| Perform failover testing | A | R | C | — | I | R |
| Manage role-based access control (RBAC) and admin access | A | R | C | C | — | — |
| Produce operational reports | A | C | C | C | — | R |
| Drive continuous improvement | A | R | C | C | I | R |

### Role descriptions

| Role | Key responsibilities |
| --- | --- |
| **Service Owner / GSA Administrator** | Overall accountability for GSA performance, compliance, and alignment with business requirements. Approves significant changes. Coordinates across identity, endpoint, and networking teams. |
| **Network Security Engineer** | Day-to-day administration: access policies, routing rules, connector/tunnel management, certificate management. Tests changes before production deployment. Escalation point for complex IT Support/Help desk issues. |
| **Identity Engineer / Identity Team** | Owns the Microsoft Entra ID tenant as it intersects with GSA. Manages Conditional Access policies that gate GSA traffic profiles and compliant-network enforcement. Administers GSA service principals and enterprise app registrations (CRUD). Troubleshoots authentication, token, and sign-in failures using Microsoft Entra sign-in logs. Partners with SOC Analyst on identity-related incidents. |
| **SOC Analyst** | Monitors security alerts. Investigates suspicious events. Fine-tunes analytics rules in Sentinel. Handles or escalates GSA-related security incidents. For detailed SecOps procedures, see the [Microsoft Entra Security Operations Guide](https://aka.ms/AzureADSecOps). |
| **IT Support / Help desk** | Tier-1 support for user access issues (client installation, connectivity problems). Follows runbooks and escalates to Network Security Engineer for complex issues. |
| **Platform Ops / Monitoring Engineer** | Oversees infrastructure health: dashboards, connector/tunnel uptime, automation scripts, and configuration backup processes. |

Tip

Cross-train at least two people for each role to avoid single points of failure. Document escalation paths and on-call rotations for after-hours coverage.

## Change management

Apply a consistent change management process for all GSA configuration changes, including a category framework, execution procedures, and a configuration backup strategy.

### Change categories

| Category | Definition | Examples | Approval required | Maintenance window |
| --- | --- | --- | --- | --- |
| **Standard** | Routine, low-risk changes that follow a preapproved procedure | Adding users to an existing policy group, updating a URL in an allow list | Preapproved (no per-change approval) | No |
| **Normal** | Changes that could affect service behavior and require review | Modifying web filtering policies, adding application segments, changing traffic forwarding rules | Service Owner or Change Advisory Board | Recommended |
| **Emergency** | Urgent changes to address an active threat or outage | Blocking a malicious URL category, disabling a compromised connector | Execute immediately; document and review after | No (but post-change review required) |
| **Major** | High-impact changes affecting many users or core architecture | Enabling a new traffic profile, restructuring connector groups, onboarding a major site | Change Advisory Board | Required |

Important

**Standard** changes are preapproved at the *category* level, not the *change* level. Each Standard change—especially **allow-list additions and removals**—must still record an explicit owner approval in the ITSM ticket, set an expiration or review date so entries don't become permanent by default, and be captured in the audit log. Without these guardrails, the "preapproved" path becomes an audit gap.

### Change execution process

For **normal** and **major** changes:

1. **Submit a change request**—Document the change description, rationale, affected components, risk assessment, rollback plan, and testing results. Use the [change request template](reference-change-request-template).
2. **Test in a non-production environment**—If possible, validate the change in a test tenant or with a pilot user group.
3. **Gain approval**—Route to the Service Owner (for normal changes) or Change Advisory Board (for major changes).
4. **Back up current configuration**—Export the affected configuration using Graph API before making changes. See the configuration export scripts in each capability guide.
5. **Communicate**—Notify affected users and support teams. Use the [communication plan template](reference-communication-plan) for major changes.
6. **Execute during maintenance window**—For service-affecting changes, schedule during low-usage hours.
7. **Verify**—Confirm the change works as intended. Check traffic logs, alert status, and user connectivity.
8. **Document**—Record the change outcome in your IT service management (ITSM) system. Close the change request.

For **emergency** changes:

1. Execute the change immediately to address the threat or outage.
2. Document the change within 24 hours (use the change request template retrospectively).
3. Review in the next scheduled change management meeting.
4. Update procedures if the emergency revealed a gap.

### Configuration backup strategy

GSA configuration lives in two places:

- **GSA-specific Graph resources**: connector groups, traffic forwarding profiles, remote networks, and filtering policies.
- **Surrounding Microsoft Entra ID objects** that gate and support GSA: Conditional Access policies, named locations, service principals, and app role assignments.

Use two complementary mechanisms: **Graph API JSON exports** for GSA-specific resources and long-term retention, and the **Microsoft Entra Backup and Recovery APIs** for tenant-wide Microsoft Entra ID objects and scoped restore.

#### GSA-specific resources — Graph API JSON export

Back up GSA configurations on a weekly automated schedule and before every normal or major change. Use the Graph API PowerShell export scripts in each capability guide:

- [Private Access configuration](how-to-operate-private-access#export-private-access-configuration-via-graph-api) (for example, connector groups, application segments)
- [Internet Access configuration](how-to-operate-internet-access#export-internet-access-configuration-via-graph-api) (for example, web filtering policies)
- [Remote Networks configuration](how-to-operate-remote-networks#export-remote-network-configuration-via-graph-api)
- [Microsoft Traffic profile configuration](how-to-operate-microsoft-traffic#export-microsoft-traffic-profile-configuration-via-graph-api)

#### GSA-related Microsoft Entra ID objects — Microsoft Entra Backup and Recovery

Microsoft Entra ID provides a native [Backup and Recovery service](/en-us/graph/api/resources/entrarecoveryservices-backup-recovery-overview?view=graph-rest-beta&amp;preserve-view=true) (beta) that takes an automatic daily snapshot of supported directory objects and allows scoped restore. The snapshots cover objects that directly affect GSA:

- **Conditional Access policies**—policies that gate GSA traffic profiles and compliant-network enforcement
- **Named location policies**—named locations referenced by CA rules (including the GSA-managed compliant network location)
- **Applications and service principals**—GSA enterprise apps, app registrations, and linked managed identities
- **App role assignments and OAuth2 permission grants**—delegated/application permissions granted to GSA
- **Users and groups**—for role-assignable and app-assigned groups used by GSA policies

Important

Microsoft Entra retains **five days** of snapshots and takes **one snapshot per day**. Snapshots are noneditable and can't be exported. Continue running the GSA-specific JSON exports in a versioned store (Git repo or Azure Storage with soft delete) for long-term retention, audit trails, and point-in-time exports outside the five-day window.

Note

The Backup and Recovery APIs are in `/beta` and not supported for production use per Microsoft Graph versioning policy. Track GA announcements before building hard dependencies in recovery runbooks.

**Required Entra roles and permissions:**

- `Microsoft Entra Backup Reader`—list snapshots, view jobs, retrieve changes (delegated to the Identity Engineer and SOC Analyst roles)
- `Microsoft Entra Backup Administrator`—create preview jobs, create recovery jobs. Cancel jobs (restrict to named break-glass / change-approved operators)
- Graph permissions: see the individual API reference topics under `microsoft.graph.entraRecoveryServices`

Tip

Always run a **preview job** with scoped filters before executing a recovery job. Only one job (preview or recovery) can run per tenant at a time, so coordinate across the Identity and Network Security Engineer roles during an incident.

**Suggested playbooks:**

| Playbook | Purpose | Key Graph call |
| --- | --- | --- |
| Get-GsaEntraSnapshot.ps1 | List the most recent snapshots and record the ID used in an incident ticket. | `GET /directory/recovery/snapshots` |
| Start-GsaEntraRecoveryPreview.ps1 | Create a scoped preview job for Conditional Access policies, named locations, and GSA service principals. Scope defaults to the GSA-relevant entity types; override with `-EntityTypes` when needed. | `POST /directory/recovery/snapshots/{id}/recoveryPreviewJobs` |
| Invoke-GsaEntraRecovery.ps1 | After the preview is reviewed and approved, execute the recovery job with the same filter scope and log the outcome. Requires `-Force` or interactive confirmation. | `POST /directory/recovery/snapshots/{id}/recoveryJobs` |

Each playbook is authored in the numbered playbook format used across the guide (see script `.NOTES` header for Trigger, Required permissions, and references). For the end-to-end concept, see [Microsoft Entra Backup and Recovery overview](/en-us/entra/backup/overview).

Important

Store the GSA JSON exports in a secured location with versioning enabled (for example, an Azure Storage account with soft delete, or a Git repository). Retain at least 30 days of GSA-specific exports. Treat the Entra snapshot history as an extra five-day safety net, not a replacement.

## Metrics and reporting

### Metrics framework

Track operational metrics across all GSA capabilities. Each capability guide defines capability-specific key performance indicators (KPIs). This section provides the cross-cutting framework and reporting cadence.

#### Cross-cutting metrics

| Metric | How to measure | Target |
| --- | --- | --- |
| Overall GSA service availability | % time at least one operational path exists for each capability | &gt; 99.9% |
| Change success rate | Changes without rollback or incident / total changes | &gt; 95% |
| Mean time to detect (MTTD) | Time from issue occurrence to alert firing | &lt; 5 minutes |
| Mean time to respond (MTTR) | Time from alert to initial response action | &lt; 15 minutes (business hours) |
| Mean time to resolve | Time from alert to issue fully resolved | &lt; 4 hours (P1), &lt; 8 hours (P2) |
| Configuration backup compliance | Successful automated backups / scheduled backups | 100% |
| RBAC hygiene | % of admin accounts reviewed in the current quarter | 100% |
| Alert noise ratio | False positive or informational alerts / total alerts | &lt; 20% |

Important

During the first 30 days after deployment, establish performance baselines for each metric before setting alert thresholds. Use baseline data from normal operations to calibrate targets—this practice prevents alert fatigue from overly aggressive thresholds. Revisit baselines quarterly as your environment evolves.

#### Cross-cutting metric alerts

Aim to back every cross-cutting metric with an automated alert when it breaches its target. Where an automated signal isn't yet available (for example, change success rate, which depends on ITSM data), schedule a structured manual review and track converting it to an automated signal as an improvement action.

| Metric breach | How to detect | Where you see it | What to do next |
| --- | --- | --- | --- |
| Backup job failure or missed schedule | Azure Automation watchdog runbook (Test-GsaBackupCompliance.ps1) runs daily and checks for failed or missing backup jobs | Alert email to your ops distribution list; Automation Account job history in the Azure portal | 1. Check the failed job output in the Automation Account.2. Run the backup manually.3. Fix the root cause (expired credentials, API throttling, storage quota).4. Confirm the next scheduled run succeeds. |
| RBAC review overdue (&lt; 100% this quarter) | Scheduled runbook (Test-GsaRbacHygiene.ps1) runs weekly and queries Graph API for unreviewed admin role assignments | Alert email listing overdue accounts and their roles | 1. Review each flagged assignment in Microsoft Entra ID under **Roles and administrators**.2. Confirm that the role is still required and least-privileged, or remove access.3. Update the RBAC review log with the review date.4. If your organization uses Identity Governance, you can use Access Reviews or Privileged Identity Management role reviews for the same control. |
| Alert noise ratio &gt; 20% | Scheduled runbook (Test-GsaAlertNoiseRatio.ps1) runs weekly and queries Sentinel incident classifications | Alert email with noise ratio and top noisy analytics rules | 1. Open Sentinel &gt; Analytics.2. Tune or add exclusions to the noisiest rules.3. Reassess after the next reporting period. |
| Change success rate &lt; 95% | Manual—review your ITSM change records monthly | Your ITSM system (ServiceNow, Jira Service Management, or equivalent) | 1. Identify failed or rolled-back changes.2. Conduct root cause analysis on each.3. To prevent recurrence, update change procedures to address gaps.4. Report findings in the quarterly ops review. |
| MTTD &gt; 5 min or MTTR &gt; 15 min | Sentinel analytics rule on incident response times | Sentinel Incidents dashboard; alert email if rule fires | 1. Review the slow-response incidents.2. Check if alert routing or on-call assignment caused the delay.3. Adjust notification channels or escalation paths. |

Tip

Deploy the three automation runbooks (Test-GsaBackupCompliance.ps1, Test-GsaRbacHygiene.ps1, Test-GsaAlertNoiseRatio.ps1) to an Azure Automation Account with a system-assigned managed identity. Grant the identity `Log Analytics Reader` on your workspace, `Automation Job Operator` on the Automation Account, and the Microsoft Graph permissions `RoleManagement.Read.Directory` and `Mail.Send`. Schedule each runbook on its recommended cadence (daily for backup compliance, weekly for the others).

### Reporting cadence

| Audience | Cadence | Content | Format |
| --- | --- | --- | --- |
| **Operations team** | Weekly | Alert summary, health check results, open incidents, upcoming changes | Dashboard or brief email |
| **Service Owner / Management** | Monthly | Service availability trends, security efficacy (threats blocked), change success rate, capacity outlook | Slide deck or executive dashboard |
| **Security leadership** | Quarterly | Threat landscape impact, compliance posture, policy efficacy, cross-product integration value | Executive summary report |
| **Continuous improvement review** | Quarterly | Metric trends, incident postmortems, improvement action items, capacity planning | Meeting with action items |

### Reporting tools

The following tools provide operational visibility across all GSA capabilities. Configure dashboards for trend analysis and management reporting—primary issue detection should come from the alerts defined in each capability guide.

#### Global Secure Access dashboard

The built-in [Global Secure Access dashboard](/en-us/entra/global-secure-access/concept-traffic-dashboard) in the Microsoft Entra admin center provides a single-pane overview of all traffic flowing through the service. Navigate to **Global Secure Access** &gt; **Dashboard** to view:

- Traffic volume and trends across all profiles (Private Access, Internet Access, Microsoft Traffic)
- Top users and destinations
- Cross-tenant access activity
- Device status summary

#### Traffic logs

The [traffic logs](/en-us/entra/global-secure-access/how-to-view-traffic-logs) provide session-level detail for all GSA traffic. Navigate to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs** to filter by user, destination, policy action, and connection status. Traffic logs are also available in Log Analytics via the `NetworkAccessTraffic` table for Kusto Query Language (KQL) queries.

#### Remote network health logs

The [remote network health logs](/en-us/entra/global-secure-access/how-to-remote-network-health-logs) provide tunnel-level status and connectivity data for all branch sites. Navigate to **Global Secure Access** &gt; **Monitor** &gt; **Remote network health logs** to view:

- Tunnel connectivity status (connected, disconnected) per remote network
- Last state change timestamps
- Border Gateway Protocol (BGP) route status for each tunnel
- Source and destination IP addresses

Remote network health data is also available in Log Analytics via the `RemoteNetworkHealthLogs` table. Use this data for historical trend analysis and automated alerting on tunnel health.

#### Enriched Microsoft 365 logs

The [enriched Microsoft 365 logs](/en-us/entra/global-secure-access/how-to-view-enriched-logs) augment standard Microsoft 365 audit events with network context from GSA (source IP, device, user agent). Navigate to **Global Secure Access** &gt; **Monitor** &gt; **Enriched Microsoft 365 logs** to correlate Microsoft 365 activity with network-level details. These logs require the Microsoft traffic profile to be enabled.

#### Alerts

The [Global Secure Access alerts](/en-us/entra/global-secure-access/concept-alerts) view surfaces platform-level issues, including unhealthy connectors, configuration changes to traffic forwarding, and integration alerts from third-party security services. Navigate to **Global Secure Access** &gt; **Monitor** &gt; **Alerts**. When exported via Microsoft Entra diagnostic settings (`NetworkAccessAlerts` category), alerts are available in Log Analytics via the `NetworkAccessAlerts` table for KQL queries and Sentinel analytics rules.

#### Microsoft Sentinel workbooks

The **Global Secure Access** workbook in Microsoft Sentinel provides advanced operational dashboards with KQL-driven visualizations for traffic volume, denied sessions, and compliant network coverage. To access:

1. In Microsoft Sentinel, go to **Threat management** &gt; **Workbooks**.
2. Search for **Global Secure Access** and open the workbook.

Note

The workbook requires the Global Secure Access solution from the [Microsoft Sentinel content hub](/en-us/azure/sentinel/sentinel-solutions-catalog). If the workbook isn't visible, go to **Content management** &gt; **Content hub**, search for **Global Secure Access**, and install the solution.

Pin frequently used views to a shared [Azure dashboard](/en-us/azure/azure-portal/azure-portal-dashboards) for team-wide visibility.

#### Security Copilot

Use [Microsoft Security Copilot](/en-us/security-copilot/) to speed cross-product investigation and correlation when an alert spans Entra, Global Secure Access, and Microsoft Sentinel data sources. Don't use it as a replacement for the dashboards, logs, and alerting workflows described earlier in this section.

Prompt examples:

- *"Summarize the last 24 hours of Global Secure Access incidents by correlating Microsoft Entra sign-in logs, Global Secure Access traffic logs, and Microsoft Sentinel incidents; group the findings by user, application, and policy, and identify the likely root cause for each cluster."*
- *"Compare the last seven days of Global Secure Access alerts to the previous 30-day baseline and highlight the top anomalies across denied sessions, connector health, and Conditional Access failures."*
- *"Show me Global Secure Access configuration changes in the last 24 hours that coincide with a spike in user access failures or Microsoft Sentinel incidents."*

#### Graph API and PowerShell

Automate report generation with custom scripts that query Log Analytics via the [Azure Monitor Query API](/en-us/azure/azure-monitor/logs/api/overview) and output formatted reports. See the automated weekly report playbook for an example.

### Automated weekly report (example playbook)

#### Playbook 1: Automated weekly operations report

| Field | Value |
| --- | --- |
| **Trigger** | Azure Automation scheduled runbook (every Monday 06:00 UTC) |
| **Frequency** | Weekly |
| **Required permissions** | `Log Analytics Reader` on the GSA Log Analytics workspace; `Mail.Send` Graph API permission for the managed identity or service principal running the runbook |
| **Steps** | 1. Connect to Azure using the Automation Account managed identity.2. Query Log Analytics for the past seven days across all GSA capabilities (total alerts by severity from `NetworkAccessAlerts`, total and failed traffic sessions from `NetworkAccessTraffic`, Global Secure Access sign-ins from `SigninLogs` filtered on `IsThroughGlobalSecureAccess`, and remote network tunnel status from `RemoteNetworkHealthLogs`).3. Format the results into an HTML email body.4. Send the report via Microsoft Graph `Send-MgUserMail` to the operations distribution list.5. Log the execution result to the Automation Account job output. |
| **Script** | See the runbook code that follows. |

```powershell
# Weekly GSA Operations Report — Azure Automation Runbook
Connect-AzAccount -Identity

$workspaceId = "<your-log-analytics-workspace-id>"
$query = @"
let timeRange = 7d;
union
  (NetworkAccessAlerts | where TimeGenerated > ago(timeRange) | summarize AlertCount=count() by AlertSeverity=tostring(Severity)),
  (NetworkAccessTraffic | where TimeGenerated > ago(timeRange) | summarize TotalSessions=count(), FailedSessions=countif(ConnectionStatus == "Failed")),
  (SigninLogs | where TimeGenerated > ago(timeRange) and IsThroughGlobalSecureAccess == true | summarize TotalSignIns=count(), FailedSignIns=countif(ResultType != "0")),
  (RemoteNetworkHealthLogs | where TimeGenerated > ago(timeRange) | summarize ConnectedTunnels=countif(Status == "tunnelConnected"), DisconnectedTunnels=countif(Status == "tunnelDisconnected"))
"@

$results = Invoke-AzOperationalInsightsQuery -WorkspaceId $workspaceId -Query $query
# Format $results into HTML and send via Send-MgUserMail
```

Tip

Store report templates in your configuration backup repository. Update them as you add new metrics or capabilities.

## Continuous improvement

### Quarterly operations review

Conduct a quarterly review covering the following areas. Assign an owner and due date for every action item.

| Area | What to review |
| --- | --- |
| Metrics | Cross-cutting and capability-specific metric trends (improving, degrading, stable) |
| Incident postmortems | Root cause, detection method, response timeline, and recurrence prevention for each significant incident |
| Policy effectiveness | Alignment with business and compliance requirements; identify gaps or over-blocking |
| Capacity planning | Growth trends for connectors, tunnels, and licenses; plan expansions for next quarter |
| Feature adoption | Results of the monthly new feature and functionality review; schedule testing and adoption for approved candidates |
| Process improvement | Operational pain points; assign corrective action items |

### New feature and functionality review

Run a structured feature review every month and bring the outcome into the quarterly operations review. Use this review to track new Global Secure Access capabilities, preview announcements, deprecations, client and connector release changes, and any documented behavior changes that affect your operating model.

| Cadence | Role | Automated by | Procedure | What to do next |
| --- | --- | --- | --- | --- |
| Monthly | Service Owner + Network Security Engineer + Identity Engineer | Manual—documentation review | Review two sources for new features, preview announcements, deprecations, release notes, and breaking changes across all GSA capabilities: [What's new in Microsoft Entra](/en-us/entra/fundamentals/whats-new) and the [Global Secure Access documentation](/en-us/entra/global-secure-access/). Record each relevant item and map it to the affected capability guide. Assess operational impact, prerequisites, licensing impact, and rollout risk. | Create change requests for features that improve security posture or operational efficiency. Schedule testing for approved candidates, track preview items on the roadmap, and update runbooks, alert thresholds, and operating procedures when Microsoft changes service behavior or retires functionality. |

Tip

Use the capability guides to capture feature-specific actions after the shared review. For example, update [Private Access operations](how-to-operate-private-access), [Internet Access operations](how-to-operate-internet-access), [Remote Networks operations](how-to-operate-remote-networks), or [Microsoft Traffic operations](how-to-operate-microsoft-traffic) when a change affects only one capability.

### Training and knowledge sharing

- Schedule quarterly knowledge-sharing sessions, especially after major GSA feature releases.
- Monitor the [Microsoft Tech Community for Global Secure Access](https://techcommunity.microsoft.com/) and the [Global Secure Access documentation](/en-us/entra/global-secure-access/) for updates.
- Stay informed via [Microsoft Entra what's new](/en-us/entra/fundamentals/whats-new) for feature announcements and deprecation notices.
- Track three release notes so your team keeps current with connector and client versions, new features, and update requirements:
    - [Microsoft Entra private network connector version release history](/en-us/entra/global-secure-access/reference-version-history)
    - [Global Secure Access client for Windows release notes](/en-us/entra/global-secure-access/reference-windows-client-release-history)
    - [Global Secure Access client for macOS release notes](/en-us/entra/global-secure-access/reference-macos-client-release-history)

Tip

Treat your guides and runbooks as living documents—update troubleshooting references after every significant incident, and update procedures after every change review. Version-control all documentation.

### Adapting to organizational changes

Review your GSA capacity and configuration when:

| Trigger | Action |
| --- | --- |
| Merger, acquisition, or divestiture | Assess new users, sites, and applications. Plan capacity and policy updates. |
| New office or branch site | Evaluate whether to use client-based access or remote network (GRE/IPsec) connectivity. See [Remote Networks operations](how-to-operate-remote-networks). |
| Significant remote workforce growth | Verify connector and license capacity. Review Private Access performance baselines. |
| New cloud application adoption | Verify the application is properly classified in web filtering policies. Add application segments if needed for Private Access. |
| Regulatory or compliance changes | Review policies for alignment. Update reporting to cover new compliance requirements. |
---
layout: Conceptual
title: Access activity logs in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/howto-access-activity-logs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: How to choose the right method for accessing and integrating the activity logs in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2026-06-24T00:00:00.0000000Z
ms.reviewer: egreenberg
ms.custom: msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: c77413a1-9a2a-3d8d-5a40-848f94ea01f2
document_version_independent_id: efa41301-301c-59a5-bb25-9cdbec1cb5bf
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/howto-access-activity-logs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/howto-access-activity-logs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/howto-access-activity-logs.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 13cc35e0-040e-94fb-d60b-187036b50a55
---

# Access activity logs in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The data collected in your Microsoft Entra logs enables you to assess many aspects of your Microsoft Entra tenant. To cover a broad range of scenarios, Microsoft Entra ID provides you with several options to access your activity log data. As an IT administrator, you need to understand the intended uses cases for these options, so that you can select the right access method for your scenario.

You can access Microsoft Entra activity logs and reports using the following methods:

- Stream activity logs to an **event hub** to integrate with other tools
- Access activity logs through the **Microsoft Graph API**
- Integrate activity logs with **Azure Monitor logs**
- Monitor activity in real-time with **Microsoft Sentinel**
- View activity logs and reports in the **Microsoft Entra admin center**
- Export activity logs for **storage and queries**

Each of these methods provides you with capabilities that might align with certain scenarios. This article describes those scenarios, including recommendations and details about related reports that use the data in the activity logs. Explore the options in this article to learn about those scenarios so you can choose the right method.

## Prerequisites

- A working Microsoft Entra tenant with the appropriate Microsoft Entra license associated with it. For a full list of license requirements, see [Microsoft Entra monitoring and health licensing](../../fundamentals/licensing#microsoft-entra-monitoring-and-health).
- [Reports Reader](../role-based-access-control/permissions-reference#reports-reader) is the least privileged role required to access the activity logs.
- [Security Administrator](../role-based-access-control/permissions-reference#security-administrator) is the least privileged role required to configure diagnostic settings.
- Audit logs are available for features that you have licensed.
- To consent to the required permissions to view logs with Microsoft Graph, you need the [Privileged Role Administrator](../role-based-access-control/permissions-reference#privileged-role-administrator).
- For a full list of roles, see [Least privileged role by task](../role-based-access-control/delegate-by-task#monitoring-and-health---audit-and-sign-in-logs-least-privileged-roles).

The required licenses vary based on the monitoring and health capability.

| Capability | Microsoft Entra ID Free | Microsoft Entra ID P1 or P2 / Microsoft Entra Suite |
| --- | --- | --- |
| Audit logs | Yes | Yes |
| Sign-in logs | Yes | Yes |
| Provisioning logs | No | Yes |
| Custom security attributes | Yes | Yes |
| Health | No | Yes |
| Microsoft Graph activity logs | No | Yes |
| Usage and insights | No | Yes |

## View logs through the Microsoft Entra admin center

For one-off investigations with a limited scope, the [Microsoft Entra admin center](https://entra.microsoft.com/) is often the easiest way to find the data you need. The user interface for each of these reports provides you with filter options enabling you to find the entries you need to solve your scenario.

The data captured in the Microsoft Entra activity logs are used in many reports and services. You can review the sign-in, audit, and provisioning logs for one-off scenarios or use reports to look at patterns and trends. The data from the activity logs help populate the Identity Protection reports, which provide information security related risk detections that Microsoft Entra ID can detect and report on. Microsoft Entra activity logs also populate Usage and insights reports, which provide usage details for your tenant's applications.

### Recommended uses

The reports available in the Azure portal provide a wide range of capabilities to monitor activities and usage in your tenant. The following list of uses and scenarios isn't exhaustive, so explore the reports for your needs.

- Research a user's sign-in activity or track an application's usage.
- Review details around group name changes, device registration, and password resets with audit logs.
- Use the Identity Protection reports for monitoring at risk users, risky workload identities, risky agents, and risky sign-ins.
- Review the sign-in success rate in the Microsoft Entra application activity (preview) report from Usage and insights to ensure that your users can access the applications in use in your tenant.
- Compare the different authentication methods your users prefer with the Authentication methods report from Usage and insights.

### Quick steps

Use the following basic steps to access the reports in the Microsoft Entra admin center.

# [Microsoft Entra activity logs](#tab/microsoft-entra-activity-logs)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Audit logs**/**Sign-in logs**/**Provisioning logs**.
3. Adjust the filter according to your needs.
    - [Learn how to filter activity logs](howto-customize-filter-logs)
    - [Explore the Microsoft Entra audit log categories and activities](reference-audit-activities)
    - [Learn about basic info in the Microsoft Entra sign-in logs](concept-sign-in-log-activity-details)

Audit logs can be accessed directly from the area of the Microsoft Entra admin center where you're working. For example, if you're in the **Groups** or **Licenses** section of Microsoft Entra ID, you can access the audit logs for those specific activities directly from that area. When you access the audit logs in this way, the filter categories are automatically set. For example, if you're in **Groups**, the audit log filter category is set to **GroupManagement**.

# [Microsoft Entra ID Protection reports](#tab/microsoft-entra-id-protection-reports)
1. Browse to **ID Protection** &gt; **Dashboard**.
2. Explore the available reports.
    - [Learn more about Identity Protection](../../id-protection/overview-identity-protection)
    - [Learn how to investigate risk](../../id-protection/howto-identity-protection-investigate-risk)

# [Usage and insights reports](#tab/usage-and-insights-reports)
1. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Usage and insights**.
2. Explore the available reports.
    - [Learn more about the Usage and insights report](concept-usage-insights-report)

---

## Stream logs to an event hub to integrate with SIEM tools

Streaming your activity logs to an event hub is required to integrate your activity logs with Security Information and Event Management (SIEM) tools, such as Splunk and SumoLogic. Before you can stream logs to an event hub, you need to [set up an Event Hubs namespace and an event hub](/en-us/azure/event-hubs/event-hubs-create) in your Azure subscription.

### Recommended uses

The SIEM tools you can integrate with your event hub can provide analysis and monitoring capabilities. If you're already using these tools to ingest data from other sources, you can stream your identity data for more comprehensive analysis and monitoring. We recommend streaming your activity logs to an event hub for the following types of scenarios:

- You need a big data streaming platform and event ingestion service to receive and process millions of events per second.
- You're looking to transform and store data by using a real-time analytics provider or batching/storage adapters.

### Quick steps

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../role-based-access-control/permissions-reference#security-administrator).
2. Create an Event Hubs namespace and event hub.
3. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Diagnostic settings**.
4. Choose the logs you want to stream, select the **Stream to an event hub**option, and complete the fields.
    - [Set up an Event Hubs namespace and an event hub](/en-us/azure/event-hubs/event-hubs-create)
    - [Learn more about streaming activity logs to an event hub](howto-stream-logs-to-event-hub)

Your independent security vendor should provide you with instructions on how to ingest data from Azure Event Hubs into their tool.

## Access logs with the Microsoft Graph API

The Microsoft Graph API provides a unified programmability model that you can use to access data for your Microsoft Entra ID P1 or P2 tenants. It doesn't require an administrator or developer to set up extra infrastructure to support your script or app.

### Recommended uses

Using Microsoft Graph explorer, you can run queries to help you with the following types of scenarios:

- View tenant activities such as who made a change to a group and when.
- Mark a Microsoft Entra sign-in event as safe or confirmed compromised.
- Retrieve a list of application sign-ins for the last 30 days.

Note

Microsoft Graph allows you to access data from multiple services that impose their own throttling limits. For more information on activity log throttling, see [Microsoft Graph service-specific throttling limits](/en-us/graph/throttling-limits#identity-and-access-service-limits).

### Quick steps

1. [Configure the prerequisites](howto-configure-prerequisites-for-reporting-api).
2. Sign in to [Graph Explorer](https://aka.ms/ge).
3. Set the HTTP method and API version.
4. Add a query then select the **Run query**button.
    - [Familiarize yourself with the Microsoft Graph properties for directory audits](/en-us/graph/api/resources/directoryaudit)
    - [Complete the MS Graph Quickstart guide](quickstart-access-log-with-graph-api)

## Integrate logs with Azure Monitor logs

With the Azure Monitor logs integration, you can enable rich visualizations, monitoring, and alerting on the connected data. Log Analytics provides enhanced query and analysis capabilities for Microsoft Entra activity logs. To integrate Microsoft Entra activity logs with Azure Monitor logs, you need a Log Analytics workspace. From there, you can run queries through Log Analytics.

### Recommended uses

Integrating Microsoft Entra logs with Azure Monitor logs provides a centralized location for querying logs. We recommend integrating logs with Azure Monitor for the following types of scenarios:

- Compare Microsoft Entra sign-in logs with logs published by other Azure services.
- Correlate sign-in logs against Azure Application insights.
- Query logs using specific search parameters.

### Quick steps

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../role-based-access-control/permissions-reference#security-administrator).
2. [Create a Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace).
3. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Diagnostic settings**.
4. Choose the logs you want to stream, select the **Send to Log Analytics workspace** option, and complete the fields.
5. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Log Analytics**and begin querying the data.
    - [Integrate Microsoft Entra logs with Azure Monitor logs](howto-integrate-activity-logs-with-azure-monitor-logs)
    - [Learn how to query using Log Analytics](howto-analyze-activity-logs-log-analytics)

## Monitor events with Microsoft Sentinel

Sending sign-in and audit logs to Microsoft Sentinel provides your security operations center with near real-time security detection and threat hunting. The term *threat hunting* refers to a proactive approach to improve the security posture of your environment. As opposed to classic protection, threat hunting tries to proactively identify potential threats that might harm your system. Your activity log data might be part of your threat hunting solution.

### Recommended uses

We recommend using the real-time security detection capabilities of Microsoft Sentinel if your organization needs security analytics and threat intelligence. Use Microsoft Sentinel if you need to:

- Collect security data across your enterprise.
- Detect threats with vast threat intelligence.
- Investigate critical incidents guided by AI.
- Respond rapidly and automate protection.

### Quick steps

1. Learn about the [prerequisites](/en-us/azure/sentinel/prerequisites), [roles, and permissions](/en-us/azure/sentinel/roles).
2. [Estimate potential costs](/en-us/azure/sentinel/billing).
3. [Onboard to Microsoft Sentinel](/en-us/azure/sentinel/quickstart-onboard).
4. [Collect Microsoft Entra data](/en-us/azure/sentinel/connect-azure-active-directory).
5. [Begin hunting for threats](/en-us/azure/sentinel/hunting).

## Export logs for storage and queries

The right solution for your long-term storage depends on your budget and what you plan on doing with the data. You've got three options:

- Archive logs to Azure Storage
- Download logs for manual storage
- Integrate logs with Azure Monitor logs

[Azure Storage](/en-us/azure/storage/common/storage-introduction) is the right solution if you aren't planning on querying your data often. For more information, see [Archive directory logs to a storage account](howto-archive-logs-to-storage-account).

If you plan to query the logs often to run reports or perform analysis on the stored logs, you should [integrate your data with Azure Monitor logs](howto-integrate-activity-logs-with-azure-monitor-logs).

If your budget is tight, and you need a cheap method to create a long-term backup of your activity logs, you can [manually download your logs](howto-download-logs). The user interface of the activity logs in the portal provides you with an option to download the data as **JSON** or **CSV**. One trade off of the manual download is that it requires more manual interaction. If you're looking for a more professional solution, use either Azure Storage or Azure Monitor.

### Recommended uses

We recommend setting up a storage account to archive your activity logs for those governance and compliance scenarios where long-term storage is required.

If you want to long-term storage *and* you want to run queries against the data, review the section on integrating your activity logs with Azure Monitor Logs.

We recommend manually downloading and storing your activity logs if you have budgetary constraints.

### Quick steps

Use the following basic steps to archive or download your activity logs.

# [Archive activity logs to a storage account](#tab/archive-activity-logs-to-a-storage-account)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../role-based-access-control/permissions-reference#security-administrator).
2. Create a storage account.
3. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Diagnostic settings**.
4. Choose the logs you want to stream, select the **Archive to a storage account**option, and complete the fields.
    - [Review the data retention policies](reference-reports-data-retention)

# [Manually download activity logs](#tab/manually-download-activity-logs)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Audit logs**/**Sign-in logs**/**Provisioning logs** from the **Monitoring** menu.
3. Select **Download**.
    - [Learn more about how to download logs](howto-download-logs).

---

## Troubleshoot empty results or HTTP 429 errors when retrieving activity logs

You might not see any results when you query activity logs (sign-in, audit, or provisioning) in the Microsoft Entra admin center or through the Microsoft Graph API. If you capture a network trace, the underlying API calls return HTTP 429 (Too Many Requests) responses. Throttling depends on current system demand rather than on tenant size, so the same query that worked earlier might return no results later. Use the following workarounds if you see no results in the admin center or HTTP 429 responses in a trace.

### Reduce the query date range

Break the query into smaller date-range chunks and repeat the query for each chunk until you cover the time period you need. The date range that succeeds varies by tenant and by current system demand, so reduce the range incrementally until results return.

### Stream logs to a Log Analytics workspace

To avoid the request throttling that affects admin center and Microsoft Graph queries, stream activity logs to a Log Analytics workspace and query the data there. Log Analytics supports richer query capabilities through Kusto Query Language (KQL). For setup instructions, see Integrate logs with Azure Monitor logs.
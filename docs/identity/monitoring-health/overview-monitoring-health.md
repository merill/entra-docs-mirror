---
layout: Conceptual
title: What is Microsoft Entra monitoring and health? - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/overview-monitoring-health
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn about the features and capabilities of the logs and reports in Microsoft Entra monitoring and health.
ms.topic: concept-article
ms.date: 2025-11-07T00:00:00.0000000Z
ms.reviewer: egreenberg
ms.custom: agent-id-ignite
locale: en-us
document_id: 2763640f-ae78-a69e-0999-2863240dc2ff
document_version_independent_id: dd39081a-afd8-dda2-5a08-7cf54bab1fa4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/overview-monitoring-health.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/overview-monitoring-health
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/overview-monitoring-health.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 615a5921-1d36-e9ae-f15a-4cbb0cd9fb6a
---

# What is Microsoft Entra monitoring and health? - Microsoft Entra ID | Microsoft Learn

The features of Microsoft Entra monitoring and health provide a comprehensive view of identity related activity in your environment. This data enables you to:

- Determine how your users utilize your apps and services.
- Detect potential risks affecting the health of your environment.
- Troubleshoot issues preventing your users from getting their work done.
- Gain insights by seeing audit events of changes to your Microsoft Entra directory.

Sign-in and audit logs comprise the activity logs behind many Microsoft Entra reports, which can be used to analyze, monitor, and troubleshoot activity in your tenant. Routing your activity logs to an analysis and monitoring solution provides greater insights into your tenant's health and security.

This article describes the types of activity logs available in Microsoft Entra ID, the reports that use the logs, and the monitoring services available to help you analyze the data.

## Identity activity logs

Activity logs help you understand the behavior of users in your organization. There are three types of activity logs in Microsoft Entra ID:

- [**Audit logs**](concept-audit-logs) include the history of every task performed in your tenant.
- [**Sign-in logs**](concept-sign-ins) capture the sign-in attempts of your users and client applications.
- [**Provisioning logs**](concept-provisioning-logs) provide information around users provisioned in your tenant through a third party service.

The activity logs can be viewed in the Azure portal or using the Microsoft Graph API. Activity logs can also be routed to various endpoints for storage or analysis. To learn about all of the options for viewing the activity logs, see [How to access activity logs](howto-access-activity-logs).

### Audit logs

Audit logs provide you with records of system activities for compliance. This data enables you to address common scenarios such as:

- Someone in my tenant got access to an admin group. Who gave them access?
- An app I recently onboarded is not working as expected. What changes were made to the app?
- What operations were performed by a specific agent?

### Sign-in logs

The sign-in logs enable you to find answers to questions such as:

- What is the sign-in pattern of a user?
- How many users have users signed in over a week?
- What agents are authenticating to my apps?

### Provisioning logs

You can use the provisioning logs to find answers to questions like:

- What groups were successfully created in ServiceNow?
- What users were successfully removed from Adobe?
- What users from Workday were successfully created in Active Directory?

## Identity reports

Reviewing the data in the Microsoft Entra activity logs can provide helpful information for IT administrators. To streamline the process of reviewing data on key scenarios, we've created several reports on common scenarios that use the activity logs.

- [Identity Protection](../../id-protection/overview-identity-protection) uses sign-in data to create reports on risky users and sign-in activities.
- Activity related to your applications, such as service principal and app credential activity, are used to create reports in [Usage and insights](concept-usage-insights-report).
- [Microsoft Entra workbooks](overview-workbooks) provide a customizable way to view and analyze the activity logs.
- Use [Microsoft Entra recommendations](overview-recommendations) to monitor and improve your tenant's security.
- [Microsoft Entra Health](concept-microsoft-entra-health) capture global service level agreement attainment and health signals for several key scenarios.

## Identity monitoring and tenant health

Reviewing Microsoft Entra activity logs is the first step in maintaining and improving the health and security of your tenant. You need to analyze the data, monitor on risky scenarios, and determine where you can make improvements. Microsoft Entra monitoring provides the necessary tools to help you make informed decisions.

Monitoring Microsoft Entra activity logs requires routing the log data to a monitoring and analysis solution. Endpoints include Azure Monitor logs, Microsoft Sentinel, or a third-party solution third-party Security Information and Event Management (SIEM) tool.

- [Stream logs to an event hub to integrate with third-party SIEM tools.](howto-stream-logs-to-event-hub)
- [Integrate logs with Azure Monitor logs.](howto-integrate-activity-logs-with-azure-monitor-logs)
- [Analyze logs with Azure Monitor logs and Log Analytics.](howto-analyze-activity-logs-log-analytics)

## Use cases

How you use the logs, reports, and monitoring services available depends on your organization's needs. To better prioritize the use cases and solutions, it might help to see how these solutions are related to each other, how they differ, and how they can be used together.

### Considerations

- **Retention** - Log retention: store audit logs and sign in logs of Microsoft Entra longer than 30 days
- **Analytics** - Logs are searchable with analytic tools
- **Operational and security insights** - Provide access to application usage, sign-in errors, self-service usage, trends, and so on.
- **SIEM integration** - Integrate and stream Microsoft Entra sign-in logs and audit logs to SIEM systems

With Microsoft Entra monitoring, you can route Microsoft Entra activity logs and retain them for long-term reporting and analysis to gain environment insights, and integrate it with SIEM tools. Use the following decision flow chart to help select an architecture.

![Graphic of decision matrix for business-need architecture.](media/overview-monitoring-health/deploy-reporting-flow-diagram.png)

For an overview of how to access, store, and analyze activity logs, see [How to access activity logs](howto-access-activity-logs).
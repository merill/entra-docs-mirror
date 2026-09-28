---
layout: Conceptual
title: How to investigate private application access requiring Microsoft Entra Private Access connector - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/howto-investigate-private-access-connector-signals
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how to monitor and troubleshoot private application access scenarios that require the Microsoft Entra Private Access connector, using Microsoft Entra Health monitoring tools.
ms.topic: how-to
ms.date: 2026-09-14T00:00:00.0000000Z
ms.reviewer: gauthamca
ai-usage: ai-assisted
locale: en-us
document_id: 18e23ed3-a0e5-bf26-2f08-faf35211f0f4
document_version_independent_id: 18e23ed3-a0e5-bf26-2f08-faf35211f0f4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/howto-investigate-private-access-connector-signals.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/howto-investigate-private-access-connector-signals
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/howto-investigate-private-access-connector-signals.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
platformId: ff043bbf-5767-58d6-7e49-ff849f8e8f9e
---

# How to investigate private application access requiring Microsoft Entra Private Access connector - Microsoft Entra ID | Microsoft Learn

Microsoft Entra Health monitoring provides a set of tenant-level health metrics you can monitor and alerts when a potential issue or failure condition is detected. There are multiple health scenarios that can be monitored, including private application access requiring availability of a Microsoft Entra Private Access connector.

To learn more about how Microsoft Entra Health works, see:

- [What is Microsoft Entra Health?](/en-us/entra/identity/monitoring-health/concept-microsoft-entra-health)
- [How to investigate Microsoft Entra health monitoring signals and alerts](/en-us/entra/identity/monitoring-health/howto-investigate-health-scenario-alerts)

This article describes the health metrics related to private application access requiring Microsoft Entra Private Access connector and how to troubleshoot a potential issue when you receive an alert.

This scenario:

- Aggregates the number of unique users accessing private applications successfully.
- Aggregates the number of unique users who failed to access private applications due to connector availability.
- Aggregates the number of unique private applications accessed successfully.
- Aggregates the number of failed accesses to unique private applications due to connector availability.

## Prerequisites

There are different roles, permissions, and license requirements to view health monitoring signals and configure and receive alerts. We recommend using a role with least privilege access to align with the [Zero Trust guidance](/en-us/security/zero-trust/zero-trust-overview).

- A tenant with a [Microsoft Entra P1 or P2 license](/en-us/entra/fundamentals/get-started-premium) is required to *view* the Microsoft Entra health scenario monitoring signals.
- A tenant with both a non-trial [Microsoft Entra P1 or P2 license](/en-us/entra/fundamentals/get-started-premium)*and* at least 100 monthly active users is required to *view alerts* and *receive alert notifications*.
- A tenant with a Microsoft Entra Private Access license is required. For details, see the licensing section of [What is Global Secure Access?](/en-us/entra/global-secure-access/overview-what-is-global-secure-access).
- The [Reports Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#reports-reader) role is the least privileged role required to *view scenario monitoring signals, alerts, and alert configurations*.
- The [Helpdesk Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#helpdesk-administrator) is the least privileged role required to *update alerts* and *update alert notification configurations*.
- The `HealthMonitoringAlert.Read.All` permission is required to *view the alerts using the Microsoft Graph API*.
- The `HealthMonitoringAlert.ReadWrite.All` permission is required to *view and modify the alerts using the Microsoft Graph API*.
- For a full list of roles, see [Least privileged role by task](/en-us/entra/identity/role-based-access-control/delegate-by-task#microsoft-entra-health-least-privileged-roles).
- The [Global Secure Access Log Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#global-secure-access-log-reader) role is required to view Microsoft Entra Private Access traffic logs.

## Investigate the signal and alert

Start your investigation by comparing the alert timeframe, signal trend, and affected entities. Then correlate the affected users and applications with connector status and logs.

1. View the details of the alert.

    - In the Microsoft Entra admin center, review the signal graph, alert timeframe, and affected entities. For more information, see [Investigate the signals and alerts](howto-investigate-health-scenario-alerts#investigate-the-signals-and-alerts).
    - For Microsoft Graph guidance, see [Microsoft Graph health monitoring overview](/en-us/graph/api/resources/healthmonitoring-overview?view=graph-rest-beta&amp;preserve-view=true).
2. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) as at least a [Reports Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#reports-reader).
3. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Health**. The page opens to the Service Level Agreement (SLA) Attainment page.
4. Select the **Health Monitoring** tab.
5. Select the **Private application access requiring Microsoft Entra Private Access connector** scenario, and then select an active alert.

    [![Screenshot of the Private application access requiring Microsoft Entra Private Access connector scenario with one active alert.](media/howto-investigate-private-access-connector-signals/private-access-alert.png)](media/howto-investigate-private-access-connector-signals/private-access-alert.png#lightbox)
6. Review your Microsoft Entra Private Access connector status. Confirm that the connector and updater services are running. For more information, see [Microsoft Entra private network connector maintenance](/en-us/entra/global-secure-access/concept-connectors#maintenance).
7. Review the connector groups and their application assignments. Confirm that each affected application is assigned to a group with healthy connectors. For more information, see [Microsoft Entra private network connector groups](/en-us/entra/global-secure-access/concept-connector-groups).
8. Review the [sign-in logs](/en-us/entra/identity/monitoring-health/concept-sign-in-log-activity-details). Look for affected users who are blocked from signing in to the application.
9. Review the [Global Secure Access traffic logs](/en-us/entra/global-secure-access/how-to-view-traffic-logs). Filter the logs to the alert timeframe and affected user or application, and look for private application transaction failures.
10. Review the [Global Secure Access audit logs](/en-us/entra/global-secure-access/how-to-access-audit-logs) for recent connector group or application assignment changes.

    [![Screenshot of audit logs filtered to the Global Secure Access service.](media/howto-investigate-private-access-connector-signals/global-secure-access-audit-logs.png)](media/howto-investigate-private-access-connector-signals/global-secure-access-audit-logs.png#lightbox)

## Understand the signal

An alert can indicate a change in the number of users or private applications that fail to connect because a connector isn't available.

- A spike can indicate that one or more connectors became unavailable, a connector group lost capacity, or an application was assigned to the wrong connector group.
- A dip can indicate that connector availability recovered. It can also indicate that traffic or application assignments changed.

Compare the alert start time with connector status, connector event logs, audit logs, and planned maintenance before you change the configuration.

## Mitigate common issues

The following common issues can cause this alert. This list isn't exhaustive, but it provides a starting point for your investigation.

### A connector is inactive or unavailable

A connector service might be stopped, its trust certificate might be expired, or the connector host might be unable to reach the Microsoft Entra service.

To investigate and mitigate the issue:

1. In the alert, identify the affected users and private applications and note the alert start time.
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Connectors**, and identify inactive connectors in the connector group that serves the affected applications.
3. On each affected connector server, confirm that the connector and updater services are running.
4. Run the Connector Diagnostics tool to check certificate validity, ports 80 and 443, outbound proxy configuration, certificate revocation list access, service state, and back-end endpoint access.
5. Review the connector **Admin** event log for service, trust certificate, registration, or connectivity errors.
6. Restore the connector service or connectivity. If the trust certificate expired, reregister or reinstall the connector by following [Troubleshoot private network connectors](/en-us/entra/global-secure-access/troubleshoot-connectors).
7. Confirm that the connector becomes active and that new traffic log entries no longer show connector-related transaction failures.

### An application is assigned to the wrong connector group

The assigned connector group might not contain a healthy connector that can reach the affected application's network.

To investigate and mitigate the issue:

1. In the alert, identify whether failures are concentrated on one or more applications.
2. Review each affected application's connector group assignment.
3. Confirm that the assigned group contains active connectors in a network that can reach the application's destination.
4. Review the audit logs for a connector group or application assignment change near the alert start time.
5. Restore the intended assignment, or add healthy connectors that can reach the application to the assigned group.
6. Test access and confirm recovery in the traffic logs and health signal.

### A connector group has insufficient capacity or resilience

A connector group with a single connector, sustained high utilization, or poor connectivity to the service or back-end applications can cause intermittent failures.

To investigate and mitigate the issue:

1. Check whether the connector group has at least two active connectors for high availability.
2. Review connector host CPU and network utilization. Keep sustained CPU and memory utilization below the documented thresholds.
3. From each connector server, test connectivity to the affected back-end application.
4. If a connector host is unavailable, remove it from active service and add a healthy or backup connector to the group.
5. If utilization is sustained, add connectors or increase host capacity. For sizing and performance guidance, see [Microsoft Entra private network connectors](/en-us/entra/global-secure-access/concept-connectors#performance-and-scalability).
6. Confirm that failures stop and the signal returns to its expected range.
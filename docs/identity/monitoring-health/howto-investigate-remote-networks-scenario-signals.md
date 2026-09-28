---
layout: Conceptual
title: How to investigate the Global Secure Access remote network connectivity - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/howto-investigate-remote-networks-scenario-signals
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how to monitor and troubleshoot remote network connectivity using Microsoft Entra Health monitoring.
ms.topic: how-to
ms.date: 2026-09-14T00:00:00.0000000Z
ms.reviewer: gauthamca
ai-usage: ai-assisted
locale: en-us
document_id: ad705e30-8ccc-3e82-a6f9-fe090764bacd
document_version_independent_id: ad705e30-8ccc-3e82-a6f9-fe090764bacd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/howto-investigate-remote-networks-scenario-signals.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/howto-investigate-remote-networks-scenario-signals
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/howto-investigate-remote-networks-scenario-signals.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 0a61f334-3877-7e95-e2d0-6a541f0c48b3
---

# How to investigate the Global Secure Access remote network connectivity - Microsoft Entra ID | Microsoft Learn

Microsoft Entra Health monitoring provides a set of tenant-level health metrics you can monitor and alerts when a potential issue or failure condition is detected. There are multiple health scenarios that can be monitored, including Global Secure Access remote network connectivity.

To learn more about how Microsoft Entra Health works, see:

- [What is Microsoft Entra Health?](/en-us/entra/identity/monitoring-health/concept-microsoft-entra-health)
- [How to investigate Microsoft Entra health monitoring signals and alerts](/en-us/entra/identity/monitoring-health/howto-investigate-health-scenario-alerts)

This article describes the health metrics related to remote network connectivity and provides steps to troubleshoot potential problems. Tunnel connectivity and BGP connectivity are separate health scenarios, but this article covers them together because BGP depends on an established IPsec tunnel.

This article covers two scenarios:

- Global Secure Access requiring remote network tunnel connectivity
    - Presents data showing the number of remote network tunnels that are connected.
    - Presents data showing the number of remote network tunnels that are disconnected.
- Global Secure Access requiring remote network BGP connectivity
    - Presents data showing the number of remote networks with BGP connected.
    - Presents data showing the number of remote networks with BGP disconnected.

## Prerequisites

There are different roles, permissions, and license requirements to view health monitoring signals and to configure and receive alerts. We recommend using a role with least privilege access to align with the [Zero Trust guidance](/en-us/security/zero-trust/zero-trust-overview).

- A tenant with a [Microsoft Entra P1 or P2 license](/en-us/entra/fundamentals/get-started-premium) is required to *view* the Microsoft Entra health scenario monitoring signals.
- A tenant with both a non-trial [Microsoft Entra P1 or P2 license](/en-us/entra/fundamentals/get-started-premium)*and* at least 100 monthly active users is required to *view alerts* and *receive alert notifications*.
- A tenant with a Microsoft Entra Global Secure Access license is required. For details, see the licensing section of [What is Global Secure Access?](/en-us/entra/global-secure-access/overview-what-is-global-secure-access).
- The [Reports Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#reports-reader) role is the least privileged role required to *view scenario monitoring signals, alerts, and alert configurations*.
- The [Helpdesk Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#helpdesk-administrator) is the least privileged role required to *update alerts* and *update alert notification configurations*.
- The `HealthMonitoringAlert.Read.All` permission is required to *view the alerts using the Microsoft Graph API*.
- The `HealthMonitoringAlert.ReadWrite.All` permission is required to *view and modify the alerts using the Microsoft Graph API*.
- For a full list of roles, see [Least privileged role by task](/en-us/entra/identity/role-based-access-control/delegate-by-task#microsoft-entra-health-least-privileged-roles).
- You must be assigned the [Global Secure Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-secure-access-administrator) or [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator) role to access remote network logs.

## Investigate the signals and alerts

Start your investigation by identifying whether the alert is for tunnel connectivity or BGP connectivity. Then compare the alert timeframe and affected remote networks with the remote network health and audit logs.

1. View the details of the alert.

    - In the [Microsoft Entra admin center](https://entra.microsoft.com/), review the signal graph, alert timeframe, and affected remote networks. For more information, see [Investigate the signals and alerts](howto-investigate-health-scenario-alerts#investigate-the-signals-and-alerts).
    - For Microsoft Graph guidance, see [Microsoft Graph health monitoring overview](/en-us/graph/api/resources/healthmonitoring-overview?view=graph-rest-beta&amp;preserve-view=true).
2. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) as at least a [Reports Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#reports-reader).
3. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Health**. The page opens to the Service Level Agreement (SLA) Attainment page.
4. Select the **Health Monitoring** tab.
5. Select the **Global Secure Access requiring remote network tunnel connectivity** or **Global Secure Access requiring remote network BGP connectivity** scenario, and then select an active alert.

    [![Screenshot of the Global Secure Access remote network BGP connectivity scenario with one active alert.](media/howto-investigate-remote-networks-scenario-signals/remote-network-border-gateway-protocol-alert.png)](media/howto-investigate-remote-networks-scenario-signals/remote-network-border-gateway-protocol-alert.png#lightbox)
6. Review the [remote network health logs](/en-us/entra/global-secure-access/how-to-remote-network-health-logs?tabs=microsoft-entra-admin-center).

    - For a tunnel alert, look for **Tunnel disconnected** events for the affected remote network, source IP address, and destination IP address.
    - For a BGP alert, look for **BGP disconnected** events. Review the **BGP Routes Advertised Count** in the corresponding **Remote network alive** events.
    - Use **Remote network alive** events to compare sent and received bytes before and during the alert.
7. Review the [Global Secure Access audit logs](/en-us/entra/global-secure-access/how-to-access-audit-logs) for recent changes to the affected remote network, device link, IPsec configuration, or traffic profile assignment.

    [![Screenshot of audit logs filtered to the Global Secure Access service.](media/howto-investigate-remote-networks-scenario-signals/global-secure-access-audit-logs.png)](media/howto-investigate-remote-networks-scenario-signals/global-secure-access-audit-logs.png#lightbox)
8. If you need longer retention or correlation, [export the remote network health logs](/en-us/entra/global-secure-access/how-to-remote-network-health-logs#configure-diagnostic-settings-to-export-logs) to Log Analytics and [analyze them with a workbook](/en-us/entra/global-secure-access/how-to-remote-network-health-logs#analyze-logs-with-a-workbook).

## Understand the signals

Tunnel and BGP alerts represent different layers of remote network connectivity:

- The tunnel connectivity signal tracks whether IPsec tunnels are connected or disconnected. If the tunnel is disconnected, BGP can't exchange routes over that tunnel.
- The BGP connectivity signal tracks whether the BGP session is connected and exchanging route information over an established tunnel. An IPsec tunnel can remain connected while BGP is disconnected.

A spike in disconnected tunnels or BGP sessions can indicate a CPE, internet service provider, configuration, or Global Secure Access edge connectivity problem. Compare the alert start time with remote network health events, audit logs, and planned network maintenance.

## Mitigate common issues

The following common issues can cause a tunnel or BGP connectivity alert. This list isn't exhaustive, but it provides a starting point for your investigation.

### One or more IPsec tunnels are disconnected

A tunnel can disconnect because of a CPE outage, internet connectivity problem, or mismatch between the CPE and Global Secure Access IPsec configuration.

To investigate and mitigate the issue:

1. In the alert, identify the affected remote network and alert start time.
2. In the remote network health logs, filter by the remote network ID. Identify **Tunnel disconnected** events and note the source and destination IP address pair.
3. Check the CPE status and logs for the matching tunnel. Confirm that the public IP addresses, IPsec parameters, shared secret or certificate, and tunnel endpoints match the Global Secure Access device link configuration.
4. Review the audit logs for changes to the remote network or device link near the alert start time.
5. Restore CPE or internet connectivity, or correct the mismatched configuration.
6. Confirm that a **Tunnel connected** event appears and that sent and received bytes resume in subsequent **Remote network alive** events.

### The IPsec tunnel is connected, but BGP is disconnected

The underlying tunnel can remain connected while the BGP neighbor relationship is down. In this state, the remote network might not exchange the routes that are required to forward traffic.

To investigate and mitigate the issue:

1. Confirm that the remote network health logs show **Tunnel connected** for the affected source and destination IP address pair.
2. Look for **BGP disconnected** events. Check the **BGP Routes Advertised Count** in **Remote network alive** events for the affected remote network.
3. On the CPE, verify the BGP neighbor IP addresses, autonomous system numbers, and route advertisement configuration.
4. Review recent CPE and Global Secure Access configuration changes.
5. Correct the BGP configuration or restart the affected BGP session according to your CPE vendor's guidance.
6. Confirm that a **BGP connected** event appears. Then confirm that the advertised route count returns to its expected value in subsequent **Remote network alive** events.

### Connectivity is intermittent or depends on a single tunnel

A remote network with one tunnel has no alternate path during CPE, ISP, or Global Secure Access edge maintenance or failure.

To investigate and mitigate the issue:

1. Review the health logs for repeated tunnel or BGP disconnect and reconnect events.
2. Confirm whether the remote network has redundant tunnels.
3. Configure at least two IPsec tunnels per location. Use zone redundancy or a secondary geographic remote network based on your availability requirements.
4. Configure tunnel weighting for active-active or active-standby routing.
5. Use BGP for dynamic route learning. If your CPE doesn't support BGP, configure static routes with appropriate metrics.
6. Export remote network health logs to Log Analytics and create alert rules for tunnel and BGP failures.

For redundancy and failover guidance, see [Enhance remote network resilience](/en-us/entra/global-secure-access/remote-network-resilience).
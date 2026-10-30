---
layout: Conceptual
title: How to use the remote network health logs - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-remote-network-health-logs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Access and analyze IPsec tunnel and BGP health logs for remote networks using the Microsoft Entra admin center, Microsoft Graph API, or Log Analytics.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: katabish
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: e0765973-ea2b-dc14-4129-f792593bc53b
document_version_independent_id: e0765973-ea2b-dc14-4129-f792593bc53b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-remote-network-health-logs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-remote-network-health-logs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-remote-network-health-logs.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: af6b208f-ed85-91be-9377-33a9c4590f20
---

# How to use the remote network health logs - Global Secure Access | Microsoft Learn

## Overview

Remote networks, such as a branch office, rely on customer premises equipment (CPE) to connect users in those locations to the online resources and services they need. Users expect that CPE to function so they can do their work. To keep everyone connected, you need to ensure the health of the IPSec tunnel and the Border Gateway Protocol (BGP) route advertisement. This long-running tunnel and routing information are the keys to your remote network health.

This article describes several methods for accessing and analyzing the remote network health logs.

- Access logs in the Microsoft Entra admin center or the Microsoft Graph API
- Export logs to Log Analytics or a Security Information and Events Management (SIEM) tool
- Analyze logs using an Azure Workbook for Microsoft Entra
- Download logs for long-term storage

## Prerequisites

To view the remote network health logs in the Microsoft Entra admin center, you need:

- One of the following roles: [Global Secure Access Administrator](../identity/role-based-access-control/permissions-reference#global-secure-access-administrator), or [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator).
- The product requires licensing. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).
- Separate roles are required for accessing the logs with the Microsoft Graph API and integrating with Log Analytics and Azure Workbooks.

## View the logs

To view the **Remote network health logs**, you can use either the Microsoft Entra admin center or the Microsoft Graph API.

# [Microsoft Entra admin center](#tab/microsoft-entra-admin-center)
To view Remote network health logs in Microsoft Entra admin center:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Global Secure Access Administrator](../identity/role-based-access-control/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Monitor** &gt; **Remote network health logs**.

    ![Screenshot that shows the Remote network health logs.](media/how-to-remote-network-health-logs/remote-network-health-logs.png)

# [Microsoft Graph API](#tab/microsoft-graph-api)
Global Secure Access remote network health logs can be viewed and managed using Microsoft Graph on the `/beta` endpoint.

You need one of the following permissions to access the logs with the Microsoft Graph API:

- Directory.ReadWrite.All
- NetworkAccess.Read.All
- NetworkAccess.ReadWrite.All
- NetworkAccess-Reports.Read.All

To access remote network health logs with Microsoft Graph API:

1. Sign in to [Graph Explorer](https://aka.ms/ge).
2. Select GET as the HTTP method.
3. Select BETA as the API version.
4. Run the following query:

```http
GET https://graph.microsoft.com/beta/networkAccess/logs/remotenetworks
```

**Response (truncated):**

```json
{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#networkAccess/logs/remoteNetworks",
  "@odata.nextLink": "https://graph.microsoft.com/beta/networkAccess/logs/remotenetworks?$skiptoken=a0850fa33aecaf5fc7240fdd13929d25cc2ffbaa9e985c2fd3787a9283ba28c0",
  "@microsoft.graph.tips": "Use $select to choose only the properties your app needs, as this can lead to performance improvements. For example: GET networkAccess/logs/remoteNetworks?$select=bgpRoutesAdvertisedCount,createdDateTime",
  "value": [
    {
     "id": "00001111-aaaa-2222-bbbb-3333cccc4444",
     "remoteNetworkId": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee",
     "createdDateTime": "2024-05-09T20:53:48.3925141Z",
     "sourceIp": "20.x.x.x",
     "destinationIp": "20.x.x.x",
     "description": null,
     "bgpRoutesAdvertisedCount": 0,
     "status": "remoteNetworkAlive",
     "sentBytes": 74156,
     "receivedBytes": 76554
     },
     {
     "id": "11112222-bbbb-3333-cccc-4444dddd5555",
     "remoteNetworkId": "11bb11bb-cc22-dd33-ee44-55ff55ff55ff",
     "createdDateTime": "2024-05-09T20:54:55.1969876Z",
     "sourceIp": "16.x.x.x",
     "destinationIp": "20.x.x.x",
     "description": null,
     "bgpRoutesAdvertisedCount": 25,
     "status": "remoteNetworkAlive",
     "sentBytes": 573962,
     "receivedBytes": 365794
     }
  ]
}
```

---

## Configure diagnostic settings to export logs

Integrating logs with a SIEM tool like Log Analytics is configured through diagnostic settings in Microsoft Entra ID. This process is covered in detail in the [Configure Microsoft Entra diagnostic settings for activity logs](../identity/monitoring-health/howto-configure-diagnostic-settings) article.

To configure diagnostic settings, you need:

- [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator) access.
- A [Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace).

The basic steps to configure diagnostic settings are as follows:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Diagnostic settings**.
3. Any existing diagnostic settings appear in the table. Select **edit settings** to change an existing setting, or select **Add diagnostic setting** to create a new setting.
4. Provide a name.
5. Select the `RemoteNetworkHealthLogs` (and any other logs) you want to include.

    ![Screenshot that shows the Microsoft Entra diagnostic settings page.](media/how-to-remote-network-health-logs/diagnostic-settings-remote-network-logs.png)
6. Select the destinations you want to send the logs to.
7. Select the subscription and the destination from the dropdown menus that appear.
8. Select the **Save** button.

Note

It might take up to three days for the logs to start appearing in the destination.

Once your logs are routed to Log Analytics, you can take advantage of the following features:

- Create alert rules to get notified for things like a BGP tunnel failure.
    - For more information, see [Create an alert rule](/en-us/azure/azure-monitor/alerts/alerts-create-activity-log-alert-rule).
- Visualize the data with an Azure Workbook for Microsoft Entra (covered in the next section).
- Integrate logs with Microsoft Sentinel for security analytics and threat intelligence.
    - For more information, follow the [Onboard Microsoft Sentinel](/en-us/azure/sentinel/quickstart-onboard) Quickstart.

## Analyze logs with a Workbook

[Azure Workbooks for Microsoft Entra](../identity/monitoring-health/overview-workbooks) provide a visual representation of your data. Once you've configured a Log Analytics workspace and diagnostic settings to integrate your logs with Log Analytics, you can use a Workbook to analyze the data through these powerful tools.

Check out these helpful resources for workbooks:

- [Create an Azure workbook](/en-us/azure/azure-monitor/visualize/workbooks-create-workbook)
- [How to use Identity Workbooks](../identity/monitoring-health/howto-use-workbooks)
- [Create a workbook alert](/en-us/azure/azure-monitor/alerts/tutorial-log-alert)

## Download logs

A **Download** button is available on all logs, both within Global Secure Access and Microsoft Entra Monitoring and health. You can download logs as a JSON or CSV file. For more information, see [How to download logs](../identity/monitoring-health/howto-download-logs).

To narrow down the results of the logs, select **Add filter**. You can filter by:

- Description
- Remote network ID
- Source IP
- Destination IP
- BGP routes advertised count

The following table describes each of the fields in the Remote network health logs.

| Name | Description |
| --- | --- |
| Created date time | Time of original event generation |
| Source IP Address | The IP address of the CPE. The Source IP/Destination IP address pair is unique for each IPsec tunnel. |
| Destination IP Address | The IP address of the Microsoft Entra gateway. The Source IP/Destination IP address pair is unique for each IPsec tunnel. |
| Status | **Tunnel connected:** This event is generated when an IPsec tunnel is successfully established.**Tunnel disconnected:** This event is generated when an IPsec tunnel is disconnected.**BGP connected:** This event is generated when a BGP connectivity is successfully established.**BGP disconnected:** This event is generated when a BGP connectivity goes down.**Remote network alive:** This periodic statistic is generated every 15 minutes for all the active tunnels. |
| Description | Optional description of the event. |
| BGP Routes Advertised Count | Optional count of BGP routes advertised over the IPsec tunnel. This value is 0 for Tunnel connected, Tunnel disconnected, BGP connected, and BGP disconnected events. |
| Sent Bytes | Optional number of bytes sent from source to destination over a tunnel during the last 15 minutes. This value is 0 for Tunnel connected, Tunnel disconnected, BGP connected, and BGP disconnected events. |
| Received Bytes | Optional number of bytes received by source from destination over a tunnel during the last 15 minutes. This value is 0 for Tunnel connected, Tunnel disconnected, BGP connected, and BGP disconnected events. |
| Remote network ID | ID of the remote network the tunnel is associated with. |
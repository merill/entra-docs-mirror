---
layout: Conceptual
title: Global Secure Access logs and monitoring - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/concept-global-secure-access-logs-monitoring
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn about the available Global Secure Access logs and monitoring options.
ms.topic: concept-article
ms.date: 2026-03-12T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: e37a5b46-0282-b307-99a6-c38b9bdb8ee3
document_version_independent_id: 5dcfa453-d7a1-6607-60e0-99027c9d33a6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/concept-global-secure-access-logs-monitoring.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/concept-global-secure-access-logs-monitoring
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/concept-global-secure-access-logs-monitoring.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: f522a82b-77c3-9348-7216-a187cbd97a2c
---

# Global Secure Access logs and monitoring - Global Secure Access | Microsoft Learn

## Overview

As an IT administrator, you need to monitor the performance, experience, and availability of the traffic flowing through your networks. Within the Global Secure Access logs there are many data points that you can review to gain insights into your network traffic. This article describes the logs and dashboards that are available to you and some common monitoring scenarios.

## Dashboard

The Global Secure Access dashboard provides you with visualizations of the traffic flowing through the Microsoft Entra Private Access and Microsoft Entra Internet Access services, which include Microsoft traffic and Private Access traffic. The dashboard provides a summary of the data related to product deployment and insights. Within these categories you can see the number of users, devices, and applications seen in the last 24 hours. You can also see device activity and cross-tenant access.

For more information, see [Global Secure Access dashboard](concept-traffic-dashboard).

## Audit logs (preview)

The Microsoft Entra audit log is a valuable source of information when researching or troubleshooting changes to your Microsoft Entra environment. Changes related to Global Secure Access are captured in the audit logs in several categories, such as filtering policy, forwarding profiles, remote network management, and more.

For more information, see [Global Secure Access audit logs (preview)](how-to-access-audit-logs).

## Traffic logs (preview)

The Global Secure Access traffic logs provide a summary of the network connections and transactions that are occurring in your environment. These logs look at *who* accessed *what* traffic from *where* to *where* and with what *result*. The traffic logs provide a snapshot of all connections in your environment and breaks that down into traffic that applies to your traffic forwarding profiles. The logs details provide the traffic type destination, source IP, and more.

For more information, see [Global Secure Access traffic logs (preview)](how-to-view-traffic-logs).

## Enriched Office 365 logs (preview)

The *Enriched Office 365 logs* provide you with the information you need to gain insights into the performance, experience, and availability of the Microsoft 365 apps your organization uses. You can integrate the logs with a Log Analytics workspace or third-party SIEM tool for further analysis.

Customers use existing *Office Audit logs* for monitoring, detection, investigation, and analytics. We understand the importance of these logs and have partnered with Microsoft 365 to include SharePoint logs. These enriched logs include details like client information and original public IP details that can be used for troubleshooting security scenarios.

For more information, see [Enriched Office 365 logs](how-to-view-enriched-logs).

## Log retention and storage

**Traffic Logs and Remote Network Health Logs:** These logs are retained within the system for 30 days. This duration allows for ample time to review and analyze recent activities and network health status.

**Audit Logs:** The retention period for Audit Logs varies depending on your Microsoft Entra ID license. The table provides a breakdown:

| Report Type | Microsoft Entra ID Free | Microsoft Entra ID P1 | Microsoft Entra ID P2 |
| --- | --- | --- | --- |
| Audit Logs | Seven days | 30 days | 30 days |

**Office Logs:** Office Logs are maintained for a shorter duration, up to only 24 hours.

**Exporting and Storing Logs for Longer Durations:** As a customer, you have the flexibility to export these logs through the diagnostic settings feature. Exporting logs allows you to maintain records for more extended periods beyond the default retention times. This can be crucial for compliance, auditing, and in-depth analysis purposes.
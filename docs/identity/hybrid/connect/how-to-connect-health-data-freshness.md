---
layout: Conceptual
title: Microsoft Entra Connect Health - Health service data isn't up to date alert - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-health-data-freshness
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This document describes the cause of "Health service data isn't up to date" alert and how to troubleshoot it.
ms.subservice: hybrid-connect
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2026-09-10T00:00:00.0000000Z
locale: en-us
document_id: 712b4701-f919-6bd4-72a4-8988f37c92b2
document_version_independent_id: 3ad47282-1957-7704-4355-f20433efb8e1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-health-data-freshness.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-health-data-freshness
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-health-data-freshness.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 2ae86390-0dce-3ca3-027f-a6f747cd4140
---

# Microsoft Entra Connect Health - Health service data isn't up to date alert - Microsoft Entra ID | Microsoft Learn

## Overview

The agents on the on-premises machines that Microsoft Entra Connect Health monitors periodically upload data to the Microsoft Entra Connect Health Service. If the service doesn't receive data from an agent, the information the portal presents will be stale. To highlight the issue, the service raises the **Health service data isn't up to date** alert. This alert is generated when the service hasn't received complete data in the past two hours.

- The **Warning** status alert fires if the Health Service received only **partial** data types sent from the server in the past two hours. The warning status alert doesn't trigger email notifications to configured recipients.
- The **Error** status alert fires if the Health Service hasn't received any data types from the server in the past two hours. The error status alert triggers email notifications to configured recipients.

The service gets the data from agents that are running on the on-premises machines, depending on the service type. The following table lists the agents that run on the machine, what they do, and the data types that the service generates. In some cases, there are multiple services involved in the process, so any of them could be the culprit.

## Understanding the alert

Select the alert row to open the alert details panel. The panel shows when the alert was raised and last detected, the affected servers, resolution guidance, and related documentation. A background process that runs every two hours generates and re-evaluates the alert.

[![Screenshot of Connect Health data freshness alert details with callouts for the issue, recommended fix, and affected servers.](media/how-to-connect-health-data-freshness/connect-health-data-freshness-alert-details.png)](media/how-to-connect-health-data-freshness/connect-health-data-freshness-alert-details.png#lightbox)

The following table maps service types to corresponding required data types:

| Service type | Agent (Windows Service name) | Purpose | Data type generated |
| --- | --- | --- | --- |
| Microsoft Entra Connect (Sync) | Microsoft Entra Connect Health Sync Insights Service | Collect Microsoft Entra Connect-specific information (connectors, synchronization rules, and so on) | - AadSyncService-SynchronizationRules  - AadSyncService-Connectors  - AadSyncService-GlobalConfigurations  - AadSyncService-RunProfileResults  - AadSyncService-ServiceConfigurations  - AadSyncService-ServiceStatus |
|  | Microsoft Entra Connect Health Sync Monitoring Service | Collect Microsoft Entra Connect-specific perf counters, ETW traces, files | Performance counter |
| AD DS | Microsoft Entra Connect Health AD DS Insights Service | Perform synthetic tests, collect topology information, replication metadata | - Adds-TopologyInfo-Json  - Common-TestData-Json (creates the test results) |
|  | Microsoft Entra Connect Health AD DS Monitoring Service | Collect ADDS-specific perf counters, ETW traces, files | - Performance counter  - Common-TestData-Json (uploads the test results) |
| AD FS | Microsoft Entra Connect Health Agent | Perform synthetic tests | TestResult (creates the test results) |
|  | Microsoft Entra Connect Health Agent | Collect ADFS usage metrics | Adfs-UsageMetrics |
|  | Microsoft Entra Connect Health Agent | Collect ADFS-specific perf counters, ETW traces, files | TestResult (uploads the test results) |

## Troubleshooting steps

The steps required to diagnose the issue is given below. The first is a set of basic checks that are common to all Service Types.

Important

This alert follows Connect Health [data retention policy](reference-connect-health-user-privacy#data-retention-policy)

- Make sure the latest versions of the agents are installed. View [release history](reference-connect-health-version-history).
- Make sure that Microsoft Entra Connect Health Agents services are **running** on the machine. For example, Connect Health for AD FS should have two services. ![Screenshot of the Microsoft Entra Connect Health agent connectivity verification results.](media/how-to-connect-health-agent-install/install5.png)
- Make sure to go over and meet the [prerequisites](how-to-connect-health-agent-install#prerequisites).
- Use [test connectivity tool](how-to-connect-health-agent-install#test-connectivity-to-azure-ad-connect-health-service) to discover connectivity issues.
- If you have an HTTP Proxy, follow these [configuration steps](how-to-connect-health-agent-install#configure-azure-ad-connect-health-agents-to-use-http-proxy).
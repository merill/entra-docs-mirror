---
layout: Conceptual
title: Check fleet metrics of Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/fleet-metrics
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to check fleet metrics of a Microsoft Entra Domain Services managed domain.
ms.assetid: 8999eec3-f9da-40b3-997a-7a2587911e96
ms.topic: how-to
ms.date: 2025-02-05T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 77e3f423-d4cc-f23b-285e-c7d680fad2cb
document_version_independent_id: 082ed1d8-f7eb-1563-0a03-722f7fa14214
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/fleet-metrics.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/fleet-metrics
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/fleet-metrics.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 90e6b3e9-2ddd-b94d-dfb0-e78e4d504eb5
---

# Check fleet metrics of Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

Administrators can use Azure Monitor Metrics to configure a scope for Microsoft Entra Domain Services and gain insights into how the service is performing. You can access Domain Services metrics from two places:

- In Azure Monitor Metrics, select **New chart** &gt; **Select a scope** and select the Domain Services instance:

    ![Screenshot of how to select Domain Services for fleet metrics.](media/fleet-metrics/select.png)
- In Domain Services, under **Monitoring**, select **Metrics**:

    ![Screenshot of how to select Domain Services as scope in Azure Monitor Metrics.](media/fleet-metrics/metrics-scope.png)

    The following screenshot shows how to select combined metrics for Total Processor Time and LDAP searches:

    ![Screenshot of combined metrics in Azure Monitor Metrics.](media/fleet-metrics/combined-metrics.png)

    You can also view metrics for a fleet of Domain Services instances:

    ![Screenshot of how to select a Domain Services instance as the scope for fleet metrics.](media/fleet-metrics/metrics-instance.png)

    The following screenshot shows combined metrics for Total Processor Time, DNS Queries, and LDAP searches by role instance:

    ![Screenshot of combined metrics for a Domain Services instance.](media/fleet-metrics/combined-metrics-instance.png)

## Metrics definitions and descriptions

You can select a metric for more details about the data collection.

![Screenshot of fleet metric descriptions.](media/fleet-metrics/descriptions.png)

The following table describes the metrics that are available for Domain Services.

| Metric | Description |
| --- | --- |
| DNS - Total Query Received/sec | The average number of queries received by DNS server in each second. The performance counter data from the domain controller backs it, and you can filter or split it by role instance. |
| Total Response Sent/sec | The average number of responses sent by DNS server in each second. The performance counter data from the domain controller backs it, and you can filter or split it by role instance. |
| NTDS - LDAP Successful Binds/sec | The number of LDAP successful binds per second for the NTDS object. The performance counter data from the domain controller backs it, and you can filter or split it by role instance. |
| % Committed Bytes In Use | The ratio of Memory\\Committed Bytes to the Memory\\Commit Limit. Committed memory is the physical memory in use for which space has been reserved in the paging file should it need to be written to disk. The commit limit is determined by the size of the paging file. If the paging file is enlarged, the commit limit increases, and the ratio is reduced. This counter displays the current percentage value only; it isn't an average. The performance counter data from the domain controller backs it, and you can filter or split it by role instance. |
| Total Processor Time | The percentage of elapsed time that the processor spends to execute a non-Idle thread. It's calculated by measuring the percentage of time that the processor spends executing the idle thread and then subtracting that value from 100%. (Each processor has an idle thread that consumes cycles when no other threads are ready to run). This counter is the primary indicator of processor activity, and displays the average percentage of busy time observed during the sample interval. It should be noted that the accounting calculation of whether the processor is idle is performed at an internal sampling interval of the system clock (10 ms). On today's fast processors, % Processor Time can therefore underestimate the processor utilization as the processor may be spending much time servicing threads between the system clock sampling interval. Workload-based timer applications are one type application that is more likely to be measured inaccurately because timers are signaled just after the sample is taken. The performance counter data from the domain controller backs it, and you can filter or split it by role instance. |
| Kerberos Authentications | The number of times that clients use a ticket to authenticate to this computer per second. The performance counter data from the domain controller backs it, and you can filter or split it by role instance. |
| NTLM Authentications | The number of NTLM authentications processed per second for the Active Directory on this domain controller or for local accounts on this member server. The performance counter data from the domain controller backs it, and you can filter or split it by role instance. |
| % Processor Time (dns) | The percentage of elapsed time that all of dns process threads used the processor to execute instructions. An instruction is the basic unit of execution in a computer, a thread is the object that executes instructions, and a process is the object created when a program is run. Code executed to handle some hardware interrupts and trap conditions are included in this count. The performance counter data from the domain controller backs it, and you can filter or split it by role instance. |
| % Processor Time (lsass) | The percentage of elapsed time that all of lsass process threads used the processor to execute instructions. An instruction is the basic unit of execution in a computer, a thread is the object that executes instructions, and a process is the object created when a program is run. Code executed to handle some hardware interrupts and trap conditions are included in this count. The performance counter data from the domain controller backs it, and you can filter or split it by role instance. |
| NTDS - LDAP Searches/sec | The average number of searches per second for the NTDS object. The performance counter data from the domain controller backs it, and you can filter or split it by role instance. |

## Azure Monitor alert

You can configure metric alerts for Domain Services to be notified of possible problems. Metric alerts are one type of alert for Azure Monitor. For more information about other types of alerts, see [What are Azure Monitor Alerts?](/en-us/azure/azure-monitor/alerts/alerts-overview).

To view and manage Azure Monitor alert, a user needs to be assigned [Azure Monitor roles](/en-us/azure/azure-monitor/roles-permissions-security).

In Azure Monitor or Domain Services Metrics, select **New alert** and configure a Domain Services instance as the scope. Then choose the metrics you want to measure from the list of available signals:

![Screenshot of available alerts.](media/fleet-metrics/available-alerts.png)

The following screenshot shows how to define a metric alert with a threshold for **Total Processor Time**:

![Screenshot of defining a threshold.](media/fleet-metrics/define.png)

You can also configure an alert notification, which can be email, SMS, or voice call:

![Screenshot of how to configure an alert notification.](media/fleet-metrics/configure-alert.png)

The following screenshot shows a metrics alert triggered for **Total Processor Time**:

![Screenshot of alert trigger.](media/fleet-metrics/trigger.png)

In this case, an email notification is sent after an alert activation:

![Screenshot of alert trigger details.](media/fleet-metrics/trigger-details.png)

Another email notification is sent after deactivation of the alert:

![Screenshot of alert resolution.](media/fleet-metrics/resolution.png)

## Select multiple resources

You can upvote to enable multiple resource selection to correlate data between resource types.

![Screenshot of feature upvote.](media/fleet-metrics/upvote.png)
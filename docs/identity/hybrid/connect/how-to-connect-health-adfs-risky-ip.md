---
layout: Conceptual
title: Microsoft Entra Connect Health with the AD FS Risky IP report - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-health-adfs-risky-ip
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This article describes the Microsoft Entra Connect Health AD FS Risky IP report.
ms.reviewer: zhiweiwangmsft
ms.subservice: hybrid-connect
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2026-09-10T00:00:00.0000000Z
ms.custom: H1Hack27Feb2017
locale: en-us
document_id: 54685274-d1d8-afb4-62ae-1f7631edd74f
document_version_independent_id: 01b85b61-d109-b71c-160a-a9ae8095b745
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-health-adfs-risky-ip.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-health-adfs-risky-ip
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-health-adfs-risky-ip.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 90d0dbf9-ab30-84d8-947e-c43d68a1830d
---

# Microsoft Entra Connect Health with the AD FS Risky IP report - Microsoft Entra ID | Microsoft Learn

Active Directory Federation Services (AD FS) customers may expose password authentication endpoints to the internet to provide authentication services for end users to access SaaS applications such as Microsoft 365.

It's possible for a bad actor to attempt logins against your AD FS system to guess an end user’s password and get access to application resources. As of Windows Server 2012 R2, AD FS provides the extranet account lockout functionality to prevent these types of attacks. If you're on an earlier version, we strongly recommend that you upgrade your AD FS system to Windows Server 2016.

Additionally, it's possible for a single IP address to attempt multiple logins against multiple users. In these cases, the number of attempts per user might be under the threshold for account lockout protection in AD FS.

Microsoft Entra Connect Health now provides the *Risky IP report*, which detects this condition and notifies administrators. Here are the key benefits of using this report:

- Detects IP addresses that exceed a threshold of failed password-based logins
- Supports failed logins resulting from bad password or extranet lockout state
- Provides email notifications to alert administrators, with customizable email settings
- Provides customizable threshold settings that match the security policy of an organization
- Provides downloadable reports for offline analysis and integration with other systems via automation

Note

To use this report, you must ensure that AD FS auditing is enabled. For more information, see [Enable auditing for AD FS](how-to-connect-health-adfs#enable-auditing-for-ad-fs).

To access this preview release, you need [Security Reader](../../role-based-access-control/permissions-reference#security-reader) permissions. 

## What's in the report?

The failed sign-in activity client IP addresses are aggregated through Web Application Proxy servers. Each item in the Risky IP report shows aggregated information about failed AD FS sign-in activities that have exceeded the designated threshold.

The report provides the following information:

| Report item | Description |
| --- | --- |
| Time Stamp | The time stamp that's based on [Microsoft Entra admin center](https://entra.microsoft.com) local time when the detection time window starts. All daily events are generated at midnight UTC time. Hourly events have the time stamp rounded to the beginning of the hour. You can find the first activity start time from “firstAuditTimestamp” in the exported file. |
| Trigger Type | The type of detection time window. The aggregation trigger types are per hour or per day. They're helpful in differentiating between a high-frequency brute force attack and a slow attack, where the number of attempts is distributed throughout the day. |
| IP Address | The single risky IP address that had either bad password or extranet lockout sign-in activities. It can be either an IPv4 or an IPv6 address. |
| Bad Password Error Count | The count of bad password errors that occur from the IP address during the detection time window. Bad password errors can happen multiple times to certain users. **Note**: This count doesn't include failed attempts resulting from expired passwords. |
| Extranet Lockout Error Count | The count of extranet lockout errors that occur from the IP address during the detection time window. The extranet lockout errors can happen multiple times to certain users. This count is displayed only if Extranet Lockout is configured in AD FS (versions 2012R2 and later). **Note**: We strongly recommend enabling this feature if you allow extranet logins that use passwords. |
| Unique Users Attempted | The count of unique user accounts that are attempted from the IP address during the detection time window. Differentiates between a single user attack pattern and a multi-user attack pattern. |

Note

- Only activities that exceed the designated threshold are displayed in the report list.
- This report tracks the past 30 days at most.
- This alert report doesn't show Exchange IP addresses or private IP addresses. They are still included in the export list.

Open [Microsoft Entra Connect Health](https://aka.ms/aadconnecthealth), select **AD FS services**, select a service, and then select the **Risky IP Addresses** report. The command bar provides **Refresh**, **Download Manager**, **Notification Settings**, and **Threshold Settings**.

Important

The Risky IP report is being deprecated. The page provides a link to the newer [Risky IP report workbook](how-to-connect-health-adfs-risky-ip-workbook), which supports customizable queries and expanded visualizations.

[![Screenshot of the Connect Health bad IP addresses report with callouts for the workbook migration notice, report actions, and results table.](media/how-to-connect-health-adfs-risky-ip/connect-health-bad-internet-protocol-addresses.png)](media/how-to-connect-health-adfs-risky-ip/connect-health-bad-internet-protocol-addresses.png#lightbox)

## Load balancer IP addresses in the list

Your load balancer aggregate might have failed, causing it to hit the alert threshold. If you're seeing load balancer IP addresses, it's highly likely that your external load balancer isn't sending the client IP address when it passes the request to the Web Application Proxy server. Configure your load balancer correctly to pass forward the client IP address.

## Download the Risky IP report

Select **Download Manager** to review the three most recent export requests or request **Download latest report**. Export requests are limited to one per hour. A completed request provides a link to the risky IP address list from the past 30 days. The export includes all failed AD FS sign-in activities in each detection time window so that you can customize filtering offline. It also includes the following details:

| Report Item | Description |
| --- | --- |
| firstAuditTimestamp | The first time stamp when the failed activities started during the detection time window. |
| lastAuditTimestamp | The last time stamp when the failed activities ended during the detection time window. |
| attemptCountThresholdIsExceeded | The flag if the current activities are exceeding the alerting threshold. |
| isWhitelistedIpAddress | The flag if the IP address is filtered from alerting and reporting. Private IP addresses (*10.x.x.x, 172.x.x.x* and *192.168.x.x*) and Exchange IP addresses are filtered and marked as *True*. If you're seeing private IP address ranges, it's highly likely that your external load balancer isn't sending the client IP address when it passes the request to the Web Application Proxy server. |

## Configure notification settings

Select **Notification Settings** to update the report's administrator contacts. By default, the risky IP alert email notification is in an *off* state. You can enable **Get email notifications for IP addresses exceeding failed activity threshold report**.

The panel also lets you enable notifications for new service alerts, notify all Global Administrators, and manage custom email recipients.

## Configure threshold settings

Select **Threshold Settings** to update the alerting thresholds. The system default values are described in the following table.

The risk IP report threshold settings are separated into four categories.

| Threshold setting | Description |
| --- | --- |
| (Bad U/P + Extranet Lockout) / Day | Reports the activity and triggers an alert notification when the count of Bad Password plus the count of Extranet Lockout exceeds the threshold, per *day*. The default value is 100. |
| (Bad U/P + Extranet Lockout) / Hour | Reports the activity and triggers an alert notification when the count of Bad Password plus the count of Extranet Lockout exceeds the threshold, per *hour*. The default value is 50. |
| Extranet Lockout / Day | Reports the activity and triggers an alert notification when the count of Extranet Lockout exceeds the threshold, per *day*. The default value is 50. |
| Extranet Lockout / Hour | Reports the activity and triggers an alert notification when the count of Extranet Lockout exceeds the threshold, per *hour*. The default value is 25. |

Note

- The change of the report threshold will be applied an hour after the setting change.
- Existing reported items will not be affected by the threshold change.
- We recommend that you analyze the number of events reported within your environment and adjust the threshold appropriately.

## FAQ

**Why am I seeing private IP address ranges in the report?**

Private IP addresses (*10.x.x.x, 172.x.x.x* and *192.168.x.x*) and Exchange IP addresses are filtered and marked as *True* in the IP approved list. If you're seeing private IP address ranges, it's highly likely that your external load balancer isn't sending the client IP address when it passes the request to the Web Application Proxy server.

**Why am I seeing load balancer IP addresses in the report?**

If you're seeing load balancer IP addresses, it's highly likely that your external load balancer isn't sending the client IP address when it passes the request to the Web Application Proxy server. Configure your load balancer correctly to pass forward the client IP address.

**How can I block the IP address?**

You should add the identified malicious IP address to the firewall or block it in Exchange.

**Why can't I see any items in this report?**

- Failed sign-in activities aren't exceeding the threshold settings.
- Ensure that no “Health service isn't up to date” alert is active in your AD FS server list. Read more about [how to troubleshoot this alert](how-to-connect-health-data-freshness).
- Audits aren't enabled in AD FS farms.

**Why can't I access the report?**

You need to have [Security Reader](../../role-based-access-control/permissions-reference#security-reader) permissions.
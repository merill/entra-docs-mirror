---
layout: Conceptual
title: How to access Global Secure Access audit logs (preview) - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-access-audit-logs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to access, archive, and analyze the audit logs for Microsoft's Security Service Edge solution.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: d3866de4-e1f0-34fe-5b07-0f6e69351e1d
document_version_independent_id: 09cd4d34-3e05-760b-33b5-f310cd559b5a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-access-audit-logs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-access-audit-logs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-access-audit-logs.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 448b0094-a286-14c0-4c9f-aa4fbf44c9ef
---

# How to access Global Secure Access audit logs (preview) - Global Secure Access | Microsoft Learn

## Overview

The Microsoft Entra audit logs are a valuable source of information when investigating or troubleshooting changes to your Microsoft Entra environment. Changes related to Global Secure Access are captured in the audit logs in several categories, such as traffic forwarding profiles, remote network management, and more. This article describes how to use the audit log to track changes to your Global Secure Access environment.

## Prerequisites

To access the audit log for your tenant, you must have one of the following roles:

- Reports Reader
- Security Reader
- Security Administrator

Audit logs are available in [all editions of Microsoft Entra](/en-us/azure/active-directory/reports-monitoring/concept-audit-logs). Storage and integration with analysis and monitoring tools may require additional licenses and roles.

## Access the audit logs

There are several ways to view the audit logs. For more information on the options and recommendations for when to use each option, see [How to access activity logs](/en-us/azure/active-directory/reports-monitoring/howto-access-activity-logs).

### Access audit logs from the Microsoft Entra admin center

You can access the audit logs from **Global Secure Access** and from **Microsoft Entra ID Monitoring & health**.

**From Global Secure Access:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) using one of the required roles.
2. Browse to **Global Secure Access** &gt; **Monitor** &gt; **Audit logs**. The filters are pre-populated with the categories and activities related to Global Secure Access.

**From Microsoft Entra monitoring and health:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) using one of the required roles.
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Audit logs**.
3. Select the **Date** range you want to query.
4. Open the **Service** filter, select **Global Secure Access**, and select **Apply**.
5. Open the **Category** filter, select at least one of the available options, and select **Apply**.

## Save audit logs

Audit log data is only kept for 30 days by default, which may not be long enough for every organization. You might also want to integrate your logs with other services for enhanced monitoring and analysis if you need to view or query logs after 30 days.

- [Stream activity logs to an event hub](/en-us/azure/active-directory/reports-monitoring/tutorial-azure-monitor-stream-logs-to-event-hub) to integrate with other tools, like Azure Monitor or Splunk.
- [Export activity logs for storage](/en-us/azure/active-directory/reports-monitoring/quickstart-azure-monitor-route-logs-to-storage-account).
- [Monitor activity in real-time with Microsoft Sentinel](/en-us/azure/sentinel/quickstart-onboard).
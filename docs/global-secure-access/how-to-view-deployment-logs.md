---
layout: Conceptual
title: View and Analyze Deployment Logs in Global Secure Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-view-deployment-logs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Monitor and troubleshoot configuration changes in Global Secure Access using deployment logs. Learn how to view logs, configure settings, and analyze fields.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.custom:
- ai-gen-docs-bap
- ai-gen-description
- ai-seo-date:04/10/2025
- ai-gen-title
locale: en-us
document_id: fb45593a-1e49-0cc0-9e60-1acfa93790f0
document_version_independent_id: fb45593a-1e49-0cc0-9e60-1acfa93790f0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-view-deployment-logs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-view-deployment-logs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-view-deployment-logs.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: be8553ea-e6d3-4538-da2b-22567e733606
---

# View and Analyze Deployment Logs in Global Secure Access - Global Secure Access | Microsoft Learn

## Overview

Deployment logs provide visibility into the status and progress of configuration changes made in Global Secure Access. Unlike other logging features, deployment logs focus specifically on tracking configuration updates. For example, forwarding profile redistributions and remote network changes. Deployment logs provide detailed insights into the deployment status and success across the global network. These logs help administrators track and troubleshoot deployment updates, such as forwarding profile redistributions and remote network updates, across the global network.

This article describes how to view and analyze deployment logs, configure diagnostic settings, and understand log fields.

## Prerequisites

- A **Global Secure Access Administrator** or **Security Administrator** role in Microsoft Entra ID.
- The product requires licensing. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

## How to access the deployment logs

You can view deployment logs using the Microsoft Entra admin center.

To access deployment logs:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference).
2. Navigate to **Global Secure Access** &gt; **Monitor** &gt; **Deployment logs**.
3. Use filters to narrow results based on activity type, status, or other fields.

Note

Deployment logs can also be accessed when a change is made to the configuration of Global Secure Access. A notification shows up at the top right corner of the page when making a configuration change. Select the notification to see the progress of the deployment. ![Screenshot that shows the deployment progress notification.](media/how-to-view-deployment-logs/deployment-progress.png)

### Filter options

To filter the deployment logs to a specific detail, select **Add filter** and then enter the detail for the filter. For example, to look at all the logs for remote network activity, select the activity and then select **Remote Network** and then select **Apply**.

![Screenshot that shows the deployment log activity details.](media/how-to-view-deployment-logs/traffic-activity-details.png)

## Supported scenarios

The Global Secure Access configuration activities included in deployment logs are:

- Remote network
- Filtering Profile
- Audit Logs Settings
- Cross Tenant Access Settings
- Conditional Access Settings
- IP Forwarding Options
- Forwarding Profile

## Deployment log fields

The following table describes the fields available in the deployment logs:

| Name | Description |
| --- | --- |
| **Date** | The timestamp when the event occurred. |
| **Activity** | The type of configuration change (for example, Redistribute Forwarding Profile). |
| **Status** | The outcome of the deployment (for example, Deployment Successful, Deployment Failed). |
| **Initiated By** | The account or admin who initiated the change. |
| **Type** | The category of the configuration change (for example, forwardingProfile, remoteNetwork). |
| **Request ID** | A unique identifier for tracking the deployment. |
| **Error Messages** | Specific error messages for failed deployments. |
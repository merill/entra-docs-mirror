---
layout: Conceptual
title: Log latency for Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/reference-log-latency
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Reference information for the factors that drive sign-in and audit log latency in Microsoft Entra ID
ms.topic: reference
ms.date: 2024-09-27T00:00:00.0000000Z
ms.reviewer: egreenberg14
ms.custom: sfi-image-nochange
locale: en-us
document_id: 2d747163-9cfc-0816-68cf-371ebb584f44
document_version_independent_id: 2d747163-9cfc-0816-68cf-371ebb584f44
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/reference-log-latency.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/reference-log-latency
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/reference-log-latency.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 1196ce1b-d29a-ba67-f2c0-5161c1eb520b
---

# Log latency for Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Latency is the amount of time it takes for Microsoft Entra ID reporting data to appear in the Monitoring and health logs. This article describes the factors that can affect latency.

## Latency and first-time setup

When you upgrade from a free version of Microsoft Entra Premium P1 or P2, you should expect a delay of roughly 24 hours from when you upgrade your tenant before all premium reporting features show data. Many premium reporting features only begin retaining data after this 24-hour period following your upgrade.

When setting up a new storage account or security information and event management (SIEM) tool, you should also expect a delay of 24 hours before reporting data appears in those tools.

When routing activity logs to a Log Analytics workspace for analysis with Azure Monitor logs, you should expect a delay of up to three days before the logs appear in the workspace.

## Reporting latency factors

Many factors influence the latency of reporting data. The type of data, the amount of data, and the infrastructure that the reporting tools are built on can all influence latency. If there's a delay in the underlying infrastructure, Microsoft Entra reports might experience a delay in reporting data.

One key factor in log latency is the path that the data travels from the source event to the logs in the Microsoft Entra admin center. Log data travels through the following systems before it appears in the logs.

1. Customer signs in to a service that uses Microsoft Entra ID as the identity and access service.
2. Log processors read the event metadata and publish it to the Azure storage queue.
3. Event metadata is processed and reviewed for success or failure.
4. Successful events are published to partner services, such as Azure Monitor and Microsoft Graph.
5. IT admin views the data in the Microsoft Entra admin center, or their SIEM tool of choice.

There are many more steps in this process that aren't reflected here. Even with these summarized steps, it's easy to see how latency can be introduced into the system.

## Last sign-in

The last sign-in of a user is one of the most common questions related to log latency. This information is provided by the `signInActivity` property in Microsoft Graph. The signInActivity property provides the last interactive and non-interactive sign-in *attempt* for a user. This property might take up to 24 hours to update. For more information, see [signInActivity resource type](/en-us/graph/api/resources/signinactivity?view=graph-rest-beta&amp;preserve-view=true).

You must be using a [Microsoft Entra role](howto-access-activity-logs#prerequisites) that grants access to the sign-in logs to see this detail, which is found in several places:

- The **Sign-ins** tile in the **My Feed** section of the user's profile.

    [![Screenshot of the user details page with the Sign-ins tile in the My Feed section highlighted.](media/reference-log-latency/user-last-sign-in-tile.png)](media/reference-log-latency/user-last-sign-in-tile-expanded.png#lightbox)
- The **Last interactive sign-in** and **Last non-interactive sign-in** columns in the **Users** list.

    [![Screenshot of the all users list with the last interactive sign-in column highlighted.](media/reference-log-latency/users-list-interactive-sign-in-column.png)](media/reference-log-latency/users-list-interactive-sign-in-column.png#lightbox)
- The sign-in logs filtered for a particular user.

    [![Screenshot of the sign-in logs filtered to a particular user.](media/reference-log-latency/user-filtered-sign-in-logs.png)](media/reference-log-latency/user-filtered-sign-in-logs.png#lightbox)

The last sign-in details that appear on the **Sign-ins** tile on the user profile and the **Last interactive sign-in** and **Last non-interactive sign-in** columns in the **Users** list are *not* real-time.

If you need to see the most recent sign-in date and time for a user, go to the sign-in logs and filter for that user.
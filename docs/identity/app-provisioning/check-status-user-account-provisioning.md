---
layout: Conceptual
title: Report automatic user account provisioning from Microsoft Entra ID to Software as a Service (SaaS) applications - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/check-status-user-account-provisioning
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Learn how to check the status of automatic user account provisioning jobs, and how to troubleshoot the provisioning of individual users.
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: cmmdesai
ms.custom: sfi-image-nochange
locale: en-us
document_id: eaf3f474-cfd3-3a18-93c8-06da1d28f92f
document_version_independent_id: c4898982-29bf-7ff2-8435-9248072ad878
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/check-status-user-account-provisioning.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/check-status-user-account-provisioning
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/check-status-user-account-provisioning.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 3410cf23-0482-dd56-e6da-f46545a8f085
---

# Report automatic user account provisioning from Microsoft Entra ID to Software as a Service (SaaS) applications - Microsoft Entra ID | Microsoft Learn

Microsoft Entra ID includes a [user account provisioning service](user-provisioning). The service helps automate the provisioning deprovisioning of user accounts in SaaS apps and other systems. The automation helps with end-to-end identity lifecycle management. Microsoft Entra ID supports preintegrated user provisioning connectors for many applications and systems. To learn more about user provisioning tutorials, see [Provisioning Tutorials](../saas-apps/tutorial-list).

This article describes how to check the status of provisioning jobs after setup, and how to troubleshoot the provisioning of individual users and groups.

## Overview

Provisioning connectors are set up and configured using the [Microsoft Entra admin center](https://entra.microsoft.com), by following the [provided documentation](../saas-apps/tutorial-list) for the supported application. When the connector is configured and running, provisioning jobs can be reported using the following methods:

- Using the [Microsoft Entra admin center](https://entra.microsoft.com)
- Streaming the provisioning logs into [Azure Monitor](application-provisioning-log-analytics). This method allows for extended data retention and building custom dashboards, alerts, and queries.
- Querying the [Microsoft Graph API](/en-us/graph/api/resources/provisioningobjectsummary) for the provisioning logs.
- Downloading the provisioning logs as a CSV or JSON file.

### Definitions

This article uses the following terms:

- **Source System** - The repository of users that the Microsoft Entra provisioning service synchronizes from. Microsoft Entra ID is the source system for most preintegrated provisioning connectors, however there are some exceptions (example: Workday Inbound Synchronization).
- **Target System** - The repository of users where the Microsoft Entra provisioning service synchronizes. The repository is typically a SaaS application, such as Salesforce, ServiceNow, G Suite, and Dropbox for Business. In some cases the repository can be an on-premises system such as Active Directory, such as Workday Inbound Synchronization to Active Directory.

## Getting provisioning reports from the Microsoft Entra admin center

To get provisioning report information for a given application:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Select **Provisioning logs** in the **Activity** section. You can also browse to the Enterprise Application for which provisioning is configured. For example, if you're provisioning users to LinkedIn Elevate, the navigation path to the application details is:

**Entra ID** &gt; **Enterprise apps** &gt; **All applications** &gt; **LinkedIn Elevate**

From the all applications area, you access both the provisioning progress bar and provisioning logs.

## Provisioning progress bar

The [provisioning progress bar](application-provisioning-when-will-provisioning-finish-specific-user#view-the-provisioning-progress-bar) is visible in the **Provisioning** tab for a given application. It appears in the **Current Status** section and shows the status of the current initial or incremental cycle. This section also shows:

- The total number of users and groups that are synchronized and currently in scope for provisioning between the source system and the target system.
- The last time the synchronization was run. Synchronizations typically occur every 20-40 minutes, after the [initial cycle](how-provisioning-works#provisioning-cycles-initial-and-incremental) completes.
- The status of an [initial cycle](how-provisioning-works#provisioning-cycles-initial-and-incremental) and if the cycle is complete.
- The status of the provisioning process and if it's being placed in quarantine. The status also shows the reason for the quarantine. For example, a status might indicate a failure to communicate with the target system due to invalid admin credentials.

The **Current Status** should be the first place admins look to check on the operational health of the provisioning job.

![Summary report](media/check-status-user-account-provisioning/provisioning-progress-bar-section.png)

You can also use Microsoft Graph to programmatically monitor the status of provisioning to an application. For more information, see [monitor provisioning](application-provisioning-configuration-api#step-5-monitor-provisioning).

## Provisioning logs

All activities performed by the provisioning service are recorded in the Microsoft Entra Provisioning logs. You can access the Provisioning logs in the Microsoft Entra admin center. You can search the provisioning data based on the name of the user or the identifier in either the source system or the target system. For details, see [Provisioning logs](../monitoring-health/concept-provisioning-logs).

## Troubleshooting

The provisioning summary report and Provisioning logs play a key role helping admins troubleshoot various user account provisioning issues.

For scenario-based guidance on how to troubleshoot automatic user provisioning, see [Problems configuring and provisioning users to an application](troubleshoot).
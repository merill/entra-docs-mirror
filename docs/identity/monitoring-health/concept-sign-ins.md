---
layout: Conceptual
title: Sign-in logs in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/concept-sign-ins
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn about the different types of sign-in logs that are available in Microsoft Entra monitoring and health.
ms.topic: concept-article
ms.date: 2025-11-07T00:00:00.0000000Z
ms.reviewer: egreenberg14
ms.custom: sfi-image-nochange,agent-id-ignite
locale: en-us
document_id: 063b43ef-9d19-f5c8-e703-8e86dba97745
document_version_independent_id: b8f4ca53-b6b5-21a0-e407-6fbfcba12c25
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/concept-sign-ins.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/concept-sign-ins
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/concept-sign-ins.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 209d8f7b-96a7-5878-a2dd-545eb6e0955d
---

# Sign-in logs in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Microsoft Entra logs all sign-ins into a Microsoft Entra tenant, which includes your internal apps and resources. As an IT administrator, you need to know what the sign-in log details mean, so that you can interpret the log values correctly.

Reviewing sign-in errors and patterns provides valuable insight into how your users access applications and services. The sign-in logs provided by Microsoft Entra ID are a powerful type of [activity log](overview-monitoring-health) that you can analyze. This article describes several key aspects of the sign-in logs.

Three other activity logs are also available to help monitor the health of your tenant:

- **[Audit](concept-audit-logs)** – Information about changes applied to your tenant, such as users and group management or updates applied to your tenant’s resources.
- **[Sign-ups (preview)](concept-sign-ups)** - For [external tenants](../../external-id/tenant-configurations) only, information about all self-service sign-up attempts, including successful sign-ups and failed attempts.
- **[Provisioning](concept-provisioning-logs)** – Activities performed by a provisioning service, such as the creation of a group in ServiceNow or a user imported from Workday.

## What can you do with sign-in logs?

You can use the sign-in logs to answer questions such as:

- How many users signed into a particular application this week?
- How many failed sign-in attempts occurred in the last 24 hours?
- Are users signing in from specific browsers or operating systems?
- Which of my Azure resources were accessed by managed identities and service principals?

You can also describe the activity associated with a sign-in request by identifying the following details:

- **Who** – The identity (User) performing the sign-in.
- **How** – The client (Application) used for the sign-in.
- **What** – The target (Resource) accessed by the identity.

Note

Entries in the sign-in logs are system generated and can't be changed or deleted.

## How do you access the sign-in logs?

There are several ways to access the logs, depending on your needs. For more information, see [How to access activity logs](howto-access-activity-logs).

To view the sign-in logs from the Microsoft Entra admin center:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Sign-in logs**.

To more effectively use the sign-in logs in the Microsoft Entra admin center, adjust the filters to only view a specific set of logs. For more information, see [Filter sign-in logs](howto-customize-filter-logs).

## What are the types of sign-in logs?

There are four types of logs in the sign-in logs preview:

- [Interactive user sign-ins](concept-interactive-sign-ins)
- [Non-interactive user sign-ins](concept-noninteractive-sign-ins)
- [Service principal sign-ins](concept-service-principal-sign-ins)
- [Managed identity sign-ins](concept-managed-identity-sign-ins)

The legacy sign-in logs experience only includes interactive user sign-ins.

### Agent logs

Agent activity logs are a new log type in our audit and sign-in logs to help you monitor agent related activities. IT administrators can view and manage agent activity directly in the Microsoft Entra admin center and using the Microsoft Graph API. For more information, see [Microsoft Entra Agent ID logs](../../agent-id/identity-professional/sign-in-audit-logs-agents).

## Sign-in data used by other services

Sign-in data is used by several services in Azure and Microsoft Entra to monitor risky sign-ins, provide insight into application usage, and more.

### Microsoft Entra ID Protection

Sign-in log data visualization that relates to risky sign-ins is available in the **Microsoft Entra ID Protection** overview, which uses the following data:

- Risky users
- Risky user sign-ins
- Risky workload identities

For more information about the Microsoft Entra ID Protection tools, see the [Microsoft Entra ID Protection overview](../../id-protection/overview-identity-protection).

### Microsoft Entra Usage and insights

To view application-specific sign-in data, browse to **Microsoft Entra ID** &gt; **Monitoring & health** &gt; **Usage & insights**. These reports provide a closer look at sign-ins for Microsoft Entra application activity and AD FS application activity. For more information, see [Microsoft Entra Usage & insights](concept-usage-insights-report).

[![Screenshot of the Usage &amp; insights report.](media/concept-sign-ins/usage-insights.png)](media/concept-sign-ins/usage-insights-expanded.png#lightbox)

There are several reports available in **Usage & insights**. Some of these reports are in preview.

- Microsoft Entra application activity (preview)
- AD FS application activity
- Authentication methods activity
- Service principal sign-in activity
- Application credential activity

### Microsoft 365 activity logs

You can view Microsoft 365 activity logs from the [Microsoft 365 admin center](/en-us/microsoft-365/admin/admin-overview/admin-center-overview). Microsoft 365 activity and Microsoft Entra activity logs share a significant number of directory resources. Only the Microsoft 365 admin center provides a full view of the Microsoft 365 activity logs.

You can access the Microsoft 365 activity logs programmatically by using the [Office 365 Management APIs](/en-us/office/office-365-management-api/office-365-management-apis-overview).
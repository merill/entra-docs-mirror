---
layout: Conceptual
title: Authentication prompts analysis workbook - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/workbook-authentication-prompts-analysis
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how to use the authentication prompts analysis workbook in Microsoft Entra ID to investigate users getting too many MFA prompts.
ms.topic: how-to
ms.date: 2024-11-04T00:00:00.0000000Z
ms.reviewer: sarbar
ms.custom: sfi-image-nochange
locale: en-us
document_id: be65ec04-2b0d-8a8e-a53a-cb5ca53ac6dd
document_version_independent_id: 324190b6-4465-bcd3-9d44-5a9781090396
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/workbook-authentication-prompts-analysis.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/workbook-authentication-prompts-analysis
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/workbook-authentication-prompts-analysis.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 95661e2f-97b4-3c6f-b574-1fc116baa21b
---

# Authentication prompts analysis workbook - Microsoft Entra ID | Microsoft Learn

As an IT Pro, you want the right information about authentication prompts in your environment so you can detect unexpected prompts and investigate further. Providing you with this type of information is the goal of the **Authentication Prompts Analysis** workbook.

## Prerequisites

To use Azure Workbooks for Microsoft Entra ID, you need:

- A Microsoft Entra tenant with a [Premium P1 license](../../fundamentals/get-started-premium)
- A Log Analytics workspace *and* access to that workspace
- The appropriate roles for Azure Monitor *and* Microsoft Entra ID

### Log Analytics workspace

You must create a [Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace)*before* you can use Microsoft Entra Workbooks. several factors determine access to Log Analytics workspaces. You need the right roles for the workspace *and* the resources sending the data.

For more information, see [Manage access to Log Analytics workspaces](/en-us/azure/azure-monitor/logs/manage-access).

### Azure Monitor roles

Azure Monitor provides [two built-in roles](/en-us/azure/azure-monitor/roles-permissions-security#monitoring-reader) for viewing monitoring data and editing monitoring settings. Azure role-based access control (RBAC) also provides two Log Analytics built-in roles that grant similar access.

- **View**:

    - Monitoring Reader
    - Log Analytics Reader
- **View and modify settings**:

    - Monitoring Contributor
    - Log Analytics Contributor

### Microsoft Entra roles

Read only access allows you to view Microsoft Entra ID log data inside a workbook, query data from Log Analytics, or read logs in the Microsoft Entra admin center. Update access adds the ability to create and edit diagnostic settings to send Microsoft Entra data to a Log Analytics workspace.

- **Read**:

    - Reports Reader
    - Security Reader
    - Global Reader
- **Update**:

    - Security Administrator

For more information on Microsoft Entra built-in roles, see [Microsoft Entra built-in roles](../role-based-access-control/permissions-reference).

For more information on the Log Analytics RBAC roles, see [Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles#log-analytics-contributor).

## Description

![Workbook category](media/workbook-authentication-prompts-analysis/workbook-category.png)

Have you recently received complaints from your users about getting too many authentication prompts?

Over-prompting users can affect productivity and can lead to users getting phished for multifactor authentication (MFA). To be clear, we aren't talking about *if* you should require MFA but *how frequently you should prompt your users*.

The following factors can cause over prompting:

- Misconfigured applications
- Over aggressive prompts policies
- Cyber-attacks

The authentication prompts analysis workbook identifies various types of authentication prompts. The types are based on different factors including users, applications, operating system, processes, and more.

You can use this workbook in the following scenarios:

- To research feedback of users getting too many prompts.
- To detect over-prompting attributed to one specific authentication method, policy application, or device.
- To view authentication prompt counts of high-profile users.
- To track legacy TLS and other authentication process details.

## How to access the workbook

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) using the appropriate combination of roles.
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Workbooks**.
3. Select the **Authentication Prompts Analysis** workbook from the **Usage** section.

## Workbook sections

This workbook breaks down authentication prompts by:

- Method
- Device state
- Application
- User
- Status
- Operating System
- Process detail
- Policy

![Authentication prompts by authentication method](media/workbook-authentication-prompts-analysis/authentication-prompts-by-authentication-method.png)

In many environments, the most used apps are business productivity apps. Anything that isn’t expected should be investigated. The following charts show authentication prompts by application.

![Authentication prompts by application](media/workbook-authentication-prompts-analysis/authentication-prompts-by-application.png)

The **prompts by application list view** shows additional information such as timestamps, and request IDs that help with investigations.

Additionally, you get a summary of the average and median prompts count for your tenant.

![Prompts by application](media/workbook-authentication-prompts-analysis/prompts-by-authentication-method.png)

This workbook also helps track impactful ways to improve your users’ experience and reduce prompts and the relative percentage.

![Recommendations for reducing prompts](media/workbook-authentication-prompts-analysis/recommendations-for-reducing-prompts.png)

## Filters

Take advantage of the filters for more granular views of the data:

![Filter](media/workbook-authentication-prompts-analysis/filters.png)

Filtering for a specific user that has many authentication requests or only showing applications with sign-in failures can also lead to interesting findings to continue to remediate.

## Best practices

- If data isn't showing up or seems to be showing up incorrectly, confirm that you set the **Log Analytics Workspace** and **Subscriptions** on the proper resources.

    ![Set workspace and subscriptions](media/workbook-authentication-prompts-analysis/workspace-and-subscriptions.png)
- If the visuals are taking too much time to load, try reducing the Time filter to 24 hours or less.

    ![Set filter](media/workbook-authentication-prompts-analysis/set-filter.png)
- To understand more about the different policies that affect MFA prompts, see [Optimize reauthentication prompts and understand session lifetime for Microsoft Entra multifactor authentication](../authentication/concepts-azure-multi-factor-authentication-prompts-session-lifetime).
- To learn how to move users from telecom-based methods to the Authenticator app, see [How to run a registration campaign to set up Microsoft Authenticator - Microsoft Authenticator app](../authentication/how-to-mfa-registration-campaign).
---
layout: Conceptual
title: Identity protection risk analysis workbook - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/workbook-risk-analysis
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how to use the identity protection risk analysis workbook in Microsoft Entra ID to explore trends and gaps in your risk policies.
ms.topic: how-to
ms.date: 2024-11-04T00:00:00.0000000Z
ms.reviewer: chuqiaoshi
locale: en-us
document_id: 7adad44f-d491-840c-9ed9-c17e976f1edf
document_version_independent_id: 33ef9c38-c809-1845-e972-1f81b3720634
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/workbook-risk-analysis.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/workbook-risk-analysis
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/workbook-risk-analysis.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ad187a7c-b4d0-f7a2-1f3b-8a9a4733950f
---

# Identity protection risk analysis workbook - Microsoft Entra ID | Microsoft Learn

Microsoft Entra ID Protection detects, remediates, and prevents compromised identities. As an IT administrator, you want to understand risk trends in your organizations and opportunities for better policy configuration. With the Identity Protection Risky Analysis Workbook, you can answer common questions about your Identity Protection implementation.

This article provides you with an overview of the **Identity Protection Risk Analysis** workbook.

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

![Workbook category](media/workbook-risk-analysis/workbook-category.png)

As an IT administrator, you need to understand trends in identity risks and gaps in your policy implementations, to ensure you're best protecting your organizations from identity compromise. The identity protection risk analysis workbook helps you analyze the state of risk in your organization.

**This workbook:**

- Provides visualizations of where in the world risk is being detected.
- Allows you to understand the trends in real time vs. offline risk detections.
- Provides insight into how effective you are at responding to risky users.

## How to access the workbook

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) using the appropriate combination of roles.
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Workbooks**.
3. Select the **Identity Protection Risk Analysis** workbook from the **Usage** section.

## Workbook sections

This workbook has five sections:

- Heatmap of risk detections
- Offline vs real-time risk detections
- Risk detection trends
- Risky users
- Summary

## Filters

This workbook supports setting a time range filter.

![Set time range filter](media/workbook-risk-analysis/time-range-filter.png)

There are more filters in the risk detection trends and risky users sections.

Risk Detection Trends:

- Detection timing type (real-time or offline)
- Risk level (low, medium, high, or none)

Risky Users:

- Risk detail (which indicates what changed a user’s risk level)
- Risk level (low, medium, high, or none)

## Best practices

- **[Enable risky sign-in policies](../../id-protection/concept-identity-protection-policies#sign-in-risk-based-conditional-access-policy)** - To prompt for multifactor authentication (MFA) on medium risk or higher. Enabling the policy reduces the proportion of active real-time risk detections by allowing legitimate users to self-remediate the risk detections with MFA.
- **[Enable a risky user policy](../../id-protection/howto-identity-protection-configure-risk-policies#user-risk-policy-in-conditional-access)** - To enable users to securely remediate their accounts when they're considered high risk. Enabling the policy reduces the number of active at-risk users in your organization by returning the user’s credentials to a safe state.
- To learn more about identity protection, see [What is identity protection](../../id-protection/overview-identity-protection).
- For more information about Microsoft Entra workbooks, see [How to use Microsoft Entra workbooks](howto-use-workbooks).
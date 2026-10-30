---
layout: Conceptual
title: Microsoft Entra ID Protection scenario for mastering risk analysis for effective remediation - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/id-protection-guide-analyze
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra-id-protection
manager: martinco
description: Learn about improving risk analysis to identify risky users, discern risk event types, and examine risk levels for access and identity decisions.
ms.reviewer: gasinh
ms.topic: concept-article
ms.date: 2025-10-31T00:00:00.0000000Z
locale: en-us
document_id: 70473716-8bfb-07f9-1eb2-33b5fbd442ce
document_version_independent_id: 70473716-8bfb-07f9-1eb2-33b5fbd442ce
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/id-protection-guide-analyze.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/id-protection-guide-analyze
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/id-protection-guide-analyze.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/9949a35d-c893-4f91-bf98-ae940fc30f5f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/21f7bb14-0703-4e59-a64b-65dd13773dd3
platformId: e50f512a-7de0-c7c7-796a-cc38e74b68a2
---

# Microsoft Entra ID Protection scenario for mastering risk analysis for effective remediation - Microsoft Entra | Microsoft Learn

The proof-of-concept (PoC) guidance in this series of articles helps you to learn, deploy, and test Microsoft Entra ID Protection to detect, investigate, and remediate identity-based risks.

An overview of the guidance begins with [Introduction to Microsoft Entra ID Protection proof-of-concept guidance](id-protection-guide-introduction).

Detailed guidance continues with these scenarios:

- [Use real-time risk detection to grant access to protected resources](id-protection-guide-detect)
- [Bring identity risk-related telemetry into security investigations](id-protection-guide-investigate)
- [Allow users to self-remediate identity risk for enterprise-managed resources](id-protection-guide-remediate)

This article helps identity administrators begin mastering risk analysis for effective remediation with [Azure Monitor Logs](/en-us/azure/azure-monitor/logs/data-platform-logs). The following list highlights analysis areas:

- Track risk events across users and sign-ins
- Correlate anomalies with [Microsoft Entra Conditional Access](../identity/conditional-access/overview) policies and sign-in logs
- Identify potential threat patterns
    - Enrich investigations and stream telemetry to [Microsoft Defender XDR](/en-us/defender-xdr/microsoft-365-defender) and [Microsoft Sentinel](/en-us/azure/sentinel/overview), a security information and event management (SIEM) tool with threat intelligence and a data-lake architecture
    - You can [search the audit log in Microsoft Defender XDR](/en-us/defender-xdr/microsoft-xdr-auditing).

Use the following sections to learn how to manage common risk event types, flagged users, and risk-level patterns with Azure Monitor logs and Microsoft Entra ID Protection.

- Enable risk analysis with the AADUserRiskEvents table
- Ensure prerequisites are met
- Create a Log Analytics workspace
- Identify risky users
- Discern risk event types
- Examine risk levels
- Get started with Azure Monitor Logs reference tables

## Enable risk analysis with the AADUserRiskEvents table

Identity risks grow in speed and complexity every year. You can use risk insights to grasp the volume and details of potential identity attacks and compromises. Enable Azure Monitor Logs reference tables to analyze risk insights with [Microsoft Entra ID Protection](../id-protection/overview-identity-protection) that detects, investigates, and remediates identity risks. Risk data goes to access decisions tools, or tools for investigation and correlation. Microsoft Entra ID Protection is continuously updated to help organizations stay ahead of emerging threats. Identity risk management becomes more proactive, scalable, and effective.

With insights, reference tables, and more, you can investigate and remediate identity risks with Conditional Access and construct targeted policies to address your organization's risks.

Learn more in the [Azure Monitor Logs overview](/en-us/azure/azure-monitor/logs/data-platform-logs).

In Microsoft Entra ID Protection, there are six risk tables to query risk events, risky users, risky [Service Principals](/en-us/azure/databricks/admin/users-groups/service-principals), and risky agents.

- AADUserRiskEvents
- AADRiskyUsers
- AADServicePrincipalRiskEvents
- AADRiskyServicePrincipals
- AADAgentRiskEvents
- AADRiskyAgents

In this article, the focus is the **AADUserRiskEvents** table. To understand more about discerning risks to your organization, see the following video.

**Mastering risk analysis with Microsoft Entra ID Protection**

## Ensure prerequisites are met

To use Azure Monitor, ensure the following prerequisites are met.

- A Microsoft Entra ID P2 Premium license
    - See [Microsoft Entra plans and pricing](https://www.microsoft.com/security/business/microsoft-entra-pricing?msockid=3c61c9beef5963ba2f03dc9cee156239)
- An Azure account with an active subscription
    - Learn about [Azure accounts](https://azure.microsoft.com/pricing/purchase-options/azure-account/)
- Microsoft.OperationalInsights/workspaces/write permissions to the resource group for the Log Analytics workspace
    - Learn about the **Log Analytics Contributor** role in [manage access to Log Analytics workspaces](/en-us/azure/azure-monitor/logs/manage-access)

## Create a Log Analytics workspace

A Log Analytics workspace is a data store to collect log data types from Azure and non-Azure resources and applications. We recommend you send all log data to one Log Analytics workspace.

1. [Create a Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace).
2. To incorporate the data you want to analyze, add diagnostics settings. See the following list:

- AuditLogs
- SignInLogs
- NonInteractiveUserSignInLogs
- ServicePrincipalSignInLogs
- ManagedIdentitySignInLogs
- RiskyUsers
- UserRiskEvents
- RiskyServicePrincipals
- ServicePrincipalRiskEvents
- RiskyAgents
- AgentRiskEvents

1. To view the Queries hub, got to the Log Analytics workspace.
2. Select **Logs**.
3. Search for **Risk**.
4. Locate the **Recent user risk events query**.
5. Select **Run**.
6. From the dropdown, change **Simple mode** to Kusto Query Language mode (**KQL mode**).

Screenshot of the **KQL mode** option.

![Screenshot of the KQL-mode option in the dropdown menu.](media/id-protection-guide-analyze/kql-mode.png)

## Identify risky users

This section and the following sections illustrate how to analyze risk with Azure Monitor. Risky users have one or more risky sign-ins, or other risky actions.

1. Run the query to summarize the count by **UserDisplayName**.
2. Add a time range in **DetectedDateTime &lt; ago()**.

In the following example query, **30d** is the date range.

```kusto
// Recent user risk events 
// Gets list of the top 100 active user risk events. 
AADUserRiskEvents 
| where DetectedDateTime > ago(30d) 
| where RiskState == "atRisk" 
| take 100 
| summarize count()by UserDisplayName 
```

Use the previous query to identify common user patterns, such as service accounts, or small user subsets generating large amounts of risk. In the example screenshot, one user accounts for significantly more risk events than others. If a single user is responsible for a disproportionate amount of risk in your tenant, we recommend requiring a secure password change.

![Screenshot of risky user data from the query.](media/id-protection-guide-analyze/risky-users.png)

## Discern risk event types

After we've looked at patterns from specific users, we recommend reviewing the detections themselves and summarizing them by detection type.

1. Use the **AADUserRiskEvents** table.
2. Summarize with **RiskEventType**.

**Example query**

```kusto
// Recent user risk events 
// Gets list of the top 100 active user risk events. 
AADUserRiskEvents 
| where DetectedDateTime > ago(30d) 
| where RiskState == "atRisk" 
| take 100  
| summarize count()by RiskEventType 
```

While reviewing risk types, pay attention to large volumes. In the following example, there are several flagged risk events. Most are related to:

- **unfamiliarFeatures**- Detect unfamiliar sign-in properties for a user
    - Enforce session controls such as sign-in frequency, application restrictions, and persistent browser controls
- **anomalousToken**- Set up Conditional Access policies to require password reset and perform multifactor authentication (MFA)
    - Block access for high-risk sign-ins
- **unlikelyTravel**- Add named locations as trusted IPs
    - Enable trusted locations for users that travel frequently

See the following screenshot of results from the active user risk events query.

![Screenshot of the results from the active-user risk events query.](media/id-protection-guide-analyze/risk-events.png)

## Examine risk levels

After we’ve looked at the user behavior and the risk event types, the next step we recommend is to examine the AADUserRiskEvents table again to review the three risk levels: low, medium, and high. Summarize risk by level and analyze total numbers of each risk level.

**Example query**

```kusto
// Recent user risk events 
// Gets list of the top 100 active user risk events. 
AADUserRiskEvents 
| where DetectedDateTime > ago(30d) 
| where RiskState == "atRisk" 
| take 100 
| summarize count()by RiskLevel  
```

In the following screenshot, there are many total detections, but only three are classified as high risk. Filtering by sensitivity—low, medium, or high—helps isolate the most critical issues. Prioritizing high-risk detections first reduces noise and ensures you address the most significant threats. For these cases, we recommend implementing a baseline Conditional Access policy that enforces a secure password change for high-risk users.

![Screenshot of query results that show three high-risk users.](media/id-protection-guide-analyze/three-high.png)

Learn more about access control decisions: [What is Conditional Access?](../identity/conditional-access/overview)

## Get started with Azure Monitor Logs reference tables

To get started, explore the Azure Monitor log reference tables for Microsoft Entra ID Protection. The links below provide a list of tables by name. These logs capture key insights, including user risk events, risky users, Service Principal risk events, and risky Service Principals, among others.

- [AADUserRiskEvents](/en-us/azure/azure-monitor/reference/tables/aaduserriskevents)
- [AADRiskyUsers](/en-us/azure/azure-monitor/reference/tables/aadriskyusers)
- [AADServicePrincipalRiskEvents](/en-us/azure/azure-monitor/reference/tables/aadserviceprincipalriskevents)
- [AADRiskyServicePrincipals](/en-us/azure/azure-monitor/reference/tables/aadriskyserviceprincipals)
- [AADAgentRiskEvents](/en-us/azure/azure-monitor/reference/tables/aadagentriskevents)
- [AADRiskyAgents](/en-us/azure/azure-monitor/reference/tables/aadriskyagents)
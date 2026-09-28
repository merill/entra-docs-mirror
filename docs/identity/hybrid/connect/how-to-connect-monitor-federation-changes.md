---
layout: Conceptual
title: Monitor changes to federation configuration in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-monitor-federation-changes
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This article explains how to monitor changes to your federation configuration with Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 49189495-34ee-cccb-a54b-e9f959167705
document_version_independent_id: 27326982-687e-b2c2-e842-f6724c14cdbd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-monitor-federation-changes.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-monitor-federation-changes
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-monitor-federation-changes.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ab2d6fa2-a2e0-5e82-74e5-dcacf3ccfe9f
---

# Monitor changes to federation configuration in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

When you federate your on-premises environment with Microsoft Entra ID, you establish a trust relationship between the on-premises identity provider and Microsoft Entra ID.

Due to this established trust, Microsoft Entra ID honors the security token issued by the on-premises identity provider post authentication, to grant access to resources protected by Microsoft Entra ID.

Therefore, it's critical that this trust (federation configuration) is monitored closely, and any unusual or suspicious activity is captured.

To monitor the trust relationship, we recommend you set up alerts to be notified when changes are made to the federation configuration.

## Set up alerts to monitor the trust relationship

Follow these steps to set up alerts to monitor the trust relationship:

1. [Configure Microsoft Entra audit logs](../../monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs) to flow to an Azure Log Analytics Workspace.
2. [Create an alert rule](/en-us/azure/azure-monitor/alerts/alerts-create-new-alert-rule) that triggers based on Microsoft Entra ID log query.
3. [Add an action group](/en-us/azure/azure-monitor/alerts/action-groups) to the alert rule that gets notified when the alert condition is met.

After the environment is configured, the data flows as follows:

1. Microsoft Entra logs are populated per the activity in the tenant.
2. The log information flows to the Azure Log Analytics workspace.
3. A background job from Azure Monitor executes the log query based on the configuration of the Alert Rule in the configuration step (2) above.

    ```
     AuditLogs 
     |  extend TargetResource = parse_json(TargetResources) 
     | where ActivityDisplayName contains "Set federation settings on domain" or ActivityDisplayName contains "Set domain authentication" 
     | project TimeGenerated, SourceSystem, TargetResource[0].displayName, AADTenantId, OperationName, InitiatedBy, Result, ActivityDisplayName, ActivityDateTime, Type 
    ```
4. If the result of the query matches the alert logic (that is, the number of results is greater than or equal to 1), then the action group kicks in. Let’s assume that it kicked in, so the flow continues in step 5.
5. Notification is sent to the action group selected while configuring the alert.

Note

In addition to setting up alerts, we recommend periodically reviewing the configured domains within your Microsoft Entra tenant and removing any stale, unrecognized, or suspicious domains.
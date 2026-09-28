---
layout: Conceptual
title: Troubleshoot Conditional Access policy changes - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/troubleshoot-policy-changes-audit-log
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Learn how to use Microsoft Entra audit logs to identify and troubleshoot Conditional Access policy modifications in your environment.
ms.topic: troubleshooting
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: calebb, martinco
ms.custom:
- sfi-image-nochange
- ai-gen-docs-bap
- ai-gen-description
- ai-seo-date:09/02/2025
locale: en-us
document_id: 0dc4ca3e-4ff7-7acd-c448-b479ffcc0f8f
document_version_independent_id: d750ee12-4af9-7db3-f297-450abf98b973
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/troubleshoot-policy-changes-audit-log.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/troubleshoot-policy-changes-audit-log
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/troubleshoot-policy-changes-audit-log.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: d1bdc26d-dff7-3999-7c69-f58a13b15a59
---

# Troubleshoot Conditional Access policy changes - Microsoft Entra ID | Microsoft Learn

## Overview

The Microsoft Entra audit log is a valuable source of information when troubleshooting why and how Conditional Access policy changes happened in your environment.

Audit log data is kept for 30 days by default, which might not be enough for every organization. Organizations can store data longer by changing diagnostic settings in Microsoft Entra ID to:

- Send data to a Log Analytics workspace
- Archive data to a storage account
- Stream data to Event Hubs
- Send data to a partner solution

Find these options under **Entra ID** &gt; **Monitoring & health** &gt; **Diagnostic settings** &gt; **Edit setting**. If you don't have a diagnostic setting, see [Create diagnostic settings to send platform logs and metrics to different destinations](/en-us/azure/azure-monitor/essentials/diagnostic-settings) for instructions to create one.

## Use the audit log

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Audit logs**.
3. Select the **Date** range to query.
4. From the **Service** filter, select **Conditional Access** and select the **Apply** button.

    By default, the audit logs display all activities. Use the **Activity** filter to narrow down the activities. For a full list of the audit log activities for Conditional Access, see the [Audit log activities](../monitoring-health/reference-audit-activities#conditional-access).
5. Select a row to view the details. The **Modified Properties** tab lists the modified JSON values for the selected audit activity.

[![Screenshot of an audit log entry showing old and new JSON values for a Conditional Access policy.](media/troubleshoot-policy-changes-audit-log/old-and-new-policy-properties.png)](media/troubleshoot-policy-changes-audit-log/old-and-new-policy-properties.png#lightbox)

## Use Log Analytics

Log Analytics lets organizations query data using built-in queries or custom-created Kusto queries. For more information, see [Get started with log queries in Azure Monitor](/en-us/azure/azure-monitor/logs/get-started-queries).

[![Screenshot of a Log Analytics query for updates to Conditional Access policies, showing the new and old value location.](media/troubleshoot-policy-changes-audit-log/log-analytics-new-old-value.png)](media/troubleshoot-policy-changes-audit-log/log-analytics-new-old-value.png#lightbox)

After enabling it, find Log Analytics in **Entra ID** &gt; **Monitoring & health** &gt; **Log Analytics**. The table most relevant to Conditional Access administrators is **AuditLogs**.

```kusto
AuditLogs 
| where OperationName == "Update Conditional Access policy"
```

Find changes under **TargetResources** &gt; **modifiedProperties**.

## Reading the values

The old and new values from the audit log and Log Analytics are in JSON format. Compare the two values to identify changes to the policy.

Old policy example:

```json
{
    "conditions": {
        "applications": {
            "applicationFilter": null,
            "excludeApplications": [
            ],
            "includeApplications": [
                "797f4846-ba00-4fd7-ba43-dac1f8f63013"
            ],
            "includeAuthenticationContextClassReferences": [
            ],
            "includeUserActions": [
            ]
        },
        "clientAppTypes": [
            "browser",
            "mobileAppsAndDesktopClients"
        ],
        "servicePrincipalRiskLevels": [
        ],
        "signInRiskLevels": [
        ],
        "userRiskLevels": [
        ],
        "users": {
            "excludeGroups": [
                "eedad040-3722-4bcb-bde5-bc7c857f4983"
            ],
            "excludeRoles": [
            ],
            "excludeUsers": [
            ],
            "includeGroups": [
            ],
            "includeRoles": [
            ],
            "includeUsers": [
                "All"
            ]
        }
    },
    "displayName": "Common Policy - Require MFA for Azure management",
    "grantControls": {
        "builtInControls": [
            "mfa"
        ],
        "customAuthenticationFactors": [
        ],
        "operator": "OR",
        "termsOfUse": [
            "a0d3eb5b-6cbe-472b-a960-0baacbd02b51"
        ]
    },
    "id": "334e26e9-9622-4e0a-a424-102ed4b185b3",
    "modifiedDateTime": "2021-08-09T17:52:40.781994+00:00",
    "state": "enabled"
}

```

Updated policy example:

```json
{
    "conditions": {
        "applications": {
            "applicationFilter": null,
            "excludeApplications": [
            ],
            "includeApplications": [
                "797f4846-ba00-4fd7-ba43-dac1f8f63013"
            ],
            "includeAuthenticationContextClassReferences": [
            ],
            "includeUserActions": [
            ]
        },
        "clientAppTypes": [
            "browser",
            "mobileAppsAndDesktopClients"
        ],
        "servicePrincipalRiskLevels": [
        ],
        "signInRiskLevels": [
        ],
        "userRiskLevels": [
        ],
        "users": {
            "excludeGroups": [
                "eedad040-3722-4bcb-bde5-bc7c857f4983"
            ],
            "excludeRoles": [
            ],
            "excludeUsers": [
            ],
            "includeGroups": [
            ],
            "includeRoles": [
            ],
            "includeUsers": [
                "All"
            ]
        }
    },
    "displayName": "Common Policy - Require MFA for Azure management",
    "grantControls": {
        "builtInControls": [
            "mfa"
        ],
        "customAuthenticationFactors": [
        ],
        "operator": "OR",
        "termsOfUse": [
        ]
    },
    "id": "334e26e9-9622-4e0a-a424-102ed4b185b3",
    "modifiedDateTime": "2021-08-09T17:52:54.9739405+00:00",
    "state": "enabled"
}

```

In the previous example, the updated policy doesn't include terms of use in the grant controls.
---
layout: Conceptual
title: Investigate related tenant signals by using Microsoft Graph (preview) - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/how-to-investigate-related-tenants-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to use Microsoft Graph to retrieve the underlying users and applications behind Tenant Governance related tenant discovery signals.
ms.topic: how-to
ms.date: 2026-07-14T00:00:00.0000000Z
locale: en-us
document_id: e1fe88da-07ce-11f5-dedb-4b903142a55d
document_version_independent_id: e1fe88da-07ce-11f5-dedb-4b903142a55d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/how-to-investigate-related-tenants-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/how-to-investigate-related-tenants-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/how-to-investigate-related-tenants-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: aa3e23e1-1378-ecb6-ba4c-b395e2d3cabe
---

# Investigate related tenant signals by using Microsoft Graph (preview) - Microsoft Entra ID Governance | Microsoft Learn

Important

Microsoft Entra Tenant Governance is currently in PREVIEW. This information relates to a prerelease product that might be substantially modified before release. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Discovery signals for a related tenant are summarized as aggregated, order-of-magnitude metrics. To investigate a signal in depth, you can retrieve the underlying users and applications that contribute to it. The admin center exposes this as a [drill-down experience](how-to-interpret-discovery-data#step-4-drill-into-a-signal-to-see-the-underlying-entities). The same data is available programmatically through Microsoft Graph.

This article describes the workflow for investigating related tenant signals with Microsoft Graph. For the full request and response schema, see the Microsoft Graph API reference linked in Related content.

## When to use investigation hints

Investigation hints let you move from an aggregated, order-of-magnitude metric to the specific users or applications behind it. Use them when you want to:

- Automate related tenant investigation as part of a security or governance workflow.
- Export the underlying users or applications behind a signal for reporting or ticketing.
- Correlate related tenant activity with other signals in your environment.

As with the [drill-down experience](how-to-interpret-discovery-data#step-4-drill-into-a-signal-to-see-the-underlying-entities), investigation hints return live data that can differ from the aggregated metric, and sign-in based signals are limited by your tenant's log retention period. For more information about interpreting these results, see [Interpret tenant discovery data](how-to-interpret-discovery-data).

## Step 1: List related tenants

Retrieve the related tenants for your tenant. Each related tenant returns its discovery metrics (such as `b2BRegistrationMetrics`, `b2BSignInActivityMetrics`, `appB2BSignInActivityMetrics`, `multiTenantApplicationMetrics`, and `billingMetrics`) expanded by default.

```http
GET https://graph.microsoft.com/beta/directory/tenantGovernance/relatedTenants
```

Identify the related tenant (by its tenant ID in the `id` property) and the signal that you want to investigate.

## Step 2: Request investigation hints for a signal

Investigation hints aren't returned by default. To get them, read a related tenant and use a nested `$expand` on the metric relationship that you're investigating. For example, to get the investigation steps for the B2B sign-in signal:

```http
GET https://graph.microsoft.com/beta/directory/tenantGovernance/relatedTenants/{relatedTenantId}?$expand=b2BSignInActivityMetrics($expand=investigationHints)
```

The `investigationHints` relationship returns an ordered collection of investigation steps. The following response is illustrative and shortened for readability.

```json
{
  "b2BSignInActivityMetrics": {
    "investigationHints": [
      {
        "stepNumber": "1",
        "text": "Guidance that explains what this step reveals about the metric.",
        "actionUrl": {
          "displayName": "b2BSignInActivityMetrics.recent.inboundMonthlyTotalUsers§single§§$output",
          "url": "https://graph.microsoft.com/beta/..."
        }
      }
    ]
  }
}
```

## Step 3: Run the investigation steps

Each step is an [actionStep](/en-us/graph/api/resources/tenantgovernanceservices-actionstep?view=graph-rest-beta&amp;preserve-view=true):

- **stepNumber**: The order to run the step in. Run steps in ascending order, because later steps can depend on the output of earlier steps.
- **text**: Human-readable guidance that describes what the step reveals.
- **actionUrl**: An [actionUrl](/en-us/graph/api/resources/tenantgovernanceservices-actionurl?view=graph-rest-beta&amp;preserve-view=true)that identifies the follow-on Microsoft Graph or Azure Resource Manager (ARM) API to call:
    - **url**: A URL template to invoke. It can contain placeholders such as `{@id}`, `{startDate}`, `{endDate}`, or `{sourceDomain}` that you resolve from the related tenant, the caller context, or the output of an earlier step. The value can be empty for steps that only transform data returned by a previous step.
    - **displayName**: A machine-readable directive in the form `metricPath§operation§input§output` that describes how to run the step and how to chain its output into later steps.

Resolve the placeholders, call each step's `url` in ascending `stepNumber` order, and combine the results to reveal the underlying users or applications behind the metric.
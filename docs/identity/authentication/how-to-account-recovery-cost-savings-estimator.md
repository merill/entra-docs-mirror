---
layout: Conceptual
title: Estimate Cost Savings for Account Recovery in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-account-recovery-cost-savings-estimator
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Use the cost savings estimator to compare help desk recovery costs against self-service account recovery in Microsoft Entra ID and project potential savings.
ms.topic: how-to
ms.date: 2026-04-02T00:00:00.0000000Z
ms.reviewer: tilarso
ms.custom: sfi-ga-nochange, sfi-image-nochange, msecd-doc-authoring-1012
locale: en-us
document_id: f116c211-85de-90ab-0cef-6fa5263eb997
document_version_independent_id: f116c211-85de-90ab-0cef-6fa5263eb997
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-account-recovery-cost-savings-estimator.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-account-recovery-cost-savings-estimator
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-account-recovery-cost-savings-estimator.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 0914ebd4-a5e5-b60d-e742-b0e412011835
---

# Estimate Cost Savings for Account Recovery in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The cost savings estimator helps organizations understand the potential financial and productivity benefits of enabling account recovery in Microsoft Entra ID. This tool compares the cost and time impact of traditional help desk recovery versus self-service recovery, providing an estimate of:

- Monthly cost savings
- Time gained per month

Important

Savings shown are estimates based on industry averages and **aren't guaranteed amounts**. Actual savings might vary depending on your subscription, licensing, and internal cost structures.

## How the cost savings estimator works

The estimator calculates:

- Monthly cost savings: The difference between help desk and self-service recovery costs.
- Time gained per month: The reduction in productivity time that's lost when users recover accounts.

### Inputs

You provide the values from the following table.

| Field | Description |
| --- | --- |
| Total users in your organization | Number of active users who may require account recovery. (Defaults to total number of enabled users in the tenant) |
| Percentage of monthly recoveries | Estimated percentage of users needing account recovery each month. |
| Average cost for Mid-tier help desk | Typical cost per recovery handled by help desk (industry average: $60). |
| Productivity time lost (minutes) | Average time a user is unable to work during recovery.*Help desk scenario*: longer (for example, 60 minutes)*Self-service scenario*: shorter (for example, 5 minutes) |

### Outputs

The tool displays two comparison panels:

- Traditional Help Desk: shows total monthly cost and time lost based on your inputs.
- Self-Service Account Recovery (SSAR): shows reduced cost and time lost when using self-service recovery.

At the bottom, you’ll see:

- Monthly cost savings: estimated dollar savings.
- Time gained per month: productivity hours regained.

## Use the estimator

1. Enter your organization’s user count and recovery percentage.
2. Adjust cost and time values to reflect your environment.
3. Compare totals for help desk compared to self-service recovery.
4. Use the savings estimate to:
    - Build a business case for self-service account recovery adoption.
    - Communicate ROI to stakeholders.
    - Plan operational improvements.

## Best practices

- Use realistic values based on your internal help desk costs and recovery times.
- Revisit estimates periodically as user counts and recovery patterns change.
- Combine data with licensing and subscription details for accurate ROI calculations.

## Example of cost savings estimate

For an organization with:

- 112 users
- 3% monthly recoveries
- Help desk cost: $60 per recovery, 60 minutes lost
- Self-service cost: $2 per recovery, 5 minutes lost

Estimated savings:

- $195 per month
- 3.1 hours regained per month
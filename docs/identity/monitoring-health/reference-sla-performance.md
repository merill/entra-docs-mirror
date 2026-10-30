---
layout: Conceptual
title: Service Level Agreement performance for Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/reference-sla-performance
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn about the service level agreement performance and attainment for authentication services in Microsoft Entra ID
ms.topic: reference
ms.date: 2026-01-06T00:00:00.0000000Z
ms.reviewer: sarbar
locale: en-us
document_id: 0921f5ca-15f4-e108-8c88-f71dfc2eaf69
document_version_independent_id: 0917b5ee-31ba-b620-f3db-fd0dcc509b9e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/reference-sla-performance.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/reference-sla-performance
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/reference-sla-performance.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 84e3ccbc-f1c9-0609-8bf9-f70ecf2bc1f9
---

# Service Level Agreement performance for Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

As an identity admin, you might need to track the Microsoft Entra service-level agreement (SLA) performance to make sure Microsoft Entra ID can support your vital apps. This article shows how the Microsoft Entra service performed according to the [SLA for Microsoft Entra ID](https://azure.microsoft.com/support/legal/sla/active-directory/v1_1/).

You can use this article in discussions with app or business owners to help them understand the performance they can expect from Microsoft Entra ID.

Note

This article applies to both workforce and external tenants. (Learn more about [tenant configurations](../../external-id/tenant-configurations)).

## How is SLA measured for Microsoft Entra ID?

Details on how downtime is defined and how uptime percentage is calculated are provided in the [SLA for Microsoft Entra ID](https://azure.microsoft.com/support/legal/sla/active-directory/v1_1/).

Performance is measured in a way that reflects customer authentication experience, rather than simply reporting on whether the system is available to outside connections. This distinction means that the calculation is based on if:

- Users can authenticate
- Microsoft Entra ID successfully issues tokens for target apps after authentication

In other words, the number of unique users who both successfully sign in each minute and are issued a token or an error response are tracked as successful user minutes. If a user's sign-in attempt isn't successfully completed within the minute, it's counted as a failed user minute and contributes to a lower availability percentage. After each month is complete, the availability rate is calculated by dividing the number of successful user minutes by the total of successful plus failed user minutes. This rate is published in the following SLA attainment table.

## No planned downtime

You rely on Microsoft Entra ID to provide identity and access management for your vital systems. To ensure Microsoft Entra ID is available when business operations require it, Microsoft doesn't plan downtime for Microsoft Entra system maintenance. Instead, maintenance is performed as the service runs, without customer impact.

## Recent worldwide SLA performance

To help you plan for moving workloads to Microsoft Entra ID, we publish past SLA performance. These numbers show the level at which Microsoft Entra ID met the requirements in the [SLA for Microsoft Entra ID](https://azure.microsoft.com/support/legal/sla/active-directory/v1_1/), for all tenants.

The numbers in the table are a global total of Microsoft Entra authentications across all customers and geographies. The number is truncated at three places after the decimal. Numbers aren't rounded up, so actual SLA attainment is higher than indicated. We publish the previous month's availability during the first half of the current month.

| Month | 2021 | 2022 | 2023 | 2024 | 2025 | 2026 |
| --- | --- | --- | --- | --- | --- | --- |
| January |  | 99.998% | 99.998% | 99.999% | 99.998% | 99.999% |
| February | 99.999% | 99.999% | 99.999% | 99.999% | 99.998% | 99.999% |
| March | 99.568% | 99.998% | 99.999% | 99.999% | 99.996% | 99.999% |
| April | 99.999% | 99.999% | 99.999% | 99.999% | 99.999%\* | 99.999% |
| May | 99.999% | 99.999% | 99.999% | 99.999% | 99.999% | 99.999% |
| June | 99.999% | 99.999% | 99.999% | 99.999% | 99.999% | 99.999% |
| July | 99.999% | 99.999% | 99.999% | 99.999% | 99.999% | 99.999% |
| August | 99.999% | 99.999% | 99.999% | 99.999% | 99.999% | 99.999% |
| September | 99.999% | 99.998% | 99.999% | 99.999% | 99.999% | 99.999% |
| October | 99.999% | 99.999% | 99.999% | 99.998% | 99.999% |  |
| November | 99.998% | 99.999% | 99.999% | 99.998% | 99.999% |  |
| December | 99.978% | 99.999% | 99.999% | 99.998% | 99.999% |  |

\*Starting in April 2025, we updated our SLA performance calculations to provide a more complete view of the user experience with authentication availability. The new calculation includes authentication successes from Microsoft Entra's resilient infrastructure, such as when the [backup authentication system](../../architecture/backup-authentication-system) succeeds on retry. Before April 2025, these successful sign-ins weren't included in the SLA calculation. With the addition of this new calculation, the SLA performance percentages will increase. For example, the April 2025 number using the previous calculation logic would have been 99.998%. With new logic, it's 99.999%.

## Incident history

All incidents that seriously affect Microsoft Entra performance are documented in the [Azure status history](https://azure.status.microsoft/status/history/). Not all events documented in Azure status history are serious enough to cause Microsoft Entra ID to go below its SLA. You can view information about the impact of incidents, and a root cause analysis of what caused the incident and what steps Microsoft took to prevent future incidents.

## SLA attainment

In addition to publicly reporting global SLA performance, Microsoft Entra ID provides tenant-level SLA performance for organizations with at least 5000 monthly active users. The Service Level Agreement (SLA) attainment is the user authentication availability for Microsoft Entra ID. For the current availability target and details on how SLA is calculated, see [SLA for Microsoft Entra ID](https://azure.microsoft.com/support/legal/sla/active-directory/v1_1/).

To see the tenant-level SLA:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Health**.

Hover your mouse over the bar for a month to view the percentage for that month. A table with the same details appears below the graph.

You can also view SLA attainment using [Microsoft Graph APIs](/en-us/graph/api/resources/azureadauthentication?view=graph-rest-beta&amp;preserve-view=true).

![Screenshot of the SLA attainment report.](media/concept-microsoft-entra-health/sla-attainment.png)
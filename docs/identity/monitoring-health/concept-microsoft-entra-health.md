---
layout: Conceptual
title: Learn about Microsoft Entra Health monitoring - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/concept-microsoft-entra-health
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Monitor the health of your tenant through several identity scenarios and authentication availability rates with Microsoft Entra Health
ms.topic: how-to
ms.date: 2026-02-09T00:00:00.0000000Z
ms.reviewer: sarbar
locale: en-us
document_id: 7bade69c-88bb-3c9d-eaaa-eb004359742d
document_version_independent_id: 7bade69c-88bb-3c9d-eaaa-eb004359742d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/concept-microsoft-entra-health.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/concept-microsoft-entra-health
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/concept-microsoft-entra-health.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: f4d61edc-42af-9232-6c6d-278cb49b2760
---

# Learn about Microsoft Entra Health monitoring - Microsoft Entra ID | Microsoft Learn

Microsoft Entra Health provides you with observability of your Microsoft Entra tenant through continuous low-latency health monitoring and look-back reporting on [Service Level Agreements (SLA)](https://azure.microsoft.com/support/legal/sla/active-directory/v1_1/). The low-latency health monitoring solution includes a set of health metric data streams, known as signals, with built-in alerts designed to help IT operations teams maintain high levels of uptime and service for common Microsoft Entra scenarios. The SLA Attainment is a monthly look-back solution that shows the core authentication availability of Microsoft Entra ID each month.

When these metrics and signals are paired together, you get a comprehensive view of the health of your Microsoft Entra tenant. Regularly monitoring the information provided in Microsoft Entra Health can help you identify trends, potential issues, and areas for improvement in your tenant's health. Email notifications can also be configured to alert you when the service identifies an anomaly in the pattern for your tenant. This article provides an overview of the Microsoft Entra Health monitoring features.

Important

Microsoft Entra Health scenario monitoring and alerts are currently in PREVIEW. This information relates to a prerelease product that might be substantially modified before release. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Access Microsoft Entra Health

Scenario monitoring and SLA Attainment are available in the Microsoft Entra Health area of the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Health**.
    - The **Health Monitoring** tab contains a summary of the signals and alerts on the available health scenarios.
    - The **SLA Attainment** tab displays the user authentication availability for Microsoft Entra ID per month. For more informtion, see [SLA performance for Microsoft Entra ID](reference-sla-performance).

## How Microsoft Entra Health monitoring (preview) works

Scenario Monitoring in Microsoft Entra Health is built on two key components: signals and alerts. Here's a high-level look at how they both work together:

1. Metrics and data are gathered, processed, and converted into meaningful signals displayed in Microsoft Entra Health monitoring.
2. These signals are fed into our anomaly detection service.
3. When the anomaly detection service identifies a significant change to a pattern in the signal, it triggers an alert.
4. When the alert is triggered, an email notification is sent to a set of users, preselected by the tenant admin. This email notification prompts recipients to investigate and determine if there's a problem.
5. After you see an alert, you need to research possible root causes, determine the next steps, and take action to mitigate the root cause. Each health alert contains an impact assessment and links to resources to help you through the process.

### Signals

Many IT administrators spend a considerable amount of time investigating several key scenarios, such as sign-ins requiring multifactor authentication (MFA). Microsoft Entra Health provides a visualization of the data associated with these metrics, so you can quickly identify trends and potential issues.

The following key scenarios can be monitored in Microsoft Entra Health:

- Interactive user sign-in requests that require MFA.
- User sign-in requests that require a managed device through a Conditional Access policy.
- User sign-in requests that require a compliant device through a Conditional Access policy.
- User sign-in requests to applications using SAML authentication.

The data associated with each of these scenarios is aggregated into a view that's specific to that scenario. If you're only interested in sign-ins from compliant devices, you can dive into that scenario without noise from other sign-in activities.

[![Screenshot of the MFA scenario monitoring data.](media/concept-microsoft-entra-health/scenario-monitoring-signal-mfa.png)](media/concept-microsoft-entra-health/scenario-monitoring-signal-mfa-expanded.png#lightbox)

Each scenario detail page provides trends and totals for that scenario for the last 30 days. This data is aggregated every 15 minutes, for low latency insights into your tenant's health.

### Alerts

The anomaly detection service looks at the data and develops dynamic alerting thresholds based on a pattern specific to your tenant. When the service identifies a significant change to that pattern at the tenant level, it triggers an alert. By regularly monitoring these scenarios and reviewing the alerts when they come in, you can more effectively monitor and improve the health of your tenant.

Alerts are specific to your tenant and to the scenario being monitored. Machine learning requires at least four weeks of data to establish a pattern for your tenant. The more data we collect on the signal, the more accurate the anomaly detection service becomes. The service looks back 25-30 minutes on the timeline and triggers an alert if the signal deviates from the pattern.

The service provides alerts for the following scenarios:

- [Sign-ins requiring a Conditional Access compliant device](scenario-health-sign-ins-compliant-managed-device)
- [Sign-ins requiring a Conditional Access managed device](scenario-health-sign-ins-compliant-managed-device)
- [Sign-ins requiring multifactor authentication (MFA)](scenario-health-sign-ins-mfa)
- [Conditional Access block policy](scenario-health-conditional-access-block-policy)
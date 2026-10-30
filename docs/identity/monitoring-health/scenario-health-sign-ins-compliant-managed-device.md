---
layout: Conceptual
title: Sign-ins requiring a compliant or managed device - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/scenario-health-sign-ins-compliant-managed-device
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn about the Microsoft Entra Health signals and alerts for sign-ins that require a compliant or managed device
ms.topic: how-to
ms.date: 2025-06-06T00:00:00.0000000Z
ms.reviewer: sarbar
locale: en-us
document_id: 7a094f50-60e6-492b-e552-9894c3f78506
document_version_independent_id: 7a094f50-60e6-492b-e552-9894c3f78506
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/scenario-health-sign-ins-compliant-managed-device.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/scenario-health-sign-ins-compliant-managed-device
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/scenario-health-sign-ins-compliant-managed-device.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: b3e2ff23-78aa-df54-6fd1-3b4e6e4aff74
---

# Sign-ins requiring a compliant or managed device - Microsoft Entra ID | Microsoft Learn

Microsoft Entra Health monitoring provides a set of tenant-level health metrics you can monitor and alerts when a potential issue or failure condition is detected. There are multiple health scenarios that can be monitored, including two related to devices:

- Sign-ins requiring a Conditional Access compliant device
- Sign-ins requiring a Conditional Access managed device

This article describes the health metrics related to compliant and managed devices and how to troubleshoot a potential issue when you receive an alert. For details on how to interact with the Health Monitoring scenarios and how to investigate all alerts, see [How to investigate health scenario alerts](howto-investigate-health-scenario-alerts).

Important

Microsoft Entra Health scenario monitoring and alerts are currently in PREVIEW. This information relates to a prerelease product that might be substantially modified before release. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Prerequisites

There are different roles, permissions, and license requirements to view health monitoring signals and configure and receive alerts. We recommend using a role with least privilege access to align with the [Zero Trust guidance](/en-us/security/zero-trust/zero-trust-overview).

- A tenant with a [Microsoft Entra P1 or P2 license](../../fundamentals/get-started-premium) is required to *view* the Microsoft Entra health scenario monitoring signals.
- A tenant with both a non-trial [Microsoft Entra P1 or P2 license](../../fundamentals/get-started-premium)*and* at least 100 monthly active users is required to *view alerts* and *receive alert notifications*.
- The [Reports Reader](../role-based-access-control/permissions-reference#reports-reader) role is the least privileged role required to *view scenario monitoring signals, alerts, and alert configurations*.
- The [Helpdesk Administrator](../role-based-access-control/permissions-reference#helpdesk-administrator) is the least privileged role required to *update alerts* and *update alert notification configurations*.
- The `HealthMonitoringAlert.Read.All` permission is required to *view the alerts using the Microsoft Graph API*.
- The `HealthMonitoringAlert.ReadWrite.All` permission is required to *view and modify the alerts using the Microsoft Graph API*.
- For a full list of roles, see [Least privileged role by task](../role-based-access-control/delegate-by-task#microsoft-entra-health-least-privileged-roles).

## Investigate the signals and alerts

Investigating an alert starts with gathering data. With Microsoft Entra Health in the Microsoft Entra admin center, you can view the signal and alert details in one place. You can also view the signals and alerts using the Microsoft Graph API. For more information, see [How to investigate health scenario alerts](howto-investigate-health-scenario-alerts) for guidance on how to gather data using the Microsoft Graph API.

1. Sign into the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Health**. The page opens to the Service Level Agreement (SLA) Attainment page.
3. Select the **Health Monitoring** tab.
4. Select the **Sign-ins requiring a compliant device** or **Sign-ins requiring a managed device** scenario and then select an active alert.

    [![Screenshot of the Microsoft Entra Health landing page.](media/scenario-health-sign-ins-compliant-managed-device/health-monitoring-landing-page-compliant-device.png)](media/scenario-health-sign-ins-compliant-managed-device/health-monitoring-landing-page-compliant-device-expanded.png#lightbox)
5. View the signal from the **View data graph** section to get familiar with the pattern and identify anomalies.

    ![Screenshot of the sign-ins requiring managed device signal.](media/scenario-health-sign-ins-compliant-managed-device/health-monitoring-compliant-device-signal.png)
6. Review your Intune device compliance policies.

    - For more information, see [Intune device compliance overview](/en-us/mem/intune/protect/device-compliance-get-started).
    - Learn how to [Monitor device compliance policies](/en-us/mem/intune/protect/compliance-policy-monitor).
    - If you're not using Intune, review your device management solution's compliance policies.
7. Investigate common Conditional Access issues.

    - [Troubleshoot Conditional Access device compliance policies](/en-us/troubleshoot/mem/intune/device-protection/troubleshoot-conditional-access#devices-appear-compliant-but-users-are-still-blocked).
    - [Troubleshoot Conditional Access sign-in problems](../conditional-access/troubleshoot-conditional-access).
8. Review the sign-in logs.

    - [Review the sign-in log details](concept-sign-in-log-activity-details).
    - Look for users being blocked from signing in *and* have a compliant device policy applied.
9. Check the audit logs for recent policy changes.

    - [Use the audit logs to troubleshoot Conditional Access policy changes](../conditional-access/troubleshoot-policy-changes-audit-log).

## Mitigate common issues

The following common issues could cause a spike in sign-ins requiring a compliant or managed device. This list isn't exhaustive, but provides a starting point for your investigation.

### Many users are blocked from signing in from known devices

If a large group of users are blocked from signing in to known devices, a spike could indicate that these devices have fallen out of compliance. If the number of affected users indicates a high percentage of your organization's users, you might be looking at a widespread issue.

To investigate:

1. From the **Affected entities** section of the selected scenario, select **View** for users.

    - A sample of affected users appears in a panel. Select a user to navigate directly to their profile where you can view their sign-in activity and other details.
    - With the Microsoft Graph API, look for the "user" `resourceType` and the `impactedCount` value in the impact summary.

    ![Screenshot of the affected entities.](media/scenario-health-sign-ins-compliant-managed-device/affected-entities-example.png)
2. Check your [Intune device compliance policy](/en-us/mem/intune/protect/device-compliance-get-started).
3. Check your [Conditional Access device compliance policies](/en-us/troubleshoot/mem/intune/device-protection/troubleshoot-conditional-access#devices-appear-compliant-but-users-are-still-blocked).

### User is blocked from signing in from an unknown device

If the increase in blocked sign-ins is coming from an unknown device, that spike could indicate that an attacker has acquired a user's credentials and is attempting to sign in from a device used for such attacks. If the number of affected users shows a small subset of users, the issue might be user-specific.

To investigate:

1. From the **Affected entities** section of the selected scenario, select **View** for users.

    - A list of affected users appears in a panel. Select a user to navigate directly to their profile where you can view their sign-in activity and other details.
    - With the Microsoft Graph API, look for the "user" `resourceType` and the `impactedCount` value in the impact summary.
2. [Review the sign-in logs](concept-sign-in-log-activity-details).
3. [Investigate risk with Microsoft Entra ID Protection](../../id-protection/howto-identity-protection-investigate-risk).

Note

Microsoft Entra ID Protection requires a Microsoft Entra P2 license.

### Network issues

There could be a regional system outage that required a large number of users to sign in at the same time.

To investigate:

1. From the **Affected entities** section of the selected scenario, select **View** for users.

    - A list of affected users appears in a panel. Select a user to navigate directly to their profile where you can view their sign-in activity and other details.
    - With the Microsoft Graph API, look for the "user" `resourceType` and the `impactedCount` value in the impact summary.
2. Check your system and network health to see if an outage or update matches the same timeframe as the anomaly.
3. [Review the sign-in logs](concept-sign-in-log-activity-details).

    - Adjust your filter to show sign-ins from a region where an affected user is located.
4. If your organization is using Global Secure Access, review the [traffic logs](../../global-secure-access/how-to-view-traffic-logs).
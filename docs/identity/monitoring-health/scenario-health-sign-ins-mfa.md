---
layout: Conceptual
title: Sign-ins requiring Microsoft Entra MFA - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/scenario-health-sign-ins-mfa
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn about the Microsoft Entra Health signals and alerts for sign-ins that require Microsoft Entra multifactor authentication
ms.topic: how-to
ms.date: 2025-06-06T00:00:00.0000000Z
ms.reviewer: sarbar
locale: en-us
document_id: 67d9242f-903d-6f16-b978-e9ced8874419
document_version_independent_id: 67d9242f-903d-6f16-b978-e9ced8874419
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/scenario-health-sign-ins-mfa.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/scenario-health-sign-ins-mfa
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/scenario-health-sign-ins-mfa.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 13b03f06-3a4c-540f-b410-c3c00e458041
---

# Sign-ins requiring Microsoft Entra MFA - Microsoft Entra ID | Microsoft Learn

Microsoft Entra Health monitoring provides a set of tenant-level health metrics you can monitor and alerts when a potential issue or failure condition is detected. There are multiple health scenarios that can be monitored, including Microsoft Entra multifactor authentication (MFA).

This scenario:

- Aggregates the number of users who successfully completed an MFA sign-in using a Microsoft Entra cloud MFA service.
- Captures interactive sign-ins with Microsoft Entra MFA, aggregating both successes and failures.
- Excludes when a user refreshes the session without completing the interactive MFA or using passwordless sign-in methods.

This article describes these health metrics and how to troubleshoot a potential issue when you receive an alert. For details on how to interact with the Health Monitoring scenarios and how to investigate all alerts, see [How to investigate health scenario alerts](howto-investigate-health-scenario-alerts).

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
4. Select the **Sign-ins requiring Entra ID MFA** scenario and then select an active alert.

    [![Screenshot of the Microsoft Entra Health landing page.](media/scenario-health-sign-ins-mfa/health-monitoring-landing-page.png)](media/scenario-health-sign-ins-mfa/health-monitoring-landing-page-expanded.png#lightbox)
5. View the signal from the **View data graph** section to get familiar with the pattern and identify anomalies.

    [![Screenshot of the sign-ins requiring MFA signal.](media/scenario-health-sign-ins-mfa/scenario-monitoring-signal-mfa.png)](media/scenario-health-sign-ins-mfa/scenario-monitoring-signal-mfa-expanded.png#lightbox)
6. Review the sign-in logs.

    - [Review the sign-in log details](concept-sign-in-log-activity-details).
    - Look for users being blocked from signing in *and* have a Conditional Access policy requiring MFA applied.
7. Check the audit logs for recent policy changes.

    - [Use the audit logs to troubleshoot Conditional Access policy changes](../conditional-access/troubleshoot-policy-changes-audit-log).

## Mitigate common issues

The following common issues could cause a spike in MFA sign-ins. This list isn't exhaustive, but provides a starting point for your investigation.

### Application configuration issues

An increase in sign-ins requiring MFA could indicate a policy change or new feature rollout potentially triggered a large number of users to sign in around the same time.

To investigate:

1. From the **Affected entities** section of the selected scenario, select **View** for applications.

    - A list of affected applications appears in a panel. Select the application to navigate directly to the application's details where you can view the audit logs and other details.
    - With the Microsoft Graph API, look for the "application" `resourceType` in the impact summary.
2. Review the audit logs for the application.

    - Determine if the application was recently added or reconfigured, which might trigger a large number of users signing in.
3. Review the sign-in logs.

    - Use the **Application** column to filter for the same application or date range to look for any other patterns.

### User authentication issues

An increase in sign-ins requiring MFA could indicate a brute force attack, where multiple unauthorized sign-in attempts are made to a user's account.

To investigate:

1. From the **Affected entities** section of the selected scenario, select **View** for users.

    - A list of affected users appears in a panel. Select a user to navigate directly to their profile where you can view their sign-in activity and other details.
    - With the Microsoft Graph API, look for the "user" `resourceType` and the `impactedCount` value in the impact summary.
2. Review the sign-in logs.

    - Use the following filters in the sign-in logs:
        - **Status**: Failure
        - **Authentication requirement**: Multifactor authentication
        - Adjust the date to match the timeframe indicated in the impact summary.
    - Are the failed sign-in attempts coming from the same IP address?
    - Are the failed sign-in attempts from the same user?
    - Run the [sign-in diagnostic](howto-use-sign-in-diagnostics) to rule out standard user error issues or initial MFA setup issues.

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
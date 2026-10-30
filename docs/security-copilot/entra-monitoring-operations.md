---
layout: Conceptual
title: Understand monitoring with Microsoft Security Copilot | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/security-copilot/entra-monitoring-operations
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: cilwerner
ms.author: cwerner
manager: pmwongera
description: Use Microsoft Security Copilot in the Microsoft Entra admin center to monitor sign-in activities, audit logs, provisioning logs, health alerts, and service level agreements.
ms.reviewer: ptyagi
ms.date: 2025-09-23T00:00:00.0000000Z
ms.update-cycle: 180-days
ms.topic: how-to
ms.service: entra
ms.custom: security-copilot
ms.collection: msec-ai-copilot
locale: en-us
document_id: a1b95a8e-5a40-70cb-68dd-db4beacb05ec
document_version_independent_id: a1b95a8e-5a40-70cb-68dd-db4beacb05ec
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/security-copilot/entra-monitoring-operations.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-copilot/entra-monitoring-operations
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/security-copilot/entra-monitoring-operations.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 1e1ed127-1844-8b3b-5838-8ae52c190ae7
---

# Understand monitoring with Microsoft Security Copilot | Microsoft Learn

Microsoft Security Copilot streamlines operational monitoring in Microsoft Entra by enabling administrators to quickly analyze sign-in activities, investigate audit logs, monitor system health, and track service performance using natural language queries. This capability helps maintain operational awareness and quickly identify and respond to issues before they impact your organization.

This article describes how an IT administrator could use Microsoft Security Copilot monitoring and operations skills to conduct an operational health review of their Microsoft Entra environment by covering the following use cases:

- Analyze sign-in activities
- Investigate audit logs for administrative and user changes
- Analyze provisioning activities
- Improve security posture through recommendations
- Monitor system health and proactively address alerts
- Track service level agreement (SLA) performance

Use the prompts and examples in this article to compile your findings into actionable insights and reports for operational reviews and incident response by your team or management.

## Prerequisites

The following roles and licenses are required for different monitoring and operations use cases:

| Use case | Role | License | Tenant |
| --- | --- | --- | --- |
| **Sign-in logs** | [Reports Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#reports-reader), [Security Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#security-reader), [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator), or [Global Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#global-reader) | [Microsoft Entra ID P1 or P2 license](/en-us/entra/id-protection/overview-identity-protection#license-requirements) | Any public cloud tenant with sign-in data |
| **Audit logs** | [Reports Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#reports-reader), [Security Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#security-reader), [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator), or [Global Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator) | Free license required | Any public cloud tenant with audit activity |
| **Provisioning logs** | [Reports Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#reports-reader), [Global Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#global-reader), or [Application Owner](/en-us/entra/identity/role-based-access-control/permissions-reference#application-owner) | Free for 7 days, then [Microsoft Entra ID P1](/en-us/entra/id-protection/overview-identity-protection#license-requirements) thereafter | Any tenant using the [Microsoft Entra provisioning service](../identity/hybrid/what-is-provisioning) |
| **Recommendations** | [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Identity Governance Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#identity-governance-administrator), [Privileged Role Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#privileged-role-administrator), [Conditional Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#conditional-access-administrator), [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator), [Hybrid Identity Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#hybrid-identity-administrator), [Authentication Policy Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#authentication-policy-administrator), [Authentication Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#authentication-administrator) | Free Microsoft Entra ID or [P1/P2](/en-us/entra/id-protection/overview-identity-protection#license-requirements) | Any tenant, also available in Workload ID |
| **Health monitoring alerts** | [Reports Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#reports-reader), [Helpdesk Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#helpdesk-administrator), [Security Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#security-reader), [Security Operator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-operator), [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator), or [Global Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#global-reader) | [Microsoft Entra ID P2 licenses](/en-us/entra/id-protection/overview-identity-protection#license-requirements) | Public cloud tenant |
| **Service Level Agreement** | [Reports Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#reports-reader) | Any Microsoft Entra ID license | Any tenant |

## Launch Security Copilot in Microsoft Entra

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with the appropriate administrative role(s) for your scenario based off the specific use cases.
2. Launch Security Copilot from the **Copilot** button in the Microsoft Entra admin center.

    ![Screenshot that shows Security Copilot in the Microsoft Entra admin center.](media/copilot-security-entra/security-copilot-entra-admin-center.png)
3. Refer to the following use cases and prompts to retrieve information or perform actions using natural language queries.

Note

If an action is blocked by insufficient permissions, a recommended role is displayed. You can use the following prompt in the Security Copilot chat to activate the required role. This is dependent on having an eligible role assignment that provides the necessary access.

- *Activate the {required role} so that I can perform {the desired task}.*

## Analyze sign-in activities

You can begin your assessment by analyzing sign-in activities across your organization. Understanding authentication patterns and identifying potential issues is crucial for maintaining security and user experience in your organization.

### Application and authentication analysis

Start by investigating sign-in patterns related to specific applications and authentication methods to ensure security policies are being followed and to identify any anomalies or issues. Use the following prompts to get the information you need:

- *Show sign-ins to a specific application.*
- *Show sign-ins without multifactor authentication.*
- *Show sign-in failures due to a specific Conditional Access policy.*
- *Show sign-ins with unsatisfied Conditional Access Policies.*

### Device and location analysis

You can further analyze sign-in activities based on device compliance, operating systems, browsers, and geographic locations to monitor for unusual patterns or potential security threats, and ensure corporate devices are being used appropriately. Use the following prompts to get the information you need:

- *Show sign-ins from non-compliant devices.*
- *Show logins from specific web browsers.*
- *Show logins from specific operating systems.*
- *Show sign-ins from specific locations.*

### User activity and security monitoring

You can hone in on individual user activities to monitor for suspicious behavior, or risky sign-ins that may indicate compromised accounts or security threats that require immediate attention. Use the following prompts to get the information you need:

- *Show sign-in activities since a specific time period.*
- *Show sign-in activity for the user Casey Jensen.*
- *Show suspicious login activities.*
- *Display risky sign-ins.*

## Investigate audit logs for administrative and user changes

Next, investigate audit logs to track changes made by administrators and users in your Microsoft Entra environment. This analysis helps identify potential security issues, ensure compliance, and ensure proper governance of administrative activities. Use the following prompts to gather the information you need:

### Group management activities

You can continue your investigation by focusing on group management activities, which is important for maintaining proper access controls and ensuring that group-related changes are tracked for security and compliance purposes. Use the following prompts to get the information you need:

- *Show me recently deleted groups.*
- *What groups were deleted recently?*
- *Last deleted groups in my directory?*
- *Who created this group?*
- *Find out who created a specific group.*
- *Group creation details.*
- *What groups were created by these users?*
- *Show groups created by specific users.*
- *List all groups created by the user Casey Jensen.*

### Security and authentication activities

To identify potential security issues, focus on security and authentication-related activities in the audit logs. This helps ensure that security policies are being followed and that any suspicious activities are promptly investigated. You can also investigate service principal activities to ensure these critical operations are functioning correctly. Use the following prompts to get the information you need:

- *Show me risky sign-ins.*
- *List suspicious logins.*
- *Are there any risky authentications?*
- *List jobs for this service principal.*

## Analyze provisioning activities

After investigating audit logs, you can focus specifically on provisioning activities within your Microsoft Entra environment. Provisioning logs provide valuable insights into user account lifecycle operations, helping administrators ensure that users are being created, updated, and deleted as intended across connected applications and systems. This analysis is crucial for maintaining the integrity of your identity infrastructure and ensuring smooth user management processes.

### User provisioning monitoring

Start by monitoring individual user provisioning activities to track account lifecycle events and ensure that provisioning operations are working correctly for specific users. Use the following prompts to get the information you need:

- *Show provisioning logs for this user.*
- *Get provisioning history for user.*
- *Show user provisioning activity.*
- *Show recent provisioning events for this user.*

### Provisioning failure analysis

When provisioning issues occur, it's important to quickly identify and resolve them to prevent user access problems. Focus on provisioning failures to understand what went wrong and take corrective action. Use the following prompts to get the information you need:

- *Show provisioning failures.*
- *List all failed provisioning attempts.*
- *Show the provisioning error logs.*

### Provisioning success tracking

Monitor successful provisioning operations to ensure that your provisioning service is functioning optimally and to track completed lifecycle events. This helps verify that intended changes are being applied correctly. Use the following prompts to get the information you need:

- *Show the successful provisioning deletions.*
- *Were any users successfully deleted by the provisioning service?*
- *Show successful provisioning disables.*
- *Were any users successfully disabled by the provisioning service?*
- *Show successful provisioning creates.*
- *List successful object creations.*

### Provisioning job status monitoring

You can also monitor the status and performance of your provisioning jobs to ensure they are running correctly and identify any issues that may need attention. Use the following prompts to get the information you need:

- *Check provisioning job status.*
- *Is my provisioning job completed?*
- *Show provisioning jobs for this service principal.*

## Improve security posture through recommendations

To get a comprehensive view of your security posture, you can leverage Microsoft Entra recommendations, which can help identify areas for improvement and provide actionable insights to enhance your organization's security and compliance with best practices.

### General recommendations and secure score

Start with general recommendations and secure score analysis to get an overview of your tenant's security posture. Use the following prompts to gather the information you need:

- *List all Entra recommendations.*
- *Show my tenant's historical Secure Score data.*
- *Show Entra recommendation "example" and its details.*
- *Show the resources affected by an Entra recommendation.*
- *Show resource "example" of Entra recommendation "example".*
- *List secure score recommendations.*
- *List best practice recommendations.*

### Targeted recommendations by category

Once you have a general overview, you can focus on specific categories of recommendations to address particular areas of concern, such as conditional access policies, application security, and tenant configuration. Use the following prompts to get the information you need:

- *List recommendations for conditional access policies.*
- *Show Entra recommendations for a specific feature area.*
- *List high-priority recommendations.*
- *List recommendations with high priority.*
- *List recommendations that are active.*
- *List recommendations to improve app portfolio health.*
- *List recommendations to reduce surface area risk.*
- *List recommendations to improve security posture of my apps.*
- *List recommendations for tenant configuration.*
- *Show Entra recommendations by impact type.*

### Application credential management

You can also focus on application credential management to ensure that your applications are secure and that credentials are being managed properly to prevent unauthorized access. Use the following prompts to get the information you need:

- *Which enterprise applications have credentials about to expire?*
- *Show me service principals with credentials that are expiring soon.*
- *Show me applications with credentials that are expiring soon.*
- *Which of our apps are stale or unused in the tenant?*
- *List the unused apps.*

## Monitor system health

You can continue your assessment by monitoring system health to detect anomalies and proactively address potential issues before they impact your organization. Proactive health monitoring can help prevent service disruptions and maintain system reliability.

### Health alert monitoring

For a general overview of your system's health, you can start by monitoring health alerts. This helps you stay informed about any issues that may require attention and ensures that your systems are functioning optimally. Use the following prompts to get the information you need:

- *What health alerts do I have in my tenant?*
- *List all active health monitoring alerts.*
- *What are my recent health monitoring alerts?*
- *What users are impacted according to the active health monitoring alerts?*
- *Show me health monitoring alert details for alert ID [alertId].*

### Scenario-specific health monitoring

Once you have a general overview, you can focus on specific health monitoring scenarios to address particular areas of concern, such as multifactor authentication (MFA) issues or device compliance. Use the following prompts or ones specific to your scenario to get the information you need:

- *Show me health monitoring alerts related to MFA sign in failure.*
- *Show me managed device health monitoring alerts.*
- *Show me compliant device health monitoring alerts.*
- *Show me device scenario health monitoring alerts.*

## Track Service Level Agreement performance

Finally, you can assess your Service Level Agreement (SLA) performance to ensure that your organization is meeting its commitments and to identify any areas for improvement. Monitor SLA for authentication availability and review SLA reports in conjunction with service outages to ensure service quality and eligibility for service credits.

### SLA performance monitoring

Use the following prompts to monitor your SLA performance and identify any potential issues that may require attention:

- *What is my SLA for Microsoft Entra authentication?*
- *What is my Microsoft Entra SLA?*
- *What is the SLA of Microsoft Entra authentication?*
- *Show me my tenant's authentication availability.*
- *Has my tenant had an SLA breach in the last "X" months?*
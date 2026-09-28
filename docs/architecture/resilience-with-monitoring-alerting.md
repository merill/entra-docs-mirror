---
layout: Conceptual
title: Resilience through monitoring and analytics using Azure AD B2C - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/resilience-with-monitoring-alerting
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Resilience through monitoring and analytics using Azure AD B2C
ms.topic: how-to
ms.reviewer: gasinh
ms.date: 2025-05-20T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 35e2198c-0061-8b0f-34f8-d52e2d8c068e
document_version_independent_id: 63b865c8-9a18-d4ad-8bd8-21a7f23f1f13
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/resilience-with-monitoring-alerting.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/resilience-with-monitoring-alerting
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/resilience-with-monitoring-alerting.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d5d9b014-6bbe-145f-70e0-b8ca72e0efe1
---

# Resilience through monitoring and analytics using Azure AD B2C - Microsoft Entra | Microsoft Learn

Important

Effective May 1, 2025, Azure Active Directory B2C (Azure AD B2C) is no longer available for new customers to purchase. To learn more, see [Is Azure AD B2C still available to purchase?](/en-us/azure/active-directory-b2c/faq?tabs=app-reg-ga#azure-ad-b2c-end-of-sale) in our FAQ.

Monitoring maximizes the availability and performance of your applications and services. It delivers a comprehensive solution for collecting, analyzing, and acting on telemetry from your infrastructure and applications. Alerts notify you when issues are found with your service or applications. You can identify and address issues before the end users of your service notice them. [Microsoft Entra ID Log Analytics](https://azure.microsoft.com/services/monitor/?OCID=AID2100131_SEM_6d16332c03501fc9c1f46c94726d2264:G:s&amp;ef_id=6d16332c03501fc9c1f46c94726d2264:G:s&amp;msclkid=6d16332c03501fc9c1f46c94726d2264#features) helps you analyze, search the audit logs and sign-in logs, and build custom views.

## Monitor and get notified through alerts

Monitoring your system and infrastructure helps ensure the overall health of your services. It starts with the definition of business metrics, such as, new user arrival, end user authentication rates, and conversion. Configure such indicators to monitor. If you're planning for an upcoming surge because of a promotion or holiday traffic, revise your estimates for the event and corresponding benchmark for the business metrics. After the event, fall back to the previous benchmark.

Similarly, to detect failures or performance disruptions, set up a good baseline and then define alerting. Respond to emerging issues promptly.

### Implement monitoring and alerting

- **Monitoring**: Use [Azure Monitor](/en-us/azure/active-directory-b2c/azure-monitor) to continuously monitor health against key Service Level Objectives (SLO). Get notification when a critical change happens. Identify Azure AD B2C policy or an application as a critical component of your business whose health needs to be monitored to maintain SLO. Identify key indicators that align with your SLOs. For example, track the following metrics, since a sudden drop in either leads to a loss in business.

    - **Total requests**: The total "n" number of requests sent to Azure AD B2C policy.
    - **Success rate (%)**: Successful requests/Total number of requests.

    Access the [key indicators](/en-us/azure/active-directory-b2c/view-audit-logs) in [application insights](/en-us/azure/active-directory-b2c/analytics-with-application-insights) where Azure AD B2C policy-based logs, [audit logs](/en-us/azure/active-directory-b2c/analytics-with-application-insights), and sign-in logs are stored.

    - **Visualizations**: Use Log Analytics to build dashboards to visually monitor the key indicators.
    - **Current period**: Create temporal charts to show changes in the total requests and success rate (%) in the current period, for example, current week.
    - **Previous period**: Create temporal charts to show changes in the total requests and success rate (%) over some previous period.
- **Alerting**: Using Log Analytics, define [alerts](/en-us/azure/azure-monitor/alerts/alerts-create-new-alert-rule) triggered when there are sudden changes in the key indicators. These changes might negatively affect the SLOs. Alerts use various forms of notification methods including email, SMS, and webhooks. Define a criterion as a threshold for the alert trigger. For example:

    - Alert for abrupt drop in total requests: Trigger an alert when total requests drop abruptly. For example, when there's a 25% drop in requests compared to previous period, raise an alert.
    - Alert for significant drop in success rate (%): Trigger an alert when success rate of the selected policy drops.
    - Upon receiving an alert, troubleshoot the issue using [Log Analytics](/en-us/azure/azure-monitor/visualize/workbooks-view-designer-conversion-overview), [Application Insights](/en-us/azure/active-directory-b2c/troubleshoot-with-application-insights), and [VS Code extension](https://marketplace.visualstudio.com/items?itemName=AzureADB2CTools.aadb2c) for Azure AD B2C. After you resolve the issue and deploy an updated application or policy, it monitors key indicators until they return to normal range.
- **Service alerts**: Use the [Azure AD B2C service level alerts](/en-us/azure/service-health/service-health-overview) to get notified of service issues, planned maintenance, health advisories, and security advisories.
- **Reporting**: [By using Log Analytics](../identity/monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs), build reports about user insights, technical challenges, and growth opportunities.

    - **Azure Dashboard**: Create [custom dashboards using Azure Dashboard](/en-us/azure/azure-monitor/app/overview-dashboard#create-custom-kpi-dashboards-using-application-insights) feature, which supports adding charts using Log Analytics queries. For example, identify pattern of successful and failed sign-ins, failure reasons and telemetry about devices used to make the requests.
    - **Abandon Azure AD B2C journeys**: Use the [workbook](https://github.com/azure-ad-b2c/siem#list-of-abandon-journeys) to track abandoned Azure AD B2C journeys wherein users started sign-in or sign-up but never finished it. Find details about policy ID and steps taken by the user before abandoning the journey.
    - **Azure AD B2C monitoring workbooks**: Use the [monitoring workbooks](https://github.com/azure-ad-b2c/siem) that include Azure AD B2C dashboard, multifactor authentication (MFA) operations, Conditional Access reports, and search logs by correlationId. This practice provides better insights into the health of your Azure AD B2C environment.
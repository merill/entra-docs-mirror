---
layout: Conceptual
title: Analyze user activity in Microsoft Entra External ID - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-user-insights
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn about how to analyze user activity and engagement for your registered application in the external tenant.
ms.topic: how-to
ms.date: 2026-05-19T00:00:00.0000000Z
ms.custom: it-pro, sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 61519ca9-e9aa-cb25-3b09-d551f21a7c66
document_version_independent_id: 61519ca9-e9aa-cb25-3b09-d551f21a7c66
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-user-insights.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-user-insights
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-user-insights.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 4700d6a5-fe0f-dd33-6d89-e92d1113b0ab
---

# Analyze user activity in Microsoft Entra External ID - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Important

**User Insights is being retired on August 31, 2026.** Plan to migrate to Azure Monitor and Log Analytics before the retirement date. See Migrate from User Insights for recommended alternatives and next steps.

The Application user activity feature under Usage & insights provides data analytics on user activity and engagement for registered applications in your tenant. You can use this feature to view, query, and analyze user activity data in the Microsoft Entra admin center. This feature can help you uncover valuable insights that can aid strategic decisions and drive business growth.

## Supported scenarios

You can use the user insights feature for the following scenarios:

- **Tracking active users** - You want to determine the total number of active users in your tenant, to assess the overall user engagement with your applications.
- **Monitoring new users added** - You want to track and identify how many users have been added to your tenant in the last month. This data is valuable for monitoring the growth of your user base.
- **Analyzing daily and monthly application sign-ins** - You want to gather data on the number of users who sign in to your applications daily and monthly to assess user engagement and spot trends.
- **Assessing MFA usage success and failure** - You want to compare the multifactor authentication (MFA) usage success and failure rates for your applications to provide insights into the security and user experience of your authentication processes. You can also use our new telecom metrics for MFA SMS and fraud detection. These preview metrics help you identify vulnerabilities and detect potential fraud.

## Prerequisites

To access and view data from application user activity, you must have:

- A Microsoft Entra External ID [external tenant](quickstart-tenant-setup).
- [Registered application(s)](/en-us/entra/identity-platform/quickstart-register-app) with some sign-in and sign-up data.

## How to access the Application user activity dashboards

The Application user activity dashboards provide insights into how users interact with your apps. You can access them from the **Application user activity** menu.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#reports-reader).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to the external tenant you created earlier from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Usage & insights**
4. Select **Application user activity** to view the dashboards.

    [![Screenshot of the Application user activity dashboards under the Usage &amp; insights menu.](media/how-to-user-insights/app-user-activity-dashboard.png)](media/how-to-user-insights/app-user-activity-dashboard.png#lightbox)

## Browse the available dashboards

There are three dashboards available with data centered around users, requests, and authentications. Each dashboard provides a summary of activities in applications with one or more sign-in attempts. The dashboards display activity data during the selected time range.

### Users dashboard

The **Users** dashboard provides a summary of daily and monthly active users, and new users added to your tenant. For this dataset, you can view the following trends:

- Daily active and inactive users over a period of 30 days.
- Monthly active users over a period of 12 months
- Monthly active users comparison by application.
- New users added over a period of 12 months.
- New users breakdown by operating system.

    ![Screenshot of the Users dashboard.](media/how-to-user-insights/users-dashboard.png)

### Authentications dashboard

The **Authentications** dashboard provides a summary of daily and monthly authentications in your tenant. For this dataset, you can view the following trends:

- Daily authentications over a period of 30 days.
- Daily authentications breakdown by operating system.
- Monthly authentications over a period of 12 months summarized by location.

    ![Screenshot of the Authentications dashboard.](media/how-to-user-insights/authentications-dashboard.png)

### MFA Usage dashboard

The **MFA Usage** dashboard gives you a summary of monthly MFA authentication performance for all your applications. For this dataset, you can view the following trends:

- Users registered for MFA
- Types of MFA usage with a summary of success vs failure count over a period of 12 months
- CAPTCHA triggers and activity in the last 30 days

    ![Screenshot of the MFA Usage dashboard.](media/how-to-user-insights/mfa-dashboard.png)

### Telecom metrics (preview)

To better understand MFA performance, we have added new metrics to the MFA Usage dashboard. These metrics provide actionable insights into SMS-based MFA usage.

- **Conditional Access policies requiring MFA**: This metric helps you identify which Conditional Access policies require MFA, allowing you to pinpoint any security gaps.
- **Number of users registered for MFA**: This metric tracks how many users are registered for MFA and which methods they use. This information helps you evaluate the level of MFA adoption.

We have added several new metrics to help you detect potential telecom fraud. Microsoft Entra External ID uses CAPTCHA for SMS MFA to help to prevent automated attacks by distinguishing human users from bots. If a risky user is detected, we block the user from signing in or ask the user to complete a CAPTCHA before sending an SMS verification code. To help you visualize the effectiveness of this method, we have added the following metrics to the dashboard:

- **Allowed**: This metric shows the number of users who successfully received an SMS during sign-in or sign-up.
- **Blocked**: This metric shows the number of users who were prevented from receiving an SMS. When telecom MFA is blocked, users are notified and advised trying an alternative authentication method.
- **Challenged**: This metric shows when a CAPTCHA challenge appears before sending the SMS. This usually happens when unusual behavior is detected. For this data point, you'll also see the following metrics:
    - **Number of users unable to complete CAPTCHA**: This metric helps you to track how many users couldn’t pass the CAPTCHA challenge. This insight helps assess if the CAPTCHA is too difficult for legitimate users, allowing adjustments to balance security with accessibility.
    - **Number of users successfully completing CAPTCHA**: This metric helps you review how many users have successfully completed the CAPTCHA challenge. This data provides insight into how effectively CAPTCHA protects against automated attacks while ensuring legitimate users can authenticate.

## Customize your dashboards

The Application user activity dashboards provide easy-to-digest graphs and charts but have limited customization options. These dashboards are available in the Microsoft Entra admin center and accessible via Microsoft Graph APIs, which are currently in beta.

Microsoft Graph APIs enable you to build powerful, customized dashboards tailored to your specific needs and preferences, offering several advantages:

- **Flexibility**: You can integrate with other data sources to present your data in a way that aligns more with your business objectives.
- **Enhanced visualization**: You can have richer and more interactive visual representations of your data.
- **Complex query handling**: You can apply advanced filters, aggregations, and calculations to your user insights data and get more granular and accurate results.

To build your own user insights dashboard, you need to configure API permissions for Microsoft Graph. You can then use the Microsoft Graph API to access the data and build custom reports in your preferred analytics tool. We recommend using Power BI to visualize the data, but you can choose any other analytical tool you prefer.

### Configure API permissions

To build your own user insights dashboard, you need to [configure API permissions for Microsoft Graph](/en-us/graph/auth-v2-service) and add the `Insights-UserMetric.Read.All` permission to your registered app.

![Screenshot of requesting API permissions.](media/how-to-user-insights/insights-permission.png)

You also have to [generate a client secret](/en-us/entra/identity-platform/howto-create-service-principal-portal#option-3-create-a-new-client-secret) and get an [access token](/en-us/graph/auth-v2-service?tabs=http#4-request-an-access-token) to interact with Microsoft Graph.

Once you have successfully created your access token, you can use the Microsoft Graph API to access the data and build custom reports.

### Create a custom Power BI report

To fetch the user insights data, you can create a Power BI report using custom connectors. Here's how you can do it:

1. Create a new blank Power BI report.
2. Create a [custom connector](/en-us/power-bi/connect-data/desktop-connect-to-data) and enter the URL for the Microsoft Graph API endpoint you want to query. For example: `https://graph.microsoft.com/beta/reports/userinsights/monthly/activeUsers` for monthly active users data.
3. Add your access token by selecting **Advanced**.
4. In the **HTTP request header parameters (optional)** section, select Authorization in the drop-down list and enter your access token.
5. Select **OK** to connect Power BI to the Microsoft Graph API and load the data.

![Screenshot of adding a token.](media/how-to-user-insights/add-token.png)

Power BI comes with Power Query Editor that can help you clean and shape your data. You can remove unnecessary columns, handle missing values, and apply transformations such as merging, grouping, filtering, and many more. For more information, see the [Query Editor overview](/en-us/power-bi/transform-model/desktop-query-overview).

## Migrate from User Insights

User Insights is being retired on **August 31, 2026**. After that date, the Application user activity dashboards and the Microsoft Graph `reports/userInsights/*` (beta) endpoints stop returning data. To keep visibility into user activity, sign-ins, and MFA usage, migrate to the alternatives in this section before the retirement date. There's no end-user impact, and historical dashboard data isn't migrated automatically.

### Recommended alternatives

- **Azure Monitor with Log Analytics (recommended).** Route Microsoft Entra sign-in and audit logs to a Log Analytics workspace, then use [Microsoft Entra workbooks](/en-us/entra/identity/monitoring-health/howto-use-workbooks) or KQL queries against the `SigninLogs` and `AuditLogs` tables to reproduce the User Insights views. For setup, see [Set up Azure Monitor in an external tenant](how-to-azure-monitor) and [Integrate Microsoft Entra logs with Azure Monitor logs](/en-us/entra/identity/monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs).
- **Microsoft Graph sign-in and audit log APIs.** For custom reports and pipelines, replace calls to `reports/userInsights/*` with [List signIns](/en-us/graph/api/signin-list), [List directoryAudits](/en-us/graph/api/directoryaudit-list), and the [reports API](/en-us/graph/api/resources/report).

### Next steps

Before August 31, 2026, inventory the dashboards, Power BI reports, and app registrations that depend on User Insights or the `reports/userInsights/*` endpoints, then rebuild the views by using Azure Monitor or the Microsoft Graph activity log APIs.
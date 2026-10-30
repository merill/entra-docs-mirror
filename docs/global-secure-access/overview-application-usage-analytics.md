---
layout: Conceptual
title: Application Usage Analytics Overview - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/overview-application-usage-analytics
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Gain visibility into application traffic to gain insights into app categories, risk scores, transactions, and organizational usage patterns.
ms.topic: overview
ms.date: 2026-03-19T00:00:00.0000000Z
ms.reviewer: kerenSemel
locale: en-us
document_id: cca30cc5-f8e4-6a40-6e31-fe9f59b6ec74
document_version_independent_id: cca30cc5-f8e4-6a40-6e31-fe9f59b6ec74
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/overview-application-usage-analytics.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/overview-application-usage-analytics
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/overview-application-usage-analytics.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 91cdfb93-b545-72ef-b27f-6538db79c148
---

# Application Usage Analytics Overview - Global Secure Access | Microsoft Learn

Application usage analytics gives IT admins actionable insights into their organization's app use by analyzing traffic patterns, data usage, and which users access the app. Admins can use these analytics to identify shadow IT, generative AI apps, and potential security or compliance risks. Usage analytics helps organizations increase visibility, improve their security posture, and optimize app use across their environment.

## Insights and Analytics dashboard

To access the **Insights and Analytics** dashboard:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Log Reader](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-log-reader).
2. Browse to **Global Secure Access** &gt; **Applications** &gt; **Insights and Analytics**.

The **Insights and Analytics** dashboard has three widgets:

### Application count

This widget shows the **Total cloud applications**, **Total private applications**, and the number of **New discovered segments** used within the selected time. To learn more about discovered segments, select the **View details** button to open the **Application discovery** page.![Screenshot of the Applications count widget with information on the total cloud and total private applications.](media/overview-application-usage-analytics/widget-applications-count.png)

### Application usage distribution

This widget shows application usage by type, with one color for cloud and another for private applications in the selected time range. You can aggregate the view by **Transactions**, **Bytes sent**, or **Bytes received**.![Screenshot of the Usage distribution widget with cloud and private applications information aggregated by bytes sent.](media/overview-application-usage-analytics/widget-usage-distribution.png)

### Application usage trend

This widget shows application usage over time, with one trend for cloud and another for private applications. You can aggregate the view by **Transactions**, **Users**, **Devices**, **Bytes sent**, or **Bytes received**.![Screenshot of the Applications usage trends widget showing private and cloud application usage over time.](media/overview-application-usage-analytics/widget-applications-usage-trends.png)

## Private application analytics

Private application analytics gives IT admins visibility and insights into their organization's private enterprise applications onboarded to Microsoft Entra by Global Secure Access. These insights include the application name, application ID, users who access the application, devices used, access type, number of transactions, traffic (bytes sent and received), and the first and last access times. Private application analytics also tracks quick access for customers who configured it.

### Key capabilities

By using private application analytics, you can:

- Identify the private applications that users access. Details include **Application name**, **Application ID**, **Traffic type**, **Access type**, the number of **Users**, **Devices**, and **Transactions**, **Sent bytes**, **Received bytes**, **Last access** date, and **First access** date. ![Screenshot of a list of discovered private applications accessed by users.](media/overview-application-usage-analytics/private-applications-list.png)

Select each private application row to open a per-app insight panel with two tabs:

- The **Usage** tab shows a graph with usage information, including insights into the number of transactions, the amount of traffic, and the number of users accessing the applications. ![Screenshot of cloud application usage statistics showing transactions over time.](media/overview-application-usage-analytics/usage-statistics.png)
- The **Users** tab shows statistics about the usage of an application segment and which users are accessing it. ![Screenshot of a list of users who accessed the cloud application, the traffic type, and the number of transactions.](media/overview-application-usage-analytics/user-principal-name.png)

## Cloud application analytics

Cloud application analytics give admins visibility and insights into the cloud applications their organization uses, including generative AI applications. These insights include the application category, risk score, number of transactions, traffic (bytes sent and received), and the users who access the applications.

This information helps admins identify generative AI applications, shadow AI applications, and shadow IT. Insights from the analytics help admins make decisions based on security and compliance status.

### Key capabilities

By using Cloud application analytics, you can:

- Identify the cloud applications that users access (using the Microsoft Defender for Cloud Apps Cloud app catalog), for both internet and Microsoft 365 traffic. Details include **Name**, **Categories**, **Risk score**, the number of **Users**, **Sent bytes**, **Received bytes**, **Last access** date, and **First access** date.![Screenshot of a list of discovered cloud applications accessed by users.](media/overview-application-usage-analytics/application-discovery-cloud.png)
- Use the **Generative AI apps only** toggle to identify the generative AI applications that users access, for both internet and Microsoft 365 traffic.[![Screenshot of a list of discovered generative AI applications accessed by users.](media/overview-application-usage-analytics/application-discovery-generative-ai.png)](media/overview-application-usage-analytics/application-discovery-generative-ai.png#lightbox)

The links on each cloud application row open to reveal specific details about that application.

#### App details and risk factors

To view app details and risk factors, select the application's **Name** link. [![Screenshot of the Cloud Apps list with an example Name link highlighted.](media/overview-application-usage-analytics/cloud-name-link.png)](media/overview-application-usage-analytics/cloud-name-link.png#lightbox)

The **Microsoft Entra App Gallery** opens, showing the selected application's app details. The app details list the **Overall Risk Score**. You can view further risk-factor details by selecting each of the **General**, **Security**, **Compliance**, or **Legal** tabs. [![Screenshot of the app details view, showing example risk factor scores.](media/overview-application-usage-analytics/risk-factor-application-details.png)](media/overview-application-usage-analytics/risk-factor-application-details.png#lightbox)

#### App user data

To view user data, select the application's **Users** link. [![Screenshot of the Cloud Apps list with an example Users link highlighted.](media/overview-application-usage-analytics/cloud-users-link.png)](media/overview-application-usage-analytics/cloud-users-link.png#lightbox)

The **Users** tab shows statistics about the usage of an application segment and which users access it. ![Screenshot of a list of users who accessed the cloud application, the traffic type, and the number of transactions.](media/overview-application-usage-analytics/user-principal-name.png)

#### App usage data

To view usage data, select the application's **Transactions** link. [![Screenshot of the Cloud Apps list with an example Transactions link highlighted.](media/overview-application-usage-analytics/cloud-transactions-link.png)](media/overview-application-usage-analytics/cloud-transactions-link.png#lightbox)

The **Usage** tab opens, showing a graph with usage information, including the number of transactions, the amount of traffic, and the number of users who access the applications. ![Screenshot of cloud application usage statistics showing transactions over time.](media/overview-application-usage-analytics/usage-statistics.png)
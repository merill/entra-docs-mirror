---
layout: Conceptual
title: Global Secure Access network traffic logs - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-view-traffic-logs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to use Global Secure Access traffic logs (preview) to monitor connections to the service, the type of traffic, and who's connecting.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 4d3f7eaf-2074-6c72-54d4-e08c716fc88d
document_version_independent_id: ba389d6b-1c0a-f85b-540d-8617527b8898
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-view-traffic-logs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-view-traffic-logs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-view-traffic-logs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c1e7d1aa-2d49-e9d3-9b60-8f70b4bb7049
---

# Global Secure Access network traffic logs - Global Secure Access | Microsoft Learn

## Overview

Monitoring the traffic for Global Secure Access is an important activity for ensuring your tenant is configured correctly and that your users are getting the best experience possible. The Global Secure Access traffic logs (preview) provide insight into who is accessing what resources, where they're accessing them from, and what action took place.

This article describes how to use the traffic logs for Global Secure Access.

## Prerequisites

- A **Global Secure Access Administrator** role in Microsoft Entra ID.
- A **Global Secure Access Log Reader** role in Microsoft Entra ID.
- The product requires licensing. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

## How the traffic logs work

The Global Secure Access logs provide details of your network traffic. To better understand those details and how you can analyze those details to monitor your environment, it's helpful to look at the three levels of the logs and their relationship to each other.

A user accessing a website represents one *session*, and within that session there may be multiple *connections*, and within that connection there may be multiple *transactions*.

- **Session**: A session is identified by the first URL a user accesses. That session could then open many connections, for example a news site that contains multiple ads from several different sites.
- **Connection**: A connection includes the source and destination IP, source and destination port, and fully qualified domain name (FQDN). The connection components comprise the 5 tuple.
- **Transaction**: A transaction is a unique request and response pair.

Within each log instance, you can see the connection ID and transaction ID in the details. By using the filters, you can look at all connections and transactions for a single session.

## How to view the traffic logs

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](/en-us/azure/active-directory/roles/permissions-reference#reports-reader).
2. **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**.

The top of the page displays a summary of all transactions as well as a breakdown for each type of traffic. Select the **Microsoft 365** or **Private access** buttons to filter the logs to each traffic type.

Note

At this time, Session ID information is not available in the log details.

### View the log details

Select any log from the list to view the details. These details provide valuable information that can be used to filter the logs for specific details or to troubleshoot a scenario. The details can be added as a column and used to filter the logs.

![Screenshot of Traffic log details page.](media/how-to-view-traffic-logs/traffic-log-details.png)

### Filter and column options

The traffic logs can provide many details, so to start only some columns are visible. Enable and disable the columns based on the analysis or troubleshooting tasks you're performing, as the logs could be difficult to view with too many columns selected. The column and filter options align with each item in the Activity details.

Select **Columns** from the top of the page to change the columns that are displayed.

To filter the traffic logs to a specific detail, select the **Add filter** button and then enter the detail you want to filter by.

For example if you want to look at all the logs from a specific connection:

1. Select the log detail and copy the `connectionId` from the Activity details.
2. Select **Add filter** and choose **Connection ID**.
3. In the field that appears, paste the `connectionId` and select **Apply**.

    ![Screenshot that shows the traffic log filter.](media/how-to-view-traffic-logs/traffic-log-filter.png)

## View connection logs

Connection logs provide a summary of all associated transactions, including the total transaction count and blocked transactions, allowing for quick identification of any blocked activity.

A connection represents multiple transactions occurring in the last 24 hours and sharing the same flow correlation ID. While the transaction logs provide detailed information about individual transactions, connection logs offer a higher-level overview by aggregating multiple transactions. Connections are logged in real time with Active/Closed status, providing admins with near real-time traffic visibility.

Currently available in preview is a new tab in the Traffic logs blade for you to view Connections:

![Screenshot of the new Connections tab on the Traffic logs page.](media/how-to-view-traffic-logs/traffic-logs-connections-tab.png)

Transactions associated with each Connection are viewed by selecting the **Transactions** tab.

### Troubleshooting scenarios

The following details may be helpful for troubleshooting and analysis:

- If you're interested in the size of the traffic being sent and received, enable the **Sent Bytes** and **Received Bytes** columns. Select the column header to sort the logs by the size of the logs.
- If you are reviewing the network activity for a risky user, you can filter the results by user principal name and then review the sites they're accessing.
- To look for traffic to the types of websites that you want to block or allow, enable the **Web category** column.

The log details provide valuable information about your network traffic. Not all details are defined in the list below, but the following details are useful for troubleshooting and analysis:

- **Transaction ID**: Unique identifier representing the request/response pair.
- **Connection ID**: Unique identifier representing the connection that initiated the log.
- **Device category**: Device type where the transaction initiated from. Either **client** or **remote network**.
- **Action**: The action taken on the network session. Either **Allowed** or **Denied**.

## Configure diagnostic settings to export logs

You can export the Global Secure Access traffic logs (preview) to an endpoint for further analysis and alerting. This integration is configured in Microsoft Entra diagnostic settings.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](/en-us/azure/active-directory/roles/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Diagnostic settings**.
3. Select **Add Diagnostic setting**.
4. Give your diagnostic setting a name.
5. Select `NetworkAccessTrafficLogs`.
6. Select the **Destination details** for where you'd like to send the logs. Choose any or all of the following destinations. Additional fields appear, depending on your selection.

    - **Send to Log Analytics workspace:** Select the appropriate details from the menus that appear.
    - **Archive to a storage account:** Provide the number of days you'd like to retain the data in the **Retention days** boxes that appear next to the log categories. Select the appropriate details from the menus that appear.
    - **Stream to an event hub:** Select the appropriate details from the menus that appear.
    - **Send to partner solution:** Select the appropriate details from the menus that appear.
---
layout: Conceptual
title: Application Discovery for Global Secure Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-application-discovery
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Use Application discovery to detect the applications accessed by users and create separate private applications.
ms.topic: how-to
ms.date: 2026-04-16T00:00:00.0000000Z
ms.reviewer: lirazbarak
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: e2844229-f2a2-51cf-72c7-decc9854ac1d
document_version_independent_id: e2844229-f2a2-51cf-72c7-decc9854ac1d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-application-discovery.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-application-discovery
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-application-discovery.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 041b2269-a33a-d423-e788-ec08c68f3592
---

# Application Discovery for Global Secure Access - Global Secure Access | Microsoft Learn

Application discovery lets administrators see which applications people use on their corporate network. By identifying who uses which applications, administrators can create private applications with precise segmentation and least privilege access, so users only get the access they need.

With Quick Access, you can quickly onboard to Private Access by publishing wide IP ranges and wildcard FQDNs, like with traditional VPN solutions. You can then transition from Quick Access to per-application publishing for better control and granularity over each application. For example, you can create a Conditional Access policy and set user assignments per application.

This article walks through how to use Application discovery to detect which applications users access (through Quick Access) and create separate private applications.

## Prerequisites

- A Microsoft Entra tenant onboarded to [Microsoft Entra Private Access](concept-private-access).
- A Microsoft Entra tenant configured with [Quick Access](how-to-configure-quick-access).
- A device configured with the Global Secure Access client ([Windows](how-to-install-windows-client), [macOS](how-to-install-macos-client), [Android](how-to-install-android-client), [iOS](how-to-install-ios-client)).

Important

Application discovery relies on traffic flowing through Quick Access. If Quick Access is not configured, or if no users have accessed applications through Quick Access, the **Application discovery** page displays no data. This empty state is expected behavior, not a product error. To populate the discovery table, [configure Quick Access](how-to-configure-quick-access) and ensure that users are actively accessing applications through it.

## Discover applications

To view a list of all the application segments in Quick Access that users accessed via the Global Secure Access client in the last 30 days (if the table is empty, verify that [Quick Access is configured](how-to-configure-quick-access) and that users have generated traffic through it):

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Applications** &gt; **Application discovery**. ![Screenshot of Application discovery screen.](media/how-to-application-discovery/application-discovery-default-view.png)

By default, the **Application discovery** view sorts application segments in descending order by number of users. The most used application segments appear at the top of the list, making them easier for the admin to find.

The administrator can adjust the time range, add other filters, and sort the application segments according to each of the columns. The administrator can also **filter by user** to see the list of the application segments accessed by a specific user. From the **Search** field, the administrator can filter by fully qualified domain name (FQDN), IP address, and port address.

Each application segment includes the following columns:

- **Destination FQDN**: The FQDN of the application segment.
- **Destination IP**: The IP of the application segment.
- **Transport protocol**: The transport protocol of the application segment. Private Access supports Transmission Control Protocol (TCP) and User Datagram Protocol (UDP).
- **Destination port**: The port of the application segment.
- **Users**: The number of users who accessed the application segment.
- **Transactions**: The number of transactions (connections) to the application segment.
- **Devices** - The number of devices used to access the application segment.
- **Sent bytes**: The total bytes of data the user device sent to the application segment.
- **Received bytes**: The total bytes of data the user device received from the application segment.
- **Last access**: The last time in the time range the application segment was accessed.
- **First access**: The first time in the time range the application segment was accessed.

## Review recommendations

Microsoft Entra recommendations provide you with actionable guidance to improve your security posture. For Application discovery, recommendations help you identify which application segments to onboard as private applications. To learn more, see [What are Microsoft Entra recommendations?](../identity/monitoring-health/overview-recommendations).

To access recommendations for Application discovery:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Identity** &gt; **Overview**.
3. Select the **Recommendations** tab.
4. Select the recommendation for Application discovery: **Onboard new discovered application segments to enterprise applications**. ![Screenshot of the Recommendations tab, showing the recommendation to onboard new discovered application segments to enterprise applications.](media/how-to-application-discovery/recommendation-onboard-discovered.png)
5. Review the recommendation details and follow the suggested **Action plan**. [![Screenshot of the impacted resources and the recommended action plan.](media/how-to-application-discovery/recommendation-action-plan.png)](media/how-to-application-discovery/recommendation-action-plan-expanded.png#lightbox)

Note

This feature is currently unavailable in Australia and Africa.

## Create a new application

Use Application discovery to create new Microsoft Entra ID applications based on the discovered application segments of the main table. To add an application segment to a new application:

1. From the Application discovery list, choose one or more application segments that correspond to an application that you would like to create. ![Screenshot of the list of application segments with two segments selected.](media/how-to-application-discovery/select-application-segments.png)
    1. Often, one application uses one application segment. For example:
        - A file server, such as: `filesrv.contoso.com`, TCP, 445.
        - A portal, such as: `internalportal.contoso.com`, TCP, 443.
    2. However, sometimes a single application uses several ports, protocols, or spans across multiple servers (FQDNs/IPs). In this case, you can choose several application segments and even add others manually. For example:
        - Publishing ADDS services in a specific AD site: `dc1.contoso.com` and `dc2.contoso.com`, TCP, 88, 135, 137, 138, 389, 445, 464, 636, 3268, 3269 and a fixed high port for Netlogon `dc1.contoso.com` and `dc2.contoso.com`, UDP, 88, 123, 389, 464.
    3. For a list of ADDS ports, see [How to configure a firewall for Active Directory domains and trusts](/en-us/troubleshoot/windows-server/active-directory/config-firewall-for-ad-domains-and-trusts).
2. Select **Add to new application**. The **Create Global Secure Access application**screen opens, showing the selected application segments.
    1. Enter a **Name** for the application and select the corresponding **Connector Group**
    2. Add or delete application segments manually if needed.
    3. Select **Save** to apply your changes. ![Screenshot of the Create Global Secure Access application screen with the Name field, Connector Group field, and Save button highlighted.](media/how-to-application-discovery/create-application.png)
3. Enable access for the appropriate users by adjusting the users and groups assigned to the new application.
    1. You should fine-tune the assignments *after* creating the application. This way, the list contains only groups of users who require access to the new application, according to the principle of least privilege.
    2. For enterprise applications:
        1. Browse to **Global Secure Access** &gt; **Applications** &gt; **Enterprise applications** &gt; **Users and groups**.
        2. Select the application you created.
        3. Modify the user and group assignments as needed.

Important

Global Secure Access prioritizes traffic for individually defined applications over Quick Access. When you move an application segment from Quick Access to a specific Global Secure Access app, all traffic to that segment follows your application configuration. No traffic to the new application goes through Quick Access, even if the segment stays within the ranges defined by Quick Access. To avoid service disruption, new applications you create through application discovery inherit all assigned users and groups from Quick Access at creation. After you validate the new application, rescope the application's permissions to only the users who need to connect to the defined segments.

1. (Optional) For extra security, you can set Conditional Access policies according to your company's security policies. For example, you might want to require multifactor authentication (MFA) and device compliance when users access a critical application.

Note

Application segments persist in the Application discovery main table even after you create an application, until a user signs in to the new application and accesses the resource. In the future, the Application discovery main table will update regardless of user interaction.

## Add to an existing application

You can use Application discovery to add application segments to an existing private application. To add an application segment to an existing application:

1. From the Application discovery list, choose one or more application segments.
2. Select **Add to an existing application**.
3. Choose the existing private application to which you would like to add the segments. The **Edit Global Secure Access application** screen opens, showing the properties of the existing application, the selected application segments (with status **Pending**), and any previously configured application segments (with status **Success**).
4. Review the configuration and revise the **Name**, **Connector Group**, and application segments, and make any necessary revisions.
5. To apply your changes, select **Save**. ![Screenshot of the Edit Global Secure Access application screen. The Status column and Save button are highlighted.](media/how-to-application-discovery/edit-application.png)

## View the details of an application segment

Before you decide to create a private application, you might want to review other details of the application segment.

1. On the Application discovery table, select the **Destination FQDN** or **Destination IP** for the application segment you wish to explore.
2. The **Usage** tab defaults to a graph of **Users** over time. You can set the graph to show the distribution of **Transactions**, **Devices**, **Bytes sent**, and **Bytes received** over time. You can also change the time range by adjusting the **Timespan** setting. ![Screenshot of the Usage tab with the Y-axis display options highlighted.](media/how-to-application-discovery/usage-tab.png)
3. The **Users** tab shows the list of users who accessed the selected application segment in the last 30 days.![Screenshot of the Users tab showing the list of users.](media/how-to-application-discovery/users-tab.png)

Important

Use the list of users to inform the decisions you make regarding the users and groups that you plan to assign to the Microsoft Entra application once you onboard the selected application segment.
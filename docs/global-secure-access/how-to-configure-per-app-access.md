---
layout: Conceptual
title: How to configure per-app access using Global Secure Access applications - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-per-app-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to configure per-app access to your private, internal resources using Global Secure Access applications for Microsoft Entra Private Access.
ms.topic: how-to
ms.date: 2026-04-29T00:00:00.0000000Z
ms.subservice: entra-private-access
ms.reviewer: katabish
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: b72d7f72-e1e1-2210-25d6-7afcba3abe20
document_version_independent_id: dfc55a75-7d5c-00c3-7b7e-0914d624e114
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-configure-per-app-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-configure-per-app-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-configure-per-app-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d02fd149-cc86-5bb0-4682-a094422ab992
---

# How to configure per-app access using Global Secure Access applications - Global Secure Access | Microsoft Learn

## Overview

Microsoft Entra Private Access provides secure access to your organization's internal resources by enabling you to control and secure access to specific network destinations on your private network. This allows you to provide granular network access based on user needs. To do this, create an Enterprise application and add the application segment that is used by the internal, private resource that you want to secure. Network requests sent from devices running the Global Secure Access client to the application segment you added to your Enterprise application will be acquired and routed to your internal application by the Global Secure Access cloud service without any ability to connect to other resources on your network. By configuring an Enterprise application, you create per-app access to your internal resources. Enterprise applications provide you a segmented, granular ability to manage how your resources are accessed on a per-app basis.

This article describes how to configure per-app access using Enterprise applications.

## Prerequisites

To configure a Global Secure Access Enterprise app, you must have:

- The **Global Secure Access Administrator** and **Application Administrator** roles in Microsoft Entra ID
- The product requires licensing. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

To manage Microsoft Entra private network connector groups, which is required for Global Secure Access apps, you must have:

- An **Application Administrator** role in Microsoft Entra ID
- Microsoft Entra ID P1 or P2 licenses

### Known limitations

For detailed information about known issues and limitations, see [Known limitations for Global Secure Access](reference-current-known-limitations).

## High level steps

Per-App Access is configured by creating a new Global Secure Access app. You create the app, select a connector group, and add network access segments. These settings make up the individual app that you can assign users and groups to.

To configure Per-App Access, you need to have a connector group with at least one active [Microsoft Entra private network](/en-us/entra/identity/app-proxy/) connector. This connector group handles the traffic to this new application. With Connectors, you can isolate apps per network and connector.

To summarize, the overall process is as follows:

1. Create a connector group with at least one active private network connector.

    - If you already have a connector group, make sure you're on the latest version.
2. Create a Global Secure Access app.
3. Assign users and groups to the app.
4. Configure Conditional Access policies.
5. Enable Microsoft Entra Private Access.

## Create a private network connector group

To configure a Global Secure Access app, you must have a connector group with at least one active private network connector.

If you don't already have a connector set up, see [Configure connectors](how-to-configure-connectors).

Note

If you've previously installed a connector, reinstall it to get the latest version. When upgrading, uninstall the existing connector and delete any related folders.

The minimum version of connector required for Private Access is **1.5.3417.0**.

## Create a Global Secure Access Enterprise application

To create a new app, you provide a name, select a connector group, and then add application segments. App segments include the fully qualified domain names (FQDNs) and IP addresses you want to tunnel through the service. You can complete all three steps at the same time, or you can add them after the initial setup is complete.

### Choose name and connector group

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with the appropriate roles.
2. Browse to **Global Secure Access** &gt; **Applications** &gt; **Enterprise applications**.
3. Select **New application**.

    ![Screenshot that shows the Enterprise apps and Add new application button.](media/how-to-configure-per-app-access/new-enterprise-app.png)
4. Enter a name for the app.
5. Select a Connector group from the dropdown menu.

    Important

    You must have at least one active connector to create an application. To learn more about connectors, see [Understand the Microsoft Entra private network connector](concept-connectors).
6. Select the **Save** button at the bottom of the page to create your app without adding private resources.

### Add application segment

An application segment is defined by 3 fields - destination, port, and protocol. If two or more application segments include the same destination, port, and protocol, they are considered to be overlapping. The **Add application segment** process is where you define the FQDNs and IP addresses that you want the Global Secure Access client to route to your target private application. You can add application segments when you create the app and later you can return to add more or edit them.

You can add fully qualified domain names (FQDN), IP addresses, and IP address ranges. Within each application segment, you can add multiple ports and port ranges.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Global Secure Access** &gt; **Applications** &gt; **Enterprise applications**.
3. Select **New application**.
4. Select **Add application segment**.
5. In the **Create application segment** panel that opens, select a **Destination type**.
6. Enter the appropriate details for the selected destination type. Depending on what you select, the subsequent fields change accordingly.

    - **IP address**:
        - Internet Protocol version 4 (IPv4) address, such as 192.168.2.1, that identifies a device on the network.
        - Provide the ports that you want to include.
    - **Fully qualified domain name**(including wildcard FQDNs):
        - Domain name that specifies the exact location of a computer or a host in the Domain Name System (DNS).
        - Provide the ports that you want to include.
        - NetBIOS isn't supported. For example, use `contoso.local/app1` instead of `contoso/app1.`
    - **IP address range (CIDR)**:
        - Classless Inter-Domain Routing (CIDR) represents a range of IP addresses where an IP address is followed by a suffix that indicates the number of network bits in the subnet mask.
        - For example, 192.168.2.0/24 indicates that the first 24 bits of the IP address represent the network address, while the remaining 8 bits represents the host address.
        - Provide the starting address, network mask, and ports.
    - **IP address range (IP to IP)**:
        - Range of IP addresses from start IP (such as 192.168.2.1) to end IP (such as 192.168.2.10).
        - Provide the IP address start, end, and ports.
7. Enter the ports and select the **Apply** button.

    - Separate multiple ports with a comma.
    - Specify port ranges with a hyphen.
    - Spaces between values are removed when you apply the changes.
    - For example, `400-500, 80, 443`.

    ![Screenshot that shows the create app segment panel with multiple ports added.](media/how-to-configure-per-app-access/app-segment-multiple-ports.png)

    The following table provides the most commonly used ports and their associated networking protocols:

    | Port | Protocol |
    | --- | --- |
    | `22` | `Secure Shell (SSH)` |
    | `80` | `Hypertext Transfer Protocol (HTTP)` |
    | `443` | `Hypertext Transfer Protocol Secure (HTTPS)` |
    | `445` | `Server Message Block (SMB) file sharing` |
    | `3389` | `Remote Desktop Protocol (RDP)` |
8. Select **Save**.

Note

You can add up to 500 application segments to your app however none of these application segments can have overlapping FQDNs, IP addresses, or IP ranges within or between any Private Access apps. A special exception is allowed for overlapping segments between Private Access apps and Quick Access to allow for VPN replacement. If a segment defined on an Enterprise App (for example 10.1.1.1:3389) overlaps with a segment defined on Quick Access (for example 10.1.1.0/24:3389), then the segment defined on the Enterprise App will be given priority by the GSA service. No traffic from any user to an application segment defined as an Enterprise App will be processed by Quick Access. This means that any user that attempts to RDP to 10.1.1.1 will be evaluated and routed per the Enterprise App configuration, including user assignments and Conditional Access policies. As a best practice, remove application segments that you define in Enterprise Apps from Quick Access, breaking IP subnets into smaller ranges so that the exclusion is possible.

### View rule priority in the client

To identify the active rule for a destination, open the Global Secure Access client and go to **Advanced Diagnostics** &gt; **Forwarding profile**. The **Forwarding profile** tab shows the active rules in the client and includes a **Priority** column.

Rules with smaller numerical priority values take precedence over rules with larger numerical values. You can also use **Policy tester** in the **Forwarding profile** tab to identify the active rule for a specific destination.

## Assign users and groups

You need to grant access to the app you created by assigning users and/or groups to the app. For more information, see [Assign users and groups to an application.](/en-us/azure/active-directory/manage-apps/assign-user-or-group-access-portal)

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Global Secure Access** &gt; **Applications** &gt; **Enterprise applications**.
3. Search for and select your application.
4. Select **Users and groups** from the side menu.
5. Add users and groups as needed.

Note

You must assign users directly assigned to the app or to the group assigned to the app. Nested groups are not supported. Also note that access assignments are not automatically transferred to a newly created Enterprise App even when there is an existing (overlapping) application segment defined in Quick Access. This is important because you can encounter an issue where users that had successfully accessed an app segment through Quick Access will be blocked from access when the app segment is moved to Enterprise Apps until you assign them access specifically to the Enterprise App. Allow 15 minutes for your configuration change to be synchronized with your Global Secure Access clients.

## Update application segments

You can add or update the FQDNs and IP addresses included in your app at any time.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Global Secure Access** &gt; **Applications** &gt; **Enterprise applications**.
3. Search for and select your application.
4. Select **Network access properties**from the side menu.
    - To add a new FQDN or IP address, select **Add application segment**.
    - To edit an existing app, select it from the **Destination type** column.

## Configure traffic routing for the app

Traffic routing is configured per Global Secure Access application. The default traffic routing method is **Random**, which distributes requests across the available connectors in the selected connector group.

For Global Secure Access applications, you can change the routing behavior to use session persistence, also called session affinity. Session persistence consistently routes requests from the same user and device to the same connector for the duration of a session.

Session persistence is useful for applications that rely on connector egress IP for authentication or access control lists (ACLs).

Tip

Session persistence only works with Global Secure Access applications, not Microsoft Entra application proxy applications.

You can configure the traffic routing method for the Global Secure Access app by updating the `trafficRoutingMethod` property on the application through Microsoft Graph. For the `trafficRoutingMethod` property definition and supported values, see [onPremisesPublishing resource type](/en-us/graph/api/resources/onpremisespublishing?view=graph-rest-beta&amp;preserve-view=true).

Update the application object with a separate `PATCH` request to Microsoft Graph:

```http
PATCH https://graph.microsoft.com/beta/applications/{appRegistrationObjectId}
Content-Type: application/json

{
    "onPremisesPublishing": {
        "trafficRoutingMethod": "sessionPersistence"
    }
}
```

Replace `{appRegistrationObjectId}` with the application registration's object ID. You can find this value in the Microsoft Entra admin center under **Identity** &gt; **Applications** &gt; **App registrations** by selecting the app registration for your Global Secure Access application and copying the **Object ID** from the **Overview** page. To return to the default behavior, set `trafficRoutingMethod` to `random`. For more information, see [Update application](/en-us/graph/api/application-update?view=graph-rest-beta&amp;preserve-view=true).

To confirm that the configuration was committed, retrieve the app registration object with a $select parameter and `GET` request to review the `onPremisesPublishing.trafficRoutingMethod` value:

```http
GET https://graph.microsoft.com/beta/applications/{appRegistrationObjectId}
```

For more information, see [Get application](/en-us/graph/api/application-get?view=graph-rest-beta&amp;preserve-view=true) and [Customize Microsoft Graph responses with query parameters](/en-us/graph/query-parameters?tabs=http#select)

## Enable or disable access with the Global Secure Access Client

You can enable or disable access to the Global Secure Access app using the Global Secure Access Client. This option is selected by default, but can be disabled, so the FQDNs and IP addresses included in the app segments aren't tunneled through the service.

![Screenshot that shows the enable access checkbox.](media/how-to-configure-per-app-access/per-app-access-enable-checkbox.png)

## Assign Conditional Access policies

Conditional Access policies for per-app access are configured at the application level for each app. Conditional Access policies can be created and applied to the application from two places:

- Go to **Global Secure Access** &gt; **Applications** &gt; **Enterprise applications**. Select an application and then select **Conditional Access** from the side menu.
- Go to **Microsoft Entra ID** &gt; **Conditional Access** &gt; **Policies**. Select **+ Create new policy**.

For more information, see [Apply Conditional Access policies to Private Access apps](how-to-target-resource-private-access-apps).

## Enable Microsoft Entra Private Access

Once you have your app configured, your private resources added, users assigned to the app, you can enable the Private access traffic forwarding profile. You can enable the profile before configuring a Global Secure Access app, but without the app and profile configured, there's no traffic to forward.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Traffic forwarding**.
3. Select the toggle for **Private access profile**.

This diagram demonstrates how Microsoft Entra Private Access works when attempting to use Remote Desktop Protocol to connect to a server on a private network.

[![Diagram of Microsoft Entra Private Access working with Remote Desktop Protocol.](media/how-to-configure-per-app-access/private-access-remote-desktop-protocol-network-diagram.png)](media/how-to-configure-per-app-access/private-access-remote-desktop-protocol-network-diagram.png#lightbox)

| Step | Description |
| --- | --- |
| 1 | User initiates RDP session to an FQDN which maps to the target server. The GSA Client intercepts the traffic and tunnels it to the SSE Edge. |
| 2 | The SSE Edge evaluates policies stored in Microsoft Entra ID such as whether the user is assigned to the application and Conditional Access policies. |
| 3 | Once the user has been authorized, Microsoft Entra ID issues a token for the Private Access application. |
| 4 | The traffic is released to continue to the Private Access service along with the application’s access token. |
| 5 | The Private Access service validates the access token and the connection is brokered to the Private Access backend service. |
| 6 | The connection is brokered to the Private Network Connector. |
| 7 | The Private Network Connector performs a DNS query to identify the IP address of the target server. |
| 8 | The DNS service on the private network sends the response. |
| 9 | The Private Network Connector forwards the traffic to the target server. The RDP session is negotiated (including RDP authentication) and is then established. |
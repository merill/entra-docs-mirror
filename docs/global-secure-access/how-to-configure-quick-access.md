---
layout: Conceptual
title: How to configure Quick Access for Global Secure Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-quick-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to specify the internal resources to secure with Microsoft Entra Private Access using a Quick Access app.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.subservice: entra-private-access
ms.reviewer: katabish
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: f34e1f5f-3c05-25ee-5ba6-21b108202d8a
document_version_independent_id: d76236a1-d2a2-13ed-9320-2add9ec63f5a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-configure-quick-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-configure-quick-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-configure-quick-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: cc91ecf5-d575-f8a3-08c4-26699343329b
---

# How to configure Quick Access for Global Secure Access - Global Secure Access | Microsoft Learn

## Overview

With Global Secure Access, you can define specific fully qualified domain names (FQDNs) or IP addresses of private resources to include in the traffic for Microsoft Entra Private Access. Your organization's employees can then access the apps and sites that you specify. This article describes how to configure Quick Access for Microsoft Entra Private Access.

Note

Use Quick Access as a transition state in your Zero Trust journey. After Quick Access has enabled you to replace your VPN, [configure per-app access](quickstart-per-app-access) to achieve application segmentation and per-app granular controls.

## Prerequisites

To configure Quick Access, you must have:

- The **Global Secure Access Administrator** and **Application Administrator** roles in Microsoft Entra ID.
- The product requires licensing. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

To manage Microsoft Entra private network connector groups, which is required for Quick Access, you must have:

- An **Application Administrator** role in Microsoft Entra ID
- Microsoft Entra ID P1 or P2 licenses

### Known limitations

For detailed information about known issues and limitations, see [Known limitations for Global Secure Access](reference-current-known-limitations).

## High-level steps

Configuring your Quick Access settings is a major component to utilizing Microsoft Entra Private Access. When you configure Quick Access for the first time, Private Access creates a new enterprise application. The properties of this new app are automatically configured to work with Private Access.

To configure Quick Access, you need to have a connector group with at least one active [Microsoft Entra private network](/en-us/entra/identity/app-proxy/) connector. The connector group handles the traffic to this new application. Once you have Quick Access and a private network connector group configured, you need to grant access to the app.

To summarize, the overall process is as follows:

1. Create a connector group with at least one active private network connector.
2. Configure Quick Access.
3. Assign users and groups to the app.
4. Configure Conditional Access policies.
5. Enable the Private access traffic forwarding profile.

## Create a private network connector group

To configure Quick Access, you must have a connector group with at least one active private network connector.

If you don't already have a connector group set up, see [Configure connectors for Quick Access](how-to-configure-connectors).

Note

If you've previously installed a connector, reinstall it to get the latest version. When upgrading, uninstall the existing connector and delete any related folders.

The minimum version of connector required for Private Access is **1.5.3417.0**.

## Configure Quick Access

On the Quick Access page, you provide a name for the Quick Access app, select a connector group, and add application segments, which include FQDNs and IP addresses. You can complete all three steps at the same time, or you can add the application segments after the initial setup is complete.

### Name and connector group

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with the appropriate roles.
2. Browse to **Global Secure Access** &gt; **Applications** &gt; **Quick access**.
3. Enter a name. *Use the name Quick Access*.
4. Select a Connector group from the dropdown menu.
5. Select **Save** to create your "Quick Access" app without FQDNs, IP addresses, and private DNS suffixes.

### Add Quick Access application segment

You define the FQDNs and IP addresses to include when you **Add Quick Access application segment**. You add these resources when you create or update the Quick Access app.

You can add fully qualified domain names (FQDN), IP addresses, and IP address ranges. Within each application segment, you can add multiple ports and port ranges.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Global Secure Access** &gt; **Applications** &gt; **Quick Access**.
3. Select **Add Quick Access application segment**.
4. In the **Create application segment** panel that opens, select a **Destination type**.
5. Enter the appropriate details for the selected destination type. Depending on what you select, the subsequent fields change accordingly.

    - **IP address**:
        - Internet Protocol version 4 (IPv4) address, such as 192.168.2.1, that identifies a device on the network.
        - Provide the ports that you want to include.
    - **Fully qualified domain name**(including wildcard FQDNs):
        - Domain name that specifies the exact location of a computer or a host in the Domain Name System (DNS).
        - Provide the ports to include.
        - Wildcard FQDNs must be specified in the format `*.contoso.com`.
    - **IP address range (CIDR)**:
        - Classless Inter-Domain Routing (CIDR) represents a range of IP addresses. An IP address is followed by a suffix indicating the number of network bits in the subnet mask.
        - For example, 192.168.2.0/24 indicates that the first 24 bits of the IP address represent the network address, while the remaining 8 bits represents the host address.
        - Provide the starting address, network mask, and ports.
    - **IP address range (IP to IP)**:
        - Range of IP addresses from start IP (such as 192.168.2.1) to end IP (such as 192.168.2.10).
        - Provide the IP address start, end, and ports.
6. Enter the ports and protocol and select **Apply**.

    - Separate multiple ports with a comma.
    - Specify port ranges with a hyphen.
    - Spaces between values are removed when you apply the changes.
    - For example, `400-500, 80, 443`.

    ![Screenshot that shows the create app segment panel with multiple ports added.](media/how-to-configure-per-app-access/app-segment-multiple-ports.png)

    The following table provides the most commonly used ports and their associated networking protocols:

    | Port | Protocol |
    | --- | --- |
    | 22 | Secure Shell (SSH) |
    | 80 | Hypertext Transfer Protocol (HTTP) |
    | 443 | Hypertext Transfer Protocol Secure (HTTPS) |
    | 445 | Server Message Block (SMB) file sharing |
    | 3389 | Remote Desktop Protocol (RDP) |
7. Select **Save** when you're finished.

Note

You can add up to 500 application segments to your Quick Access app.

### Add private DNS suffixes

[Private DNS support for Microsoft Entra Private Access](concept-private-name-resolution) lets you query your own internal DNS servers to resolve IP addresses for internal domain names. Let’s look at an example. Let’s say you have an internal IP range of `10.8.0.0` to `10.8.255.255`. You configure this range in your Quick Access application definition. You want users to access a web application responding on IP `10.8.0.5` when they type `https://benefits` in their web browser. But you don’t want to configure a FQDN for the application. Using Private DNS, you configure a corresponding DNS Suffix so that the Global Secure Access client knows how to route the request correctly.

Additionally, you can provide a single sign-on (SSO) experience for Kerberos resources by configuring Kerberos Authentication to domain controllers using Private DNS. To learn more about creating an SSO experience, see [Use Kerberos for single sign-on (SSO) to your resources with Microsoft Entra Private Access](how-to-configure-kerberos-sso).

Add a DNS suffix to use for private DNS.

1. Select **Private DNS** tab.
2. Select the checkbox to **enable private DNS**.
3. Select **Add DNS suffix**.
4. Enter the DNS suffix and then select **Add**.

## Assign users and groups

When you configure Quick Access, a new enterprise app is created on your behalf. You need to grant access to the Quick Access app you created by assigning users and/or groups to the app.

You can view the properties from **Quick Access** or navigate to **Enterprise applications** and search for your Quick Access app.

Tip

To find an app on the **Enterprise applications** page, clear all filters so that you don't filter out the app you are looking for.

1. Select **Edit application settings** from Quick Access.

    ![Screenshot that shows edit application settings.](media/how-to-configure-quick-access/edit-application-settings.png)
2. Select **Users and groups** from the side menu.
3. Add users and groups as needed.

    - For more information, see [Assign users and groups to an application](/en-us/azure/active-directory/manage-apps/assign-user-or-group-access-portal).

Note

Users must be directly assigned to the app or to the group assigned to the app. Nested groups are not supported.

## Link Conditional Access policies

Conditional Access policies can be applied to your Quick Access app. Applying Conditional Access policies provides more options for managing access to applications, sites, and services.

Creating a Conditional Access policy is covered in detail in [How to create a Conditional Access policy for Private Access apps](how-to-target-resource-private-access-apps).

## Enable Microsoft Entra Private Access

Once you have your Quick Access app configured, your private resources added, users assigned to the app, you can enable the Private access profile from the **Traffic forwarding** area of Global Secure Access. You can enable the profile before configuring Quick Access, but without the app and profile configured, there's no traffic to forward. To learn how to enable the Private Access traffic forwarding profile, see [How to manage the Private Access traffic forwarding profile](how-to-manage-private-access-profile).
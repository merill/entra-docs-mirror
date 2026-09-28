---
layout: Conceptual
title: How to manage the Internet Access profile - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-manage-internet-access-profile
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to manage the Internet Access traffic forwarding profile for Microsoft Entra Internet Access.
ms.topic: how-to
ms.date: 2026-08-02T00:00:00.0000000Z
ms.subservice: entra-internet-access
ms.reviewer: katabish
ai-usage: ai-assisted
locale: en-us
document_id: 57c35445-1a97-3d3c-3771-112982fe8320
document_version_independent_id: 57c35445-1a97-3d3c-3771-112982fe8320
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-manage-internet-access-profile.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-manage-internet-access-profile
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-manage-internet-access-profile.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/341fdab2-4964-4759-8241-f5820b012a47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cc1f92bb-c0d6-4d40-99ce-dabea3161a84
platformId: ee71955d-85f0-6363-3200-782e2e5ad60c
---

# How to manage the Internet Access profile - Global Secure Access | Microsoft Learn

## Overview

The Internet Access traffic forwarding profile routes internet traffic through the Global Secure Access client and remote networks. Enabling this traffic forwarding profile allows users to connect to the internet in a controlled and secure way. You can configure which traffic to include or exclude from Global Secure Access based on IP addresses, IP address ranges, IP subnets, and Fully Qualified Domain Names (FQDNs). You can also deploy Global Secure Access side by side with another Secure Web Gateway (SWG) vendor by using the **Custom Acquire** policy to selectively acquire specific traffic, or the **Agentic Acquire** policy to acquire traffic from local AI agents (such as GitHub Copilot CLI or Claude CLI), while using other vendors for rest of the internet.

## Prerequisites

To enable the Internet Access forwarding profile for your tenant, you must have:

- A [Global Secure Access Administrator](../identity/role-based-access-control/permissions-reference#global-secure-access-administrator) role in Microsoft Entra ID.
- The product requires licensing. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

## Internet Access traffic forwarding profile policies

View the policies that relate to the Internet Access traffic forwarding profile. There are six policies in total. To view them:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Traffic forwarding**.
3. Select the **View** link in the Internet Access policies section.

The Internet Access policies include:

- **Custom Bypass** Contains user-defined traffic/endpoints that are *excluded* from the Internet traffic profile. In other words, you define the traffic that the profile shouldn't acquire. You might typically exclude traffic such as your VPN endpoints, squat IP ranges, and endpoints that leverage a network Access Control List (ACL).
- **Default Bypass** Contains predefined traffic that the Internet traffic profile doesn't acquire. For example, private IP ranges. You can't change rules in this policy.
- **Microsoft Traffic Bypass** Contains predefined Microsoft endpoints that are explicitly excluded from the Internet traffic profile and are instead acquired using Microsoft traffic profile. You can't change rules in this policy.
- **Custom Acquire** Contains user-defined traffic/endpoints that are explicitly *acquired* by the Internet traffic profile. Unlike the **Default Acquire** policy, which is limited to ports 80 and 443 over TCP, Custom Acquire lets you selectively acquire traffic for specific IP addresses, IP address ranges, IP subnets, and Fully Qualified Domain Names (FQDNs) on any ports and protocol (TCP or UDP) you specify. This lets you deploy Global Secure Access side by side with another Secure Web Gateway (SWG) vendor: Global Secure Access acquires the traffic you specify (for example, `chat.com`), while the other vendor covers the rest of your internet traffic.
- **Default Acquire** Contains predefined traffic that gets acquired by the Internet traffic profile. This includes internet traffic on ports 80, 443 over TCP. The policy takes lowest precedence after all bypass and custom acquire rules are evaluated. You can't change rules in this policy.
- **Agentic Acquire** A special policy that signals the Global Secure Access client to acquire all web traffic that originates from local AI agents running on the device, such as GitHub Copilot CLI, Claude CLI, and similar local agents. Enable it to deploy Global Secure Access for agentic (AI agent) protection side by side with another SWG vendor that covers user traffic. You can't change rules in this policy.

## How to add a custom bypass policy

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Traffic forwarding**.
3. In the Internet Access traffic forwarding profile area, in the **Internet Access policies** section, select the **View** link
4. Expand the **Custom Bypass** policy.
5. Select **Add rule**.
6. Choose a **destination type**: Fully Qualified Domain Name (FQDN), IP address, IP subnet, or IP range. You can add multiple comma-separated destination values. Don't add whitespace. For example, `chat.com,contoso.com` or `10.0.0.1/32,10.0.0.2/32`.
7. Enter a valid **destination** and specify the **ports** and **protocol** (TCP or UDP) to bypass.
8. Select **Save**.

## How to add a custom acquire policy

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Traffic forwarding**.
3. In the Internet Access traffic forwarding profile area, in the **Internet Access policies** section, select the **View** link.
4. Expand the **Custom Acquire** policy.
5. Select **Add rule**.
6. Choose a **destination type**: Fully Qualified Domain Name (FQDN), IP address, IP subnet, or IP range. You can add multiple comma-separated destination values. Don't add whitespace. For example, `chat.com,contoso.com` or `10.0.0.1/32,10.0.0.2/32`.
7. Enter a valid **destination** and specify the **ports** and **protocol** (TCP or UDP) to acquire.
8. Disable the **Default Acquire** policy using the toggle next to it. Click **OK** when prompted.
9. Select **Save**.

Note

Traffic is evaluated from top to bottom, which means it only gets acquired by the Internet traffic profile if it’s not being bypassed in one of the bypass rules.

## How to enable agentic acquire policy

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Traffic forwarding**.
3. In the Internet Access traffic forwarding profile area, in the **Internet Access policies** section, select the **View** link.
4. For first time setup, click the **Create Agentic Acquire** button to create the policy. If policy is already created, use the toggle to enable it. Click **OK** when prompted.
5. Disable the **Custom Acquire** and **Default Acquire** policy using the toggles next to them. Click **OK** when prompted.

Note

Agentic Acquire is only supported on Windows and Mac platforms. Minimum required client version for Windows is **2.31.125** and for Mac is **1.1.26030604**.

## User and group assignments

You can scope the Internet Access profile to specific users and groups.

For more information about user and group assignment, see [How to assign and manage users and groups with traffic forwarding profiles](how-to-manage-users-groups-assignment).

## Enable the Internet Access traffic forwarding profile

To enable the Microsoft Entra Internet Access forwarding profile to forward user traffic:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Traffic forwarding**.
3. Set policies on the traffic profile. For example, set a custom bypass rule to exclude specific traffic.
4. Enable the **Internet access profile**. Internet traffic starts forwarding from all client devices to Microsoft's Security Service Edge (SSE) proxy, where you configure granular security policies. 
    Note

    When you enable the Internet Access forwarding profile, you should also enable the Microsoft traffic forwarding profile for optimal routing of Microsoft traffic. You enable the **Microsoft traffic profile** by selecting the profile checkbox on the same page where you enable the Internet Access traffic forwarding profile. For more information about the Microsoft traffic forwarding profile, see [How to enable and manage the Microsoft profile](how-to-manage-microsoft-profile).

## Validate the Internet Access traffic forwarding profile

A rule added to a policy takes 10-20 minutes to appear in the client on a user's computer. If the rule doesn't appear after this time, disable and then re-enable the Internet Access traffic forwarding profile.

To validate the traffic forwarding profile, traffic forwarding policies, and rules:

1. In the system tray, right click the Global Secure Access client and select **Advanced diagnostics**.
2. Open a web browser and navigate to a destination on the internal network. Confirm that traffic isn't being captured.
3. Open a web browser and navigate to a destination that is bypassed. Confirm that traffic isn't being captured.
4. Open a web browser and navigate to a public destination that is acquired by the profile. Confirm the traffic is being acquired under the **Internet channel**.
---
layout: Conceptual
title: 'Tutorial: Enable the Microsoft traffic profile - Global Secure Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/tutorial-microsoft-traffic-enable-profile
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to enable the Microsoft traffic profile in Global Secure Access, assign users, install the client, and verify traffic forwarding.
ms.topic: tutorial
ms.date: 2026-06-22T00:00:00.0000000Z
ms.subservice: entra-internet-access
ms.reviewer: jebley
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 2e2d41fa-4468-7583-c63b-95182d63606a
document_version_independent_id: 2e2d41fa-4468-7583-c63b-95182d63606a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/tutorial-microsoft-traffic-enable-profile.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/tutorial-microsoft-traffic-enable-profile
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/tutorial-microsoft-traffic-enable-profile.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: ba1d5c4b-2a34-705b-e461-84b80daab5d8
---

# Tutorial: Enable the Microsoft traffic profile - Global Secure Access | Microsoft Learn

The Microsoft traffic profile routes supported Microsoft 365 and Microsoft Entra ID traffic through Global Secure Access. Enabling this profile helps you apply controls such as source IP restoration, compliant network checks, and universal tenant restrictions to Microsoft traffic.

In this tutorial, you learn how to:

- Enable the Microsoft traffic profile.
- Assign users and groups to the profile.
- Install the Global Secure Access client on a Windows device.
- Verify that the traffic forwarding profile is configured.

## Key concepts

Traffic forwarding profiles tell the Global Secure Access client which traffic to capture and route through Microsoft's security service edge (SSE).

| Profile | Traffic type | Purpose |
| --- | --- | --- |
| Microsoft traffic | Microsoft 365 and Microsoft Entra ID services | Optimized routing for supported Microsoft services, universal tenant restrictions, and compliant network checks. |
| Private Access | Internal corporate resources | Zero Trust access to private resources without requiring a legacy VPN. |
| Internet Access | All other internet traffic | Web filtering, threat protection, and Transport Layer Security (TLS) inspection. |

When you enable the Microsoft traffic profile, the Global Secure Access client acquires supported Microsoft traffic and forwards it to Microsoft's SSE proxy. Microsoft traffic is never routed through the Internet Access profile. Traffic available for acquisition in the Microsoft traffic profile can only be acquired in the Microsoft traffic profile.

## Step 1: Enable the Microsoft traffic profile

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) as a Global Secure Access Administrator and Application Administrator.
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Traffic forwarding**.
3. Enable the **Microsoft traffic profile**.

    [![Screenshot of the Traffic forwarding page with the Microsoft traffic profile enabled.](media/tutorial-microsoft-traffic/microsoft-traffic-profile.png)](media/tutorial-microsoft-traffic/microsoft-traffic-profile.png#lightbox)

## Step 2: Assign users and groups

The Microsoft traffic profile must be assigned to users before it takes effect. You need the Application Administrator role to assign the traffic profile to selected users and groups. You can assign the profile to all users or scope it to specific users and groups for a phased rollout or proof-of-concept testing.

1. On the **Traffic forwarding** page, locate the **Microsoft traffic profile** section.
2. Under **User and group assignments**, select **View**.
3. Under **Assigned**, select the current user and group assignment link, such as **0 users, 0 groups assigned**.
4. Select **Add user/group**.
5. Search for and select the pilot users or groups that you want to include.
6. Select **Assign**.

Microsoft 365 and Microsoft Entra ID traffic is now forwarded from client devices to Microsoft's SSE proxy for users who have the Global Secure Access client installed and are assigned to the Microsoft traffic profile.

## Step 3: Install the Global Secure Access client

1. Download the Global Secure Access client for Windows 11.

    - For standard Windows 11 devices, use the [Global Secure Access Windows client](https://aka.ms/GlobalSecureAccess-Windows).
    - For Arm-based Windows 11 devices, use the [Global Secure Access Windows client for Arm](https://aka.ms/GlobalSecureAccess-WindowsOnArm).
2. Select the downloaded file and complete the wizard to install the Global Secure Access client.
3. After installation is complete, verify that the Global Secure Access client icon appears in the Windows system tray.

    [![Screenshot that shows the Global Secure Access client icon in the Windows system tray.](media/tutorial-microsoft-traffic/global-secure-access-tray-icon.png)](media/tutorial-microsoft-traffic/global-secure-access-tray-icon.png#lightbox)

## Step 4: Verify results

1. Right-click the Global Secure Access icon in the Windows system tray and select **Advanced Diagnostics**.
2. Select **Forwarding profile**.
3. Verify that the Microsoft Entra rules and Microsoft 365 rules are present.
4. Optionally, review the **Health check** tab results.

[![Screenshot that shows Microsoft 365 rules and Entra rules in the Global Secure Access client forwarding profile.](media/tutorial-microsoft-traffic/global-secure-access-client-forwarding-profile-rules.png)](media/tutorial-microsoft-traffic/global-secure-access-client-forwarding-profile-rules.png#lightbox)

The Global Secure Access client automatically checks for traffic forwarding profile updates every five minutes. You can see the date and time of the last check next to the **Forwarding profile last checked** field on the **Forwarding profile** tab. If you don't see the results you expect, wait five minutes and then select **Refresh**.

## Review Microsoft traffic policies

The Microsoft traffic profile includes the following policy groups:

- Exchange Online.
- SharePoint Online and Microsoft OneDrive.
- Microsoft Teams.
- Microsoft 365 Common and Office Online.

To view the policy groups, select **View** for **Microsoft traffic policies**.

[![Screenshot of the Microsoft traffic profile with the View link for Microsoft traffic policies highlighted.](media/tutorial-microsoft-traffic/view-microsoft-traffic-policies.png)](media/tutorial-microsoft-traffic/view-microsoft-traffic-policies.png#lightbox)

The policy groups are listed with a checkbox that indicates whether the policy group is enabled. Expand a policy group to view the IP addresses and FQDNs included in the group.

[![Screenshot that shows the Microsoft traffic profile policy groups.](media/tutorial-microsoft-traffic/microsoft-traffic-policies.png)](media/tutorial-microsoft-traffic/microsoft-traffic-policies.png#lightbox)

The following example shows the Exchange Online policy group expanded with its rules.

[![Screenshot that shows Exchange Online rules in the Microsoft traffic profile.](media/tutorial-microsoft-traffic/exchange-online-rules.png)](media/tutorial-microsoft-traffic/exchange-online-rules.png#lightbox)

## What you learned

In this exercise, you accomplished the following tasks:

- **Enabled the Microsoft traffic profile:** You activated the Global Secure Access client's ability to acquire supported Microsoft traffic.
- **Scoped the deployment:** You assigned the profile to pilot users or groups.
- **Installed the client:** You prepared a Windows device to acquire Microsoft traffic.
- **Verified the profile:** You confirmed that Microsoft traffic forwarding rules are present on the client.
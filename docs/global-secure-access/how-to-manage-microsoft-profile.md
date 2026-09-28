---
layout: Conceptual
title: How to Enable and Manage the Microsoft Profile - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-manage-microsoft-profile
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Enable the Microsoft traffic forwarding profile to route traffic to Microsoft 365 services including Exchange Online, SharePoint, and OneDrive through Global Secure Access.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.subservice: entra-internet-access
ai-usage: ai-assisted
locale: en-us
document_id: 7dd33522-9838-e34b-de3e-429e3434ee89
document_version_independent_id: 7dd33522-9838-e34b-de3e-429e3434ee89
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-manage-microsoft-profile.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-manage-microsoft-profile
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-manage-microsoft-profile.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: abe4be65-9d29-f46f-04d5-22e22e61d9e4
---

# How to Enable and Manage the Microsoft Profile - Global Secure Access | Microsoft Learn

## Overview

With the Microsoft profile enabled, Microsoft Entra Internet Access acquires the traffic going to Microsoft services. The **Microsoft** profile manages the following policy groups:

- Exchange Online
- SharePoint Online and Microsoft OneDrive
- Microsoft Teams
- Microsoft 365 Common and Office Online

## Prerequisites

To enable the Microsoft traffic forwarding profile for your tenant, you must have:

- A [Global Secure Access Administrator](../identity/role-based-access-control/permissions-reference#global-secure-access-administrator) role in Microsoft Entra ID to enable traffic profiles.
- A [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator) role to create and interact with Conditional Access policies.
- The product requires licensing. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

### Known limitations

For detailed information about known issues and limitations, see [Known limitations for Global Secure Access](reference-current-known-limitations).

## Enable the Microsoft traffic profile

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Traffic forwarding**.
3. Enable the **Microsoft traffic profile**. Microsoft traffic starts forwarding from all client devices to Microsoft's Security Service Edge (SSE) proxy, where you can configure advanced security features specific to Microsoft traffic.

    [![Screenshot of the traffic forwarding page with the Microsoft access profile enabled.](media/how-to-manage-microsoft-profile/microsoft-traffic-profile.png)](media/how-to-manage-microsoft-profile/microsoft-traffic-profile-expanded.png#lightbox)

## Microsoft traffic policies

To manage the details included in the Microsoft traffic forwarding policy, select the **View** link for **Microsoft traffic policies**.

![Screenshot of the Microsoft access profile, with the view applications link highlighted.](media/how-to-manage-microsoft-profile/microsoft-traffic-policies.png)

The policy groups are listed, with a checkbox to indicate if the policy group is enabled. Expand a policy group to view all of the IPs and FQDNs included in the group.

![Screenshot that shows the Microsoft profile details.](media/how-to-manage-microsoft-profile/microsoft-profile-details.png)

The policy groups include the following details:

- **Destination type**: FQDN or IP subnet
- **Destination**: The details of the FQDN or IP subnet
- **Ports**: TCP or UDP ports that are combined with the IP addresses to form the network endpoint
- **Protocol**: TCP (Transmission Control Protocol) or UDP (User Datagram Protocol)
- **Action**: Forward or Bypass

You can configure the traffic acquisition rules to bypass traffic acquisition. If you do, the users are still able to access resources; however, the Global Secure Access service doesn't process the traffic. You can bypass traffic to a specific FQDN or IP address, an entire policy group within the profile, or the entire Microsoft profile itself. If you only need to forward some of the Microsoft resources within a policy group, enable the group then change the **Action** in the details accordingly.

Important

When a rule is set to Bypass in the Microsoft traffic profile, the Internet Access traffic profile will not acquire this traffic. Even with the Internet Access profile enabled, the bypassed traffic will skip Global Secure Access acquisition and use that client's network routing path to egress to the Internet. Traffic available for acquisition in the Microsoft traffic profile can be only acquired in the Microsoft traffic profile.

The following example shows setting the `*.sharepoint.com` FQDN to **Bypass** so the traffic isn't forwarded to the service.

![Screenshot that shows the Action dropdown menu.](media/how-to-manage-microsoft-profile/microsoft-policies-forward-bypass.png)

If the Global Secure Access client isn't able to connect to the service (for example due to an authorization or Conditional Access failure), the service *bypasses* the traffic. Traffic is sent direct-and-local instead of being blocked. In this scenario, you can create a Conditional Access policy for the [compliant network check](how-to-compliant-network), to block traffic if the client isn't able to connect to the service.

## Linked Conditional Access policies

[Conditional Access policies](../identity/conditional-access/overview) are created and applied to the traffic forwarding profile in the Conditional Access area of Microsoft Entra ID. For example, you can create a policy that requires compliant devices when users are establishing the network connection for services in the Microsoft traffic profile.

If you see "None" in the **Linked Conditional Access policies** section, there isn't a Conditional Access policy linked to the traffic forwarding profile. To create a Conditional Access policy, see [Universal Conditional Access through Global Secure Access](how-to-target-resource-microsoft-profile).

### Edit an existing Conditional Access policy

If the traffic forwarding profile has a linked Conditional Access policy, you can view and edit that policy.

1. Select the **View** link for **Linked Conditional Access policies**.

    ![Screenshot that shows traffic forwarding profiles with Conditional Access link highlighted.](media/how-to-manage-microsoft-profile/microsoft-conditional-access-policy-link.png)
2. Select a policy from the list. The details of the policy open in Conditional Access.

    ![Screenshot that shows the applied Conditional Access policies.](media/how-to-manage-microsoft-profile/conditional-access-applied-policies.png)

## Microsoft traffic profile remote network assignments

Traffic profiles can be assigned to remote networks, so that the network traffic is forwarded to Global Secure Access without having to install the client on end user devices. As long as the device is behind the customer premises equipment (CPE), the client isn't required. You must create a remote network before you can add it to the profile. For more information, see [How to create remote networks](how-to-create-remote-networks).

**To assign a remote network to the Microsoft profile**:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Traffic forwarding**.
3. From the **Remote network assignments** section, select the **View** link for the profile.
4. Select a remote network from the list and select **Add**.

## User and group assignments

You can scope the Microsoft profile to specific users and groups instead of applying the traffic profile to all users. For more information about user and group assignment, see [How to assign and manage users and groups with traffic forwarding profiles](how-to-manage-users-groups-assignment).
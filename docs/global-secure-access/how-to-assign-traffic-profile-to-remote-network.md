---
layout: Conceptual
title: How to Assign a Remote Network to a Traffic Forwarding Profile for Global Secure Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-assign-traffic-profile-to-remote-network
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Assign remote networks to traffic forwarding profiles through the Microsoft Entra admin center or Microsoft Graph API to route branch office traffic through Global Secure Access.
ms.topic: how-to
ms.reviewer: abhijeetsinha
ms.date: 2026-04-15T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 6ed45532-463a-0b39-3c65-56747790537a
document_version_independent_id: 53f2cb34-64e0-8fd8-8dd5-ce84c2879df6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-assign-traffic-profile-to-remote-network.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-assign-traffic-profile-to-remote-network
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-assign-traffic-profile-to-remote-network.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 6337d7cc-0629-c322-f113-286a68c06ea2
---

# How to Assign a Remote Network to a Traffic Forwarding Profile for Global Secure Access - Global Secure Access | Microsoft Learn

## Overview

If you tunnel your Microsoft traffic through the Global Secure Access service, you can assign remote networks to the traffic forwarding profile. Your end users can access Microsoft resources by connecting to the service from a remote network, such as a branch office location.

You can assign a remote network to the traffic forwarding profile in several ways:

- When you create or manage a remote network in the Microsoft Entra admin center
- When you enable or manage the traffic forwarding profile in the Microsoft Entra admin center
- By using the Microsoft Graph API

### Traffic profile enforcement on remote network device links

Global Secure Access enforces traffic forwarding profiles for all device links, such as IPsec tunnels, associated with a remote network. It forwards only traffic types that match an enabled and associated traffic forwarding profile. The Global Secure Access gateway drops all other traffic.

This enforcement means:

- If you associate only the **Microsoft traffic profile** with a remote network, the Global Secure Access gateway drops any non-Microsoft traffic (such as general internet traffic) sent over the device link.
- If you associate only the **Internet Access traffic profile** with a remote network, the Global Secure Access gateway drops any Microsoft traffic sent over the device link.

Important

To avoid unintended traffic loss, associate **both** the **Microsoft traffic profile** and the **Internet Access traffic profile** with your remote network if your license permits. This configuration ensures that the appropriate profile handles all traffic forwarded over the IPsec tunnel rather than silently dropping it at the gateway.

For details on available traffic forwarding profiles and their configuration, see [Global Secure Access traffic forwarding profiles](/en-us/entra/global-secure-access/concept-traffic-forwarding).

## Prerequisites

To assign a remote network to a traffic forwarding profile, you must have:

- A **Global Secure Access Administrator** role in Microsoft Entra ID.
- The product requires licensing. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

### Known limitations

For detailed information about known issues and limitations, see [Known limitations for Global Secure Access](reference-current-known-limitations).

## Assign the remote network to Microsoft or the internet traffic profile

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Remote networks**.
3. Select a remote network.
4. Select **Traffic profiles**.
5. Select (or unselect) the checkbox for **Microsoft traffic profile**.
6. Select **Save**.

    ![Screenshot of the Create a remote network page, open to the Traffic profiles tab, with Microsoft traffic profile selected.](media/how-to-assign-traffic-profile-to-remote-network/microsoft-traffic-profile-selected.png)

## Assign a remote network to the Microsoft traffic forwarding profile

1. Browse to **Global Secure Access** &gt; **Connect** &gt; **Traffic forwarding**.
2. Select **Add/edit assignments** for **Microsoft traffic profile**.

    [![Screenshot of the add/edit assignment on the Microsoft traffic profile.](media/how-to-assign-traffic-profile-to-remote-network/microsoft-traffic-profile-remote-network.png)](media/how-to-assign-traffic-profile-to-remote-network/microsoft-traffic-profile-remote-network.png#lightbox)

### Assign a traffic profile to a remote network using the Microsoft Graph API

To associate a traffic profile with your remote network by using the Microsoft Graph API, complete two steps. First, get the traffic forwarding profile ID. This ID is unique for all tenants. Then, use the traffic forwarding profile ID to assign the traffic forwarding profile to your remote network.

Assign a traffic forwarding profile by using Microsoft Graph on the `/beta` endpoint.

1. Open a web browser and go to **Graph Explorer** at https://aka.ms/ge.
2. Select **GET** as the HTTP method from the dropdown.
3. Select the API version as **beta**.
4. Enter the query. 

    ```
    GET https://graph.microsoft.com/beta/networkaccess/forwardingprofiles 
    ```
5. Select **Run query**.
6. Find the ID of the desired traffic forwarding profile.
7. Select **PATCH** as the HTTP method from the dropdown.
8. Enter the query. 

    ```
        PATCH https://graph.microsoft.com/beta/networkaccess/branches/d2b05c5-1e2e-4f1d-ba5a-1a678382ef16/forwardingProfiles
        {
            "@odata.context": "#$delta",
            "value":
            [{
                "ID": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee"
            }]
        }
    ```
9. Select **Run query** to update the branch.
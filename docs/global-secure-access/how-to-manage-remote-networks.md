---
layout: Conceptual
title: How to Update and Delete Remote Networks for Global Secure Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-manage-remote-networks
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Modify remote network configurations, delete unused networks, and manage device links and traffic profile assignments for Global Secure Access.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 10167d25-cc1f-385f-0a74-7674e33c0e8b
document_version_independent_id: 93fbd791-ec5f-ac04-3350-9674be6ce77d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-manage-remote-networks.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-manage-remote-networks
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-manage-remote-networks.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 05cbc4cc-7b7d-1bd1-7ea0-86754c88b3eb
---

# How to Update and Delete Remote Networks for Global Secure Access - Global Secure Access | Microsoft Learn

## Overview

Remote networks connect your users in remote locations to Global Secure Access. Adding, updating, and removing remote networks from your environment are likely common tasks for many organizations.

This article explains how to manage your existing remote networks for Global Secure Access.

## Prerequisites

- A **Global Secure Access Administrator** role in Microsoft Entra ID.
- The product requires licensing. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

### Known limitations

For detailed information about known issues and limitations, see [Known limitations for Global Secure Access](reference-current-known-limitations).

## Update remote networks

You can update remote networks in the Microsoft Entra admin center or using the Microsoft Graph API.

# [Microsoft Entra admin center](#tab/microsoft-entra-admin-center)
To update the details of your remote networks:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Remote networks**.
3. Select the remote network you need to update.

There are three sections with details you can edit. **Basics**, **Links**, and **Traffic profiles**.

#### Update basic settings

The basics page provides a way to delete a selected remote network. You change the name of a remote network after you create it. Select the pencil icon to edit the name of the remote network.

![Screenshot that shows the basics tab with the pencil icon highlighted.](media/how-to-manage-remote-networks/remote-network-basics.png)

#### Update device links

Add a new device link or delete an existing device link from this page. You can't edit the details of a device link after it was created. Select the trash can icon to delete a remote network device link.

![Screenshot that shows the delete option in the device links page.](media/how-to-manage-remote-networks/delete-device-link.png)

#### Update traffic profiles

From this page, you can enable or disable the available traffic forwarding profiles. The Microsoft traffic and Internet Access profiles can be assigned to remote networks. The Private Access profile requires the Global Secure Access client. For more information, see [Assign a traffic profile to a remote network](how-to-assign-traffic-profile-to-remote-network).

![Screenshot of the Create a remote network page, open to the Traffic profiles tab, with Microsoft traffic profile selected.](media/how-to-manage-remote-networks/microsoft-traffic-profile-selected.png)

You can also assign a remote network to the Microsoft traffic forwarding profile from **Traffic forwarding** area of Global Secure Access. Browse to **Connect** &gt; **Traffic forwarding** and select **Add/edit assignments** for the traffic profile. For more information, see [Global Secure Access traffic forwarding](concept-traffic-forwarding).

# [Microsoft Graph API](#tab/microsoft-graph-api)
To edit the details of a remote network:

1. Sign in to [Graph Explorer](https://aka.ms/ge).
2. Select **PATCH** as the HTTP method from the dropdown.
3. Select the API version to **BETA**.
4. Enter the query.

```http
    PATCH https://graph.microsoft.com/beta/networkaccess/connectivity/branches/8d2b05c5-1e2e-4f1d-ba5a-1a678382ef16
    {
        "@odata.context": "#$delta",
        "name": "ContosoRemoteNetwork2"
    }
```

1. Select **Run query** to update the remote network.

---

## Delete a remote network

You can delete remote networks in the Microsoft Entra admin center or using the Microsoft Graph API.

# [Microsoft Entra admin center](#tab/microsoft-entra-admin-center)
1. Sign in to the Microsoft Entra admin center at https://entra.microsoft.com.
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Remote networks**.
3. Select the remote network you need to delete.
4. Select **Delete**.
5. Select **Delete** from the confirmation message.

![Screenshot that shows delete remote network.](media/how-to-manage-remote-networks/delete-remote-network.png)

# [Microsoft Graph API](#tab/microsoft-graph-api)
1. Sign in to [Graph Explorer](https://aka.ms/ge).
2. Select **PATCH** as the HTTP method from the dropdown.
3. Select the API version to **beta**.
4. Enter the query.

```http
   DELETE https://graph.microsoft.com/beta/networkaccess/connectivity/branches/97e2a6ea-c6c4-4bbe-83ca-add9b18b1c6b 
```

1. Select **Run query** to delete the remote network.

---
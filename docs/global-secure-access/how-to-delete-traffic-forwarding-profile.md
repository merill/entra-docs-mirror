---
layout: Conceptual
title: Delete a Microsoft Entra Private Access traffic forwarding profile - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-delete-traffic-forwarding-profile
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to delete a custom Private Access traffic forwarding profile in Global Secure Access.
ms.topic: how-to
ms.date: 2026-09-20T00:00:00.0000000Z
ms.subservice: entra-private-access
ms.reviewer: katabish
ai-usage: ai-assisted
locale: en-us
document_id: 5ae287cc-a11f-e554-0fc0-8e2e0c89c5dd
document_version_independent_id: 5ae287cc-a11f-e554-0fc0-8e2e0c89c5dd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-delete-traffic-forwarding-profile.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-delete-traffic-forwarding-profile
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-delete-traffic-forwarding-profile.md
platformId: 0dbd1f1d-0440-fb69-9907-d7f2040dfbd0
---

# Delete a Microsoft Entra Private Access traffic forwarding profile - Global Secure Access | Microsoft Learn

You can delete a custom Private Access traffic forwarding profile when your organization no longer needs its acquisition rules or assignments.

Default traffic forwarding profiles are created by the service and can't be deleted. Deleted custom profiles can't be restored.

Important

Before deleting a custom profile, review its application, user, group, device, and device-platform assignments. Move any required configuration to another profile before you delete it.

## Prerequisites

To delete a custom Private Access traffic forwarding profile, you must have:

- A [Global Secure Access Administrator](../identity/role-based-access-control/permissions-reference#global-secure-access-administrator) role in Microsoft Entra ID.
- A custom Private Access traffic forwarding profile.

## Delete a custom profile

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a Global Secure Access Administrator.
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Traffic forwarding**.
3. Select the custom Private Access traffic forwarding profile that you want to delete.
4. Select **Delete** from the command bar.

    ![Screenshot of a custom Private Access traffic forwarding profile with Delete highlighted.](media/how-to-delete-traffic-forwarding-profile/delete-private-access-profile.png)
5. Review the confirmation, and then confirm the deletion.

The deleted profile no longer applies to its assigned users or devices.
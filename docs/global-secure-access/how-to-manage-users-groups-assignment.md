---
layout: Conceptual
title: Assign users and devices to traffic forwarding profiles - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-manage-users-groups-assignment
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Assign users, groups, devices, and device platforms to Global Secure Access traffic forwarding profiles.
ms.topic: how-to
ms.date: 2026-09-20T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: d6d985c9-8fcf-527c-daeb-c3d0037a3ba9
document_version_independent_id: d6d985c9-8fcf-527c-daeb-c3d0037a3ba9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-manage-users-groups-assignment.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-manage-users-groups-assignment
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-manage-users-groups-assignment.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: 60f6a694-0db5-3032-ad5f-74b90ea92d37
---

# Assign users and devices to traffic forwarding profiles - Global Secure Access | Microsoft Learn

## Overview

You can assign specific users, groups, devices, and device platforms to a Global Secure Access traffic forwarding profile. Assignments let you deploy a profile gradually and provide different traffic acquisition rules to different users and devices.

This article explains assignments for traffic forwarding profiles, including custom Private Access profiles.

## Prerequisites

To manage assignments, you must have:

- A [Global Secure Access Administrator](../identity/role-based-access-control/permissions-reference#global-secure-access-administrator) role in Microsoft Entra ID to view and manage the traffic forwarding profile.
- The required Global Secure Access product licenses. For details, see [What is Global Secure Access](overview-what-is-global-secure-access).
- The latest supported Global Secure Access client on applicable devices. The minimum client version for user and group assignment is 1.7.376.0.

## How assignments are evaluated

A traffic forwarding profile has two assignment conditions:

- **User and device assignments** determine which users, groups, or individual devices are in scope.
- **Device platform assignments** determine which device platforms are in scope.

The conditions are evaluated with an `AND`. A device receives a profile only when it matches both conditions.

If multiple enabled profiles for the same traffic type apply to a user and device, only the applicable profile with the highest priority is used.

## Assign users, groups, and devices

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a Global Secure Access Administrator and Application Administrator.
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Traffic forwarding**.
3. Select the traffic forwarding profile.
4. Select **Assignments**.
5. Next to **User and device assignments**, select **View**.
6. Select one of the following options:

    - **No users and devices**: The profile isn't assigned through the Global Secure Access client.
    - **All users and devices**: All devices with the Global Secure Access client are in scope, subject to the device-platform assignment.
    - **Selected users and devices**: Select specific users, groups, or devices.

    ![Screenshot of the Edit user and device assignments pane with All users and devices selected.](media/how-to-manage-users-groups-assignment/edit-user-device-assignments.png)
7. If you selected **Selected users and devices**, select the assignment link, choose the users, groups, and devices, and then select **Select**.
8. Select **Save**.

## Assign device platforms

1. From the profile's **Assignments** page, select **View** next to **Device platform assignments**.
2. Select the device platforms that should receive the profile.
3. Select **Save**.

You can combine platform assignment with user and device assignment. For example:

- Assign **All users and devices** and select **iOS** to apply the profile to all iOS devices with the Global Secure Access client.
- Assign a user group and select **Windows** and **macOS** to apply the profile only to desktop devices used by members of that group.

## Assignment evaluation examples

| User and device assignments | Device platform assignments | Result |
| --- | --- | --- |
| All users and devices | All device platforms | All devices with the Global Secure Access client receive the profile. |
| All users and devices | Windows and macOS | All Windows and macOS devices with the client receive the profile. |
| All users and devices | None | No devices receive the profile. |
| Five users and two devices | All device platforms | All client devices used by the five users and the two selected devices receive the profile. |
| Five users and two devices | Android | Android client devices used by the five users and the selected devices receive the profile only if those devices are Android devices. |
| No users, groups, or devices | Any platform | No devices receive the profile. |

## Assign a profile to all devices on a platform

To assign a profile to all devices on a specific platform:

1. Set **User and device assignments** to **All users and devices**.
2. Under **Device platform assignments**, select only the target platform.
3. Save both assignment settings.

## Automatic assignment through user attributes

You can assign a dynamic group whose members satisfy specific user criteria. For more information, see [Create or update a dynamic group in Microsoft Entra ID](../identity/users/groups-create-rule).

## Validate the effective profile

1. Sign in to a registered device as a user included in the assignment.
2. Right-click the Global Secure Access client, and then select **Advanced diagnostics** &gt; **Forwarding profile**.
3. Expand the applicable traffic type, such as **Private Access rules**.
4. Confirm that the expected application segments appear.

If more than one profile could apply, confirm that the profile with the highest priority is effective.

## Notes about identity, groups, and devices

- Traffic profiles are fetched for the Microsoft Entra user signed in to the device, not the user signed in to the client.
- If no Microsoft Entra user is signed in, a profile is fetched only when **All users and devices** is selected.
- Multiple users signed in to the same device simultaneously aren't supported.
- Group assignment supports security groups and nested group membership is supported.
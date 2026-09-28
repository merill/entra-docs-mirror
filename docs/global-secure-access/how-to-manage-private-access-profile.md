---
layout: Conceptual
title: Manage Private Access traffic forwarding profiles - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-manage-private-access-profile
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Configure and manage default and custom Private Access traffic forwarding profiles in Global Secure Access.
ms.topic: how-to
ms.date: 2026-09-20T00:00:00.0000000Z
ms.subservice: entra-private-access
ms.reviewer: katabish
ai-usage: ai-assisted
locale: en-us
document_id: 44fd3ef8-5f5e-e7c8-48cc-2507dfc8833b
document_version_independent_id: 4bf4651c-3780-799f-6fef-9577f547a25c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-manage-private-access-profile.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-manage-private-access-profile
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-manage-private-access-profile.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
platformId: b9749676-2afe-2f13-6497-7597a70a5bbc
---

# Manage Private Access traffic forwarding profiles - Global Secure Access | Microsoft Learn

## Overview

Private Access traffic forwarding profiles route traffic from the Global Secure Access client to private resources. Enabling this traffic forwarding profile allows remote workers to connect to internal resources without a VPN. With the features of Microsoft Entra Private Access, you can control which private resources to tunnel through the service and apply Conditional Access policies to secure access to those services. You can use the default Private Access profile or create custom profiles with different applications, assignments, device platforms, priorities, and status.

Multiple profiles let you provide different private application access to internal and external users, desktop and mobile devices, or other groups with distinct access requirements.

## Prerequisites

To manage Private Access traffic forwarding profiles, you must have:

- A [Global Secure Access Administrator](../identity/role-based-access-control/permissions-reference#global-secure-access-administrator) role in Microsoft Entra ID.
- An [Application Administrator](../identity/role-based-access-control/permissions-reference#application-administrator) role to manage Private Access applications.
- A [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator) role to create and manage Conditional Access policies.
- Microsoft Entra Private Access or Microsoft Entra Suite licensing. For more information, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access).

### Known limitations

For detailed information about known issues and limitations, see [Known limitations for Global Secure Access](reference-current-known-limitations).

During preview:

- You can create up to 10 custom Private Access traffic forwarding profiles.
- A Private Access application must be included in the default Private Access profile before it can be selected for a custom profile.

## View Private Access profiles

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a Global Secure Access Administrator.
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Traffic forwarding**.

The page displays the system-created profiles and any custom profiles. Select a profile name to manage its **Basics**, **Acquisition rules**, and **Assignments**.

To add a custom profile, see [Create a Private Access traffic forwarding profile](how-to-create-traffic-forwarding-profile).

## Manage profile settings

Select **Basics** to update the custom profile's name, description, priority, or status.

Priority determines which profile is effective if multiple Private Access profiles apply to the same user and device. Only the applicable profile with the highest priority is used by the client.

## Manage acquisition rules

Acquisition rules determine which private resources are included in a profile.

1. Select the Private Access profile.
2. Select **Acquisition rules**.
3. Configure whether the profile includes Quick Access.
4. Select the applications link to add or remove Private Access applications.

    ![Screenshot of the Acquisition rules page for a custom Private Access profile.](media/how-to-manage-private-access-profile/custom-profile-acquisition-rules.png)

Use **Select all** to include all available applications, and then remove the applications that shouldn't be part of the profile.

### Associate an application with multiple profiles

You can also manage profile associations from the Private Access application:

1. Browse to **Global Secure Access** &gt; **Applications** &gt; **Enterprise applications**.
2. Select the application, and then select **Network access properties**.
3. Select **Manage attached profiles**.
4. Select one or more profiles, and then select **Save**.

An application can be associated with multiple Private Access traffic forwarding profiles.

## Manage profile assignments

Select **Assignments** to configure:

- **User and device assignments**: Assign no users or devices, all users and devices, or selected users, groups, and devices.
- **Device platform assignments**: Select the device platforms that receive the profile.

    ![Screenshot of the Assignments page showing user and device assignments and device platform assignments.](media/how-to-manage-private-access-profile/private-access-profile-assignments.png)

The two assignment conditions are evaluated together. For example, if a profile is assigned to selected users and the Android platform, only Android devices used by those selected users receive the profile.

For detailed steps and assignment examples, see [Assign users and devices to traffic forwarding profiles](how-to-manage-users-groups-assignment).

## Linked Conditional Access policies

Conditional Access policies for Private Access are configured at the application level. You can create and apply a Conditional Access policy from either location:

- Browse to **Global Secure Access** &gt; **Applications** &gt; **Enterprise applications**. Select an application, and then select **Conditional Access**.
- Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**, and then select **New policy**.

For more information, see [Apply Conditional Access policies to Private Access applications](how-to-target-resource-private-access-apps).

## Delete a custom profile

Custom Private Access profiles can be deleted. The system-created default profile can't be deleted. Deleted custom profiles can't be restored.

For detailed steps, see [Delete a Private Access traffic forwarding profile](how-to-delete-traffic-forwarding-profile).
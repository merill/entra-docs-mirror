---
layout: Conceptual
title: How to manage local administrators on Microsoft Entra joined devices - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/assign-local-admin
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Learn how to assign Azure roles to the local administrators group of a Windows device.
ms.topic: how-to
ms.date: 2026-06-17T00:00:00.0000000Z
ms.reviewer: 
ms.custom: sfi-ga-nochange
locale: en-us
document_id: 823c9751-c496-f972-3b1b-640a1bd81412
document_version_independent_id: 6951f3d5-c766-133c-4785-9cd4192bae19
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/assign-local-admin.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/assign-local-admin
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/assign-local-admin.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 32d8211e-c9ff-5203-aed8-8963a11c38ad
---

# How to manage local administrators on Microsoft Entra joined devices - Microsoft Entra ID | Microsoft Learn

To manage a Windows device, you need to be a member of the local administrators group. As part of the Microsoft Entra join process, Microsoft Entra ID updates the membership of this group on a device. You can customize the membership update to satisfy your business requirements. A membership update is, for example, helpful if you want to enable your helpdesk staff to do tasks requiring administrator rights on a device.

This article explains how the local administrators membership update works and how you can customize it during a Microsoft Entra join. The content of this article doesn't apply to **Microsoft Entra hybrid joined** devices.

## How it works

At the time of Microsoft Entra join, the following security principals are added to the local administrators group on the device:

- The [Microsoft Entra Joined Device Local Administrator](../role-based-access-control/permissions-reference#microsoft-entra-joined-device-local-administrator) and the [Global Administrator](../role-based-access-control/permissions-reference#global-administrator) roles
- The user performing the Microsoft Entra join

Note

This is done during the join operation only. If an administrator makes changes after this point they will need to update the group membership on the device.

By adding users to the Microsoft Entra Joined Device Local Administrator role, you can update the users that can manage a device anytime in Microsoft Entra ID without modifying anything on the device. The Microsoft Entra Joined Device Local Administrator role is added to the local administrators group to support the principle of least privilege.

## Manage administrator roles

To view and update the membership of an [administrator role](../role-based-access-control/permissions-reference) role, see:

- [View all members of an administrator role in Microsoft Entra ID](../role-based-access-control/view-assignments)
- [Assign a user to administrator roles in Microsoft Entra ID](../role-based-access-control/manage-roles-portal)

## Manage the Microsoft Entra Joined Device Local Administrator role

You can manage the [Microsoft Entra Joined Device Local Administrator](../role-based-access-control/permissions-reference#microsoft-entra-joined-device-local-administrator) role from **Device settings**.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID** &gt; **Devices** &gt; **All devices** &gt; **Device settings**.
3. Select **Manage Additional local administrators on all Microsoft Entra joined devices**.
4. Select **Add assignments** then choose the other administrators you want to add and select **Add**.

To modify the Microsoft Entra Joined Device Local Administrator role, configure **Additional local administrators on all Microsoft Entra joined devices**.

Note

This option requires Microsoft Entra ID P1 or P2 licenses.

Microsoft Entra Joined Device Local Administrators are assigned to all Microsoft Entra joined devices. You can't scope this role to a specific set of devices. Updating the Microsoft Entra Joined Device Local Administrator role doesn't necessarily have an immediate impact on the affected users. On devices where a user is already signed in to, the privilege elevation takes place when *both* the below actions happen:

- Up to 4 hours passed for Microsoft Entra ID to issue a new Primary Refresh Token with the appropriate privileges.
- User signs out and signs back in, not lock/unlock, to refresh their profile.

Users aren't directly listed in the local administrator group, their permissions are received through the Primary Refresh Token.

Note

The above actions are not applicable to users who have not signed in to the relevant device previously. In this case, the administrator privileges are applied immediately after their first sign in to the device.

## Manage administrator privileges using Microsoft Entra groups

You can use Microsoft Entra groups to manage administrator privileges on Microsoft Entra joined devices with the [Local Users and Groups](/en-us/windows/client-management/mdm/policy-csp-localusersandgroups) mobile device management (MDM) policy. This policy allows you to assign individual users or Microsoft Entra groups to the local administrators group on a Microsoft Entra joined device, providing you with the granularity to configure distinct administrators for different groups of devices.

Organizations can use Intune to manage these policies using [Custom OMA-URI Settings](/en-us/mem/intune/configuration/custom-settings-windows-10) or [Account protection policy](/en-us/mem/intune/protect/endpoint-security-account-protection-policy). A few considerations for using this policy:

- Adding Microsoft Entra groups through the policy requires the group's security identifier (SID) that can be obtained by executing the [Microsoft Graph API for Groups](/en-us/graph/api/resources/group). The SID equates to the property `securityIdentifier` in the API response.
- Administrator privileges using this policy are evaluated only for the following well-known groups on a Windows 10 or newer device - Administrators, Users, Guests, Power Users, Remote Desktop Users, and Remote Management Users.
- Managing local administrators using Microsoft Entra groups isn't applicable to Microsoft Entra hybrid joined or Microsoft Entra registered devices.
- Microsoft Entra groups deployed to a device with this policy don't apply to remote desktop connections. To control remote desktop permissions for Microsoft Entra joined devices, you need to add the individual user's SID to the appropriate group.

Important

Windows sign-in with Microsoft Entra ID supports evaluation of up to 20 groups for administrator rights. We recommend having no more than 20 Microsoft Entra groups on each device, and having a user as a member in no more than 20 groups, to ensure that administrator rights are correctly assigned. This limitation also applies to nested groups.

## Manage regular users

By default, Microsoft Entra ID adds the user performing the Microsoft Entra join to the administrator group on the device. If you want to prevent regular users from becoming local administrators, you have the following options:

- **Device registration policy** - The device registration policy controls whether users who perform Microsoft Entra join become local administrators on the devices they join. This setting affects membership in the local Administrators group on the joined device. It doesn't assign a Microsoft Entra directory role, such as Global Administrator, and it doesn't add the user to the Microsoft Entra Joined Device Local Administrator role. In Microsoft Graph, this setting is represented by the `azureADJoin.localAdmins.registeringUsers` property of the [device registration policy](/en-us/graph/api/resources/deviceregistrationpolicy).
- [Windows Autopilot](/en-us/autopilot/windows-autopilot) - Windows Autopilot provides you with an option to prevent primary user performing the join from becoming a local administrator by [creating an Autopilot profile](/en-us/autopilot/enrollment-autopilot#create-an-autopilot-deployment-profile).
- [Bulk enrollment](/en-us/mem/intune/enrollment/windows-bulk-enroll) - a Microsoft Entra join that is performed in the context of a bulk enrollment happens in the context of an autocreated user. Users signing in after a device is joined aren't added to the administrators group.

## Manually elevate a user on a device

In addition to using the Microsoft Entra join process, you can also manually elevate a regular user to become a local administrator on one specific device. This step requires you to already be a member of the local administrators group.

Starting with the **Windows 10 1709** release, you can perform this task from **Settings** &gt; **Accounts** &gt; **Other users**. Select **Add a work or school user**, enter the user's user principal name (UPN) under **User account** and select *Administrator* under **Account type**

Additionally, you can also add users using the command prompt:

- If your tenant users are synchronized from on-premises Active Directory, use `net localgroup administrators /add "<domain>\<username>"`, where `<domain>` is your on-premises Active Directory domain name and `<username>` is the user's SAM account name.
- If your tenant users are created in Microsoft Entra ID, use `net localgroup administrators /add "AzureAD\<UserUPN>"`, where `<UserUPN>` is the user's User Principal Name.

## Considerations

- You can only assign role based groups to the Microsoft Entra Joined Device Local Administrator role.
- The Microsoft Entra Joined Device Local Administrator role is assigned to all Microsoft Entra joined devices. This role can't be scoped to a specific set of devices.
- Local administrator rights on Windows devices aren't applicable to [Microsoft Entra B2B guest users](../../external-id/what-is-b2b).
- When you remove users from the Microsoft Entra Joined Device Local Administrator role, changes aren't instant. Users still have local administrator privilege on a device as long as they're signed in to it. The privilege is revoked during their next sign-in when a new primary refresh token is issued. This revocation, similar to the privilege elevation, could take up to 4 hours.
---
layout: Conceptual
title: Device management permissions for Microsoft Entra custom roles - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/custom-device-permissions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: Device management permissions for Microsoft Entra custom roles in the Microsoft Entra admin center, PowerShell, or Microsoft Graph API.
ms.topic: reference
ms.date: 2024-07-18T00:00:00.0000000Z
ms.custom: it-pro, sfi-image-nochange
locale: en-us
document_id: 3749f638-0e9b-6d47-c310-3675b61b9d9c
document_version_independent_id: 7d9e793b-1c11-53e9-82c4-33e680224d58
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/custom-device-permissions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/custom-device-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/custom-device-permissions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 89e24574-2da2-cbef-b8dd-58172e31f44f
---

# Device management permissions for Microsoft Entra custom roles - Microsoft Entra ID | Microsoft Learn

Device management permissions can be used in custom role definitions in Microsoft Entra ID to grant fine-grained access such as the following:

- Enable or disable devices
- Delete devices
- Read BitLocker recovery keys
- Read BitLocker metadata
- Read device registration policies
- Update device registration policies

This article lists the permissions you can use in your custom roles for different device management scenarios. For information about how to create custom roles, see [Create a custom role in Microsoft Entra ID](custom-create).

## Enable or disable devices

The following permissions are available to toggle device states.

- microsoft.directory/devices/enable
- microsoft.directory/devices/disable

## Read BitLocker recovery keys

The following permission is available to read BitLocker metadata and recovery keys. Note that this single permission provides read for both BitLocker metadata and recovery keys.

- microsoft.directory/bitlockerKeys/key/read

You can view the BitLocker recovery key by selecting a device from the **All Devices** page, and then selecting **Show Recovery Key**. For more information about reading BitLocker recovery keys, see [View or copy BitLocker keys](../devices/manage-device-identities#view-or-copy-bitlocker-keys).

![Screenshot showing Bitlocker keys in Azure portal.](media/custom-device-permissions/bitlocker-keys.png)

Note

When devices that utilize [Windows Autopilot](/en-us/mem/autopilot/windows-autopilot) are reused to join to Entra, **and there is a new device owner**, that new device owner must contact an administrator to acquire the BitLocker recovery key for that device. Custom role or administrative unit scoped administrators will lose access to BitLocker recovery keys for those devices that have undergone device ownership changes. These scoped administrators will need to contact a non-scoped administrator for the recovery keys. For more information, see the article [Find the primary user of an Intune device](/en-us/mem/intune/remote-actions/find-primary-user#change-a-devices-primary-user).

## Read BitLocker metadata

The following permission is available to read the BitLocker metadata for all devices.

- microsoft.directory/bitlockerKeys/metadata/read

You can read the BitLocker metadata for all devices, but you can't read the BitLocker recovery key.

![Screenshot showing Bitlocker metadata in Azure portal.](media/custom-device-permissions/bitlocker-metadata.png)

## Read device registration policies

The following permission is available to read tenant-wide device registration settings.

- microsoft.directory/deviceRegistrationPolicy/standard/read

You can read device settings in the Microsoft Entra admin center.

![Screenshot showing Device settings page in Azure portal.](media/custom-device-permissions/device-settings.png)

## Update device registration policies

The following permission is available to update tenant-wide device registration settings.

- microsoft.directory/deviceRegistrationPolicy/basic/update

## Full list of permissions

#### Read

| Permission | Description |
| --- | --- |
| microsoft.directory/devices/createdFrom/read | Read created from Internet of Things (IoT) device template links |
| microsoft.directory/devices/registeredOwners/read | Read registered owners of devices |
| microsoft.directory/devices/registeredUsers/read | Read registered users of devices |
| microsoft.directory/devices/standard/read | Read basic properties on devices |
| microsoft.directory/bitlockerKeys/key/read | Read bitlocker metadata and key on devices |
| microsoft.directory/bitlockerKeys/metadata/read | Read bitlocker key metadata on devices |
| microsoft.directory/deviceRegistrationPolicy/standard/read | Read standard properties on device registration policies |

#### Update

| Permission | Description |
| --- | --- |
| microsoft.directory/devices/registeredOwners/update | Update registered owners of devices |
| microsoft.directory/devices/registeredUsers/update | Update registered users of devices |
| microsoft.directory/devices/enable | Enable devices in Microsoft Entra ID |
| microsoft.directory/devices/disable | Disable devices in Microsoft Entra ID |
| microsoft.directory/deviceRegistrationPolicy/basic/update | Update basic properties on device registration policies |

#### Delete

| Permission | Description |
| --- | --- |
| microsoft.directory/devices/delete | Delete devices from Microsoft Entra ID |
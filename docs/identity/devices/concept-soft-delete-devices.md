---
layout: Conceptual
title: Device soft delete in Microsoft Entra ID (preview) - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/concept-soft-delete-devices
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Learn about device soft delete (preview) in Microsoft Entra ID, which moves deleted devices to a recoverable state instead of permanently removing them.
ms.topic: concept-article
ms.custom: msecd-doc-authoring-108
ms.date: 2026-04-05T00:00:00.0000000Z
locale: en-us
document_id: 66c36767-879b-a455-b1df-ee49b8aabd6c
document_version_independent_id: 66c36767-879b-a455-b1df-ee49b8aabd6c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/concept-soft-delete-devices.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/concept-soft-delete-devices
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/concept-soft-delete-devices.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3467cf8e-4703-c5b1-fe5f-7aa376bef799
---

# Device soft delete in Microsoft Entra ID (preview) - Microsoft Entra ID | Microsoft Learn

Device soft delete is a recoverability feature in Microsoft Entra ID that moves deleted device objects to a suspended state instead of permanently removing them. When a device is soft deleted, the Azure Device Registration Service (ADRS) de-registers the device and moves the device object into a separate soft-deleted container in the directory. The device is removed from active device lists but remains recoverable for up to 30 days.

This feature helps prevent accidental loss of important device data, such as BitLocker recovery keys and Local Administrator Password Solution (LAPS) passwords. It also reduces the risk of hitting tenant object quotas from orphaned device objects and provides an undo option for device deletions, similar to how soft delete works for users and groups.

Important

Device soft delete is currently in preview. Some features and behaviors might change before general availability.

## How device soft delete works

When an administrator or device owner deletes a device from Microsoft Entra ID, the device object isn't permanently removed. Instead, ADRS initiates a de-registration sequence that disables the device's authentication refresh tokens, then moves the device object into the soft-deleted container. The device retains its unique identifier and key material in the soft-deleted state.

While a device is in the soft-deleted state:

- The device can't authenticate or access cloud resources protected by Microsoft Entra ID.
- The device object can't be modified or updated by management tools.
- The device is hidden from the Azure portal device list, Intune, and Microsoft Graph queries. Queries for the device return an HTTP 404 Not Found error.
- The device's DeviceId remains reserved. No new device can register with the same DeviceId until the soft-deleted device is restored or permanently deleted.
- Soft-deleted devices still count toward the directory object quota, though a tombstone object counts as one-quarter of an active object.

After 30 days in the soft-deleted state, the device is automatically hard deleted (permanently removed).

## Supported device types

During the preview, device soft delete is supported for the following device types:

- **Microsoft Entra joined devices** — Enterprise-managed devices directly joined to Microsoft Entra ID.
- **Microsoft Entra hybrid joined devices** — Enterprise-managed devices joined to your on-premises Active Directory domain and registered with Microsoft Entra ID.
- **Microsoft Entra registered devices** — Personal or BYOD devices registered with a work or school account.

The following device types aren't currently supported for soft delete and are hard deleted immediately when removed:

- Devices without a recognized trust type, such as those created directly via Microsoft Graph API
- Certain specialty device types, including secure VMs with managed identities, non-persistent VDI instances, and printers

## Role requirements

Only specific roles can initiate, restore, or permanently delete devices:

- **Cloud Device Administrators**, **Intune Administrators**, and **Global Administrators** can soft delete any device, restore soft-deleted devices, and permanently delete soft-deleted devices.
- **Device owners** (the user who joined or registered the device) can soft delete their own device but can't restore or permanently delete it.

Custom roles with soft-delete or restore permissions aren't available at this time.

## Data preserved during soft delete

When a device is soft deleted, critical data associated with the device object is preserved in the soft-deleted container:

- **BitLocker recovery keys** — Recovery keys stored with the device remain accessible to administrators. After restoration, keys continue to be available, including for self-service BitLocker key recovery by the registered owner.
- **LAPS passwords** — Local administrator passwords managed through LAPS are retained.
- **Device identity and key material** — The device's unique identifiers and key material are maintained, which enables full restoration of the device object.

When a device is restored, the device object moves back to the active container with these properties intact.

## Compliance reset

When a device is soft deleted, Microsoft Entra ID resets several compliance-related properties to prevent the device from returning unexpected values if restored. Specifically:

- **IsCompliant** is set to **False**.
- Other compliance-related flags are set to null or false.

The MDM application ID, which identifies the management authority such as Intune, is retained and not cleared during soft delete. The device remains associated with its management authority after restoration.

After a device is restored, the IsCompliant value remains False until the device checks in with its management authority and a fresh compliance evaluation completes. This behavior is expected and typically resolves after the device syncs with Intune or another MDM provider.

## Restore a soft-deleted device

During the preview, soft-deleted devices can be restored using Microsoft Graph API or PowerShell. A portal experience for viewing and restoring soft-deleted devices is planned for general availability (GA).

To verify whether a device is soft deleted, administrators can use:

- **Microsoft Graph API** — Query the deleted items endpoint: `GET https://graph.microsoft.com/beta/directory/deletedItems/microsoft.graph.device` to list all soft-deleted devices.
- **PowerShell** — Use the Microsoft Graph PowerShell module to list soft-deleted device objects.

When a device is restored:

- The device object moves from the soft-deleted container back to the active directory container.
- The device can authenticate and be managed again. Users might need to sign in again or reboot the device to refresh the session.
- Compliance-related properties remain in their reset state until the device checks in with its management authority.

Important

Only Cloud Device Administrators, Intune Administrators, and Global Administrators can restore soft-deleted devices.

## Permanent deletion

A hard delete permanently removes a device object from Microsoft Entra ID. Hard deletion occurs in these situations:

- A soft-deleted device isn't restored within 30 days.
- An administrator explicitly performs a permanent delete on a soft-deleted device.
- The device type doesn't support soft delete.

Once a device is hard deleted, all associated data, including BitLocker recovery keys and LAPS passwords, is permanently lost and can't be recovered. The device object must be fully recreated.

Caution

Hard-deleted devices and their associated data can't be recovered. Verify that you no longer need a device's BitLocker recovery keys or other data before permanently deleting it.

## Microsoft Entra Connect and soft delete

In hybrid environments where Microsoft Entra Connect syncs devices between on-premises Active Directory and Microsoft Entra ID, soft delete interacts with sync operations. If a device is accidentally removed from the sync scope (for example, by moving a computer object out of a synced organizational unit), Microsoft Entra Connect can detect the soft-deleted object during the next sync cycle and restore it instead of creating a duplicate.

This auto-restore behavior helps prevent credential loss from accidental mass deletions caused by sync scope changes. When Microsoft Entra Connect attempts to recreate a device that was soft deleted (matching on the same DeviceId), the system recognizes the soft-deleted object and restores it.

## Limitations

- During the preview, there's no portal experience for viewing or restoring soft-deleted devices. Restoration requires PowerShell or Microsoft Graph API.
- Custom RBAC roles for device soft-delete or restore operations aren't supported.
- DeviceId uniqueness is enforced across both active and soft-deleted containers. A new device can't register with the same DeviceId as a soft-deleted device until that device is restored or permanently deleted.
- Older Azure AD Graph APIs that don't recognize soft delete might hard delete a device instead of soft deleting it.
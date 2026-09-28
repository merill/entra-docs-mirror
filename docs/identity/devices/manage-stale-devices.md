---
layout: Conceptual
title: How to manage stale devices in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/manage-stale-devices
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Learn how to remove stale devices from your database of registered devices in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-06-27T00:00:00.0000000Z
ms.reviewer: 
locale: en-us
document_id: ad8e93b0-2d8b-68c0-62ee-be44831b1557
document_version_independent_id: b55939f9-e552-9818-80b7-535601d4bc7b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/manage-stale-devices.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/manage-stale-devices
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/manage-stale-devices.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 8bfb7f55-9d5c-35a6-bd2c-6b25ec457af9
---

# How to manage stale devices in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Ideally, to complete the lifecycle, registered devices should be unregistered when they aren't needed anymore. Because of lost, stolen, broken devices, or OS reinstallations you typically have some stale devices in your environment. As an IT admin, you probably want a method to remove stale devices, so that you can focus your resources on managing devices that actually require management.

In this article, you learn how to efficiently manage stale devices in your environment.

## What is a stale device?

A stale device is a device registered with Microsoft Entra ID that hasn't accessed any cloud apps for a specific timeframe. Stale devices have an impact on your ability to manage and support your devices and users in the tenant because:

- Duplicate devices can make it difficult for your helpdesk staff to identify which device is currently active.
- An increased number of devices creates unnecessary device writebacks increasing the time for Microsoft Entra Connect syncs.
- As a general hygiene and to meet compliance, you might want to have a clean slate of devices.

Stale devices in Microsoft Entra ID can interfere with the general lifecycle policies for devices in your organization.

## Detect stale devices

Because a stale device is defined as a registered device that hasn't been used to access any cloud apps for a specific timeframe, detecting stale devices requires a timestamp-related property. In Microsoft Entra ID, this property is called **ApproximateLastSignInDateTime** or **activity timestamp**. If the delta between now and the value of the **activity timestamp** exceeds the timeframe you've defined for active devices, a device is considered to be stale.

## How is the value of the activity timestamp managed?

The evaluation of the activity timestamp is triggered by an authentication attempt of a device. Microsoft Entra ID evaluates the activity timestamp when:

- A Conditional Access policies requiring [managed devices](../conditional-access/concept-conditional-access-grant) or [approved client apps](../conditional-access/policy-all-users-device-compliance) has been triggered.
- Windows 10 or newer devices that are either Microsoft Entra joined or Microsoft Entra hybrid joined are active on the network.
- Intune managed devices have checked in to the service.

If the delta between the existing value of the activity timestamp and the current value is more than 14 days (+/-5 day variance), the existing value is replaced with the new value.

## How do I get the activity timestamp?

You have two options to retrieve the value of the activity timestamp:

- The **Activity** column on the all devices page.

    ![Screenshot listing the name, owner, and other information of devices. One column lists the activity time stamp.](media/manage-stale-devices/01.png)
- The [Get-MgDevice](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/get-mgdevice) cmdlet.

    ![Screenshot showing command-line output. One line is highlighted and lists a time stamp for the ApproximateLastSignInDateTime value.](media/manage-stale-devices/02.png)

## Plan the cleanup of your stale devices

To efficiently cleanup stale devices in your environment, you should define a related policy. This policy helps you to ensure that you capture all considerations that are related to stale devices. The following sections provide you with examples for common policy considerations.

### Understand device lifecycle context

Before you clean up stale devices, confirm where each device is in its identity lifecycle. A device identity can move through provisioning, registration, trust establishment, management attachment, steady-state use, recovery, retirement, and transition to another join model. Stale Microsoft Entra device objects can appear when a device is rebuilt or recovered, when Microsoft Entra hybrid join trust is broken, or when registration doesn't complete.

Common signs include:

- Duplicate device objects after an OS reinstall, reimage, or recovery.
- Device objects in the **Pending** state that require re-registration.
- Devices with no recent Microsoft Entra activity that still exist in on-premises AD or device management tools.

Caution

If your organization uses BitLocker drive encryption, you should ensure that BitLocker recovery keys are either backed up or no longer needed before deleting devices. Failure to do this may cause loss of data.

If you use features like [Autopilot](/en-us/autopilot/registration-overview#deregister-from-autopilot-using-intune) or [Universal Print](/en-us/universal-print/reference/portal/register-unregister-printers), those devices should be cleaned up in their respective admin portals.

### Cleanup account

To update a device in Microsoft Entra ID, you need an account that has one of the following roles assigned:

- [Cloud Device Administrator](../role-based-access-control/permissions-reference#cloud-device-administrator)
- [Intune Administrator](../role-based-access-control/permissions-reference#intune-administrator)

In your cleanup policy, select accounts that have the required roles assigned.

### Timeframe

Define a timeframe that is your indicator for a stale device. When defining your timeframe, factor the window noted for updating the activity timestamp into your value. For example, you shouldn't consider a timestamp that is younger than 21 days (includes variance) as an indicator for a stale device. There are scenarios that can make a device look like stale while it isn't. For example, the owner of the affected device can be on vacation or on a sick leave that exceeds your timeframe for stale devices.

### Disable devices

It isn't advisable to immediately delete a device that appears to be stale because you can't undo a deletion if there's a false positive. As a best practice, disable a device for a grace period before deleting it. In your policy, define a timeframe to disable a device before deleting it.

### MDM-controlled devices

If your device is under control of Intune or any other Mobile Device Management (MDM) solution, retire the device in the management system before disabling or deleting it. For more information, see the article [Remove devices by using wipe, retire, or manually unenrolling the device](/en-us/mem/intune/remote-actions/devices-wipe).

### System-managed devices

Don't delete system-managed devices. These devices are generally devices such as Autopilot. Once deleted, these devices can't be reprovisioned.

### Microsoft Entra hybrid joined devices

Your Microsoft Entra hybrid joined devices should follow your policies for on-premises stale device management.

To clean up Microsoft Entra ID:

- **Windows 10 or newer devices** - Disable or delete Windows 10 or newer devices in your on-premises AD, and let Microsoft Entra Connect synchronize the changed device status to Microsoft Entra ID.
- **Windows 7/8** - Disable or delete Windows 7/8 devices in your on-premises AD first. You can't use Microsoft Entra Connect to disable or delete Windows 7/8 devices in Microsoft Entra ID. Instead, when you make the change in your on-premises, you must disable/delete in Microsoft Entra ID.

Note

- Deleting devices in your on-premises Active Directory or Microsoft Entra ID does not remove registration on the client. It will only prevent access to resources using device as an identity (such as Conditional Access). Read additional information on how to [remove registration on the client](faq).
- Deleting a Windows 10 or newer device only in Microsoft Entra ID will re-synchronize the device from your on-premises using Microsoft Entra Connect but as a new object in "Pending" state. A re-registration is required on the device.
- Removing the device from sync scope for Windows 10 or newer /Server 2016 devices will delete the Microsoft Entra device. Adding it back to sync scope will place a new object in "Pending" state. A re-registration of the device is required.
- If you are not using Microsoft Entra Connect for Windows 10 or newer devices to synchronize (such as ONLY using AD FS for registration), you must manage lifecycle similar to Windows 7/8 devices.

### Microsoft Entra joined devices

Disable or delete Microsoft Entra joined devices in the Microsoft Entra ID.

Note

- Deleting a Microsoft Entra device does not remove registration on the client. It will only prevent access to resources using device as an identity (such as Conditional Access).
- Read more on [how to unjoin on Microsoft Entra ID](faq)

### Microsoft Entra registered devices

Disable or delete Microsoft Entra registered devices in the Microsoft Entra ID.

Note

- Deleting a Microsoft Entra registered device in Microsoft Entra ID does not remove registration on the client. It will only prevent access to resources using device as an identity (such as Conditional Access).
- Read more on [how to remove a registration on the client](faq)

## Clean up stale devices

While you can clean up stale devices in the Microsoft Entra admin center, it's more efficient to handle this process using a PowerShell script. Use the latest PowerShell V2 module to use the timestamp filter and to filter out system-managed devices such as Autopilot.

A typical routine consists of the following steps:

1. Connect to Microsoft Entra ID using the [Connect-MgGraph](/en-us/powershell/microsoftgraph/authentication-commands) cmdlet
2. Get the list of devices.
3. Disable the device using the [Update-MgDevice](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/update-mgdevice) cmdlet (disable by using -AccountEnabled option).
4. Wait for the grace period of however many days you choose before deleting the device.
5. Remove the device using the [Remove-MgDevice](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/remove-mgdevice) cmdlet.

### Get the list of devices

To get all devices and store the returned data in a CSV file:

```PowerShell
Get-MgDevice -All | select-object -Property AccountEnabled, DeviceId, OperatingSystem, OperatingSystemVersion, DisplayName, TrustType, ApproximateLastSignInDateTime | export-csv devicelist-summary.csv -NoTypeInformation
```

If you have a large number of devices in your directory, use the timestamp filter to narrow down the number of returned devices. To get all devices that haven't logged on in 90 days and store the returned data in a CSV file:

```PowerShell
$dt = (Get-Date).AddDays(-90)
Get-MgDevice -All | Where {$_.ApproximateLastSignInDateTime -le $dt} | select-object -Property AccountEnabled, DeviceId, OperatingSystem, OperatingSystemVersion, DisplayName, TrustType, ApproximateLastSignInDateTime | export-csv devicelist-olderthan-90days-summary.csv -NoTypeInformation
```

Warning

Some active devices may have a blank time stamp.

#### Set devices to disabled

Using the same commands we can pipe the output to the set command to disable the devices over a certain age.

```powershell
$dt = (Get-Date).AddDays(-90)
$params = @{accountEnabled = $false
}

$Devices = Get-MgDevice -All | Where {$_.ApproximateLastSignInDateTime -le $dt}
foreach ($Device in $Devices) { 
   Update-MgDevice -DeviceId $Device.Id -BodyParameter $params 
}
```

### Delete devices

Caution

The `Remove-MgDevice` cmdlet does not provide a warning. Running this command will delete devices without prompting. **There is no way to recover deleted devices**.

Before administrators delete any devices, back up any BitLocker recovery keys you might need in the future. There's no way to recover BitLocker recovery keys after deleting the associated device.

Building on the disable devices example we look for disabled devices, now inactive for 120 days, and pipe the output to `Remove-MgDevice` to delete those devices.

```powershell
$dt = (Get-Date).AddDays(-120)
$Devices = Get-MgDevice -All | Where {($_.ApproximateLastSignInDateTime -le $dt) -and ($_.AccountEnabled -eq $false)}
foreach ($Device in $Devices) {
   Remove-MgDevice -DeviceId $Device.Id
}
```

## What you should know

### Why is the timestamp not updated more frequently?

The timestamp is updated to support device lifecycle scenarios. This attribute isn't an audit. Use the sign-in audit logs for more frequent updates on the device. Some active devices might have a blank time stamp.

### Why should I worry about my BitLocker keys?

When configured, BitLocker keys for Windows 10 or newer devices are stored on the device object in Microsoft Entra ID. If you delete a stale device, you also delete the BitLocker keys that are stored on the device. Confirm that your cleanup policy aligns with the actual lifecycle of your device before deleting a stale device.

### Why should I worry about Windows Autopilot devices?

When you delete a Microsoft Entra device that was associated with a Windows Autopilot object the following three scenarios can occur if the device will be repurposed in future:

- With Windows Autopilot user-driven deployments without using pre-provisioning, a new Microsoft Entra device is created, but isn’t be tagged with the ZTDID.
- With Windows Autopilot self-deploying mode deployments, they'll fail because an associate Microsoft Entra device can’t be found. (This failure is a security mechanism to make sure that no "impostor" devices try to join Microsoft Entra ID with no credentials.) The failure indicates a ZTDID mismatch.
- With Windows Autopilot pre-provisioning deployments, they fail because an associated Microsoft Entra device can’t be found. (Behind the scenes, pre-provisioning deployments use the same self-deploying mode process, so they enforce the same security mechanisms.)

Use the [Get-MgDeviceManagementWindowsAutopilotDeviceIdentity](/en-us/powershell/module/microsoft.graph.devicemanagement.enrollment/get-mgdevicemanagementwindowsautopilotdeviceidentity) to list of Windows Autopilot devices in your organization and compare it to the list of devices to clean up.

### How do I know all the type of devices joined?

To learn more about the different types, see the [device management overview](overview).

### What happens when I disable a device?

Any authentication where a device is being used to authenticate to Microsoft Entra ID are denied. Common examples are:

- **Microsoft Entra hybrid joined device** - Users might be able to use the device to sign-in to their on-premises domain. However, they can't access Microsoft Entra resources such as Microsoft 365.
- **Microsoft Entra joined device** - Users can't use the device to sign in.
- **Mobile devices** - User can't access Microsoft Entra resources such as Microsoft 365.
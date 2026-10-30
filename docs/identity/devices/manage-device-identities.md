---
layout: Conceptual
title: Manage devices in Microsoft Entra ID using the Microsoft Entra admin center - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/manage-device-identities
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: This article describes how to use the Microsoft Entra admin center to manage device identities and monitor related event information.
ms.topic: how-to
ms.date: 2026-06-17T00:00:00.0000000Z
ms.reviewer: myra-ramdenbourg
ms.custom: sfi-image-nochange
locale: en-us
document_id: a8119688-e88d-2916-3dcf-bf777a5fc80c
document_version_independent_id: e767d695-1c9f-64e4-e6c4-fef07b0f3d2e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/manage-device-identities.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/manage-device-identities
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/manage-device-identities.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 295390ca-aab1-5f76-adce-5faa90dc55b0
---

# Manage devices in Microsoft Entra ID using the Microsoft Entra admin center - Microsoft Entra ID | Microsoft Learn

Microsoft Entra ID provides a central place to manage device identities and monitor related event information.

[![Screenshot that shows the devices overview.](media/manage-device-identities/devices-azure-portal.png)](media/manage-device-identities/devices-azure-portal.png#lightbox)

You can access the devices overview by completing these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a user with at least [default user permissions](../../fundamentals/users-default-permissions).
2. Go to **Entra ID** &gt; **Devices** &gt; **Overview**.

In the devices overview, you can view the number of total devices, stale devices, noncompliant devices, and unmanaged devices. It provides links to Intune, Conditional Access, BitLocker keys, and basic monitoring. Other features like Conditional Access and Microsoft Intune require additional role assignments

Device counts on the overview page don't update in real time. Changes should be reflected every few hours.

From there, you can go to **All devices** to:

- Identify devices, including:
    - Devices joined or registered in Microsoft Entra ID.
    - Devices deployed via [Windows Autopilot](/en-us/autopilot/windows-autopilot).
    - Printers that use [Universal Print](/en-us/universal-print/fundamentals/universal-print-getting-started).
- Complete device identity management tasks like enable, disable, delete, and manage.
    - The management options for [Printers](/en-us/universal-print/fundamentals/) and [Windows Autopilot](/en-us/autopilot/windows-autopilot) are limited in Microsoft Entra ID. These devices must be managed from their respective admin interfaces.
- Configure your device identity settings.
- Enable or disable enterprise state roaming.
- Review device-related audit logs.
- Download devices.

[![Screenshot that shows the All devices view.](media/manage-device-identities/all-devices-azure-portal.png)](media/manage-device-identities/all-devices-azure-portal.png#lightbox)

Tip

- Microsoft Entra hybrid joined Windows 10 or newer devices don't have an owner unless the primary user is set in Microsoft Intune. If you're looking for a device by owner and don't find it, search by the device ID.
- If you see a device that's **Microsoft Entra hybrid joined** with a state of **Pending** in the **Registered** column, the device has been synchronized from Microsoft Entra Connect and is waiting to complete registration from the client. See [How to plan your Microsoft Entra hybrid join implementation](hybrid-join-plan). For more information, see [Device management frequently asked questions](faq).
- For some iOS devices, device names that contain apostrophes can use different characters that look like apostrophes. So searching for such devices is a little tricky. If you don't see correct search results, be sure the search string contains the matching apostrophe character.

## Manage an Intune device

If you have rights to manage devices in Intune, you can manage devices for which mobile device management is listed as **Microsoft Intune**. If the device isn't enrolled with Microsoft Intune, the **Manage** option isn't available.

## Enable or disable a Microsoft Entra device

There are two ways to enable or disable devices:

- The toolbar on the **All devices** page, after you select one or more devices.
- The toolbar, after you drill down for a specific device.

Important

- You must be an Intune Administrator or Cloud Device Administrator to enable or disable a device.
- Disabling a device prevents it from authenticating via Microsoft Entra ID. This prevents it from accessing your Microsoft Entra resources that are protected by device-based Conditional Access and from using Windows Hello for Business credentials.
- Disabling a device revokes the Primary Refresh Token (PRT) and any refresh tokens on the device.
- Printers can't be enabled or disabled in Microsoft Entra ID.

## Delete a Microsoft Entra device

There are two ways to delete a device:

- The toolbar on the **All devices** page, after you select one or more devices.
- The toolbar, after you drill down for a specific device.

Important

- You must be a Cloud Device Administrator, Intune Administrator or Windows 365 Administrator to delete a device.
- Printers can't be deleted before they're deleted from Universal Print.
- Windows Autopilot devices can't be deleted before they're deleted from Intune.
- Deleting a device:
    - Prevents it from accessing your Microsoft Entra resources.
    - Removes all details attached to the device. For example, BitLocker keys for Windows devices.
    - Is a nonrecoverable activity. We don't recommend it unless it's required.

If a device is managed in another management authority, like Microsoft Intune, be sure it's wiped or retired before you delete it. See [How to manage stale devices](manage-stale-devices) before you delete a device.

## View or copy a device ID

You can use a device ID to verify the device ID details on the device or to troubleshoot via PowerShell. To access the copy option, select the device.

![Screenshot that shows a device ID and the copy button.](media/manage-device-identities/device-details.png)

## View or copy BitLocker keys

You can view and copy BitLocker keys to allow users to recover encrypted drives. These keys are available only for Windows devices that are encrypted and store their keys in Microsoft Entra ID. You can find these keys when you view a device's details by selecting **Show Recovery Key**. Selecting **Show Recovery Key** generates an audit log entry, which you can find in the `KeyManagement` category.

![Screenshot that shows how to view BitLocker keys.](media/manage-device-identities/show-bitlocker-key.png)

To view or copy BitLocker keys, you need to be the owner of the device or have one of these roles:

- [Cloud Device Administrator](../role-based-access-control/permissions-reference#cloud-device-administrator)
- [Helpdesk Administrator](../role-based-access-control/permissions-reference#helpdesk-administrator)
- [Intune Administrator](../role-based-access-control/permissions-reference#intune-administrator)
- [Security Administrator](../role-based-access-control/permissions-reference#security-administrator)
- [Security Reader](../role-based-access-control/permissions-reference#security-reader)

Note

When devices that utilize [Windows Autopilot](/en-us/mem/autopilot/windows-autopilot) are reused, **and there is a new device owner**, that new device owner must contact an administrator to acquire the BitLocker recovery key for that device. Custom role or administrative unit scoped administrators will continue to have access to BitLocker recovery keys for those devices that have undergone device ownership changes, unless the new device owner belongs to a custom role or administrative unit scope. In such an instance, the user will need to contact other scoped administrator for the recovery keys. For more information, see the article [Find the primary user of an Intune device](/en-us/mem/intune/remote-actions/find-primary-user#change-a-devices-primary-user).

## View and filter your devices

You can filter the device list by these attributes:

- Enabled state
- Compliant state
- Join type (Microsoft Entra joined, Microsoft Entra hybrid joined, Microsoft Entra registered)
- Activity timestamp
- OS type and OS version
    - Windows is displayed for Windows 11 and Windows 10 devices (with KB5006738).
    - Windows Server is displayed for [supported versions managed with Microsoft Defender for Endpoint](/en-us/mem/intune/protect/mde-security-integration#supported-platforms).
- Device type (printer, secure VM, shared device, registered device)
- MDM
- Autopilot
- Extension attributes
- Administrative unit
- Owner

## Download devices

Any user can use the **Download devices** option to export a CSV file that lists devices. You can apply filters to determine which devices to list. If you don't apply any filters, all devices are listed. The exported list includes these device identity attributes:

`id,deviceId,isManaged,profileType,systemLabels,model,displayName,accountEnabled,operatingSystem,operatingSystemVersion,trustType(joinType),mdm,securitySettingsManagement,isCompliant,registrationDateTime,approximateLastSignInDateTime,owner,upnName`

Note

trustType is where JoinType can be determined. A common translation is:

- AzureAD -&gt; Microsoft Entra joined
- Workplace -&gt; Microsoft Entra registered
- ServerAD -&gt; Microsoft Entra hybrid joined

The following filters can be applied for the export task:

- Enabled state
- Compliant state
- Join type
- Activity timestamp
- OS type
- Device type

Additionally, columns can be managed by selecting **Manage view &gt; Columns** to toggle which columns you would like to export.

Note

Selecting **Owner** or **User principal name** can make processing take longer. If you prefer faster results, leave these options unchecked; enable them when you need the extra information.

## Configure device settings

If you want to manage device identities by using the Microsoft Entra admin center, the devices need to be either [registered or joined](overview) to Microsoft Entra ID. As an administrator, you can control the process of registering and joining devices by configuring the following device settings.

You must be assigned one of the following roles to read or modify device settings:

- [Cloud Device Administrator](../role-based-access-control/permissions-reference#cloud-device-administrator) (read and modify)
- [Intune Administrator](../role-based-access-control/permissions-reference#intune-administrator) (read only)
- [Windows 365 Administrator](../role-based-access-control/permissions-reference#windows-365-administrator) (read only)

Tip

If users observe errors when attempting registering or joining devices, ensure the settings for **[register](/en-us/editor/MicrosoftDocs/entra-docs-pr/docs%2Fidentity%2Fdevices%2Fmanage-device-identities.md/main/295390ca-aab1-5f76-adce-5faa90dc55b0/concept-device-registration.md)** or **[join](/en-us/editor/MicrosoftDocs/entra-docs-pr/docs%2Fidentity%2Fdevices%2Fmanage-device-identities.md/main/295390ca-aab1-5f76-adce-5faa90dc55b0/concept-directory-join.md)** are configured appropriately for their supported OS platforms. Different operating systems support register or join respectively.

![Screenshot that shows device settings related to Microsoft Entra ID.](media/manage-device-identities/device-settings-azure-portal.png)

- **Users may join devices to Microsoft Entra ID**: This setting enables you to select the users who can register their devices as Microsoft Entra joined devices. The default is **All**.

    Note

    The **Users may join devices to Microsoft Entra ID** setting is applicable only to Microsoft Entra join on Windows 10 or newer, macOS, or Linux. This setting doesn't apply to Microsoft Entra hybrid joined devices, [Microsoft Entra joined VMs in Azure](howto-vm-sign-in-azure-ad-windows#enable-microsoft-entra-sign-in-for-a-windows-virtual-machine-in-azure), or Microsoft Entra joined devices that use [Windows Autopilot self-deployment mode](/en-us/autopilot/self-deploying) because these methods work in a userless context.
- **Users may register their devices with Microsoft Entra ID**: You need to configure this setting to allow users to register Windows 10 or newer personal, iOS, Android, and macOS devices with Microsoft Entra ID. If you select **None**, devices aren't allowed to register with Microsoft Entra ID. Enrollment with Microsoft Intune or mobile device management for Microsoft 365 requires registration. If you've configured either of these services, **ALL** is selected, and **NONE** is unavailable.
- **Require multifactor authentication to register or join devices with Microsoft Entra ID**:

    - We recommend organizations use the [Register or join devices user action](../conditional-access/concept-conditional-access-cloud-apps#user-actions) in Conditional Access to enforce multifactor authentication. You must configure this toggle to **No** if you use a [Conditional Access policy to require multifactor authentication](../conditional-access/policy-all-users-device-registration).
    - This setting allows you to specify whether users are required to provide another authentication factor to join or register their devices to Microsoft Entra ID. The default is **No**. We recommend that you require multifactor authentication when a device is registered or joined. Before you enable multifactor authentication for this service, you must ensure that multifactor authentication is configured for users that register their devices. For more information on Microsoft Entra multifactor authentication services, see [getting started with Microsoft Entra multifactor authentication](../authentication/concept-mfa-howitworks). This setting might not work with third-party identity providers.

    Note

    The **Require multifactor authentication to register or join devices with Microsoft Entra ID** setting applies to devices that are either Microsoft Entra joined (with some exceptions) or Microsoft Entra registered. This setting doesn't apply to Microsoft Entra hybrid joined devices, [Microsoft Entra joined VMs in Azure](howto-vm-sign-in-azure-ad-windows#enable-microsoft-entra-sign-in-for-a-windows-virtual-machine-in-azure), or Microsoft Entra joined devices that use [Windows Autopilot self-deployment mode](/en-us/autopilot/self-deploying).
- **Maximum number of devices**: This setting enables you to select the maximum number of Microsoft Entra joined or Microsoft Entra registered devices that a user can have in Microsoft Entra ID. If users reach this limit, they can't add more devices until one or more of the existing devices are removed. The default value is **50**. You can increase the value up to 100. If you enter a value above 100, Microsoft Entra ID sets it to 100. You can also use **Unlimited** to enforce no limit other than existing quota limits.

    Note

    The **Maximum number of devices** setting applies to devices that are either Microsoft Entra joined or Microsoft Entra registered. This setting doesn't apply to Microsoft Entra hybrid joined devices.
- **Manage Additional local administrators on Microsoft Entra joined devices**: This setting lets you select users who are granted local administrator rights on all Microsoft Entra joined devices in the tenant. These users are assigned to the Microsoft Entra Joined Device Local Administrator role, which applies tenant-wide.
- **Registering user is added as local administrator on the device during Microsoft Entra join**: This setting controls whether users who perform Microsoft Entra join are added to the local Administrators group on the device they join. This setting affects local device administrator membership only. It doesn't assign a Microsoft Entra directory role, such as Global Administrator, and it doesn't add the user to the Microsoft Entra Joined Device Local Administrator role. To verify the result, check the local Administrators group on the device or use a device management tool. In Microsoft Graph, this setting is represented by the `azureADJoin.localAdmins.registeringUsers` property of the [device registration policy](/en-us/graph/api/resources/deviceregistrationpolicy).
- **Enable Microsoft Entra Local Administrator Password Solution (LAPS) (preview)**: LAPS is the management of local account passwords on Windows devices. LAPS provides a solution to securely manage and retrieve the built-in local admin password. With cloud version of LAPS, customers can enable storing and rotation of local admin passwords for both Microsoft Entra ID and Microsoft Entra hybrid join devices. To learn how to manage LAPS in Microsoft Entra ID, see [the overview article](howto-manage-local-admin-passwords).
- **Restrict non-admin users from recovering the BitLocker key(s) for their owned devices**: Admins can block self-service BitLocker key access to the registered owner of the device. Default users without the BitLocker read permission are unable to view or copy their BitLocker key(s) for their owned devices. You must be at least a [Privileged Role Administrator](../role-based-access-control/permissions-reference#privileged-role-administrator) to update this setting.
- **Enterprise State Roaming**: For information about this setting, see [the overview article](enterprise-state-roaming-enable).

## Audit logs

Device activities are visible in the activity logs. These logs include activities triggered by the device registration service and by users:

- Device creation and adding owners/users on the device
- Changes to device settings
- Device operations like deleting or updating a device
- Bulk operations like downloading all devices

Note

When performing bulk operations, such as import or create, you can encounter a problem if the bulk operation doesn't complete within the hour. To work around this issue, we recommend splitting the number of records processed per batch. For example, before starting an export you could limit the result set by filtering on a group type or user name to reduce the size of the results. By refining your filters, essentially you limit the data returned by the bulk operation. For more information, see [Bulk operations service limitations](../../fundamentals/bulk-operations-service-limitations).

The entry point to the auditing data is **Audit logs** in the **Activity** section of the **Devices** page.

The audit log has a default list view that shows:

- The date and time of the occurrence.
- The targets.
- The initiator/actor of an activity.
- The activity.

![Screenshot that shows a table in the Activity section of the Devices page. The table shows the date, target, actor, and activity for four audit logs.](media/manage-device-identities/63.png)

You can customize the list view by selecting **Columns** in the toolbar:

![Screenshot that shows the toolbar of the Devices page.](media/manage-device-identities/64.png)

To reduce the reported data to a level that works for you, you can filter it by using these fields:

- **Category**
- **Activity Resource Type**
- **Activity**
- **Date Range**
- **Target**
- **Initiated By (Actor)**

You can also search for specific entries.

![Screenshot that shows audit data filtering controls.](media/manage-device-identities/65.png)
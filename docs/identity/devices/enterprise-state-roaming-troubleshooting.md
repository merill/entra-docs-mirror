---
layout: Conceptual
title: Troubleshoot Enterprise State Roaming in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/enterprise-state-roaming-troubleshooting
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Provides answers to some questions IT administrators might have about settings and app data sync.
ms.topic: troubleshooting
ms.date: 2025-06-27T00:00:00.0000000Z
ms.reviewer: sempofu, micrider
locale: en-us
document_id: af15f989-31c5-1730-869d-66531023658b
document_version_independent_id: 72248318-2edd-8b80-5d42-45f35daba812
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/enterprise-state-roaming-troubleshooting.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/enterprise-state-roaming-troubleshooting
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/enterprise-state-roaming-troubleshooting.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
platformId: 13eb1bf6-2be3-27bb-0656-911d48d5284a
---

# Troubleshoot Enterprise State Roaming in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article provides information on how to troubleshoot and diagnose issues with Enterprise State Roaming, and provides a list of known issues.

Note

We recommend that you use the Azure Az PowerShell module to interact with Azure. See [Install Azure PowerShell](/en-us/powershell/azure/install-azure-powershell) to get started. To learn how to migrate to the Az PowerShell module, see [Migrate Azure PowerShell from AzureRM to Az](/en-us/powershell/azure/migrate-from-azurerm-to-az).

Note

The article does not apply to the new Microsoft Edge Chromium-based browser released on January 15, 2020. For more information on the Sync behavior for the new Microsoft Edge, see the article [Microsoft Edge Sync](/en-us/deployedge/microsoft-edge-enterprise-sync).

## Preliminary steps for troubleshooting

Before you start troubleshooting, verify that the user and device are configured properly, and that all the requirements of Enterprise State Roaming are met.

1. Windows 10 or newer, with the latest updates, and a minimum Version 22H2 (OS Build 19045 or later) is installed on the device.
2. The device is Microsoft Entra joined or Microsoft Entra hybrid joined. For more information, see [how to get a device under the control of Microsoft Entra ID](overview).
3. Ensure that **Enterprise State Roaming** is enabled for the tenant in Microsoft Entra ID as described in [To enable Enterprise State Roaming](enterprise-state-roaming-enable). You can enable roaming for all users or for only a selected group of users.
4. The user is assigned a Microsoft Entra ID P1 or P2 license.
5. The device must be restarted and the user must sign in again to access Enterprise State Roaming features.

## Troubleshooting and diagnosing issues

This section gives suggestions on how to troubleshoot and diagnose problems related to Enterprise State Roaming.

## Verify sync, and the "Sync your settings" settings page

1. After joining your Windows 10 or newer PC to a domain that is configured to allow Enterprise State Roaming, sign on with your work account. Go to **Settings** &gt; **Accounts** &gt; **Sync Your Settings** and confirm that sync and the individual settings are on, and that the top of the settings page indicates that you're syncing with your work account. Confirm the same account is also used as your account in **Settings** &gt; **Accounts** &gt; **Your Info**.
2. Verify that sync works across multiple machines by making some changes on the original machine, such as changing the "Country or Region" or using other supported settings see [Enterprise State Roaming settings catalog](/en-us/windows/configuration/windows-backup/catalog-esr). Watch the change propagate to the second machine within five minutes.

    - Locking and unlocking the screen (Win + L) can help trigger a sync.
    - You must be signing in with the same account on both PCs for sync to work – as Enterprise State Roaming is tied to the user account and not the machine account.

**Potential issue**: If the controls in the **Settings** page aren't available, and you see the message "Some Windows features are only available if you're using a Microsoft account or work account." This issue might arise for devices that are set up to be domain-joined and registered to Microsoft Entra ID, but the device hasn't authenticated to Microsoft Entra ID yet. A possible cause is that the device policy must be applied, but this application happens asynchronously, and might take a few hours.

### Verify the device registration status

Enterprise State Roaming requires the device to be registered with Microsoft Entra ID. Although not specific to Enterprise State Roaming, using the following instructions can help confirm that the Windows 10 or newer Client is registered, and confirm thumbprint, Microsoft Entra settings URL, NGC status, and other information.

1. Open the command prompt unelevated. To do this in Windows, open the Run launcher (Win + R) and type "cmd" to open.
2. Once the command prompt is open, type `*dsregcmd.exe /status*`.
3. For expected output, the **AzureAdJoined** field value should be `YES`, **WamDefaultSet** field value should be `YES`, and the **WamDefaultGUID** field value should be a GUID with `(AzureAD)` at the end.

**Potential issue**: **WamDefaultSet** and **AzureAdJoined** both have "NO" in the field value, the device was domain-joined and registered with Microsoft Entra ID, and the device doesn't sync. If it's showing this, the device might need to wait for policy to be applied or the authentication for the device failed when connecting to Microsoft Entra ID. The user might have to wait a few hours for the policy to be applied. Other troubleshooting steps might include retrying autoregistration by signing out and back in, or launching the task in Task Scheduler. In some cases, running "*dsregcmd.exe /leave*" in an elevated command prompt window, rebooting, and trying registration again might help with this issue.

**Potential issue**: The field for **SettingsUrl** is empty and the device doesn't sync. The user might have last logged in to the device before Enterprise State Roaming was enabled. Restart the device and have the user sign-in. Optionally, in the portal, try having the IT Admin navigate to **Entra ID** &gt; **Devices** &gt; **Overview** &gt; **Enterprise State Roaming** disable and re-enable **Users may sync settings and app data across devices**. To disable click on "None" and to re-enable click on "All" or "Selected". Once re-enabled, restart the device and have the user sign-in. If this doesn't resolve the issue, **SettingsUrl** might be empty if there's a bad device certificate. In this case, running "*dsregcmd.exe /leave*" in an elevated command prompt window, rebooting, and trying registration again might help with this issue.

## Enterprise State Roaming and multifactor authentication

Under certain conditions, Enterprise State Roaming can fail to sync data if Microsoft Entra multifactor authentication is configured. For more information on these symptoms, see the support document [KB3193683](https://support.microsoft.com/kb/3193683).

**Potential issue**: If your device is configured to require multifactor authentication on the Microsoft Entra admin center, you might fail to sync settings while signing in to a Windows 10 or newer device using a password. This type of multifactor authentication configuration is intended to protect an Azure administrator account. Admin users might still be able to sync by signing in to their Windows 10 or newer devices with their Windows Hello for Business PIN or by completing multifactor authentication while accessing other Azure services like Microsoft 365.

**Potential issue**: Sync can fail if the admin configures the Active Directory Federation Services multifactor authentication Conditional Access policy and the access token on the device expires. Ensure that you sign in and sign out using the Windows Hello for Business PIN or complete multifactor authentication while accessing other Azure services like Microsoft 365.

### Event Viewer

For advanced troubleshooting, Event Viewer can be used to find specific errors. The events can be found under Event Viewer &gt; **Applications and Services Logs** &gt; **Microsoft** &gt; **Windows** &gt; **CloudStore** and for identity-related issues with sync **Applications and Services Logs** &gt; **Microsoft** &gt; **Windows** &gt; **AAD**.
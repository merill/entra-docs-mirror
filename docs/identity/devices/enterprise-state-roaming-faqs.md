---
layout: FAQ
title: Enterprise State Roaming FAQ - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/enterprise-state-roaming-faqs
summary: >
  <p>This article answers some questions IT administrators might have about settings and app data sync.</p>
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Frequently asked questions about ESR
ms.topic: faq
ms.date: 2025-06-27T00:00:00.0000000Z
ms.reviewer: sempofu, micrider
locale: en-us
document_id: 448e1185-6acc-5928-9932-a360230319bd
document_version_independent_id: 1d907bdc-b1ad-fb3d-8d75-93e1da810148
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/enterprise-state-roaming-faqs.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/enterprise-state-roaming-faqs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/enterprise-state-roaming-faqs.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/e0ffb20c-01c6-407b-a9bd-29111652a1dc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/3904bce4-d817-48cf-85fd-b6146fca83b7
platformId: 44f9c34a-4e97-bd7f-59bb-350bfb9a5de4
---

# Enterprise State Roaming FAQ - Microsoft Entra ID | Microsoft Learn

This article answers some questions IT administrators might have about settings and app data sync.

## What account is used for settings sync?

In Windows 8.1, settings sync always used consumer Microsoft accounts. Enterprise users had the ability to connect a Microsoft account to their Active Directory domain account to gain access to settings sync. In Windows 10 and newer, this connected Microsoft account functionality is being replaced with a primary/secondary account framework.

The primary account is defined as the account used to sign in to Windows. This can be a Microsoft account, a Microsoft Entra account, an on-premises Active Directory account, or a local account. In addition to the primary account, Windows 10 and newer users can add one or more secondary cloud accounts to their device. A secondary account is generally a Microsoft account, a Microsoft Entra account, or some other account such as Gmail or Facebook. These secondary accounts provide access to other services such as single sign-on and the Windows Store, but they aren't capable of powering settings sync.

Data is never mixed between the different user accounts on the device. There are two rules for settings sync:

- Windows settings always roam with the primary account.
- App data is tagged with the account used to acquire the app. Only apps tagged with the primary account sync. App ownership tagging is determined when an app is side-loaded through the Windows Store or mobile device management (MDM).

If an application owner can't be identified, it will roam with the primary account. If a device is upgraded from Windows 8 or Windows 8.1 to Windows 10 and newer, all the apps are tagged as acquired by the Microsoft account. This is because most users acquire apps through the Windows Store, and there was no Windows Store support for Microsoft Entra accounts prior to Windows 10. If an app is installed via an offline license, the app is tagged using the primary account on the device.

Note

Windows 10 or newer devices that are enterprise-owned and are connected to Microsoft Entra ID can no longer connect their Microsoft accounts to a domain account. The ability to connect a Microsoft account to a domain account and have all the user's data sync to the Microsoft account (that is, the Microsoft account roaming via the connected Microsoft account and Active Directory functionality) is removed from Windows 10 and newer devices that are joined to a connected Active Directory or Microsoft Entra environment.

## How do I upgrade from Microsoft account settings sync in Windows 8 to Microsoft Entra settings sync in Windows 10 or newer?

After upgrading to Windows 10 and newer, you continue to sync user settings via Microsoft account as long as you're a domain-joined user, and the Active Directory domain doesn't connect with Microsoft Entra ID.

If the on-premises Active Directory domain does connect with Microsoft Entra ID, your device attempts to sync settings using the connected Microsoft Entra account. If the Microsoft Entra administrator doesn't enable Enterprise State Roaming, your connected Microsoft Entra account stops syncing settings. If you're running Windows 10 and newer and you sign in with a Microsoft Entra identity, you start syncing windows settings as soon as your administrator enables settings sync via Microsoft Entra ID.

If you stored any personal data on your corporate device, you should know Windows OS and application data begin syncing to Microsoft Entra ID. This has the following implications:

- Your personal Microsoft account settings will drift from the settings on your work or school Microsoft Entra accounts. This is because the Microsoft account and Microsoft Entra settings sync are now using separate accounts.
- Personal data such as Wi-Fi passwords, web credentials, and Internet Explorer favorites that were previously synced via a connected Microsoft account is synced via Microsoft Entra ID.

## How do Microsoft account and Microsoft Entra Enterprise State Roaming interoperability work?

In the November 2015 or later releases of Windows 10, Enterprise State Roaming is only supported for a single account at a time. If you sign in to Windows by using a work or school Microsoft Entra account, all data syncs via Microsoft Entra ID. If you sign in to Windows by using a personal Microsoft account, all data syncs via the Microsoft account. Universal app data roam using only the primary sign-in account on the device, and it roams only if the app's license is owned by the primary account. Universal app data for the apps owned by any secondary accounts isn't synced.

## Do settings sync for Microsoft Entra accounts from multiple tenants?

When multiple Microsoft Entra accounts from different Microsoft Entra tenants are on the same device, you must update the device's registry to communicate with the Azure Rights Management service for each Microsoft Entra tenant.

1. Find the GUID for each Microsoft Entra tenant. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com), browse to **Entra ID** &gt; **Overview** &gt; **Properties** &gt; **Tenant ID**.
2. After you have the GUID, you'll need to add the registry key **HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\SettingSync\WinMSIPC&lt;tenant ID GUID&gt;**. From the **tenant ID GUID** key, create a new Multi-String value (REG-MULTI-SZ) named **AllowedRMSServerUrls**. For its data, specify the licensing distribution point URLs of the other Azure tenants that the device accesses.
3. You can find the licensing distribution point URLs by running the **Get-AadrmConfiguration** cmdlet from the AADRM module. If the values for the **LicensingIntranetDistributionPointUrl** and **LicensingExtranetDistributionPointUrl** are different, specify both values. If the values are the same, specify the value once.

## Can I store synced settings and data on-premises?

Enterprise State Roaming stores all synced data in the Microsoft cloud. UE-V offers an on-premises roaming solution.

## How is the data secured?

Prior to Nov 2022 all user data was secured using [Azure Rights Management](/en-us/azure/information-protection/what-is-information-protection).

Starting in November 2022, Microsoft no longer uses Azure Rights Management for all data encryption. Microsoft is committed to safeguarding customer data. Certain sensitive data such as passwords are encrypted client side with keys derived from the Microsoft Entra tenant to ensure an extra layer of security. All user data (including nonsensitive data) is encrypted in transit and at rest in the cloud. For a list of sensitive and nonsensitive data items roamed, see [Enterprise State Roaming settings catalog](/en-us/windows/configuration/windows-backup/catalog-esr).

## Can I manage sync for a specific app or setting?

In Windows 10 or newer, administrators can disable sync for all settings sync groups on a managed device with MDM or Group Policy.

## How can I enable or disable roaming?

In the **Settings** app, go to **Accounts** &gt; **Sync your settings**. From this page, you can see which account is being used to roam settings, and you can enable or disable individual groups of settings to be roamed.

## What is Microsoft's recommendation for enabling roaming in Windows 10 or newer?

Microsoft has a few different settings roaming solutions available, including UE-V and Enterprise State Roaming. If your organization isn't ready or comfortable with moving data to the cloud, then we recommend that you use UE-V as your primary roaming technology. If your organization requires roaming support for existing Windows desktop applications but is eager to move to the cloud, we recommend that you use both Enterprise State Roaming and UE-V. Although UE-V and Enterprise State Roaming are similar technologies, they aren't mutually exclusive. They complement each other to help ensure that your organization provides the roaming services that your users need.

When using both Enterprise State Roaming and UE-V, Enterprise State Roaming is the primary roaming agent on the device. UE-V is being used to supplement Win32 applications.

- Enterprise State Roaming is the primary roaming agent on the device. UE-V is being used to supplement the "Win32 gap."
- UE-V roaming for Windows settings and modern UWP app data should be disabled when using the UE-V group policies. These settings are already covered by Enterprise State Roaming.

## How does Enterprise State Roaming support virtual desktop infrastructure (VDI)?

Enterprise State Roaming is supported on Windows 10 or newer client SKUs, but not on server SKUs. If a client VM is hosted on a hypervisor machine and you remotely sign in to the virtual machine, your data will roam. If multiple users share the same OS and users remotely sign in to a server for a full desktop experience, roaming might not work. The latter session-based scenario isn't officially supported.

## What happened to the per-user device sync status report?

The per-user device sync status report was removed from the Microsoft Entra admin center. The report was removed because it only provided details for unsupported versions of Windows. Enterprise state roaming requires Windows 11 or Windows 10 version 21H2 or newer.
---
layout: Conceptual
title: Group Policy and MDM settings for ESR - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/enterprise-state-roaming-group-policy-settings
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Management settings for Enterprise State Roaming
ms.topic: reference
ms.date: 2025-06-27T00:00:00.0000000Z
ms.reviewer: sempofu, micrider
locale: en-us
document_id: 7b4c6acf-b61d-b98d-6176-dc9646c699da
document_version_independent_id: b2dd8f2f-3d1b-c460-a3bc-a1d3a832dce2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/enterprise-state-roaming-group-policy-settings.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/enterprise-state-roaming-group-policy-settings
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/enterprise-state-roaming-group-policy-settings.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
- https://authoring-docs-microsoft.poolparty.biz/devrel/e0ffb20c-01c6-407b-a9bd-29111652a1dc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
- https://authoring-docs-microsoft.poolparty.biz/devrel/3904bce4-d817-48cf-85fd-b6146fca83b7
platformId: e16d1b1a-4f64-7bb9-2147-3a12c94c3356
---

# Group Policy and MDM settings for ESR - Microsoft Entra ID | Microsoft Learn

Use these Group Policy and mobile device management (MDM) settings only on corporate-owned devices because these policies are applied to the user’s entire device. Applying an MDM policy to disable settings sync for a personal, user-owned device negatively impacts the use of that device. These policies affect other user accounts on the device.

Enterprises that want to manage roaming for personal (unmanaged) devices can use the Microsoft Entra admin center to enable or disable roaming, rather than using Group Policy or MDM. The following tables describe the policy settings available.

Note

This article applies to the Microsoft Edge Legacy HTML-based browser launched with Windows 10 in July 2015. The article does not apply to the new Microsoft Edge Chromium-based browser released on January 15, 2020. For more information on the Sync behavior for the new Microsoft Edge, see the article [Microsoft Edge Sync](/en-us/deployedge/microsoft-edge-enterprise-sync).

## MDM settings

The MDM policy settings apply to Windows 10 or newer. Refer to [Enterprise State Roaming settings catalog](/en-us/windows/configuration/windows-backup/catalog-esr) for details on what devices are supported for Microsoft Entra ID-based syncing.

| Name | Description |
| --- | --- |
| Allow Microsoft Account Connection | Allows users to authenticate using a Microsoft account on the device |
| Allow Sync My Settings | Allows users to roam Windows settings and app data; Disabling this policy disables sync and backups on mobile devices |

## Group Policy settings

The Group Policy settings apply to Windows 10 or newer devices that are joined to an Active Directory domain. The table also includes legacy settings that would appear to manage sync settings. Legacy settings that don't work for Enterprise State Roaming for Windows 10 or newer are noted with ‘Do not use’ in the description.

These settings are located in Group Policy under: **Computer Configuration** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **Sync your settings**.

| Name | Description |
| --- | --- |
| Accounts: Block Microsoft Accounts | This policy setting prevents users from adding new Microsoft accounts on this computer |
| Do not sync | Prevents users to roam Windows settings and app data |
| Do not sync personalize | Disables syncing of the Themes group |
| Do not sync browser settings | Disables syncing of the Internet Explorer group |
| Do not sync passwords | Disables syncing of Passwords group |
| Do not sync other Windows settings | Disables syncing of Other Windows settings group |
| Do not sync desktop personalization | Do not use; has no effect |
| Do not sync on metered connections | Disables roaming on metered connections, such as cellular 3G |
| Do not sync apps | Do not use; has no effect |
| Do not sync app settings | Disables roaming of app data |
| Do not sync start settings | Do not use; has no effect |
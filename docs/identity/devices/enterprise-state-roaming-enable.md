---
layout: Conceptual
title: Migrate Microsoft Entra Enterprise State Roaming - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/enterprise-state-roaming-enable
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Learn how to migrate Enterprise State Roaming management from Microsoft Entra ID to Windows settings backup and restore policies.
ms.topic: how-to
ms.date: 2026-09-14T00:00:00.0000000Z
ms.reviewer: sempofu, micrider
ms.custom: references_regions, sfi-ga-blocked, msecd-doc-authoring-1028
ai-usage: ai-assisted
locale: en-us
document_id: 8c5cde55-2936-090a-cd04-84312a8c1974
document_version_independent_id: 4700126d-12fe-9956-28d5-b3fbefa7fb45
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/enterprise-state-roaming-enable.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/enterprise-state-roaming-enable
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/enterprise-state-roaming-enable.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: bf46511f-f361-aea6-47af-e61f817f2617
---

# Migrate Microsoft Entra Enterprise State Roaming - Microsoft Entra ID | Microsoft Learn

Enterprise State Roaming (ESR) lets users sync supported Windows settings across devices associated with their Microsoft Entra ID account. ESR management moved from the Microsoft Entra admin center to Windows settings backup and restore in July 2026. IT administrators now configure backup policies by using Microsoft Intune, another mobile device management (MDM) provider, or Group Policy.

The set of ESR settings remains unchanged. Only the management experience has changed. For the current list of supported settings, see the [Enterprise State Roaming settings catalog](/en-us/windows/configuration/windows-backup/catalog-esr).

ESR is separate from [consumer settings sync](https://go.microsoft.com/fwlink/?linkid=2015135), which uses a personal Microsoft account. Before July 2026, a [Global Administrator](../role-based-access-control/permissions-reference#global-administrator) could configure ESR through [device settings](manage-device-identities) in the [Microsoft Entra admin center](https://entra.microsoft.com). That portal management option is no longer available.

Important

You can no longer manage ESR through the Microsoft Entra admin center. Configure Windows settings backup and restore policies to continue roaming supported settings. If you take no action, Windows honors existing ESR and Group Policy or MDM roaming controls for one year and prioritizes Group Policy or MDM. After that period, ESR no longer works until you configure Windows settings backup and restore policies.

## Migrate Enterprise State Roaming management

To migrate ESR management, follow these steps:

1. Review your current use of ESR and identify the users and devices that need settings backup and roaming.
2. Confirm that your devices meet the backup requirements and that users have an eligible license. For current requirements and licensing information, see [Windows settings backup and restore](/en-us/windows/configuration/windows-backup/), the [Enterprise State Roaming settings catalog](/en-us/windows/configuration/windows-backup/catalog-esr), and the [Microsoft Entra product page](https://azure.microsoft.com/services/active-directory).
3. Configure the **Enable Windows Backup** policy by using Microsoft Intune, the Policy configuration service provider (CSP), or Group Policy.
4. Assign the policy to the users or devices that need settings backup and roaming.
5. Verify that the policy applies successfully.

Note

Configure Windows settings backup and restore by using either Group Policy or CSP. Don't combine both policy sources because conflicting settings can cause unexpected results.

For information about the legacy controls that limit which settings sync, see [Group Policy and MDM settings for settings sync](enterprise-state-roaming-group-policy-settings).

Backup is supported for eligible Microsoft Entra joined and [Microsoft Entra hybrid joined](hybrid-join-plan) devices. For current operating system versions and build requirements, see [Windows settings backup and restore system requirements](/en-us/windows/configuration/windows-backup/#system-requirements).

Microsoft Edge sync is managed separately from ESR. For more information, see [Microsoft Edge Sync](/en-us/deployedge/microsoft-edge-enterprise-sync). For legacy ESR diagnostics, see [Troubleshoot Enterprise State Roaming](enterprise-state-roaming-troubleshooting).

## Data storage and retention

Windows settings backup and restore treats user-specific settings as personal data and stores the data in the tenant's region. In the public cloud, the country or region selected when the tenant is created maps to a geographic location in Exchange Online.

By default, data is retained while it's associated with an active account and device. For current information about storage, encryption, compliance, and retention, see the [Windows settings backup and restore FAQ](/en-us/windows/configuration/windows-backup/faq#data-storage-and-retention). For legacy ESR-specific questions, see the [Settings and data roaming FAQ](enterprise-state-roaming-faqs). For general information about cloud locations, see [Azure regions](https://azure.microsoft.com/regions/). If you need help determining a data location, review [Azure support options](https://azure.microsoft.com/support/options/) or contact [Azure support](https://azure.microsoft.com/support/).
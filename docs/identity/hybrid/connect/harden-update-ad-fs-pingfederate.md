---
layout: Conceptual
title: Hardening updates for Microsoft Entra Connect Sync - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/harden-update-ad-fs-pingfederate
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Learn how to upgrade Microsoft Entra Connect Sync to meet the minimum version requirements and prevent synchronization failures after September 30, 2026.
ms.reviewer: sharonrutto
ms.date: 2025-09-19T00:00:00.0000000Z
ms.topic: concept-article
ms.subservice: hybrid-connect
locale: en-us
document_id: bd4d07a7-0877-b8ca-8bbe-83676ded4205
document_version_independent_id: bd4d07a7-0877-b8ca-8bbe-83676ded4205
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/harden-update-ad-fs-pingfederate.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/harden-update-ad-fs-pingfederate
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/harden-update-ad-fs-pingfederate.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: a745a7a1-f476-42e7-8daf-10579ce3a3df
---

# Hardening updates for Microsoft Entra Connect Sync - Microsoft Entra ID | Microsoft Learn

As part of increasing the security posture of Microsoft Entra Connect, Microsoft deployed a dedicated first-party application to enable the synchronization between Active Directory and Microsoft Entra ID. This new application will manifest as a first party service principal called the "Microsoft Entra AD Synchronization Service" (Application Id: `6bf85cfa-ac8a-4be5-b5de-425a0d0dc016`) and will be visible in the Enterprise Applications experience within the Microsoft Entra admin center. This application is critical for the continued operation of on-premises to Microsoft Entra ID synchronization functionality through Entra Connect.

We have since released a new version (2.5.79.0) of Microsoft Entra Connect that contains this service change. All customers are required to upgrade to the minimum versions by September 30, 2026 to avoid service disruptions.

## Expected impacts

If you aren’t upgraded to the minimum required version (2.5.79.0), you might encounter the following impact to the Microsoft Entra Connect Sync service when the service change takes effect:

All synchronization services in Microsoft Entra Connect Sync will fail.

Note

If you’re unable to upgrade by the deadline, you can restore the impacted functionalities by upgrading to the latest version. However, **all synchronization services will fail** during the period between **September 30, 2026, and when you upgrade**.

## Minimum versions

To avoid any service impact, customers should be on the following version by September 30, 2026:

Version [2.5.79.0](/en-us/entra/identity/hybrid/connect/reference-connect-version-history#25790) or higher.

The Microsoft Entra Connect Sync .msi installation file for this version is exclusively available on Microsoft Entra Admin Center under [Microsoft Entra Connect](https://entra.microsoft.com/#view/Microsoft_AAD_Connect_Provisioning/AADConnectMenuBlade/%7E/GetStarted).

Important

Make sure you familiarize yourself with the [minimum requirements](/en-us/entra/identity/hybrid/connect/how-to-connect-install-prerequisites) for the versions, including but not limited to:

- [.NET framework of 4.7.2](https://dotnet.microsoft.com/en-us/download/dotnet-framework/net472#:%7E:text=Downloads%20for%20building%20and%20running%20applications%20with%20.NET%20Framework%204.7.2)
- [TLS1.2](/en-us/entra/identity/hybrid/connect/reference-connect-tls-enforcement)

To assist customers with the upgrade process, we occasionally auto upgrade customers where supported. If you would like to be auto upgraded, ensure you have the [auto upgrade feature](/en-us/entra/identity/hybrid/connect/how-to-connect-install-automatic-upgrade) configured. For [auto upgrade to work](/en-us/entra/identity/hybrid/connect/security-updates-pks), you should be on version [2.3.20.0](/en-us/entra/identity/hybrid/connect/reference-connect-version-history#23200) or higher.

## Consider moving to Microsoft Entra Cloud Sync

If you're eligible, we recommend migrating from Microsoft Entra Connect Sync to Microsoft Entra Cloud Sync. Microsoft Entra Cloud Sync is the new sync client that works from the cloud and allows customers to set up and manage their sync preferences online. We recommend that you use Cloud Sync because we're introducing new features that improve the sync experiences through Cloud Sync. You can avoid future migrations by choosing Cloud Sync if that's the right option for you. Use the [supported sync scenarios comparison](../common-scenarios) to see if Cloud Sync is the right sync client for you.

See the following video to understand how Cloud sync provides value to your business.

For more information, see [What is cloud sync?](/en-us/azure/active-directory/cloud-sync/what-is-cloud-sync)

## Upgrading Microsoft Entra Connect Sync

If you aren't yet eligible to move to Cloud Sync, use this table for more information on upgrading.

| Title | Description |
| --- | --- |
| [Upgrading from a previous version](how-to-upgrade-previous-version) | Information on moving from one version of Microsoft Entra Connect to another |
| [Information on deprecation](deprecated-azure-ad-connect) | Information on using a deprecated or unsupported version of Microsoft Entra Connect (some information is applicable to versions that are impacted by a service change) |
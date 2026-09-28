---
layout: Conceptual
title: Security hardening to the autoupgrade process for Microsoft Entra Connect and Microsoft Entra Connect Health  - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/security-updates-pks
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This article describes security improvements to improve autoupgrade.
ms.topic: how-to
ms.date: 2025-09-17T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 204602fa-d96b-b087-e839-0771ac247188
document_version_independent_id: 204602fa-d96b-b087-e839-0771ac247188
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/security-updates-pks.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/security-updates-pks
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/security-updates-pks.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: d09286fc-0daa-b8e9-12a2-56af11ed7687
---

# Security hardening to the autoupgrade process for Microsoft Entra Connect and Microsoft Entra Connect Health  - Microsoft Entra ID | Microsoft Learn

Since September 2023, we've been autoupgrading Microsoft Entra Connect Sync and Microsoft Entra Connect Health customers to an updated build as part of a precautionary security-related service change. Customers who were autoupgraded won't be impacted by the service change, but if you opted out of autoupgrade or autoupgrade failed, we **strongly recommend** that you upgrade to the [latest versions](reference-connect-version-history) by **September 30, 2026**.

## Expected impacts

The following table provides information on the features and impact to services, you may encounter, if you aren't on the minimum recommended versions.

| Service | Impact |
| --- | --- |
| Microsoft Entra Connect | All synchronization services will fail |
| Microsoft Entra Connect Health Connect Sync agent | A subset of [alerts](how-to-connect-health-alert-catalog#alerts-for-microsoft-entra-connect-sync) are impacted:  - Connection to Microsoft Entra ID failed due to authentication failure  - High CPU usage detected - High Memory Consumption Detected  - Password Hash Synchronization has stopped working  - Export to Microsoft Entra ID was Stopped. Accidental delete threshold was reached - Password Hash Synchronization heartbeat was skipped in the last 120 minutes  - Microsoft Entra Sync service can't start due to invalid encryption keys  - Microsoft Entra Sync service not running: Windows Service account Creds Expired |
| Microsoft Entra Connect HealthAD DS agent | [All alerts](how-to-connect-health-alert-catalog#alerts-for-active-directory-domain-services) |
| Microsoft Entra Connect Health AD FS agent | [All alerts](how-to-connect-health-alert-catalog#alerts-for-active-directory-federation-services) |

## Minimum versions

To take advantage of our latest security improvements, we strongly encourage customers to upgrade to the following builds by **September 30, 2026**. To avoid any service impact, you should be using the following minimum versions:

- Microsoft Entra Connect: [2.5.79.0](reference-connect-version-history#25790) or higher
- Microsoft Entra Connect Health
    - Connect Sync agent: [4.5.2466.0](https://aka.ms/connecthealth-download) or higher
    - AD DS agent: version: [4.5.2466.0](https://aka.ms/connecthealth-adds-download) or higher
    - AD FS agent: version: [4.5.2466.0](https://aka.ms/connecthealth-adfs-download) or higher

To upgrade to the latest version.

Important

**Mandatory Upgrade Required**: All synchronization services in Microsoft Entra Connect Sync will stop working on **September 30, 2026** if you're not on at least version 2.5.79.0. In May 2025, we released this version with a back-end service change that hardens our services. Upgrade before this deadline to avoid any service disruption.

If you're unable to upgrade before the deadline, all synchronization services will fail until you upgrade to the latest version. Make sure you meet the minimum requirements including .NET Framework 4.7.2 and TLS 1.2.

## Consider moving to Microsoft Entra Cloud Sync

If you're eligible, we recommend migrating from Microsoft Entra Connect Sync to Microsoft Entra Cloud Sync. Microsoft Entra Cloud Sync is the new sync client that works from the cloud and allows customers to set up and manage their sync preferences online. We recommend that you use Cloud Sync because we're introducing new features that improve the sync experiences through Cloud Sync. You can avoid future migrations by choosing Cloud Sync if that's the right option for you. Use the [supported sync scenarios comparison](../common-scenarios) to see if Cloud Sync is the right sync client for you.

See the video below to understand how Cloud sync provides value to your business.

For more information, see [What is cloud sync?](/en-us/azure/active-directory/cloud-sync/what-is-cloud-sync)

## Upgrading Microsoft Entra Connect Sync

If you aren’t yet eligible to move to Cloud Sync, use this table for more information on upgrading.

| Title | Description |
| --- | --- |
| [Upgrading from a previous version](how-to-upgrade-previous-version) | Information on moving from one version of Microsoft Entra Connect to another |
| [Information on deprecation](deprecated-azure-ad-connect) | Information on using a deprecated or unsupported version of Microsoft Entra Connect (some information is applicable to versions that are impacted by a service change) |
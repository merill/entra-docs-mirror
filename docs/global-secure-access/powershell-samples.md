---
layout: Conceptual
title: PowerShell samples for Global Secure Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/powershell-samples
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Use these PowerShell samples to automate common Global Secure Access tasks, including connector registration, client install, traffic forwarding bypasses, break glass scenarios, TLS certificate creation, operations monitoring, and recovery.
ms.topic: sample
ms.date: 2026-06-17T00:00:00.0000000Z
ms.reviewer: katabish
ai-usage: ai-assisted
locale: en-us
document_id: 8713e454-fa9c-30d9-2701-62726b8b553a
document_version_independent_id: 8713e454-fa9c-30d9-2701-62726b8b553a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/powershell-samples.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/powershell-samples
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/powershell-samples.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: a7f9cc50-da42-a285-a0af-53c8ea672bbe
---

# PowerShell samples for Global Secure Access - Global Secure Access | Microsoft Learn

## Overview

These sample scripts provide guidance on common Global Secure Access tasks using PowerShell. Most samples require the [Microsoft Graph Beta PowerShell module](/en-us/powershell/microsoftgraph/installation) 2.10 or newer, unless otherwise noted.

The samples are grouped by scenario.

## Connector setup

| Sample | Description |
| --- | --- |
| [Get token for connector](scripts/powershell-get-token) | Get the auth token for registering your Microsoft Entra private network connector through Azure, AWS, or GCP Marketplaces. |

## Client deployment

| Sample | Description |
| --- | --- |
| [Install the Global Secure Access Windows client as a proof of concept](scripts/powershell-windows-client-install-proof-of-concept) | Automate installation of the Global Secure Access Windows client and apply essential registry configurations for proof-of-concept deployments. |

## Traffic forwarding and bypass

| Sample | Description |
| --- | --- |
| [Add a custom bypass rule to Internet Access](scripts/powershell-bypass-script) | Programmatically add a custom bypass rule to the Microsoft Entra Internet Access forwarding policy to bypass specified domains or IPs. |
| [Add Intune device compliance bypasses to Internet Access](scripts/powershell-add-internet-access-device-compliance-bypasses) | Add Intune-related network endpoints to the Internet Access custom bypass policy to mitigate device compliance issues. |

## Break glass

| Sample | Description |
| --- | --- |
| [Disable traffic forwarding and Compliant Network policies (break glass)](scripts/powershell-break-glass) | Quickly disable traffic forwarding profiles and switch Conditional Access policies that use the Compliant Network condition into Report-Only mode during an outage. |
| [Restore Compliant Network requirement after break glass](scripts/powershell-break-glass-recovery) | Re-enable the forwarding profiles and Conditional Access policies that were disabled by the break glass script after an outage is resolved. |

## TLS inspection certificates

| Sample | Description |
| --- | --- |
| [Create and sign TLS certificates using Active Directory Certificate Services](scripts/powershell-active-directory-certificate-service) | Generate a certificate signing request through the TLS inspection Graph API, sign it with ADCS, and upload the certificate and chain to TLS inspection settings. |
| [Create and sign TLS certificates using OpenSSL](scripts/powershell-open-secure-sockets-layer) | Generate a certificate signing request through the TLS inspection Graph API, sign it with a self-signed root CA created by OpenSSL, and upload the certificate and chain to TLS inspection settings. |

## Operations monitoring

| Sample | Description |
| --- | --- |
| [Shared helper functions for operations scripts](scripts/powershell-global-secure-access-operations-helpers) | Use shared authentication, Log Analytics token, and alert email helper functions for operations automation scripts. |
| [Verify configuration backup compliance](scripts/powershell-test-backup-compliance) | Check recent Azure Automation jobs for your Global Secure Access configuration backup runbook and alert when backups fail or miss a scheduled run. |
| [Check role assignment reviews](scripts/powershell-test-role-based-access-control-hygiene) | Query Global Secure Access-related role assignments and identify administrator accounts that need quarterly review. |
| [Calculate alert noise ratio](scripts/powershell-test-alert-noise-ratio) | Calculate the Microsoft Sentinel alert noise ratio for Global Secure Access detections and identify noisy analytics rules. |

## Recovery

| Sample | Description |
| --- | --- |
| [List Microsoft Entra snapshots](scripts/powershell-get-entra-snapshot) | List Microsoft Entra Backup and Recovery snapshots for the tenant and identify the latest available snapshot. |
| [Preview Microsoft Entra recovery](scripts/powershell-start-entra-recovery-preview) | Create a non-destructive recovery preview job scoped to directory objects that affect Global Secure Access. |
| [Run Microsoft Entra recovery](scripts/powershell-invoke-entra-recovery) | Run a Microsoft Entra recovery job after reviewing and approving the matching preview job. |
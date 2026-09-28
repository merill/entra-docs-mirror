---
layout: Conceptual
title: PowerShell samples in Application Management - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/app-management-powershell-samples
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: These PowerShell samples are used for apps you manage in your Microsoft Entra tenant. You can use these sample scripts to find expiration information about secrets and certificates.
ms.topic: sample
ms.date: 2025-01-23T00:00:00.0000000Z
ms.reviewer: mifarca
ms.custom: enterprise-apps, no-azure-ad-ps-ref
locale: en-us
document_id: 48d644c2-348a-b70c-9fc4-3b0ce2ab70f7
document_version_independent_id: 555d8635-1e85-2500-1dec-f8ff1d6f295a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/app-management-powershell-samples.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/app-management-powershell-samples
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/app-management-powershell-samples.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 83eb502a-63e8-8053-f0a1-3f5237b515f6
---

# PowerShell samples in Application Management - Microsoft Entra ID | Microsoft Learn

The following table includes links to PowerShell script examples for Microsoft Entra Application Management.

These samples require the [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/installation) SDK module.

| Link | Description |
| --- | --- |
| **Application Management scripts** |  |
| [Export secrets and certs (app registrations)](scripts/powershell-export-all-app-registrations-secrets-and-certs) | Export secrets and certificates for app registrations in Microsoft Entra tenant. |
| [Export secrets and certs (enterprise apps)](scripts/powershell-export-all-enterprise-apps-secrets-and-certs) | Export secrets and certificates for enterprise apps in Microsoft Entra tenant. |
| [Export expiring secrets and certs (app registrations)](scripts/powershell-export-apps-with-expiring-secrets) | Export app registrations with expiring secrets and certificates and their Owners in Microsoft Entra tenant. |
| [Export expiring secrets and certs (enterprise apps)](scripts/powershell-export-enterprise-apps-with-expiring-secrets) | Export enterprise apps with expiring secrets and certificates and their Owners in Microsoft Entra tenant. |
| [Export secrets and certs expiring beyond required date](scripts/powershell-export-apps-with-secrets-beyond-required) | Export App Registrations with secrets and certificates expiring beyond the required date in Microsoft Entra tenant. This scenario uses the noninteractive Client\_Credentials Oauth flow. |
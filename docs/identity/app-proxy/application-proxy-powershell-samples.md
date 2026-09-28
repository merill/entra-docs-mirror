---
layout: Conceptual
title: PowerShell samples for Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-powershell-samples
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Use these PowerShell samples for Microsoft Entra application proxy to get information about application proxy apps and connectors in your directory, assign users and groups to apps, and get certificate information.
ms.topic: sample
ms.date: 2026-03-11T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
locale: en-us
document_id: 16807070-c587-70ec-bbdc-e8cf9ca10352
document_version_independent_id: b8f9a2c7-ec00-7109-e064-f63c7a691805
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-powershell-samples.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-powershell-samples
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-powershell-samples.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 952fd8ae-730e-e64f-55fa-2c8d9e81b0a7
---

# PowerShell samples for Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn

## Overview

The following table includes links to PowerShell script examples for Microsoft Entra application proxy. These samples require the [Microsoft Graph Beta PowerShell module](/en-us/powershell/microsoftgraph/installation) 2.10 or newer, unless otherwise noted.

For more information about the cmdlets used in these samples, see [application proxy application management](/en-us/powershell/module/azuread/#application_proxy_application_management) and [private network connector management](/en-us/powershell/module/azuread/#application_proxy_connector_management).

| Link | Description |
| --- | --- |
| **Application proxy apps** |  |
| [List basic information for all application proxy apps](scripts/powershell-get-all-app-proxy-apps-basic) | Lists basic information (AppId, DisplayName, ObjId) about all the application proxy apps in your directory. |
| [List extended information for all application proxy apps](scripts/powershell-get-all-app-proxy-apps-extended) | Lists extended information (AppId, DisplayName, ExternalUrl, InternalUrl, ExternalAuthenticationType) about all the application proxy apps in your directory. |
| [List all application proxy apps by connector group](scripts/powershell-get-all-app-proxy-apps-by-connector-group) | Lists information about all the application proxy apps in your directory and which connector groups the apps are assigned to. |
| [Get all application proxy apps with a token lifetime policy](scripts/powershell-get-all-app-proxy-apps-with-policy) | Lists all application proxy apps in your directory with a token lifetime policy and its details. |
| **Connector groups** |  |
| [Get all connector groups and connectors in the directory](scripts/powershell-get-all-connectors) | Lists all the connector groups and connectors in your directory. |
| [Move all apps assigned to a connector group to another connector group](scripts/powershell-move-all-apps-to-connector-group) | Moves all applications currently assigned to a connector group to a different connector group. |
| **Users and group assigned** |  |
| [Display users and groups assigned to an application proxy application](scripts/powershell-display-users-group-of-app) | Lists the users and groups assigned to a specific application proxy application. |
| [Assign a user to an application](scripts/powershell-assign-user-to-app) | Assigns a specific user to an application. |
| [Assign a group to an application](scripts/powershell-assign-group-to-app) | Assigns a specific group to an application. |
| **External URL configuration** |  |
| [Get all application proxy apps using default domains (.msappproxy.net)](scripts/powershell-get-all-default-domain-apps) | Lists all the application proxy applications using default domains (.msappproxy.net). |
| [Get all application proxy apps using wildcard publishing](scripts/powershell-get-all-wildcard-apps) | Lists all application proxy apps using wildcard publishing. |
| **Custom Domain configuration** |  |
| [Get all application proxy apps using custom domains and certificate information](scripts/powershell-get-all-custom-domains-and-certs) | Lists all application proxy apps that are using custom domains and the certificate information associated with the custom domains. |
| [Get all Microsoft Entra ID Proxy application apps published with no certificate uploaded](scripts/powershell-get-all-custom-domain-no-cert) | Lists all application proxy apps that are using custom domains but don't have a valid TLS/SSL certificate uploaded. |
| [Get all Microsoft Entra ID Proxy application apps published with the identical certificate](scripts/powershell-get-custom-domain-identical-cert) | Lists all the Microsoft Entra ID Proxy application apps published with the identical certificate. |
| [Get all Microsoft Entra ID Proxy application apps published with the identical certificate and replace it](scripts/powershell-get-custom-domain-replace-cert) | For Microsoft Entra ID Proxy application apps that are published with an identical certificate, allows you to replace the certificate in bulk. |
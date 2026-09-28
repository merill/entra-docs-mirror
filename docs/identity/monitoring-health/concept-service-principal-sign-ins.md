---
layout: Conceptual
title: Service principal sign-in logs - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/concept-service-principal-sign-ins
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn about the activity captured in the service principal sign-in logs in Microsoft Entra monitoring and health.
ms.topic: troubleshooting-general
ms.date: 2025-03-17T00:00:00.0000000Z
ms.reviewer: egreenberg14
ms.custom: sfi-image-nochange
locale: en-us
document_id: 0f448074-7a23-54fd-e2ce-25d3f359851c
document_version_independent_id: 0f448074-7a23-54fd-e2ce-25d3f359851c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/concept-service-principal-sign-ins.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/concept-service-principal-sign-ins
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/concept-service-principal-sign-ins.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7b6dccd5-8eac-17b9-6703-a8397637965c
---

# Service principal sign-in logs - Microsoft Entra ID | Microsoft Learn

Unlike interactive and non-interactive user sign-ins, service principal sign-ins don't involve a user. Instead, they're sign-ins by any nonuser account, such as apps or service principals (except managed identity sign-in, which are in included only in the managed identity sign-in log). In these sign-ins, the app or service provides its own credential, such as a certificate or app secret to authenticate or access resources.

[![Screenshot of the service principal sign-in log.](media/concept-service-principal-sign-ins/sign-in-logs-service-principal.png)](media/concept-service-principal-sign-ins/sign-in-logs-service-principal-expanded.png#lightbox)

## Log details

The following examples show the type of information captured in the service principal sign-in logs:

- A service principal uses a certificate to authenticate and access the Microsoft Graph.
- An application uses a client secret to authenticate in the OAuth Client Credentials flow.

You can't customize the fields shown in this report.

Note

Entries in the sign-in logs are system generated and can't be changed or deleted.

## How does it work?

To make it easier to digest the data in the service principal sign-in logs, service principal sign-in events are grouped. Sign-ins from the same entity under the same conditions are aggregated into a single row. You can expand the row to see all the different sign-ins and their different time stamps. Sign-ins are aggregated in the service principal report when the following data matches:

- Service principal name or ID
- Status
- IP address
- Resource name or ID
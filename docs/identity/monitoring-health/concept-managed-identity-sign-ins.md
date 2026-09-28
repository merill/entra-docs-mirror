---
layout: Conceptual
title: Managed identity sign-in logs - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/concept-managed-identity-sign-ins
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn about the type of information captured in the managed identity sign-in logs in Microsoft Entra monitoring and health.
ms.topic: troubleshooting-general
ms.date: 2026-02-09T00:00:00.0000000Z
ms.reviewer: egreenberg14
ms.custom: sfi-image-nochange
locale: en-us
document_id: 661f448d-5d99-1c4c-6476-276fb296ac11
document_version_independent_id: 661f448d-5d99-1c4c-6476-276fb296ac11
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/concept-managed-identity-sign-ins.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/concept-managed-identity-sign-ins
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/concept-managed-identity-sign-ins.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 607ec317-359a-8c26-d94b-7b93ecbe590b
---

# Managed identity sign-in logs - Microsoft Entra ID | Microsoft Learn

Managed identities for Azure resources sign-ins are sign-ins that were performed by resources that have their secrets managed by Azure to simplify credential management. A virtual machine with managed credentials uses Microsoft Entra ID to get an access token.

![Screenshot of the managed identity sign-in log.](media/concept-managed-identity-sign-ins/sign-in-logs-managed-identity.png)

You can't customize the fields shown in this report.

To make it easier to digest the data, these sign-in events are grouped together. Sign-ins from the same entity are aggregated into a single row. You can expand the row to see all the different sign-ins and their different time stamps. Sign-ins are aggregated in the managed identities report when all of the following data matches:

- Managed identity name or ID
- Status
- Resource name or ID

Select an item in the list view to display all sign-ins that are grouped under a node. Select a grouped item to see all details of the sign-in.

Note

Entries in the sign-in logs are system generated and can't be changed or deleted.
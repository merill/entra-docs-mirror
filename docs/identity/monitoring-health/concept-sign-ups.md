---
layout: Conceptual
title: Sign-up logs in Microsoft Entra External ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/concept-sign-ups
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn about the sign-up logs that are available in Microsoft Entra External ID monitoring and health.
ms.topic: troubleshooting-general
ms.date: 2025-06-30T00:00:00.0000000Z
ms.reviewer: pmwongera
locale: en-us
document_id: 0ed023a7-d611-fdb9-83ac-2e2135d85f3e
document_version_independent_id: 0ed023a7-d611-fdb9-83ac-2e2135d85f3e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/concept-sign-ups.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/concept-sign-ups
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/concept-sign-ups.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 29cbfb7b-adba-567d-34ac-2d8368f80a0f
---

# Sign-up logs in Microsoft Entra External ID - Microsoft Entra ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../../includes/media/applies-to/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Microsoft Entra External ID logs all self-service sign-up events, including both successful sign-ups and failed attempts. The logs include information that helps organizations optimize their sign-up processes, enhance the user experience, and improve overall customer engagement. This article explains how to access and use the sign-up logs.

The sign-up logs provided by Microsoft Entra External ID are a powerful type of [activity log](overview-monitoring-health) that you can analyze. In addition to the External ID sign-up logs, three other activity logs are also available to help monitor the health of your external tenant:

- **[Sign-ins](concept-sign-ins)** – Information about sign-ins and how your resources are used by your users.
- **[Audit](concept-audit-logs)** – Information about changes applied to your tenant, such as users and group management or updates applied to your tenant’s resources.
- **[Provisioning](concept-provisioning-logs)** – Activities performed by a provisioning service, such as the creation of a group in ServiceNow or a user imported from Workday.

## What can you do with sign-up logs?

You can use the sign-up logs to find the following information:

- The percentage of sign-up attempts that result in account creation.
- The stage in the sign-up process with the highest drop-off rate.
- How drop-off rates compare between social sign-ups and local account sign-ups.

You can also describe the activity associated with a sign-up request by identifying the following details:

- Who performed the sign-up
- When the user performed the sign-up
- How the user signed up (for example, local account or social identity provider)
- What app they accessed to sign up
- Whether the sign-up was successful
- Where an unsuccessful sign-up failed in the sign-up flow
- Whether the user who tried to sign up already had an account
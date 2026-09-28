---
layout: Conceptual
title: Non-interactive sign-in logs - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/concept-noninteractive-sign-ins
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn about the type of activity captured in the non-interactive sign-in logs in Microsoft Entra monitoring and health.
ms.topic: concept-article
ms.date: 2026-02-09T00:00:00.0000000Z
ms.reviewer: egreenberg14
ms.custom: sfi-image-nochange
locale: en-us
document_id: 74109879-b5b9-858f-e8bf-8090f6290c57
document_version_independent_id: 74109879-b5b9-858f-e8bf-8090f6290c57
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/concept-noninteractive-sign-ins.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/concept-noninteractive-sign-ins
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/concept-noninteractive-sign-ins.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 41a0c465-8be0-b4c0-ecc1-6bd24e7bd91b
---

# Non-interactive sign-in logs - Microsoft Entra ID | Microsoft Learn

Microsoft Entra monitoring and health provides several types of sign-in logs to help you monitor the health of your tenant. Non-interactive sign-ins are a subset of the user sign-in logs in the Microsoft Entra admin center.

## What is a non-interactive user sign-in?

Non-interactive sign-ins are done *on behalf of a* user. These delegated sign-ins were performed by a client app or OS components on behalf of a user and don't require the user to provide an authentication factor. Instead, Microsoft Entra ID recognizes when the user's token needs to be refreshed and does so behind the scenes, without interrupting the user's session. In general, the user perceives these sign-ins as happening in the background.

[![Screenshot of the non-interactive user sign-in log.](media/concept-noninteractive-sign-ins/sign-in-logs-user-noninteractive.png)](media/concept-noninteractive-sign-ins/sign-in-logs-user-noninteractive-expanded.png#lightbox)

## Log details

The following examples show the type of information captured in the non-interactive user sign-in logs:

- A client app uses an OAuth 2.0 refresh token to get an access token.
- A client uses an OAuth 2.0 authorization code to get an access token and refresh token.
- A user performs single sign-on (SSO) to a web or Windows app on a Microsoft Entra joined PC (without providing an authentication factor or interacting with a Microsoft Entra prompt).
- A user signs in to a second Microsoft Office app while they have a session on a mobile device using FOCI (Family of Client IDs).

In addition to the default fields, the non-interactive sign-in log also shows:

- Resource ID
- Number of grouped sign-ins

You can't customize the fields shown in this report.

Note

Entries in the sign-in logs are system generated and can't be changed or deleted.

## How does it work?

To make it easier to digest the data, non-interactive sign-in events are grouped. Clients often create many non-interactive sign-ins on behalf of the same user in a short time period. The non-interactive sign-ins share the same characteristics except for the time the sign-in was attempted. For example, a client might get an access token once per hour on behalf of a user. If the state of the user or client doesn't change, the IP address, resource, and all other information is the same for each access token request. The only state that does change is the date and time of the sign-in.

[![Screenshot of an aggregate sign-in expanded to show all rows.](media/concept-noninteractive-sign-ins/aggregate-sign-in.png)](media/concept-noninteractive-sign-ins/aggregate-sign-in-expanded.png#lightbox)

When Microsoft Entra logs multiple sign-ins that are identical other than time and date, those sign-ins are from the same entity and are aggregated into a single row. A row with multiple identical sign-ins (except for date and time issued) has a value greater than one in the *# sign-ins* column. These aggregated sign-ins might also appear to have the same time stamps. The **Time aggregate** filter can set to 1 hour, 6 hours, or 24 hours. You can expand the row to see all the different sign-ins and their different time stamps.

Sign-ins are aggregated in the non-interactive users when the following data matches:

- Application
- User
- IP address
- Status
- Resource ID

## Special considerations

- The IP address of non-interactive sign-ins performed by [confidential clients](../../identity-platform/msal-client-applications) doesn't match the actual source IP of where the refresh token request is coming from. Instead, it shows the original IP used for the original token issuance.
- As of April 11, 2025, all new sign-ins that obtain a refresh token with FIDO2 keys are now logged in the non-interactive sign-in logs.
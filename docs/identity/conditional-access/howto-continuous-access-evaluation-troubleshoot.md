---
layout: Conceptual
title: Monitor and troubleshoot sign-ins with continuous access evaluation in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/howto-continuous-access-evaluation-troubleshoot
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Troubleshoot and respond to changes in user state faster with continuous access evaluation in Microsoft Entra ID.
ms.topic: troubleshooting
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: sreyanthmora
ms.custom: sfi-image-nochange
locale: en-us
document_id: 1f75ff6d-edd0-0f70-ad35-96608a85c7db
document_version_independent_id: abe1c46c-8c76-5a86-3236-d5b10870ce08
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/howto-continuous-access-evaluation-troubleshoot.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/howto-continuous-access-evaluation-troubleshoot
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/howto-continuous-access-evaluation-troubleshoot.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 6d66bedb-13ae-776e-7154-f581cee3c27f
---

# Monitor and troubleshoot sign-ins with continuous access evaluation in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

## Overview

Administrators can monitor and troubleshoot sign in events where [continuous access evaluation (CAE)](concept-continuous-access-evaluation) is applied in multiple ways.

## Continuous access evaluation sign-in reporting

Administrators can monitor user sign-ins where continuous access evaluation (CAE) is applied. This information is found in the Microsoft Entra sign-in logs:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Reader](../role-based-access-control/permissions-reference#security-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Sign-in logs**.
3. Apply the **Is CAE Token** filter.

[![Screenshot showing how to add a filter to the sign-in log to see where CAE is being applied or not.](media/howto-continuous-access-evaluation-troubleshoot/sign-ins-log-apply-filter.png)](media/howto-continuous-access-evaluation-troubleshoot/sign-ins-log-apply-filter.png#lightbox)

From here, admins are presented with information about their user’s sign-in events. Select any sign-in to see details about the session, like which Conditional Access policies applied and if CAE enabled.

There are multiple sign-in requests for each authentication. Some are on the interactive tab, while others are on the non-interactive tab. CAE is only marked true for one of the requests it can be on the interactive tab or non-interactive tab. Admins must check both tabs to confirm whether the user's authentication is CAE enabled or not.

### Searching for specific sign-in attempts

Sign-in logs show success and failure events. Use filters to narrow your search. For example, if a user signs in to Teams, apply the Application filter and set it to Teams. Admins might need to check the sign-ins from both interactive and non-interactive tabs to locate the specific sign-in. To further narrow the search, admins might apply multiple filters.

## Continuous access evaluation workbooks

The continuous access evaluation insights workbook lets admins view and monitor CAE usage insights for their tenants. The table shows authentication attempts with IP mismatches. This workbook is available as a template under the Conditional Access category.

### Accessing the CAE workbook template

You need to complete Log Analytics integration before workbooks are shown. To learn how to stream Microsoft Entra sign-in logs to a Log Analytics workspace, see [Integrate Microsoft Entra logs with Azure Monitor logs](../monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Reader](../role-based-access-control/permissions-reference#security-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Workbooks**.
3. Under **Public Templates**, search for **Continuous access evaluation insights**.

The **Continuous access evaluation insights** workbook contains the following table:

### Potential IP address mismatch between Microsoft Entra ID and resource provider

The potential IP address mismatch between Microsoft Entra ID and resource provider table lets admins investigate sessions where the IP address detected by Microsoft Entra ID doesn't match the IP address detected by the resource provider.

This workbook table highlights these scenarios by showing the respective IP addresses and whether a CAE token was issued during the session.

### Continuous access evaluation insights per sign-in

The continuous access evaluation insights per sign-in page in the workbook connects multiple requests from the sign-in logs and displays a single request where a CAE token was issued.

This workbook is useful, for example, when a user opens Outlook on their desktop and tries to access resources in Exchange Online. This sign-in action might map to multiple interactive and non-interactive sign-in requests in the logs making issues hard to diagnose.

## IP address configuration

Your identity provider and resource providers might see different IP addresses. This mismatch can occur due to the following reasons:

- Your network implements split tunneling.
- Your resource provider is using an IPv6 address and Microsoft Entra ID is using an IPv4 address.
- Because of network configurations, Microsoft Entra ID sees one IP address from the client and your resource provider sees a different IP address from the client.

If this scenario exists in your environment, to avoid infinite loops, Microsoft Entra ID issues a one-hour CAE token and doesn't enforce client location change during that one-hour period. Even in this case, security is improved compared to traditional one-hour tokens since we're still evaluating the other events besides client location change events.

Admins can view records filtered by time range and application, and compare the number of mismatched IPs detected with the total number of sign-ins during a specified period.

To unblock users, admins can add specific IP addresses to a trusted named location.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Named locations**. Here you can create or update trusted IP locations.

Note

Before adding an IP address as a trusted named location, confirm that the IP address belongs to the intended organization.

For more information about named locations, see [Using the location condition](concept-assignment-network).
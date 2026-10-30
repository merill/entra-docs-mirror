---
layout: Conceptual
title: Interactive user sign-in logs - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/concept-interactive-sign-ins
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn about the type of information captured in the interactive user sign-in logs in Microsoft Entra monitoring and health.
ms.topic: troubleshooting-general
ms.date: 2026-02-09T00:00:00.0000000Z
ms.reviewer: egreenberg14
ms.custom: sfi-image-nochange
locale: en-us
document_id: f6744a6b-f1e8-938e-e0fd-dad028adb32d
document_version_independent_id: f6744a6b-f1e8-938e-e0fd-dad028adb32d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/concept-interactive-sign-ins.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/concept-interactive-sign-ins
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/concept-interactive-sign-ins.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: ed238fd7-33c5-def5-5777-525ec405237a
---

# Interactive user sign-in logs - Microsoft Entra ID | Microsoft Learn

Microsoft Entra monitoring and health provides several types of sign-in logs to help you monitor the health of your tenant. The interactive user sign-ins are the default view in the Microsoft Entra admin center.

## What is an interactive user sign-in?

Interactive sign-ins are performed *by* a user. They provide an authentication factor to Microsoft Entra ID. That authentication factor could also interact with a helper app, such as the Microsoft Authenticator app. Users can provide passwords, responses to MFA challenges, biometric factors, or QR codes to Microsoft Entra ID or to a helper app. This log also includes federated sign-ins from identity providers that are federated to Microsoft Entra ID.

[![Screenshot of the interactive user sign-in log.](media/concept-interactive-sign-ins/sign-in-logs-user-interactive.png)](media/concept-interactive-sign-ins/sign-in-logs-user-interactive-expanded.png#lightbox)

## Log details

The following examples show the type of information captured in the interactive user sign-in logs:

- A user provides username and password in the Microsoft Entra sign-in screen.
- A user passes an SMS MFA challenge.
- A user provides a biometric gesture to unlock their Windows PC with Windows Hello for Business.
- A user is federated to Microsoft Entra ID with an AD FS SAML assertion.

In addition to the default fields, the interactive sign-in logs also show:

- The sign-in location
- Whether Conditional Access was applied
- Cross-tenant access details, such as home and resource tenant IDs

Note

Entries in the sign-in logs are system generated and can't be changed or deleted.

## Special considerations

### Partner access to downstream tenant resources

The interactive sign-in logs now include details about when a partner accesses a downstream tenant's resources. By looking at the **Cross tenant access type**, **Home tenant ID**, and **Resource tenant ID** columns, which are now visible by default, you can see when a partner logs into a downstream tenant resource.

- Filter on **Service Provider** in the **Cross tenant access type** column to isolate events related to partner sign-ins.
- Compare the details in the **Home tenant ID** and **Resource tenant ID** columns to identify sign-ins coming from your partner's tenant to the downstream tenant.

### Non-interactive sign-ins on the interactive sign-in logs

Previously, some non-interactive sign-ins were included in the interactive user sign-in log for better visibility. This increased visibility was necessary before the non-interactive user sign-in logs were introduced in November 2020. Non-interactive sign-ins involving FIDO2 keys were previously marked as interactive sign-ins, even though they were technically non-interactive. As of April 11, 2025, all new sign-ins that obtain a refresh token with FIDO2 keys are now logged in the non-interactive sign-in logs.

### Passthrough sign-ins

Microsoft Entra ID issues tokens for authentication and authorization. In some situations, a user who is signed in to the Contoso tenant might try to access resources in the Fabrikam tenant, where they don't have access. A no-authorization token called a passthrough token, is issued to the Fabrikam tenant. The passthrough token doesn't allow the user to access any resources.

Previously, when reviewing the logs for this situation, the sign-in logs for the home tenant (in this scenario, Contoso) didn't show a sign-in attempt because *the token wasn't granting access to a resource with any claims*. The sign-in token was only used to display the appropriate failure message.

Passthrough sign-in attempts now appear in the home tenant sign-in logs and any relevant tenant restriction sign-in logs. This update provides more visibility into user sign-in attempts from your users and deeper insights into your tenant restriction policies.

The `crossTenantAccessType` property now shows `passthrough` to differentiate passthrough sign-ins and is available in the Microsoft Entra admin center and Microsoft Graph.

### First-party, app-only service principal sign-ins

The service principal sign-in logs don't include first-party, app-only sign-in activity. This type of activity happens when first-party apps get tokens for an internal Microsoft job where there's no direction or context from a user. We exclude these logs so you're not paying for logs related to internal Microsoft tokens within your tenant.

You might identify Microsoft Graph events that don't correlate to a service principal sign-in if you're routing `MicrosoftGraphActivityLogs` with `SignInLogs` to the same Log Analytics workspace. This integration allows you to cross reference the token issued for the Microsoft Graph API call with the sign-in activity. The `UniqueTokenIdentifier` for sign-in logs and the `SignInActivityId` in the Microsoft Graph activity logs would be missing from the service principal sign-in logs.

### Conditional Access

Sign-ins that show **Not applied** for Conditional Access can be difficult to interpret. If the sign-in is interrupted, the sign-in appears on the logs but shows **Not applied** for Conditional Access. Another common scenario is signing in to Windows Hello for Business. This sign-in doesn't have Conditional Access applied because the user is signing in to the device, not to cloud resources protected by Conditional Access.

## TimeGenerated field

If you're integrating your sign-in logs with Azure Monitor logs and Log Analytics, you might notice that the `TimeGenerated` field in the logs doesn't match the time the sign-in occurred. This discrepancy is due to the way the logs are ingested into Azure Monitor. The `TimeGenerated` field is the time the entry was received and published by Log Analytics, not the time the sign-in occurred. The `CreatedDateTime` field in the logs shows the time the sign-in occurred.

Similarly, risky sign-in events also display `TimeGenerated` as the time when the risky event was detected, not when the sign-in occurred. To find the actual sign-in time, you can use the `CorrelationId` to find the sign-in event in the logs and locate the sign-in time.
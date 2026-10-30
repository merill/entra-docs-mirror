---
layout: Conceptual
title: Learn about Global Secure Access Alerts - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/concept-alerts
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how Global Secure Access alerts notify you about security issues and operational concerns, helping to strengthen your organization's security posture.
ms.topic: overview
ms.date: 2025-12-08T00:00:00.0000000Z
ms.reviewer: kerenSemel
ai-usage: ai-assisted
locale: en-us
document_id: e92d7b11-2351-5158-13de-350e195cb151
document_version_independent_id: e92d7b11-2351-5158-13de-350e195cb151
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/concept-alerts.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/concept-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/concept-alerts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 92379fa6-adf1-3dce-de03-70a872e99c2b
---

# Learn about Global Secure Access Alerts - Global Secure Access | Microsoft Learn

Global Secure Access alerts provide real-time notifications about potential security issues and operational concerns within your organization's network. Alerts include details about severity, related MITRE techniques, provider information, and related entities.

Alerts provide visibility into activities, threats, and entities of interest such as users, devices, and applications. Alerts offer operational insights to resolve deployment and health issues. They also deliver security insights from detections and related activities, strengthening your overall security posture.

The Global Secure Access alert structure aligns with the [Microsoft Sentinel security alert schema](/en-us/azure/sentinel/security-alert-schema), enabling a smooth integration with [Microsoft Defender XDR](/en-us/defender-xdr/microsoft-365-defender).

With alerts, Global Secure Access admins can:

- View statistics on alert types and severity.
- Investigate alerts and related data by using filters and linked information.
- Export alerts for use with security information and event management (SIEM) tools or other solutions.

## Types of alerts

Global Secure Access includes the following alert types:

### Token/Device Inconsistency alert

You see this alert when the same access token is used on more than one device.

### Increased External Tenant Activity alert

You see this alert when there's an unusual rise in activity with external tenants. This alert looks at a 14-day sliding window, with access to tenants other than the home tenant.

### Unhealthy Remote Network alert

You see this alert when there are deficiencies in remote network availability. This alert checks hourly for remote network health events like BGPDisconnect or TunnelDisconnect.

### Netskope alerts

The Netskope alerts include:

- **Threat Protection**: You see this alert when Netskope detects malware or suspicious content in traffic.
- **Data Loss Prevention** (DLP): You see this alert when sensitive data matches a DLP profile during inspection.
- **Fallback**: You see this alert when Netskope can't fully process traffic due to technical limitations like file size limits, scan timeouts, or unsupported file types.

Important

Netskope alerts require the Netskope Advanced Threat Protection (ATP) and DLP modules in Global Secure Access. For more information, see [Netskope's Advanced Threat Protection and Data Loss Prevention](concept-netskope-integration).

## View alerts

To view Global Secure Access alerts:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Monitor** &gt; **Alerts**.

[![Screenshot of the Global Secure Access Alerts view.](media/concept-alerts/alerts-view.png)](media/concept-alerts/alerts-view.png#lightbox)

You can filter and sort alerts based on severity, date, and type to quickly identify and respond to potential security issues.

You can also view the **Alerts** widget in the [Global Secure Access dashboard](concept-traffic-dashboard) for a summary of recent alerts.
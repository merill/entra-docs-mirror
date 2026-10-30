---
layout: Conceptual
title: Enable Source IP Restoration with Global Secure Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-source-ip-restoration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to enable source IP restoration to ensure the source IP matches in downstream resources.
ms.topic: how-to
ms.date: 2026-04-03T00:00:00.0000000Z
ms.reviewer: dhruvinrshah
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 2e6783d0-e149-0a91-ec5e-01d93b6bae19
document_version_independent_id: 35c92294-6ce0-7160-3686-00d9fb213b92
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-source-ip-restoration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-source-ip-restoration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-source-ip-restoration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 78f7a486-0a7c-0283-b683-2017ab0c6380
---

# Enable Source IP Restoration with Global Secure Access - Global Secure Access | Microsoft Learn

When you use cloud-based network proxy and SSE solutions, they abstract the original source IP of the user from the service that the user connects to. Instead, the service detects the user's IP address as the egress address of the cloud-based network proxy. While this abstraction helps with privacy-related concerns in consumer scenarios, not having the original source IP information makes it difficult to achieve enterprise security goals. For example, without an actual client egress IP address, you can't apply Microsoft Entra ID Conditional Access policies based on your organization's well-known IP addresses, and audit logs don't reflect accurate location information.

Source IP restoration is part of the Adaptive Access feature of Microsoft Entra Internet Access for Microsoft Services. Source IP restoration detects and securely communicates the original egress IP address of the end user to Microsoft Entra ID and Microsoft Graph, bringing the following benefits to your organization:

- You can continue to enforce IP-based location policies in [Microsoft Entra ID Conditional Access](/en-us/azure/active-directory/conditional-access/overview).
- It improves the accuracy of risk detection in [Microsoft Entra ID Protection risk detections](/en-us/entra/id-protection/concept-identity-protection-risks).
- It elevates your threat detection and response by recording accurate source IP in [Microsoft Entra sign-in logs](/en-us/azure/active-directory/reports-monitoring/concept-all-sign-ins) and in [Microsoft Entra audit logs](/en-us/entra/identity/monitoring-health/concept-audit-logs).

## Prerequisites

- Administrators who configure source IP restoration settings must have one of the following role assignments:
    - The [Global Secure Access Administrator role](/en-us/azure/active-directory/roles/permissions-reference)
    - The [Global Administrator role](/en-us/azure/active-directory/roles/permissions-reference)
- The product requires Microsoft Entra ID P1 licenses. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).
- You must enable the [Microsoft Traffic Profile](concept-microsoft-traffic-profile) to use source IP restoration.

### Known limitations

For detailed information about known issues and limitations, see [Known limitations for Global Secure Access](reference-current-known-limitations).

## Enable Global Secure Access signaling for Microsoft Entra ID and Microsoft Graph

Note

Source IP restoration is now enabled by default for new tenants. If you enabled Global Secure Access features in your tenant before June 2025, you might need to explicitly enable source IP restoration.

To enable the required setting to allow source IP restoration, an administrator must take the following steps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Settings** &gt; **Session management** &gt; **Adaptive Access**.
3. Select the toggle to **Enable Conditional Access Signaling for Microsoft Entra ID**.

By using this functionality, Microsoft Entra ID and Microsoft Graph receive the public egress source IP address of the user.

[![Screenshot showing the toggle to enable Conditional Access Signaling for Microsoft Entra ID.](media/how-to-source-ip-restoration/enable-conditional-access-signaling.png)](media/how-to-source-ip-restoration/enable-conditional-access-signaling.png#lightbox)

Caution

If you create Conditional Access policies based on IP location checks, and you disable Global Secure Access signaling, you might unintentionally block targeted end users from accessing the resources. If you must disable this feature, first delete any corresponding Conditional Access policies.

## Sign-in log behavior

To see source IP restoration in action, administrators can take the following steps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Reader](/en-us/azure/active-directory/roles/permissions-reference#security-reader).
2. Browse to **Entra ID** &gt; **Users** &gt; select one of your test users &gt; **Sign-in logs**.
3. When you enable source IP restoration, you see IP addresses that include the user's actual IP address.
    - When you disable source IP restoration, you can't see the user's actual IP address.

Sign-in log data might take some time to appear. This delay is normal because the data undergoes some processing before it appears.

[![Screenshot of the sign-in logs showing events with source IP restoration on, then off, then on again.](media/how-to-source-ip-restoration/user-log-data.png)](media/how-to-source-ip-restoration/user-log-data.png#lightbox)
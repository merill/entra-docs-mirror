---
layout: Conceptual
title: 'Tutorial: Enable source IP restoration - Global Secure Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/tutorial-microsoft-traffic-source-ip-restoration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to enable source IP restoration for Microsoft traffic in Global Secure Access and validate Microsoft Entra sign-in logs.
ms.topic: tutorial
ms.date: 2026-06-22T00:00:00.0000000Z
ms.subservice: entra-internet-access
ms.reviewer: jebley
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 92a9ace5-7f15-9a57-bf1e-15717be882ef
document_version_independent_id: 92a9ace5-7f15-9a57-bf1e-15717be882ef
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/tutorial-microsoft-traffic-source-ip-restoration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/tutorial-microsoft-traffic-source-ip-restoration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/tutorial-microsoft-traffic-source-ip-restoration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 47088178-99fc-d0bf-d191-39db092845ee
---

# Tutorial: Enable source IP restoration - Global Secure Access | Microsoft Learn

When users connect through a cloud-based proxy or security service edge (SSE) solution, downstream services can see the egress IP address of the cloud proxy instead of the user's original source IP. Without the original source IP, IP-based Conditional Access policies, risk detections, audit logs, and sign-in logs can be less accurate.

Source IP restoration detects and securely communicates the original egress IP address of the end user to Microsoft Entra ID and Microsoft Graph.

In this tutorial, you learn how to:

- Recognize what source IP restoration does and why it matters.
- Enable Global Secure Access signaling for Microsoft Entra ID and Microsoft Graph.
- Verify that Microsoft Entra sign-in logs show the user's actual source IP.

## Key concepts

Source IP restoration helps your organization:

- Continue to enforce IP-based location policies in Microsoft Entra Conditional Access.
- Improve the accuracy of Microsoft Entra ID Protection risk detections.
- Record accurate source IP information in Microsoft Entra sign-in logs and audit logs.

Source IP restoration is enabled by default for new tenants. If you enabled Global Secure Access features in your tenant before June 2025, you might need to explicitly enable source IP restoration.

## Step 1: Enable Global Secure Access signaling for Microsoft Entra ID and Microsoft Graph

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a Global Secure Access Administrator.
2. Browse to **Global Secure Access** &gt; **Settings** &gt; **Session management** &gt; **Adaptive Access**.
3. Select the toggle to **Enable Conditional Access Signaling for Microsoft Entra ID**.

    [![Screenshot that shows the Enable Conditional Access Signaling for Microsoft Entra ID toggle enabled.](media/tutorial-microsoft-traffic/conditional-access-signaling.png)](media/tutorial-microsoft-traffic/conditional-access-signaling.png#lightbox)

By enabling this setting, Microsoft Entra ID and Microsoft Graph receive the public egress source IP address of the user.

Caution

If your organization has active Conditional Access policies based on IP location checks, and you later disable Global Secure Access signaling, you might unintentionally block targeted end users from accessing resources. If you must disable this feature, first delete any corresponding Conditional Access policies.

## Step 2: Generate a sign-in log

1. On the device with the Global Secure Access client installed and running, open a browser.
2. Go to any application that's integrated with your Microsoft Entra ID tenant.
3. Complete the sign-in.

## Step 3: Verify sign-in log behavior

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a Security Reader.
2. Browse to **Entra ID** &gt; **Users**.
3. Select your test user.
4. Select **Sign-in logs**.
5. Select the sign-in event that you generated in the previous step.
6. Verify that the sign-in log includes the user's actual public egress IP address.

    [![Screenshot of sign-in activity details that show the user IP address and Through Global Secure Access set to Yes.](media/tutorial-microsoft-traffic/source-ip-restoration.png)](media/tutorial-microsoft-traffic/source-ip-restoration.png#lightbox)

Sign-in log data might take some time to appear. This delay is normal because the data undergoes processing before it appears.

## What you learned

In this exercise, you accomplished the following tasks:

- **Enabled Conditional Access signaling for Microsoft Entra ID:** Microsoft Entra ID and Microsoft Graph can receive the user's actual public egress IP.
- **Verified source IP restoration in sign-in logs:** You confirmed that Microsoft Entra sign-in logs reflect source IP information for sessions that use the Microsoft traffic profile.
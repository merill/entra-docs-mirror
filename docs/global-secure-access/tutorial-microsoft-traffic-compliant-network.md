---
layout: Conceptual
title: 'Tutorial: Enable the compliant network check - Global Secure Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/tutorial-microsoft-traffic-compliant-network
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to configure a Conditional Access policy that requires a compliant network with Global Secure Access.
ms.topic: tutorial
ms.date: 2026-06-22T00:00:00.0000000Z
ms.subservice: entra-internet-access
ms.reviewer: jebley
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 505c9e5c-d4f3-640a-0511-e1f999fa29b4
document_version_independent_id: 505c9e5c-d4f3-640a-0511-e1f999fa29b4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/tutorial-microsoft-traffic-compliant-network.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/tutorial-microsoft-traffic-compliant-network
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/tutorial-microsoft-traffic-compliant-network.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 1e229e64-d695-a0bf-103c-d8441b32e106
---

# Tutorial: Enable the compliant network check - Global Secure Access | Microsoft Learn

The compliant network check ensures users connect through the Global Secure Access service for your tenant before they access protected resources. This tenant-bound network signal lets you use location-based Conditional Access policies without maintaining egress IP address lists or routing traffic through a VPN for source IP anchoring.

In this tutorial, you learn how to:

- Recognize what the compliant network check does and why it matters.
- Create a Conditional Access policy that blocks access from anywhere except the compliant network.
- Validate that protected apps are blocked when the Global Secure Access client is disabled.

## Key concepts

Compliant network enforcement reduces the risk of token theft and replay attacks. Microsoft Entra ID performs authentication-plane enforcement when a user authenticates. If an adversary steals a session token and tries to replay it from a device that isn't connected to your organization's compliant network, Microsoft Entra ID denies the request and blocks further access.

The compliant network check is tenant-specific. If you define a policy that requires compliant network in one tenant, only users who connect through the Global Secure Access service for that tenant can satisfy the control.

The compliant network is different from IPv4, IPv6, or geographic named locations that you configure in Conditional Access. You don't need to review or maintain compliant network IP addresses or ranges.

Note

You must [enable source IP restoration](tutorial-microsoft-traffic-source-ip-restoration) in order to target the compliant network in Conditional Access.

## Step 1: Create the compliant network Conditional Access policy

A typical policy blocks all network locations except compliant networks. Start with a pilot group and a specific test application before you apply the policy broadly.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a Conditional Access Administrator.
2. Browse to **Entra ID** &gt; **Conditional Access**.
3. Select **Create new policy**.
4. Enter a meaningful policy name, such as **Require compliant network - Pilot**.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select a test user or pilot group.
6. Under **Target resources** &gt; **Include**, select a specific test application.
7. Under **Network**:
    1. Set **Configure** to **Yes**.
    2. Under **Include**, select **Any location**.
    3. Under **Exclude**, select **All Compliant Network locations**.
8. Under **Access controls** &gt; **Grant**, select **Block access**, and then select **Select**.
9. Confirm your settings and set **Enable policy** to **On**.
10. Select **Create**.

## Step 2: Validate the compliant network policy

1. On a pilot device with the Global Secure Access client installed and running, attempt to sign in to an app included in the Conditional Access policy configured in step 1. You should be able to sign in normally.
2. Pause the Global Secure Access client by right-clicking the application in the Windows system tray and selecting **Disable**.
3. Open a new browser session and try to sign in again.
4. Confirm that Microsoft Entra ID blocks access.

    [![Screenshot that shows a Microsoft sign-in error stating that the user can't access the resource right now.](media/tutorial-microsoft-traffic/compliant-network-block.png)](media/tutorial-microsoft-traffic/compliant-network-block.png#lightbox)
5. Re-enable the Global Secure Access client and confirm that access is restored.

If you're already signed in to an application, access isn't interrupted immediately. Microsoft Entra ID reevaluates the compliant network check the next time sign-in is required, such as when the application session expires. Use a fresh browser session or sign out first when you validate.

## What you learned

In this exercise, you accomplished the following tasks:

- **Confirmed Conditional Access signaling:** You verified that Microsoft Entra ID can evaluate the compliant network signal.
- **Created a compliant network Conditional Access policy:** Your pilot users must connect through Global Secure Access before they can reach apps integrated with Microsoft Entra ID.
- **Validated enforcement:** You confirmed that access succeeds with the Global Secure Access client running and is blocked when the client is disabled.
---
layout: Conceptual
title: Configure a Conditional Access Policy for Explicit Forward Proxy - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-conditional-access-policy-for-explicit-forward-proxy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to configure a Conditional Access policy for Explicit Forward Proxy.
ms.topic: how-to
ms.date: 2026-04-06T00:00:00.0000000Z
ms.reviewer: alexpav
locale: en-us
document_id: 303721b0-7fd5-78ed-4445-9437af9ada68
document_version_independent_id: 303721b0-7fd5-78ed-4445-9437af9ada68
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-configure-conditional-access-policy-for-explicit-forward-proxy.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-configure-conditional-access-policy-for-explicit-forward-proxy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-configure-conditional-access-policy-for-explicit-forward-proxy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 3a301b14-c346-59ab-ad0b-c63d9e2cd10e
---

# Configure a Conditional Access Policy for Explicit Forward Proxy - Global Secure Access | Microsoft Learn

Explicit Forward Proxy for Microsoft Entra Internet Access relies on IP affinity, among other mechanisms, for session management. Although a Conditional Access policy isn't required, we recommend that you configure one that restricts the use of Explicit Forward Proxy to networks that your organization trusts. Additionally, you use Conditional Access policies to assign the Microsoft Entra Internet Access security profiles to users.

## Prerequisites

- Administrators who configure and manage the Conditional Access policy for Explicit Forward Proxy must have at least the Conditional Access Administrator role.
- Enable Explicit Forward Proxy in the **Global Secure Access** &gt; **Session management** section of the Microsoft Entra admin center. Enabling Explicit Forward Proxy creates the workload identity in your tenant. This workload identity is the target for the Conditional Access policy.
- Configure a security profile in **Global Secure Access** &gt; **Secure** &gt; **Security Profiles**.
- Define a named location that represents known company networks in Microsoft Entra Conditional Access.

Note

As you configure groups in the following sections, keep in mind that Explicit Forward Proxy (preview) is not currently included in the **All internet resources with Global Secure Access** group.

## Scope Explicit Forward Proxy to known networks

1. Go to the Microsoft Entra admin center. Under **Entra ID**, select **Conditional Access**. Then, select **+Create new policy**.
2. Give the policy a name that aligns with your organization's policy naming standards. For example, use **GSA – Explicit Forward Proxy Known Locations Policy**.
3. Under **Assignments**, select **Users and Groups**. Typically, you would scope this policy to **All Users** and make exceptions (for example, your break-glass accounts) as necessary on the **Exclude** tab.
4. Under **Target Resources**, choose **Select resources** &gt; **Select specific resources**. Search for the **GSA-ExplicitForwardProxy** workload identity and select it.
5. On the **Network** tab of the new policy, select **Configure** and leave the defaults under **Include** – **Any network or location**. Under **Exclude**, select a named location that represents known networks from which you allow the use of Explicit Forward Proxy.
6. On the **Grant** tab, select **Block**.
7. Set the **Enable policy control** toggle to **On**, and then select the **Create** button.

## Assign security profiles to Explicit Forward Proxy

You assign security profiles by using Microsoft Entra Conditional Access policies. You can assign policies to Explicit Forward Proxy by explicitly targeting the **GSA-ExplicitForwardProxy** workload identity.

1. Go to the Microsoft Entra admin center. Under **Entra ID**, select **Conditional Access**. Then, select **+Create new policy**.
2. Give the policy a name that aligns with your organization's policy naming standards. For example, use **GSA – Explicit Forward Proxy Security Profile**.
3. Under **Assignments**, select **Users and Groups**. You can scope the policy to apply to all users, or you can create multiple policies to assign different security profiles to different groups of users. Configure exceptions (for example, your break-glass accounts) as necessary on the **Exclude** tab.
4. Under **Target Resources**, choose **Select resources** &gt; **Select specific resources**. Search for the **GSA-ExplicitForwardProxy** workload identity and select it.
5. On the **Session** tab of the new policy, select **Use Global Secure Access security profile**. You don't have to configure the **Grant** section.
6. Set the **Enable policy control** toggle to **On**, and then select the **Create** button.
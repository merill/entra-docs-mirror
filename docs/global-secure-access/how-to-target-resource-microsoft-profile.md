---
layout: Conceptual
title: Microsoft traffic Conditional Access policies - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-target-resource-microsoft-profile
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to apply Conditional Access policies to the Global Secure Access traffic.
ms.subservice: entra-internet-access
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: alexpav
ai-usage: ai-assisted
locale: en-us
document_id: 8b0b82d0-6aab-6ccf-fbad-d418dee9e2e7
document_version_independent_id: 8b0b82d0-6aab-6ccf-fbad-d418dee9e2e7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-target-resource-microsoft-profile.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-target-resource-microsoft-profile
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-target-resource-microsoft-profile.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: b20deb0c-2524-a945-de48-870bef0c449f
---

# Microsoft traffic Conditional Access policies - Global Secure Access | Microsoft Learn

## Overview

You apply Conditional Access policies to Global Secure Access traffic. With Conditional Access, you can require multifactor authentication and device compliance for accessing Microsoft resources.

This article describes how to apply Conditional Access policies to your Global Secure Access internet traffic.

## Prerequisites

- Administrators who interact with **Global Secure Access**features must have one or more of the following role assignments depending on the tasks they're performing.
    - The [Global Secure Access Administrator role](../identity/role-based-access-control/permissions-reference#global-secure-access-administrator) role to manage the Global Secure Access features.
    - The [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator) role to create and interact with Conditional Access policies.
- The product requires licensing. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

## Create a Conditional Access policy targeting Global Secure Access internet traffic

### Example policy

The following example policy targets all users except for your break-glass accounts and guest/external users, requiring multifactor authentication, device compliance, or a Microsoft Entra hybrid joined device for Global Secure Access internet traffic.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access**.
3. Select **Create new policy**.
4. Give your policy a name. Create a meaningful standard for the names of your policies.
5. Under **Assignments**, select the **Users and groups** link.

    1. Under **Include**, select **All users**.
    2. Under **Exclude**:
        1. Select **Users and groups** and choose your organization's emergency access or break-glass accounts.
        2. Select **Guest or external users** and select all checkboxes.
6. Under **Target resources** &gt; **Resources (formerly cloud apps)**.

    1. Choose **All internet resources with Global Secure Access**.

    ![Screenshot showing a Conditional Access policy targeting a traffic profile.](media/how-to-target-resource-microsoft-profile/target-resource-traffic-profile.png)

    Note

    To only enforce the *Internet Access traffic forwarding profile* and **not** the *Microsoft traffic forwarding profile* then choose **Select resources** and select **Internet resources** from the app picker and configure a security profile.
7. Under **Access controls** &gt; **Grant**.

    1. Select **Require multifactor authentication**, **Require device to be marked as compliant**, and **Require Microsoft Entra hybrid joined device**
    2. **For multiple controls** select **Require one of the selected controls**.
    3. Select **Select**.

After administrators confirm the policy settings using [report-only mode](../identity/conditional-access/concept-conditional-access-report-only), an administrator can move the **Enable policy** toggle from **Report-only** to **On**.

### User exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../identity/role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../identity/managed-identities-azure-resources/overview).
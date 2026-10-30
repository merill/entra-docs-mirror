---
layout: Conceptual
title: How to Apply Conditional Access Policies to Microsoft Entra Private Access Apps - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-target-resource-private-access-apps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Configure Conditional Access policies for Quick Access and Private Access apps to control access to internal resources based on user, device, and location conditions.
ms.subservice: entra-private-access
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: katabish
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 194a9c43-4205-8199-0e0c-397a7a8d8cc8
document_version_independent_id: 55aba542-834d-f764-5ce3-9500ccbe0d84
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-target-resource-private-access-apps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-target-resource-private-access-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-target-resource-private-access-apps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
platformId: 073e3604-1f17-5663-1c01-72bbeaf431e9
---

# How to Apply Conditional Access Policies to Microsoft Entra Private Access Apps - Global Secure Access | Microsoft Learn

## Overview

Applying Conditional Access policies to your Microsoft Entra Private Access apps is a powerful way to enforce security policies for your internal, private resources. You can apply Conditional Access policies to your Quick Access and Private Access apps from Global Secure Access.

This article describes how to apply Conditional Access policies to your Quick Access and Private Access apps.

## Prerequisites

- Administrators who interact with **Global Secure Access**features must have one or more of the following role assignments depending on the tasks they're performing.
    - The [Global Secure Access Administrator role](/en-us/azure/active-directory/roles/permissions-reference) role to manage the Global Secure Access features.
    - The [Conditional Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#conditional-access-administrator) to create and interact with Conditional Access policies.
- You need to have configured Quick Access or Private Access.
- The product requires licensing. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

### Known limitations

For detailed information about known issues and limitations, see [Known limitations for Global Secure Access](reference-current-known-limitations).

## Conditional Access and Global Secure Access

You can create a Conditional Access policy for your Quick Access or Private Access apps from Global Secure Access. Starting the process from Global Secure Access automatically adds the selected app as the **Target resource** for the policy. All you need to do is configure the policy settings.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#conditional-access-administrator).
2. Browse to **Global Secure Access** &gt; **Applications** &gt; **Enterprise applications.**
3. Select an application from the list.

    ![Screenshot that shows the Enterprise applications details.](media/how-to-target-resource-private-access-apps/enterprise-apps.png)
4. Select **Conditional Access** from the side menu. Any existing Conditional Access policies appear in a list.
5. Select **New policy**. The selected app appears in the **Target resources** details.
6. Configure the conditions, access controls, and assign users and groups as needed.

You can also apply Conditional Access policies to a group of applications based on custom attributes. For more information, go to [Filter for applications in Conditional Access policy](/en-us/azure/active-directory/conditional-access/concept-filter-for-applications).

### Assignments and Access controls example

Adjust the following policy details to create a Conditional Access policy requiring multifactor authentication, device compliance, or a Microsoft Entra hybrid joined device for your Quick Access application. The user assignments ensure that your organization's emergency access or break-glass accounts are excluded from the policy.

1. Under **Assignments**, select **Users**:
    1. Under **Include**, select **All users**.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
2. Under **Access controls** &gt; **Grant**:
    1. Select **Require multifactor authentication**, **Require device to be marked as compliant**, and **Require Microsoft Entra hybrid joined device**
3. Confirm your settings and set **Enable policy** to **Report-only**.

After administrators confirm the policy settings using [report-only mode](/en-us/azure/active-directory/conditional-access/howto-conditional-access-insights-reporting), an administrator can move the **Enable policy** toggle from **Report-only** to **On**.

### User exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../identity/role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../identity/managed-identities-azure-resources/overview).
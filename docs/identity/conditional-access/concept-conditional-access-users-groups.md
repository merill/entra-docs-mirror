---
layout: Conceptual
title: 'Conditional Access Setup: Users, Groups, Agents, and Workload Identities - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-conditional-access-users-groups
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Learn how to include or exclude users, groups, and workload identities in Conditional Access policies for secure and flexible access management.
ms.topic: concept-article
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: lhuangnorth
locale: en-us
document_id: cae7bc92-8489-ff66-9ce0-b4fab08eb7b8
document_version_independent_id: 55dfcb5c-62cd-8485-7d55-de3459cb2854
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/concept-conditional-access-users-groups.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/concept-conditional-access-users-groups
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/concept-conditional-access-users-groups.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 28ad6f9f-347d-fdf0-b6dc-4c2b790d8f98
---

# Conditional Access Setup: Users, Groups, Agents, and Workload Identities - Microsoft Entra ID | Microsoft Learn

## Overview

A Conditional Access policy includes a user, group, agent, or workload identity assignment as one of the signals in the decision process. These identities can be included or excluded from Conditional Access policies. Microsoft Entra ID evaluates all policies and ensures all requirements are met before granting access.

## Include users

This list typically includes all users an organization targets in a Conditional Access policy.

The following options are available when creating a Conditional Access policy.

- None
    - No users are selected
- All users
    - All users in the directory, including B2B guests.
- Select users and groups
    - Guest or external users
        - This selection lets you target Conditional Access policies to specific guest or external user types and tenants containing those users. There are [several different types of guest or external users that can be selected](../../external-id/authentication-conditional-access#conditional-access-for-external-users), and multiple selections can be made:
            - B2B collaboration guest users
            - B2B collaboration member users
            - B2B direct connect users
            - Local guest users, for example any user belonging to the home tenant with the user type attribute set to guest
            - Service provider users, for example a Cloud Solution Provider (CSP)
            - Other external users, or users not represented by the other user type selections
        - One or more tenants can be specified for the selected user types, or you can specify all tenants.
    - Directory roles
        - Lets admins select specific [built-in directory roles](../role-based-access-control/permissions-reference)to determine policy assignment. For example, organizations might create a more restrictive policy on users actively assigned a privileged role. Other role types aren't supported, including administrative unit-scoped roles and custom roles.
            - Conditional Access allows admins to select some [roles that are listed as deprecated](../role-based-access-control/permissions-reference#deprecated-roles). These roles still appear in the underlying API and we allow admins to apply policy to them.
    - Users and groups
        - Allows targeting of specific sets of users. For example, organizations can select a group that contains all members of the HR department when an HR app is selected as the cloud app. A group can be any type of user group in Microsoft Entra ID, including dynamic or assigned security and distribution groups. Policy is applied to nested users and groups.

Important

When selecting which users and groups are included in a Conditional Access Policy, there's a limit to the number of individual users that can be added directly to a Conditional Access policy. If many individual users need to be added to a Conditional Access policy, place them in a group and assign the group to the policy.

If users or groups belong to more than 2048 groups, their access might be blocked. This limit applies to both direct and nested group membership.

Warning

Conditional Access policies don't support users assigned a directory role [scoped to an administrative unit](../role-based-access-control/manage-roles-portal) or directory roles scoped directly to an object, like through [custom roles](../role-based-access-control/custom-create).

Note

When targeting policies to B2B direct connect external users, these policies are applied to B2B collaboration users accessing Teams or SharePoint Online who are also eligible for B2B direct connect. The same applies for policies targeted to B2B collaboration external users, meaning users accessing Teams shared channels have B2B collaboration policies apply if they also have a guest user presence in the tenant.

## Exclude users

When organizations both include and exclude a user or group, the user or group is excluded from the policy. The exclude action overrides the include action in a policy. Exclusions are commonly used for emergency access accounts or break-glass accounts. More information about emergency access accounts and why they're important can be found in the following articles:

- [Manage emergency access accounts in Microsoft Entra ID](../role-based-access-control/security-emergency-access)
- [Create a resilient access control management strategy with Microsoft Entra ID](../authentication/concept-resilient-controls)

The following options are available for exclusion when creating a Conditional Access policy.

- Guest or external users
    - This selection provides several choices that can be used to target Conditional Access policies to specific guest or external user types and specific tenants containing those types of users. There are [several different types of guest or external users that can be selected](../../external-id/authentication-conditional-access#conditional-access-for-external-users), and multiple selections can be made:
        - B2B collaboration guest users
        - B2B collaboration member users
        - B2B direct connect users
        - Local guest users, for example any user belonging to the home tenant with the user type attribute set to guest
        - Service provider users, for example a Cloud Solution Provider (CSP)
        - Other external users, or users not represented by the other user type selections
    - One or more tenants can be specified for the selected user types, or you can specify all tenants.
- Directory roles
    - Allows admins to select specific [Microsoft Entra directory roles](../role-based-access-control/permissions-reference) used to determine assignment.
- Users and groups
    - Allows targeting of specific sets of users. For example, organizations can select a group that contains all members of the HR department when an HR app is selected as the cloud app. A group can be any type of group in Microsoft Entra ID, including dynamic or assigned security and distribution groups. Policy is applied to nested users and groups.

### Preventing admin lockout

To prevent admin lockout, when creating a policy applied to **All users** and **All apps**, the following warning appears.

> 
> Don't lock yourself out! Apply a policy to a small set of users first to verify it behaves as expected. Also exclude at least one admin from this policy. This ensures that you still have access and can update a policy if a change is required. Review the affected users and apps.

By default, the policy provides an option to exclude the current user, but an admin can override it as shown in the following image.

![Warning, don't lock yourself out!](media/concept-conditional-access-users-groups/conditional-access-users-and-groups-lockout-warning.png)

If you find yourself locked out, see [What to do if you're locked out?](troubleshoot-conditional-access#what-to-do-if-youre-locked-out).

### External partner access

Conditional Access policies that target external users might interfere with service provider access, such as granular delegated admin privileges. Learn more in [Introduction to granular delegated admin privileges (GDAP)](/en-us/partner-center/gdap-introduction). For policies that are intended to target service provider tenants, use the **Service provider user** external user type available in the **Guest or external users** selection options.

## Agents (Preview)

Agents are first-class accounts within Microsoft Entra ID that provide unique identification and authentication capabilities for AI agents. Conditional Access policies targeting these objects have specific recommendations addressed in the article [Conditional Access and agent identities](agent-id)

Policy can be scoped to:

- All agent identities
- Select agents acting as users
- Select agent identities based on [attributes](../../fundamentals/custom-security-attributes-overview)
- Select individual agent identities

## Workload identities

A workload identity is an identity that allows an application or service principal access to resources, sometimes in the context of a user. Conditional Access policies can be applied to single tenant service principals registered in your tenant. Microsoft and third-party SaaS applications, including multitenant apps, are not covered by these policies. Managed identities aren't covered by policy.

Organizations can target specific workload identities to be included or excluded from policy.

For more information, see the article [Conditional Access for workload identities](workload-identity).
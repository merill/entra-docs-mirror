---
layout: Conceptual
title: Manage external access to resources with Conditional Access - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/7-secure-access-conditional-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Learn to use Conditional Access policies to secure external access to resources.
ms.topic: how-to
ms.date: 2023-02-23T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 808c5ef4-b3fb-eb0f-1d72-05137b9939b3
document_version_independent_id: d555df00-bd80-cc58-b1f6-2521ff0a2fb1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/7-secure-access-conditional-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/7-secure-access-conditional-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/7-secure-access-conditional-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 8dbd985f-b241-f336-b211-55471b8157f2
---

# Manage external access to resources with Conditional Access - Microsoft Entra | Microsoft Learn

Conditional Access interprets signals, enforces policies, and determines if a user is granted access to resources. In this article, learn about applying Conditional Access policies to external users. The article assumes you might not have access to entitlement management, a feature you can use with Conditional Access.

Learn more:

- [What is Conditional Access?](../identity/conditional-access/overview)
- [Plan a Conditional Access deployment](../identity/conditional-access/plan-conditional-access)
- [What is entitlement management?](../id-governance/entitlement-management-overview)

The following diagram illustrates signals to Conditional Access that trigger access processes.

![Diagram of Conditional Access signal input and resulting access processes.](media/secure-external-access/7-conditional-access-signals.png)

## Before you begin

This article is number 7 in a series of 10 articles. We recommend you review the articles in order. Go to the **Next steps** section to see the entire series.

## Align a security plan with Conditional Access policies

In the third article, in the set of 10 articles, there's guidance on creating a security plan. Use that plan to help create Conditional Access policies for external access. Part of the security plan includes:

- Grouped applications and resources for simplified access
- Sign-in requirements for external users

Important

Create internal and external user test accounts to test policies before applying them.

See article three, [Create a security plan for external access to resources](3-secure-access-plan)

## Conditional Access policies for external access

The following sections are best practices for governing external access with Conditional Access policies.

### Entitlement management or groups

If you can't use connected organizations in entitlement management, create a Microsoft Entra security group, or Microsoft 365 Group for partner organizations. Assign users from that partner to the group. You can use the groups in Conditional Access policies.

Learn more:

- [What is entitlement management?](../id-governance/entitlement-management-overview)
- [Manage Microsoft Entra groups and group membership](/en-us/entra/fundamentals/how-to-manage-groups)
- [Overview of Microsoft 365 Groups for administrators](/en-us/microsoft-365/admin/create-groups/office-365-groups?view=o365-worldwide&amp;preserve-view=true)

### Conditional Access policy creation

Create as few Conditional Access policies as possible. For applications that have the same access requirements, add them to the same policy.

Conditional Access policies apply to a maximum of 250 applications. If more than 250 applications have the same access requirement, create duplicate policies. For instance, Policy A applies to apps 1-250, Policy B applies to apps 251-500, and so on.

### Naming convention

Use a naming convention that clarifies policy purpose. External access examples are:

- ExternalAccess\_actiontaken\_AppGroup
- ExternalAccess\_Block\_FinanceApps

## Allow external access to specific external users

There are scenarios when it's necessary to allow access for a small, specific group.

Before you begin, we recommend you create a security group, which contains external users who access resources. See, [Manage Microsoft Entra groups and group membership](/en-us/entra/fundamentals/how-to-manage-groups).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access**.
3. Select **Create new policy**.
4. Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All guests and external users**.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts and the external users security group.
6. Under **Target resources** &gt; **Resources (formerly cloud apps)**, select the following options:
    1. Under **Include**, select **All resources (formerly 'All cloud apps')**
    2. Under **Exclude**, select applications you want to exclude.
7. Under **Access controls** &gt; **Grant**, select **Block access**, then select **Select**.
8. Select **Create** to create to enable your policy.

Note

After administrators confirm the settings using [report-only mode](../identity/conditional-access/howto-conditional-access-insights-reporting), they can move the **Enable policy** toggle from **Report-only** to **On**.

Learn more: [Manage emergency access accounts in Microsoft Entra ID](../identity/role-based-access-control/security-emergency-access)

## Service provider access

Conditional Access policies for external users might interfere with service provider access, for example granular delegated administrate privileges.

Learn more: [Introduction to granular delegated admin privileges (GDAP)](/en-us/partner-center/gdap-introduction)

## Conditional Access templates

Conditional Access templates are a convenient method to deploy new policies aligned with Microsoft recommendations. These templates provide protection aligned with commonly used policies across various customer types and locations.

Learn more: [Conditional Access templates (Preview)](../identity/conditional-access/concept-conditional-access-policy-common)
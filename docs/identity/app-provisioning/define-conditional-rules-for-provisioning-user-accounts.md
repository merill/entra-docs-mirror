---
layout: Conceptual
title: Scoping users or groups to be provisioned with scoping filters in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/define-conditional-rules-for-provisioning-user-accounts
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Learn how to use scoping filters to define attribute-based rules that determine which users or groups are provisioned in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2026-08-06T00:00:00.0000000Z
ms.reviewer: arvinh
zone_pivot_groups: app-provisioning-cross-tenant-synchronization
ai-usage: ai-assisted
locale: en-us
document_id: 9a77e752-0785-c3bd-9b33-f37bb7af6acd
document_version_independent_id: d865098d-299a-ddeb-6eed-9a1db3175de3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/define-conditional-rules-for-provisioning-user-accounts
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: e459dffc-f048-1cbe-7e0c-c7b8d84446b4
---

# Scoping users or groups to be provisioned with scoping filters in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Learn how to use scoping filters in the Microsoft Entra provisioning service to define attribute based rules. The rules are used to determine which users or groups are provisioned.

## Scoping filter use cases

::: zone pivot="app-provisioning"

You use scoping filters to prevent objects in applications that support automated user provisioning from being provisioned if an object doesn't satisfy your business requirements. A scoping filter allows you to include or exclude any users who have an attribute that matches a specific value. For example, when provisioning users from Microsoft Entra ID to a SaaS application used by a sales team, you can specify that only users with a "Department" attribute of "Sales" should be in scope for provisioning.

Scoping filters can be used differently depending on the type of provisioning connector:

- **Outbound provisioning from Microsoft Entra ID to SaaS applications**. When Microsoft Entra ID is the source system, [user and group assignments](../enterprise-apps/assign-user-or-group-access-portal) are the most common method for determining which users are in scope for provisioning. These assignments also are used for enabling single sign-on and provide a single method to manage access and provisioning. Scoping filters can be used optionally, in addition to assignments or instead of them, to filter users based on attribute values.

    Tip

    The more users and groups in scope for provisioning, the longer the synchronization process can take. Setting the scope to sync assigned users and groups, limiting the number of groups assigned to the app, and limiting the size of the groups will reduce the time it takes to synchronize everyone that is in scope.
- **Inbound provisioning from HCM applications to Microsoft Entra ID and Active Directory**. When an [HCM application such as Workday](../saas-apps/workday-tutorial) is the source system, scoping filters are the primary method for determining which users should be provisioned from the HCM application to Active Directory or Microsoft Entra ID.

By default, Microsoft Entra provisioning connectors don't have any attribute-based scoping filters configured.

::: zone-end

::: zone pivot="cross-tenant-synchronization"

When Microsoft Entra ID is the source system, [user and group assignments](../enterprise-apps/assign-user-or-group-access-portal) are the most common method for determining which users are in scope for provisioning. Reducing the number of users in scope improves performance and synchronizing assigned users and groups instead of synchronizing all users and groups is recommended.

Scoping filters can be used optionally, in addition to scoping by assignment. A scoping filter allows the Microsoft Entra provisioning service to include or exclude any users who have an attribute that matches a specific value. For example, when provisioning users from a sales team, you can specify that only users with a "Department" attribute of "Sales" should be in scope for provisioning.

::: zone-end

## Scoping filter construction

A scoping filter consists of one or more *clauses*. Clauses determine which users are allowed to pass through the scoping filter by evaluating each user's attributes. For example, you might have one clause that requires that a user's "State" attribute equals "New York", so only New York users are provisioned into the application.

A single clause defines a single condition for a single attribute value. If multiple clauses are created in a single scoping filter, they're evaluated together using "AND" logic. The "AND" logic means all clauses must evaluate to "true" in order for a user to be provisioned.

Finally, multiple scoping filters can be created for a single application. If multiple scoping filters are present, they're evaluated together by using "OR" logic. The "OR" logic means that if all the clauses in any of the configured scoping filters evaluate to "true", the user is provisioned.

Each user or group processed by the Microsoft Entra provisioning service is always evaluated individually against each scoping filter.

As an example, consider the following scoping filter:

![Scoping filter](media/define-conditional-rules-for-provisioning-user-accounts/scoping-filter.png)

According to this scoping filter, users must satisfy the following criteria to be provisioned:

- They must be in New York.
- They must work in the Engineering department.
- Their company employee ID must be between 1,000,000 and 2,000,000.
- Their job title must not be null or empty.

## Create scoping filters

Scoping filters are configured as part of the attribute mappings for each Microsoft Entra user provisioning connector. The following procedure assumes that you already set up automatic provisioning for [one of the supported applications](../saas-apps/tutorial-list) and are adding a scoping filter to it.

### Create a scoping filter

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).

::: zone pivot="app-provisioning"

1. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
2. Select the application for which you have configured automatic provisioning: for example, **ServiceNow**.

::: zone-end

::: zone pivot="cross-tenant-synchronization"

1. Browse to **Entra ID** &gt; **Cross-tenant Synchronization** &gt; **Configurations**.
2. Select your configuration.

::: zone-end

1. Select the **Provisioning** tab.
2. Under **Manage**, select **Scoping filters**. The scoping filters page displays two tabs: **Users** and **Groups**. Select the tab for the object type you want to scope.
3. Select the pencil icon to edit. The **Configure Scoping Filters** wizard opens and walks you through the following steps:

    a. **Scope Settings** — Configure which objects are enabled for provisioning.

    b. **Scope by assignment** — Choose whether to scope users and groups by assignment (recommended).

    c. **Users and groups** — Select the users and groups to include in scope. This option determines which users are assigned to the app. This is the same list of users and groups used for single sign-on. For more information, see [Assign users and groups to an application](../enterprise-apps/assign-user-or-group-access-portal).

    d. **Scope by attribute** — Define attribute-based scoping clauses. Select a source **Attribute Name**, an **Operator**, and an **Attribute Value** to match against.

    e. **Review** — Review your scoping filter configuration and confirm changes.
4. In the **Scope by attribute** step, define clauses to filter users based on attribute values. The following operators are supported:

    a. **&**. Clause returns "true" if the evaluated attribute exists in the input string value.

    b. **!&**. Clause returns "true" if the evaluated attribute does not exist in the input string value.

    c. **ENDS\_WITH**. Clause returns "true" if the evaluated attribute ends with the input string value.

    d. **EQUALS**. Clause returns "true" if the evaluated attribute matches the input string value exactly (case sensitive).

    e. **Greater\_Than.** Clause returns "true" if the evaluated attribute is greater than the value. The value specified on the scoping filter must be an integer and the attribute on the user must be an integer [0,1,2,...].

    f. **Greater\_Than\_OR\_EQUALS.** Clause returns "true" if the evaluated attribute is greater than or equal to the value. The value specified on the scoping filter must be an integer and the attribute on the user must be an integer [0,1,2,...].

    g. **Includes.** Clause returns "true" if the evaluated attribute contains the string value (case sensitive) as described [here](/en-us/dotnet/api/system.string.contains).

    h. **IS FALSE**. Clause returns "true" if the evaluated attribute contains a Boolean value of false.

    i. **IS NOT NULL**. Clause returns "true" if the evaluated attribute isn't empty.

    j. **IS NULL**. Clause returns "true" if the evaluated attribute is empty.

    k. **IS TRUE**. Clause returns "true" if the evaluated attribute contains a Boolean value of true.

    l. **NOT EQUALS**. Clause returns "true" if the evaluated attribute doesn't match the input string value (case sensitive).

    m. **NOT REGEX MATCH**. Clause returns "true" if the evaluated attribute doesn't match a regular expression pattern. It returns "false" if the attribute is null / empty.

    n. **REGEX MATCH**. Clause returns "true" if the evaluated attribute matches a regular expression pattern. For example: `([1-9][0-9])` matches any number between 10 and 99 (case sensitive).

    Important

    - The IsMemberOf filter is not supported currently.
    - The members attribute on a group is not supported currently.
    - Filtering is not supported for multi-valued attributes.
    - Scoping filters will return "false" if the value is null / empty.
5. Add more scoping clauses as needed within the **Scope by attribute** step.
6. On the **Review** step, verify your scoping filter configuration and select **Save**.

Important

Saving a new scoping filter triggers a new full sync for the application, where all users in the source system are evaluated again against the new scoping filter. If a user in the application was previously in scope for provisioning, but falls out of scope, their account is disabled or deprovisioned in the application. To override this default behavior, refer to [Skip deletion for user accounts that go out of scope](skip-out-of-scope-deletions).

## Common scoping filters

| Target Attribute | Operator | Value | Description |
| --- | --- | --- | --- |
| userPrincipalName | REGEX MATCH | `.*\@domain.com` | All users with `userPrincipal` that have the domain `@domain.com` are in scope for provisioning. |
| userPrincipalName | NOT REGEX MATCH | `.*\@domain.com` | All users with `userPrincipal` that has the domain `@domain.com` are out of scope for provisioning. |
| department | EQUALS | `sales` | All users from the sales department are in scope for provisioning |
| workerID | REGEX MATCH | `(1[0-9][0-9][0-9][0-9][0-9][0-9])` | All employees with `workerID` between 1000000 and 2000000 are in scope for provisioning. |
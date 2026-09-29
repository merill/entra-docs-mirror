---
layout: Conceptual
title: Provision a user or group on demand using the Microsoft Entra provisioning service - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/provision-on-demand
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Learn how to provision users on demand in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: arvinh
zone_pivot_groups: app-provisioning-cross-tenant-synchronization
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: c9db97ae-1ca2-e216-617a-52fdab9d007e
document_version_independent_id: c17d58bd-c122-2d60-e8e1-239b5dbb1af8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/provision-on-demand.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/provision-on-demand
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/provision-on-demand.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: c8b2c483-936c-a29d-90e7-5bdc533887a0
---

# Provision a user or group on demand using the Microsoft Entra provisioning service - Microsoft Entra ID | Microsoft Learn

Use on-demand provisioning to provision a user or group in seconds. Among other things, you can use this capability to:

- Troubleshoot configuration issues quickly.
- Validate expressions that you've defined.
- Test scoping filters.

## How to use on-demand provisioning

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).

::: zone pivot="app-provisioning"

1. Browse to **Entra ID** &gt; **Enterprise apps** &gt; select your application.
2. Select **Provisioning**.

::: zone-end

::: zone pivot="cross-tenant-synchronization"

1. Browse to **Entra ID** &gt; **External Identities** &gt; **Cross-tenant synchronization** &gt; **Configurations**

Note

Cross-tenant synchronization is currently not supported in [external tenants](/en-us/entra/external-id/customers/overview-customers-ciam).

1. Select your configuration, and then go to the **Provisioning** configuration page.

::: zone-end

1. Configure provisioning by providing your admin credentials.
2. Select **Provision on demand**.
3. Search for a user by first name, last name, display name, user principal name, or email address. Alternatively, you can search for a group and pick up to five users.

    Note

    For Cloud HR provisioning app (Workday / SuccessFactors to Active Directory / Microsoft Entra ID), the input value is different. For Workday scenario, please provide "WorkerID" or "WID" of the user in Workday. For SuccessFactors scenario, please provide "personIdExternal" of the user in SuccessFactors.
4. Select **Provision** at the bottom of the page.

    [![Screenshot that shows the Microsoft Entra admin center UI for provisioning a user on demand.](media/provision-on-demand/on-demand-provision-user.png)](media/provision-on-demand/on-demand-provision-user.png#lightbox)

## Understand the provisioning steps

The on-demand provisioning process attempts to show the steps that the provisioning service takes when provisioning a user. There are typically five steps to provision a user. One or more of those steps, explained in the following sections, are shown during the on-demand provisioning experience.

### Step 1: Test connection

The provisioning service attempts to authorize access to the target system by making a request for a "test user". The provisioning service expects a response that indicates that the service authorized to continue with the provisioning steps. This step is shown only when it fails. It's not shown during the on-demand provisioning experience when the step is successful.

#### Troubleshooting tips

- Ensure that you've provided valid credentials, such as the secret token and tenant URL, to the target system. The required credentials vary by application. For detailed configuration tutorials, see the [tutorial list](../saas-apps/tutorial-list).
- Make sure that the target system supports filtering on the matching attributes defined in the **Attribute mappings** pane. You might need to check the API documentation provided by the application developer to understand the supported filters.
- For System for Cross-domain Identity Management (SCIM) applications, use a REST API tool like cURL. Such tools help you ensure that the application responds to authorization requests in the way that the Microsoft Entra provisioning service expects. Have a look at an [example request](use-scim-to-provision-users-and-groups#request-3).

### Step 2: Import user

Next, the provisioning service retrieves the user from the source system. The user attributes that the service retrieves are used later to:

- Evaluate whether the user is in scope for provisioning.
- Check the target system for an existing user.
- Determine what user attributes to export to the target system.

#### View details

The **View details** section shows the properties of the user that were imported from the source system (for example, Microsoft Entra ID).

#### Troubleshooting tips

- Importing the user can fail when the matching attribute is missing on the user object in the source system. To resolve this failure, try one of these approaches:

    - Update the user object with a value for the matching attribute.
    - Change the matching attribute in your provisioning configuration.
- If an attribute that you expected is missing from the imported list, ensure that the attribute has a value on the user object in the source system. The provisioning service currently doesn't support provisioning null attributes.
- Make sure that the **Attribute mapping** page of your provisioning configuration contains the attribute that you expect.

### Step 3: Determine if user is in scope

Next, the provisioning service determines whether the user is in [scope](how-provisioning-works#scoping) for provisioning. The service considers aspects such as:

- Whether the user is assigned to the application.
- Whether scope is set to **Sync assigned** or **Sync all**.
- The scoping filters defined in your provisioning configuration.

#### View details

The **View details** section shows the scoping conditions that were evaluated. You might see one or more of the following properties:

- **Active in source system** indicates that the user has the property `IsActive` set to **true** in Microsoft Entra ID.
- **Assigned to application** indicates that the user is assigned to the application in Microsoft Entra ID.
- **Scope sync all** indicates that the scope setting allows all users and groups in the tenant.
- **User has required role** indicates that the user has the necessary roles to be provisioned into the application.
- **Scoping filters** are also shown if you have defined scoping filters for your application. The filter is displayed with the following format: {scoping filter title} {scoping filter attribute} {scoping filter operator} {scoping filter value}.

#### Troubleshooting tips

- Make sure that you've defined a valid scoping role. For example, avoid using the [Greater_Than operator](define-conditional-rules-for-provisioning-user-accounts#create-a-scoping-filter) with a noninteger value.
- If the user doesn't have the necessary role, review the [tips for provisioning users assigned to the default access role](application-provisioning-config-problem-no-users-provisioned#provisioning-users-assigned-to-the-default-access-role).

### Step 4: Match user between source and target

In this step, the service attempts to match the user that was retrieved in the import step with a user in the target system.

#### View details

The **View details** page shows the properties of the users that were matched in the target system. The context pane changes as follows:

- If no users are matched in the target system, no properties are shown.
- If one user matches in the target system, the properties of that user are shown.
- If multiple users match, the properties of both users are shown.
- If multiple matching attributes are part of your attribute mappings, each matching attribute is evaluated sequentially and the matched users for that attribute are shown.

#### Troubleshooting tips

- The provisioning service might not be able to match a user in the source system uniquely with a user in the target. Resolve this problem by ensuring that the matching attribute is unique.
- Make sure that the target system supports filtering on the attribute that's defined as the matching attribute.

### Step 5: Perform action

Finally, the provisioning service takes an action, such as creating, updating, deleting, or skipping the user.

Here's an example of what you might see after the successful on-demand provisioning of a user:

[![Screenshot that shows the successful on-demand provisioning of a user.](media/provision-on-demand/success-on-demand-provision.png)](media/provision-on-demand/success-on-demand-provision.png#lightbox)

#### View details

The **View details** section displays the attributes that were modified in the target system. This display represents the final output of the provisioning service activity and the attributes that were exported. If this step fails, the attributes displayed represent the attributes that the provisioning service attempted to modify.

#### Troubleshooting tips

- Failures for exporting changes can vary greatly. Check the [documentation for provisioning logs](../monitoring-health/howto-analyze-provisioning-logs#error-codes) for common failures.
- On-demand provisioning says the group or user can't be provisioned because they're not assigned to the application. There's a replication delay of up to a few minutes between when an object is assigned to an application and when that assignment is honored in on-demand provisioning. You may need to wait a few minutes and try again.

## Frequently asked questions

- **Do you need to turn provisioning off to use on-demand provisioning?** For applications that use a long-lived bearer token or a user name and password for authorization, no more steps are required. Applications that use OAuth for authorization currently require the provisioning job to be stopped before using on-demand provisioning. Applications such as G Suite, Box, and Slack fall into this category. Work is in progress to support on-demand provisioning for all applications without having to stop provisioning jobs.
- **How long does on-demand provisioning take?** On-demand provisioning typically takes less than 30 seconds.

## Known limitations

There are currently a few known limitations to on-demand provisioning. Post your [suggestions and feedback](https://aka.ms/appprovisioningfeaturerequest) so we can better determine what improvements to make next.

::: zone pivot="app-provisioning"

Note

The following limitations are specific to the on-demand provisioning capability. For information about whether an application supports provisioning groups, deletions, or other capabilities, check the tutorial for that application.

- On-demand provisioning of groups supports updating up to five members at a time. Connectors for cross-tenant synchronization, Workday, and so on. do not support group provisioning and as a result do not support on-demand provisioning of groups.
- The on-demand provisioning request API can only accept a single group with up to 5 members at a time.

::: zone-end

::: zone pivot="cross-tenant-synchronization"

- On-demand provisioning of groups is not supported for cross-tenant synchronization.

::: zone-end

- On-demand provisioning supports provisioning one user at a time through the Microsoft Entra admin center.
- Restoring a previously soft-deleted user in the target tenant with on-demand provisioning isn't supported. If you try to soft-delete a user with on-demand provisioning and then restore the user, it can result in duplicate users.
- On-demand provisioning of roles isn't supported.
- On-demand provisioning supports disabling users that have been unassigned from the application. However, it doesn't support disabling or deleting users that have been disabled or deleted from Microsoft Entra ID. Those users don't appear when you search for a user.
- On-demand provisioning doesn't support nested groups that aren't directly assigned to the application.
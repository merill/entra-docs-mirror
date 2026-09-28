---
layout: Conceptual
title: Change request settings for an access package in entitlement management - Microsoft Entra - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-access-package-request-policy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to change request settings for an access package in entitlement management.
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2025-06-26T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: b5c2265d-e9be-44a7-755d-3ab059151c01
document_version_independent_id: 7a012f04-aeb5-503f-468b-bfac562a4151
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-access-package-request-policy.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-access-package-request-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-access-package-request-policy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: 8f557db5-55b4-4a30-3b8a-299c7c8b2161
---

# Change request settings for an access package in entitlement management - Microsoft Entra - Microsoft Entra ID Governance | Microsoft Learn

As an access package manager, you can change the identities who can request an access package at any time by editing a policy for access package assignment requests, or adding a new policy to the access package. This article describes how to change the request settings for an existing access package assignment policy.

## Choose between one or multiple policies

The way you specify who can request an access package is with a policy. Before creating a new policy or editing an existing policy in an access package, you need to determine how many policies the access package needs.

When you create an access package, you can specify the request, approval and lifecycle settings, which are stored on the first policy of the access package. Most access packages have a single policy for identities to request access, but a single access package can have multiple policies. You would create multiple policies for an access package if you want to allow different sets of identities to be granted assignments with different request and approval settings.

For example, a single policy can't be used to assign internal and external identities to the same access package. However, you can create two policies in the same access package, one for internal identities and one for external identities. If there are multiple policies that apply to a user to request, they're prompted at the time of their request to select the policy they would like to be assigned to. The following diagram shows an access package with two policies.

![Diagram that illustrates multiple policies, along with multiple resource roles, can be contained within an access package.](media/entitlement-management-access-package-request-policy/access-package-policy.png)

In addition to policies for identities to request access, you can also have policies for [automatic assignment](entitlement-management-access-package-auto-assignment-policy), and policies for direct assignment by administrators or catalog owners.

### How many policies will I need?

| Scenario | Number of policies |
| --- | --- |
| I want all identities in my directory to have the same request and approval settings for an access package | One |
| I want all identities in certain connected organizations to be able to request an access package | One |
| I want to allow identities in my directory and also identities outside my directory to request an access package | Two |
| I want to specify different approval settings for some identities | One for each group of identities |
| I want some identities access package assignments to expire while other identities can extend their access | One for each group of identities |
| I want some identities to request access and other identities to be assigned access by an administrator | Two |
| I want some identities in my organization to receive access automatically, other identities in my organization to be able to request, and other identities to be assigned access by an administrator | Three |

For information about the priority logic that is used when multiple policies apply, see [Multiple policies](entitlement-management-troubleshoot#multiple-policies).

## Open an existing access package and add a new policy with different request settings

If you have a set of identities that should have different request and approval settings, you'll likely need to create a new policy. Follow these steps to start adding a new policy to an existing access package:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner and the Access package manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the Access packages page, open the access package you want to edit.
4. Select **Policies** and then **Add policy**.
5. On the **Basics** tab, type a name and a description for the policy.

    ![Create policy with name and description](media/entitlement-management-access-package-request-policy/policy-name-description.png)
6. Select **Next** to open the **Requests** tab.
7. Change the **Users who can request access** setting. Use the steps in the following sections to change the setting to one of the following options:

    - For users, service principals, and agent identities in your directory
    - For users not in your directory
    - None (administrator direct assignments only)

## For users, service principals, and agent identities in your directory

Follow these steps if you want to allow identities in your directory to be able to request this access package. When defining the request policy, you can specify individual identities, or more commonly groups of identities. For example, your organization could already have a group such as **All employees**. If that group is added in the policy for identities who can request access, then any member of that group can then request access.

1. In the **Users who can request access** section, select **For users, service principals, and agent identities in your directory**.

    When you select this option, new options appear to further refine who in your directory can request this access package.

    ![Access package - Requests - For users in your directory](media/entitlement-management-access-package-request-policy/for-users-in-your-directory.png)
2. Select one of the following options:

    | - | Description |
    | --- | --- |
    | **Specific users and groups** | Choose this option if you want only the users and groups in your directory that you specify to be able to request this access package. |
    | **All members (excluding guests)** | Choose this option if you want all member users in your directory to be able to request this access package. This option doesn't include any guest users you might have invited into your directory. |
    | **All users (including guests)** | Choose this option if you want all member users and guest users in your directory to be able to request this access package. |
    | **All Service principals** | Choose this option if you want all service principals in your directory to be able to request this access package. |
    | **All agents** | Choose this option if you want all agents in your directory to be able to have access assigned to them. |

    Guest users refer to external users that have been invited into your directory with [Microsoft Entra B2B](../external-id/what-is-b2b). For more information about the differences between member users and guest users, see [What are the default user permissions in Microsoft Entra ID?](../fundamentals/users-default-permissions).

    The **All Service principals** and **All agents** options require Microsoft Entra Agent ID. For more information, see [Governing agent identities](agent-id-governance-overview).
3. If you selected **Specific users and groups**, select **Add users and groups**.
4. In the Select users and groups pane, select the users and groups you want to add.

    ![Access package - Requests - Select users and groups](media/entitlement-management-access-package-request-policy/select-users-groups.png)
5. Select **Select** to add the users and groups.
6. If you want to require approval, use the steps in [Change approval settings for an access package in entitlement management](entitlement-management-access-package-approval-policy) to configure approval settings.
7. Go to the Who can request access section.

## For users not in your directory

**Users not in your directory** refers to users who are in another Microsoft Entra directory or domain. These users might not have yet been invited into your directory. Microsoft Entra directories must be configured to allow invitations in **Collaboration restrictions**. For more information, see [Configure external collaboration settings](../external-id/external-collaboration-settings-configure).

Note

A guest user account will be created for a user not yet in your directory whose request is approved or auto-approved. The guest will be invited, but will not receive an invite email. Instead, they'll receive an email when their access package assignment is delivered. By default, later when that guest user no longer has any access package assignments, because their last assignment has expired or been canceled, that guest user account will be blocked from sign in and subsequently deleted. If you want to have guest users remain in your directory indefinitely, even if they have no access package assignments, you can change the settings for your entitlement management configuration. For more information about the guest user object, see [Properties of a Microsoft Entra B2B collaboration user](../external-id/user-properties).

Follow these steps if you want to allow users not in your directory to request this access package:

1. In the **Users who can request access** section, select **For users not in your directory**.

    When you select this option, new options appear.

    ![Screenshot of access package selection for users not in your directory.](media/entitlement-management-access-package-request-policy/for-users-not-in-your-directory.png)
2. Select whether the users who can request access are required to be affiliated with an existing connected organization, or can be anyone on the Internet. A connected organization is one that you have a preexisting relationship with, which might have an external Microsoft Entra directory or another identity provider. Select one of the following options:

    | - | Description |
    | --- | --- |
    | **Specific connected organizations** | Choose this option if you want to select from a list of organizations that your administrator previously added. All users from the selected organizations can request this access package. |
    | **All configured connected organizations** | Choose this option if all users from all your configured connected organizations can request this access package. Only users from configured connected organizations can request access packages, so if a user isn't from a Microsoft Entra tenant, domain or identity provider associated with an existing connected organization, they won't be able to request. |
    | **All users (All connected organizations + any new external users)** | Choose this option if any user on the internet should be able to request this access package. If they don't belong to a connected organization in your directory, a connected organization will automatically be created for them when they request the package. The automatically created connected organization is in a **proposed** state. For more information about the proposed state, see [State property of connected organizations](entitlement-management-organization#state-property-of-connected-organizations). |
3. If you selected **Specific connected organizations**, select **Add directories** to select from a list of connected organizations that your administrator previously added.
4. Type the name or domain name to search for a previously connected organization.

    ![Access package - Requests - Select directories](media/entitlement-management-access-package-request-policy/select-directories.png)

    If the organization you want to collaborate with isn't in the list, you can ask your administrator to add it as a connected organization. For more information, see [Add a connected organization](entitlement-management-organization).
5. Once you've selected all your connected organizations, select **Select**.

    Note

    All users from the selected connected organizations can request this access package. For a connected organization that has a Microsoft Entra directory, users from all verified domains associated with the Microsoft Entra directory can request, unless those domains are blocked by the Azure B2B allow or blocklist. For more information, see [Allow or block invitations to B2B users from specific organizations](../external-id/allow-deny-list).
6. Next, use the steps in [Change approval settings for an access package in entitlement management](entitlement-management-access-package-approval-policy) to configure approval settings to specify who should approve requests from users not in your organization.
7. Go to the Who can request access section.

## None (administrator direct assignments only)

Follow these steps if you want to bypass access requests and allow administrators to directly assign specific users to this access package. Users won't have to request the access package. You can still set lifecycle settings, but there are no request settings.

1. In the **Users who can request access** section, select **None (administrator direct assignments only)**.

    ![Screenshot of an access package for the selection &quot;None administrator direct assignments only&quot;.](media/entitlement-management-access-package-request-policy/none-admin-direct-assignments-only.png)

    After you create the access package, you can directly assign specific users, including guest users who are already in the directory. However, if **Who can get access** is set to **None (administrator direct assignments only)**, an external user who isn't yet in your directory can't be invited through the assignment. To invite an external user through an access package assignment, use a policy that allows users not in your directory. The external user must be within the scope of the policy, such as being part of a configured connected organization in scope or being allowed by **All users (All connected organizations + any external user)**. If you don't want external users to request the access package, leave all options under **Who can request access** unchecked except for **Admin**. For information about directly assigning a user, see [View, add, and remove assignments for an access package](entitlement-management-access-package-assignments).
2. Skip to the Who can request access section.

Note

When assigning users to an access package, administrators will need to verify that the users are eligible for that access package based on the existing policy requirements. Otherwise, the users won't successfully be assigned to the access package. If the access package contains a policy that requires user requests to be approved, users can't be directly assigned to the package without necessary approval(s) from the designated approver(s).

## Open and edit an existing policy's request settings

To change the request and approval settings for an access package, you need to open the corresponding policy with those settings. Follow these steps to open and edit the request settings for an access package assignment policy:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner and the Access package manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the Access packages page, open the access package whose policy request settings you want to edit.
4. Select **Policies** and then select the policy you want to edit.

    The Policy details pane opens at the bottom of the page.

    ![Access package - Policy details pane](media/entitlement-management-shared/policy-details.png)
5. Select **Edit** to edit the policy.

    ![Access package - Edit policy](media/entitlement-management-shared/policy-edit.png)
6. Select the **Requests** tab to open the request settings.
7. Use the steps in the previous sections to change the request settings as needed.
8. Go to the Who can request access section.

## Who can request access

Note

Previously, a setting called "*Enable new requests and assignments*" controlled self-service access requests. This capability is now more accurately reflected by the "*Self*" option.

1. After choosing who can get access and the scope you are able to specify who can request access to the access package. Here you can grant Self, Admin, or Manager the ability to request access to the access package.

    You can always enable it in the future after you have finished creating the access package.

    If you selected **None (administrator direct assignments only)** then the who can request access section boxes are not selectable.

    ![Screenshot of access package policy who can request access.](media/entitlement-management-access-package-approval-policy/enable-requests.png)
2. Select **Next**.
3. If you want to require requestors to provide additional information when requesting access to an access package, use the steps in [Change approval and requestor information settings for an access package in entitlement management](entitlement-management-access-package-approval-policy#collect-additional-requestor-information-for-approval) to configure requestor information.
4. Configure lifecycle settings.
5. If you're editing a policy select **Update**. If you're adding a new policy, select **Create**.

## Create an access package assignment policy programmatically

There are two ways to create an access package assignment policy programmatically, through Microsoft Graph and through the PowerShell cmdlets for Microsoft Graph.

### Create an access package assignment policy through Graph

You can create a policy using Microsoft Graph. A user in an appropriate role with an application that has the delegated `EntitlementManagement.ReadWrite.All` permission, an application in a catalog role, or an application with the `EntitlementManagement.ReadWrite.All` application permission, can call the [create an assignmentPolicy](/en-us/graph/api/entitlementmanagement-post-assignmentpolicies?tabs=http&amp;view=graph-rest-1.0&amp;preserve-view=true) API.

### Create an access package assignment policy through PowerShell

You can also create an access package in PowerShell with the cmdlets from the [Microsoft Graph PowerShell cmdlets for Identity Governance](https://www.powershellgallery.com/packages/Microsoft.Graph.Identity.Governance/) module version 2.1.x or later module version.

This following script illustrates creating a policy for direct assignment to an access package. In this policy, only the administrator can assign access, and there are no approvals or access reviews. See [Create an automatic assignment policy](entitlement-management-access-package-auto-assignment-policy#create-an-access-package-assignment-policy-through-powershell) for an example of how to create an automatic assignment policy, and [create an assignmentPolicy](/en-us/graph/api/entitlementmanagement-post-assignmentpolicies?tabs=http&amp;view=graph-rest-1.0&amp;preserve-view=true) for more examples.

```powershell
Connect-MgGraph -Scopes "EntitlementManagement.ReadWrite.All"

$apid = "00001111-aaaa-2222-bbbb-3333cccc4444"

$params = @{
    displayName = "New Policy"
    description = "policy for assignment"
    allowedTargetScope = "notSpecified"
    specificAllowedTargets = @(
    )
    expiration = @{
        endDateTime = $null
        duration = $null
        type = "noExpiration"
    }
    requestorSettings = @{
        enableTargetsToSelfAddAccess = $false
        enableTargetsToSelfUpdateAccess = $false
        enableTargetsToSelfRemoveAccess = $false
        allowCustomAssignmentSchedule = $true
        enableOnBehalfRequestorsToAddAccess = $false
        enableOnBehalfRequestorsToUpdateAccess = $false
        enableOnBehalfRequestorsToRemoveAccess = $false
        onBehalfRequestors = @(
        )
    }
    requestApprovalSettings = @{
        isApprovalRequiredForAdd = $false
        isApprovalRequiredForUpdate = $false
        stages = @(
        )
    }
    accessPackage = @{
        id = $apid
    }
}

New-MgEntitlementManagementAssignmentPolicy -BodyParameter $params
```

## Prevent requests from identities with incompatible access

In addition to the policy checks on who can request, you might wish to further restrict access, in order to avoid an identity who already has some access - via a group or another access package - from obtaining excessive access.

If you want to configure that an identity can't request an access package, if they already have an assignment to another access package, or are a member of a group, use the steps at [Configure separation of duties checks for an access package](entitlement-management-access-package-incompatible).
---
layout: Conceptual
title: Privileged Identity Management (PIM) for Groups - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/concept-pim-for-groups
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: How to manage Microsoft Entra Privileged Identity Management (PIM) for Groups.
ms.topic: overview
ms.date: 2026-04-23T00:00:00.0000000Z
ms.custom: pim, sfi-ga-nochange
locale: en-us
document_id: 1949aee4-d229-ff99-c44c-fdce838e09a8
document_version_independent_id: 12ac1eb6-a875-4da2-4eaf-f7d26a40fd6b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/concept-pim-for-groups.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/concept-pim-for-groups
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/concept-pim-for-groups.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 2e8f72e7-0c73-6da5-0663-76be7d76e3c5
---

# Privileged Identity Management (PIM) for Groups - Microsoft Entra ID Governance | Microsoft Learn

## Overview

Microsoft Entra ID allows you to grant users just-in-time membership and ownership of groups through Privileged Identity Management (PIM) for Groups. Groups can be used to control access to a variety of scenarios, including Microsoft Entra roles, Azure roles, Azure SQL, Azure Key Vault, Intune, other application roles, and third-party applications.

## What is PIM for Groups?

PIM for Groups is part of Microsoft Entra Privileged Identity Management – alongside PIM for Microsoft Entra roles and PIM for Azure Resources, PIM for Groups enables users to activate the ownership or membership of a Microsoft Entra security group or Microsoft 365 group. Groups can be used to govern access to various scenarios that include Microsoft Entra roles, Azure roles, Azure SQL, Azure Key Vault, Intune, other application roles, and third-party applications.

With PIM for Groups you can use policies similar to ones you use in PIM for Microsoft Entra roles and PIM for Azure Resources: you can require approval for membership or ownership activation, enforce multifactor authentication (MFA), require justification, limit maximum activation time, and more. Each group in PIM for Groups has two policies: one for activation of membership and another for activation of ownership in the group. Up until January 2023, the PIM for Groups feature was called “Privileged Access Groups”.

Note

For groups used for elevating into Microsoft Entra roles, we recommend that you require an approval process for eligible member assignments. Assignments that can be activated without approval can leave you vulnerable to a security risk from less-privileged administrators, who might be able to reset a user's credentials and then activate the assignment on their behalf.

Confirm that groups used for role elevation are created as [role-assignable](../../identity/role-based-access-control/groups-concept). You must be assigned at least the Privileged Authentication Administrator role to change the credentials of members and owners of a role-assignable group.

## PIM for Groups and ownership deactivation

Microsoft Entra ID doesn't allow you to remove the last (active) owner of a group. For example, consider a group that has active owner A and eligible owner B. If user B activates their ownership with PIM and then later user A is removed from the group or from the tenant, deactivation of user B's ownership won't succeed.

PIM will try to deactivate user B's ownership for up to 30 days. If another active owner C is added to the group, the deactivation will succeed. If deactivation is unsuccessful after 30 days, PIM will stop trying to deactivate user B's ownership and user B will continue to be an active owner.

## What are Microsoft Entra role-assignable groups?

When working with Microsoft Entra ID, you can assign a Microsoft Entra security group or Microsoft 365 group to a Microsoft Entra role. This is possible only with groups that are created as role-assignable.

To learn more about Microsoft Entra role-assignable groups, see [Create a role-assignable group in Microsoft Entra ID](../../identity/role-based-access-control/groups-create-eligible).

Role-assignable groups benefit from extra protections compared to non-role-assignable groups:

- **Role-assignable groups** - only the Global Administrator, Privileged Role Administrator, or the group Owner can manage the group. Also, no other users can change the credentials of the members and owners of the group, including eligible members and owners who haven't activated yet. This feature helps prevent an admin from elevating to a higher privileged role without going through a request and approval procedure.
- **Non-role-assignable groups** - various Microsoft Entra roles can manage these groups – that includes Exchange Administrators, Groups Administrators, User Administrators. Also, various Microsoft Entra roles can change the credentials of the users who are (active) members of the group – that includes Authentication Administrators, Helpdesk Administrators, User Administrators.

To learn more about Microsoft Entra built-in roles and their permissions, see [Microsoft Entra built-in roles](../../identity/role-based-access-control/permissions-reference).

The Microsoft Entra role-assignable group feature isn't part of Microsoft Entra Privileged Identity Management (Microsoft Entra PIM). For more information on licensing, see [Microsoft Entra ID Governance licensing fundamentals](../licensing-fundamentals).

## Relationship between role-assignable groups and PIM for Groups

Groups in Microsoft Entra ID can be classified as either role-assignable or non-role-assignable. Additionally, any group can be enabled or not enabled for use with Microsoft Entra Privileged Identity Management (PIM) for Groups. These are independent properties of the group. Any Microsoft Entra security group and any Microsoft 365 group (except dynamic membership groups and groups synchronized from on-premises environment) can be enabled in PIM for Groups. The group doesn't have to be role-assignable group to be enabled in PIM for Groups.

If you want to assign a Microsoft Entra role to a group, it has to be role-assignable. Even if you don't intend to assign a Microsoft Entra role to the group but the group provides access to sensitive resources, it's still recommended to consider creating the group as role-assignable. This is because of extra protections role-assignable groups have – see “What are Microsoft Entra role-assignable groups?” in the section above.

Important

Up until January 2023, it was required that every Privileged Access Group (former name for this PIM for Groups feature) had to be role-assignable group. This restriction is currently removed. Because of that, it's now possible to enable more than 500 groups per tenant in PIM, but only up to 500 groups can be role-assignable.

## Make a group of users eligible for a Microsoft Entra role

There are two ways to make a group of users eligible for Microsoft Entra role:

1. Make active assignments of users to the group, and then assign the group to a role as eligible for activation.
2. Make active assignment of a role to a group and assign users to be eligible to group membership.

To provide a group of users with just-in-time access to Microsoft Entra roles with permissions in SharePoint, Exchange, or Microsoft Purview portal (for example, Exchange Administrator role), be sure to make active assignments of users to the group, and then assign the group to a role as eligible for activation (Option #1 above). If you choose to make active assignment of a group to a role and assign users to be eligible to group membership instead, it might take significant time to have all permissions of the role activated and ready to use.

In other words, to avoid activation delays, use [PIM for Microsoft Entra roles](pim-how-to-add-role-to-user) instead of PIM for Groups to provide just-in-time access to SharePoint, Exchange, or Microsoft Purview portal. For more information, see [Error when accessing SharePoint or OneDrive after role activation in PIM](/en-us/sharepoint/troubleshoot/administration/access-denied-to-pim-user-accounts).

## Privileged Identity Management and group nesting

In Microsoft Entra ID, role-assignable groups can’t have other groups nested inside them. To learn more, see [Use Microsoft Entra groups to manage role assignments](../../identity/role-based-access-control/groups-concept). This is applicable to active membership: one group can't be an active member of another group that is role-assignable.

One group can be an eligible member of another group, even if one of those groups is role-assignable.

If a user is an active member of Group A, and Group A is an eligible member of Group B, the user can activate their membership in Group B. This activation is only for the user that requested the activation for, it doesn't mean that the entire Group A becomes an active member of Group B.

## Privileged Identity Management and app provisioning

If the group is configured for [app provisioning](../../identity/app-provisioning/), activation of group membership triggers provisioning of group membership (and user account itself if it wasn’t provisioned previously) to the application using SCIM protocol.

There's functionality that triggers provisioning right after group membership is activated in PIM. Provisioning configuration depends on the application. Generally, it's recommended to have at least two groups assigned to the application. Depending on the number of roles in your application, you might choose to define additional “privileged groups”:

| Group | Purpose | Members | Group membership | Role assigned in the application |
| --- | --- | --- | --- | --- |
| All users group | Ensure that all users that need access to the application are constantly provisioned to the application. | All users that need to access application. | Active | None, or low-privileged role |
| Privileged group | Provide just-in-time access to privileged role in the application. | Users that need to have just-in-time access to privileged role in the application. | Eligible | Privileged role |

**Key considerations**

- How long does it take to have a user provisioned to the application?
    - When a user is added to a group in Microsoft Entra ID outside of activating their group membership using Microsoft Entra Privileged Identity Management (PIM):
        - The group membership is provisioned in the application during the next synchronization cycle. The synchronization cycle runs every 40 minutes.
    - When a user activates their group membership in Microsoft Entra PIM:
        - The group membership is provisioned in 2 – 10 minutes. When there is a high rate of requests at one time, requests are throttled at a rate of five requests per 10 seconds.
        - For the first five users within a 10-second period activating their group membership for a specific application, group membership is provisioned in the application within 2-10 minutes.
        - For the sixth user and above within a 10-second period activating their group membership for a specific application, group membership is provisioned to the application in the next synchronization cycle. The synchronization cycle runs every 40 minutes. The throttling limits are per enterprise application.
- If the user is unable to access the necessary group in the target application, review the PIM logs and provisioning logs to ensure that the group membership was updated successfully. Depending on how the target application has been architected, it might take additional time for the group membership to take effect in the application.
- Using [Azure Monitor](/en-us/entra/identity/app-provisioning/application-provisioning-log-analytics), you can create alerts for failures.
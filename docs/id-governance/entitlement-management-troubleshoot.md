---
layout: Conceptual
title: Troubleshoot entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-troubleshoot
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn about some items you should check to help you troubleshoot Microsoft Entra entitlement management.
editor: markwahl-msft
ms.subservice: entitlement-management
ms.topic: troubleshooting
ms.date: 2025-06-02T00:00:00.0000000Z
ms.reviewer: markwahl-msft
ms.custom: sfi-ga-nochange
locale: en-us
document_id: 86dcc449-d02e-b6da-8cf3-e3bd4ed59665
document_version_independent_id: 8cb0a6f4-4ed2-18e0-5948-fb49986023d5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-troubleshoot.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-troubleshoot
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-troubleshoot.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
platformId: bdd0489f-28bd-9ea1-b6a8-f7ae42e2c03c
---

# Troubleshoot entitlement management - Microsoft Entra ID Governance | Microsoft Learn

This article describes some items you should check to help you troubleshoot entitlement management.

## Administration

- If you get an access denied message when configuring entitlement management, and you're a Global Administrator, ensure that your directory has a [Microsoft Entra ID P2 or Microsoft Entra ID Governance (or EMS E5) license](entitlement-management-overview#license-requirements). If you've recently renewed an expired Microsoft Entra ID P2 or Microsoft Entra ID Governance subscription, then it may take 8 hours for this license renewal to be visible.
- If your tenant's Microsoft Entra ID P2 or Microsoft Entra ID Governance license expires, then you won't be able to process new access requests or perform access reviews.
- If you get an access denied message when creating or viewing access packages, and you're a member of a Catalog creator group, you must [create a catalog](entitlement-management-catalog-create) prior to creating your first access package.

## Resources

- Roles for applications are defined by the application itself and are managed in Microsoft Entra ID. If an application doesn't have any resource roles, entitlement management assigns users to a **Default Access** role.

    The Microsoft Entra admin center might also show service principals for services that can't be selected as applications. In particular, **Exchange Online** and **SharePoint Online** are services, not applications that have resource roles in the directory, so they can't be included in an access package. Instead, use group-based licensing to establish an appropriate license for a user who needs access to those services.
- Applications that only support Personal Microsoft Account users for authentication, and don't support organizational accounts in your directory, don't have application roles, and can't be added to access package catalogs.
- For a group to be a resource in an access package, it must be able to be modifiable in Microsoft Entra ID. Groups that originate in an on-premises Active Directory can't be assigned as resources because their owner or member attributes can't be changed in Microsoft Entra ID. Groups that originate in Exchange Online as Distribution groups can't be modified in Microsoft Entra ID either.
- SharePoint Online document libraries and individual documents can't be added as resources. Instead, create a [Microsoft Entra security group](/en-us/entra/fundamentals/how-to-manage-groups), include that group and a site role in the access package, and in SharePoint Online use that group to control access to the document library or document.
- If there are users that have already been assigned to a resource that you want to manage with an access package, be sure that the users are assigned to the access package with an appropriate policy. For example, you might want to include a group in an access package that already has users in the group. If those users in the group require continued access, they must have an appropriate policy for the access packages so that they don't lose their access to the group. You can assign the access package by either asking the users to request the access package containing that resource, or by directly assigning them to the access package. For more information, see [Change request and approval settings for an access package](entitlement-management-access-package-request-policy).
- When you remove a member of a team, they're removed from the Microsoft 365 Group as well. Removal from the team's chat functionality might be delayed. For more information, see [Group membership](/en-us/microsoftteams/office-365-groups#group-membership).

## Access packages

- If you attempt to delete an access package or policy and see an error message that says there are active assignments, if you don't see any users with assignments, check to see whether any recently deleted users still have assignments. During the 30-day window after a user is deleted, the user account can be restored.

## External users

- When an external user wants to request access to an access package, make sure they're using the **My Access portal link** for the access package. For more information, see [Share link to request an access package](entitlement-management-access-package-settings). If an external user just visits **myaccess.microsoft.com** and doesn't use the full My Access portal link, then they see the access packages available to them in their own organization and not in your organization.
- If an external user is unable to request access to an access package or is unable to access resources, be sure to check your [settings for external users](entitlement-management-external-users#settings-for-external-users).
- If a new external user that hasn't previously signed in your directory receives an access package including a SharePoint Online site, their access package shows as not fully delivered until their account is provisioned in SharePoint Online. For more information about sharing settings, see [Review your SharePoint Online external sharing settings](entitlement-management-external-users#review-your-sharepoint-online-external-sharing-settings).

## Requests

- When a user wants to request access to an access package, be sure that they're using the **My Access portal link** for the access package. For more information, see [Share link to request an access package](entitlement-management-access-package-settings).
- If you open the My Access portal with your browser set to in-private or incognito mode, this might conflict with the sign-in behavior. We recommend that you don't use in-private or incognito mode for your browser when you visit the My Access portal.
- When a user who isn't yet in your directory signs in to the My Access portal to request an access package, be sure they authenticate using their organizational account. The organizational account can be either an account in the resource directory, or in a directory that is included in one of the policies of the access package. If the user's account isn't an organizational account, or the directory where they authenticate isn't included in the policy, then the user won't see the access package. For more information, see [Request access to an access package](entitlement-management-request-access).
- If a user is blocked from signing in to the resource directory, they won't be able to request access in the My Access portal. Before the user can request access, you must remove the sign-in block from the user's profile. To remove the sign-in block, in the Microsoft Entra admin center, browse to **Entra ID** &gt; **Users**, select the user, select **Edit properties**, and then select the **Settings** section and check the **Account enabled** box. For more information, see [Add or update a user's profile information using Microsoft Entra ID](../fundamentals/how-to-manage-user-profile-info). You can also check if the user was blocked due to an [Conditional Access policy](../identity/conditional-access/concept-conditional-access-users-groups#exclude-users).
- In the My Access portal, if a user is both a requestor and an approver, they won't see their request for an access package on the **Approvals** page. This behavior is intentional - a user can't approve their own request. Ensure that the access package they're requesting has additional approvers configured on the policy. For more information, see [Change request and approval settings for an access package](entitlement-management-access-package-request-policy).

### View a request's delivery errors

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner, Access package manager, and Access package assignment manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access packages**.
3. Select **Requests**.
4. Select the request you want to view.

    If the request has any delivery errors, the request status is **Undelivered** or **Partially delivered**.

    If there are any delivery errors, a count of delivery errors are displayed in the request's detail pane.
5. Select the count to see all of the request's delivery errors.

### Reprocess a request

If an error is met after triggering an access package reprocess request, you must wait while the system reprocesses the request. The system tries multiple times to reprocess for several hours, so you can't force reprocessing during this time.

You can only reprocess a request that has a status of **Delivery failed** or **Partially delivered** and a completed date of less than one week. The **reprocess** button would be grayed out otherwise.

![Reprocess button grayed out](media/entitlement-management-troubleshoot/cancel-reprocess-grayedout.png)

- If the error is fixed during the trials window, the request status changes to **Delivering**. The request reprocesses without further actions from the user.
- If the error wasn't fixed during the trials window, the request status can be **Delivery failed** or **partially delivered**. You can then use the **reprocess** button. You have seven days to reprocess the request.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner, Access package manager, and Access package assignment manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access packages** to open an access package.
3. Select **Requests**.
4. Select the request you want to reprocess.
5. In the request details pane, select **Reprocess request**.

    ![Reprocess a failed request](media/entitlement-management-troubleshoot/reprocess-request.png)

### Cancel a pending request

You can only cancel a pending request that hasn't yet been delivered or whose delivery has failed. The **cancel** button would be grayed out otherwise.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner, Access package manager, and Access package assignment manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access packages** to open an access package.
3. Select **Requests**.
4. Select the request you want to cancel.
5. In the request details pane, select **Cancel request**.

## Automatic assignment policies

- Each automatic assignment policy can include at most 15,000 users in scope of its rule. Other users in scope of the rule might not be assigned access.

## Multiple policies

- Entitlement management follows least privilege best practices. When a user requests access to an access package that has multiple policies that apply, entitlement management includes logic to help ensure stricter or more specific policies are prioritized over generic policies. If a policy is generic, entitlement management might not display the policy to the requestor or might automatically select a stricter policy.
- For example, consider an access package with two policies for users in the directory, in which both policies apply to the requestor. The first policy is for specific users that include the requestor. The second policy is for all users in the directory. In this scenario, the first policy is automatically selected for the requestor because it's more strict. The requestor isn't given the option to select the second policy.
- When multiple policies apply, the policy that is automatically selected or the policies that are displayed to the requestor is based on the following priority logic:

    | Policy priority | Scope |
    | --- | --- |
    | P1 | Specific users and groups in your directory OR Specific connected organizations |
    | P2 | All members in your directory (excluding guests) |
    | P3 | All users in your directory (including guests) OR Specific connected organizations |
    | P4 | All configured connected organizations OR All users (all connected organizations + any new external users) |

    If any policy is in a higher priority category, the lower priority categories are ignored. For an example of how multiple policies with same priority are displayed to the requestor, see [Select a policy](entitlement-management-request-access#select-a-policy).
---
layout: Conceptual
title: Request access packages on-behalf-of other identities - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-request-behalf
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This article describes how to set up an access package so that managers can approve, or deny, requests for identities they own, sponsor, or are reporting to them.
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2025-06-18T00:00:00.0000000Z
locale: en-us
document_id: 9d8db191-8399-6819-c5aa-a35e517aed96
document_version_independent_id: 9d8db191-8399-6819-c5aa-a35e517aed96
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-request-behalf.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-request-behalf
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-request-behalf.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: dc690b0a-c065-8a53-e772-b4699be05364
---

# Request access packages on-behalf-of other identities - Microsoft Entra ID Governance | Microsoft Learn

Entitlement Management enables admins to create access packages to manage their organization’s resources. Admins can either directly assign identities to an access package, or configure an access package policy that allows users and group members to request access. The option to create self-service processes is useful, especially as organizations scale and hire more employees. However, new employees joining an organization might not always know what they need access to, or how they can request access. In this case, a new employee would likely rely on their manager to guide them through the access request process. Instead of having new employees navigate the request process, managers can request access packages for their employees, making onboarding faster and more seamless. To enable this functionality for managers, admins can select an option when setting up an access package policy that allows managers to request access on their employees' behalf.

Expanding self-service request flows to allow requests on behalf of identities ensures that identities have timely access to necessary resources, and increases productivity.

## Scenarios for managers requesting on behalf of employees

Imagine your organization hires hundreds of new employees each year, and you're being tasked with training new hires on IT processes, including how to request access for resources in My Access. Training sessions are only at the beginning of each month, so managers of new hires who start later in the month often reach out for ad-hoc training. This is becoming increasingly common.

Instead of conducting numerous ad-hoc training sessions to ensure new hires know how to request access in their first week or weeks at the organization, you can set up access package policies that allow managers to request access on behalf of their employees.

Now, managers are empowered to request access on behalf of new hires who haven't gone through the IT training. This ensures that employees have the tools and resources necessary to start on day one, and increases new hire satisfaction as they don’t need to wait for access or navigate the request process on their own.

## Scenarios for users requesting on behalf of other users

Imagine you're leading a project that includes employees, contractors, or external collaborators. You already know which resources each person needs, but some participants might be unfamiliar with My Access or your organization's access request process. Asking everyone to submit their own request can lead to confusion and delays, especially when a project needs to get started quickly. Instead, your organization can set up access package policies that allow designated users, such as project leads, team coordinators, or help desk personnel, to request access on behalf of others. This allows you to select the person who needs access, choose the appropriate access package, and provide the required request details for them. The request still follows the approval and access lifecycle processes defined in the policy, helping your organization maintain oversight while making the experience easier for users

## Scenarios for requesting on behalf of agent identities

The ability for administrators to request on behalf of agent identities they own or sponsor is also another key scenario for requesting access packages on behalf of other identities. With the ability to request an access package for an agent identity, You're able to ensure that agents working on behalf of you in your environment has the access to what they need to do their job, but nothing further. For more information on managing agents, see: [Manage Agents in Microsoft Entra](../agent-id/manage-agent).

## Prerequisites

This feature requires Microsoft Entra ID Governance or Microsoft Entra Suite subscriptions, for your organization's users. Some capabilities, within this feature, may operate with a Microsoft Entra ID P2 subscription. For more information, see the articles of each capability for more details. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

Note

Both the manager/user (requestor) and the employee/user (target) must be licensed for Microsoft Entra ID Governance or Microsoft Entra Suite to use the on-behalf-of request feature.

### License requirements for requesting on behalf of agent identities (preview)

Using [Microsoft Entra ID Governance](licensing-fundamentals) for agent identities requires one of the following license plans:

- **Microsoft 365 E7**, which includes Agent 365 and Microsoft Entra Suite, to provide governance of user and agent identities.
- **Microsoft Agent 365** license paired with at least Microsoft Entra P1 or Microsoft 365 E3.

For more information, see [Microsoft Agent 365 plans and pricing](https://www.microsoft.com/microsoft-agent-365#plans-and-pricing). For the full list of agent-specific capabilities, refer to the **Microsoft Agent 365** column in the [Microsoft Entra ID Governance licensing table](licensing-fundamentals).

## Configure an access package policy allowing on behalf of requests

Follow these steps to edit the policies, allowing on behalf of requests, for an existing access package:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access packages**.
3. Select the access package you want to set up for on behalf of requests.
4. Select the policy you wish to edit or create a new policy.
5. On the **Requests** tab, in the **Who can request access** section, select the users that will be eligible to request this access package. Selecting **Manager** will allow managers to make requests on behalf of their employees. Selecting **Users in your directory** will allow those individuals to make requests on behalf of other people in the organization as long as the user is in the directory.[![Screenshot of editing an access package's request on behalf of policy.](media/entitlement-management-request-behalf/configure-request-policy-for-anyone.png)](media/entitlement-management-request-behalf/configure-request-policy-for-anyone.png#lightbox)
6. Save your policy.

## Request an access package on behalf of an employee

As a manager, you can request an access package for a direct report by doing the following steps:

1. Sign in to the My Access portal at https://myaccess.microsoft.com. For US Government, the domain in the My Access portal link is `myaccess.microsoft.us`.
2. On the My Access Portal page, select **Access packages**.
3. On the Access packages page, locate the access package you want to request for a direct report and select **Request**.
4. On the Request pane under **Request details**, select requesting for **Someone else**. ![Screenshot of manager requesting access package for direct employee.](media/entitlement-management-request-behalf/manager-request-package.png)
5. Fill in additional information needed to request an access package for the direct report. ![Screenshot of justification questions for requesting an access package for a direct report.](media/entitlement-management-request-behalf/manager-request-questions.png)
6. Select **Submit request**.

## Approve access on behalf of employee requested by manager

To approve an access package on behalf of an employee as a manager, do the following steps to approve access:

1. Sign in to the My Access portal at https://myaccess.microsoft.com. For US Government, the domain in the My Access portal link is `myaccess.microsoft.us`.
2. In the left menu, select **Approvals** to see a list of access requests pending approval.
3. On the **Pending** tab, find the request. [![Screenshot of the pending approval requests in my access.](media/entitlement-management-request-behalf/myaccess-approval-request.png)](media/entitlement-management-request-behalf/myaccess-approval-request.png#lightbox)
4. Either approve, or deny, the request on behalf of the employee.

## Manage team assignments using the My Access portal

For access package assignments with policies that support on behalf of requests, managers can also manage access package assignments of their direct reports using the My Access portal when admins elect to turn on the feature. Management capabilities include:

- The ability to see active access package assignment of all of their direct reports.
- The ability to remove assignments for reports if the policy supports on behalf of requests.

Note

This My Access experience is for managers who manage access package assignments for their direct reports when the access package policy and My Access settings support on-behalf-of requests. Administrative assignment-management tasks for delegated entitlement management roles, such as Access package assignment manager, are performed in the Microsoft Entra admin center or by using authorized programmatic methods. Before managing teams in the My Access Portal, make sure you have the manage team settings configured by doing the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator). 
    Tip

    Other least privilege roles that can complete this task include the Catalog owner and the Access package manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Control configurations**.
3. On the control configurations page, select **view settings** on the My Access settings for end users card. [![Screenshot of the my access settings for end user card.](media/entitlement-management-request-behalf/my-access-settings-end-users.png)](media/entitlement-management-request-behalf/my-access-settings-end-users.png#lightbox)
4. On the end user settings page, make sure **View access package assignments for direct reports (preview)** is checked. ![Screenshot for the settings for end users using my access.](media/entitlement-management-request-behalf/my-access-settings.png)
5. Select **Save**. With the setting enabled, do the following steps to manage your team assignments using the My Access portal:
6. Sign in to the My Access portal at https://myaccess.microsoft.com as the direct manager of the team who you want to manage access package assignments for. For US Government, the domain in the My Access portal link is `myaccess.microsoft.us`.
7. In the left menu, select **Manage team** to see a list of your direct reports. [![Screenshot of the list of team members on the manage team page.](media/entitlement-management-request-behalf/manage-team-list.png)](media/entitlement-management-request-behalf/manage-team-list.png#lightbox)
8. Select an employee to see a list of their assignments.
9. On the assignments page, you can see a list of their current access package assignments. You can also select **Remove access** to end that specific access package assignment for the user. [![Screenshot of managing team in the my access portal.](media/entitlement-management-request-behalf/manage-team-reviews.png)](media/entitlement-management-request-behalf/manage-team-reviews.png#lightbox)

## Request an access package on behalf of an agent identity

As the owner or sponsor of an agent identity, you can request an access package for that agent identity by doing the following steps:

1. Sign in to the My Access portal at https://myaccess.microsoft.com.
2. On the My Access Portal page, select **Access packages**.
3. On the Access packages page, locate the access package you want to request for an agent identity to have, and select **Request**.
4. On the Request pane under **Request details**, select **Requesting for Sponsored agent** or **Requesting for Owned agent**.
5. Select the agent identity and then select **Continue**.
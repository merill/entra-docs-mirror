---
layout: Conceptual
title: Access packages for agent identities in Microsoft Entra - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/agent-access-packages
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: This article explains how access packages provide governance for agent identity access to resources.
ms.date: 2026-05-01T00:00:00.0000000Z
ms.topic: concept-article
locale: en-us
document_id: ae0bba18-ca23-6088-df5c-b2cc55b61c60
document_version_independent_id: ae0bba18-ca23-6088-df5c-b2cc55b61c60
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/agent-access-packages.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/agent-access-packages
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/agent-access-packages.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 1dfc34cf-e157-18bc-d3b0-5c6f2f5ed500
---

# Access packages for agent identities in Microsoft Entra - Microsoft Entra Agent ID | Microsoft Learn

Microsoft Entra entitlement management provides access packages as a governance mechanism. Access packages ensure that agent access assignments are intentional, auditable, and time-bound. Access packages represent a structured approach to managing agent identity permissions, contrasting with ad-hoc permission assignments that might lack appropriate governance controls. Access packages enable standardized access for many AI Agents with the same access needs, for example, a fleet of customer support AI Agents. Through access packages, organizations can establish consistent governance practices for agent identity, agent's user account, and service principal access to resources. For more information, see [Governing agent identities](/en-us/entra/id-governance/agent-id-governance-overview).

## Prerequisites

Before creating an access package, confirm the following prerequisites are met in your organization:

1. Agents are using Microsoft Entra Agent ID agent identities, or service principals, for authorization to access resources.
2. The authorization is one of:

    - Agents need their identity to be assigned OAuth *application permissions* for a target resource, such as Microsoft Graph or an application, to be able to access a target resource's APIs.
    - Agents need their identity to be assigned OAuth *delegated permissions* for a target resource, such as Microsoft Graph or an application, to be able to assist a user when accessing a target resource's APIs.
    - Agents need their identity to be assigned as members of groups.
    - Agents need their identity to be assigned to directory roles. The allowable roles are listed in [Microsoft Entra roles allowed for agents](authorization-agent-id#microsoft-entra-roles-allowed-for-agents).
3. You have or can create an entitlement management catalog suitable to hold those resources. The access package that you'll be creating, and any resources included in it, will be added to the catalog. For more information, see [create a catalog](/en-us/entra/id-governance/entitlement-management-catalog-create).

    Note

    If you'll be adding OAuth API permissions or directory roles to the access package as resource roles, then the catalog will be [marked as privileged](/en-us/entra/id-governance/entitlement-management-catalog-create#What-changes-for-privileged-catalogs) when they are added to the access package.

## Create an access package for agent identities

To use access packages for agents, the IT admin first configures a new access package with the relevant resources, including Entra roles, group memberships, and OAuth permission grants to application APIs. Then the admin configures in the access package the required policy settings. These settings define who can get access, who can request access, approvals, access expiration, and extension.

As agent identities and service principals can't be added through access packages to application roles, SAP roles, or SharePoint Online site roles, you won't be able to reuse an existing access package that contains any of those resource roles. Instead, create a new access package.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    If you'll be adding OAuth API permissions or directory roles to the access package as resource roles, then you will need to be a Global Administrator.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access packages**.
3. Select **New access package**.
4. On the **Basics** tab, you give the access package a name, and description and specify which catalog to create the access package in. In the **Catalog** dropdown list, select the catalog where you want to put the access package.
5. Select **Next: Resource roles**. On the **Resource roles** tab, you select the resource roles to include in the access package. Access packages for agent identities can have security group memberships, directory roles, or API permissions as resource roles. For more information, see [add a group](/en-us/entra/id-governance/entitlement-management-access-package-resources#add-a-group-or-team-resource-role), [add a Microsoft Entra role](/en-us/entra/id-governance/entitlement-management-access-package-resources#add-a-microsoft-entra-role-assignment), and [add an API permission](/en-us/entra/id-governance/entitlement-management-access-package-resources#add-an-api-permission-preview). Don't add application roles, SAP roles, or SharePoint Online site roles to an access package for agent identities.

    Tip

    If you're not sure which resource roles to include, you can skip adding them while creating the access package, and then [add them](/en-us/entra/id-governance/entitlement-management-access-package-resources) later. For API permissions, resource ownership validation occurs both when you onboard permissions to an access package and when you add them to an access package. This validation helps ensure that only authorized resource owners can introduce or expand access to API permissions through access packages.
6. Select **Next: Requests**. On the **Requests** tab, you create the first policy to specify who can request the access package. in the **Who can get access** section, select **For users, service principals, and agent identities in your directory**. In **Select specific scope**, select the option of **All agents**.

    Note

    If your agents are using service principals rather than Microsoft Entra agent identities, then also create an access package assignment policy with the option **All Service principals** to allow service principals in your directory to be able to request this access package.
7. Determine how many approval stages are needed. Set the **How many stages** toggle to **1** for single-stage approval, **2** for two-stage approval, or **3** for three-stage approval. Then configure approval stages and who the approvers should be. For more information, see [single stage approval](/en-us/entra/id-governance/entitlement-management-access-package-create#single-stage-approval).
8. Once you have specified each approval stage, select **Next: Requestor Information**.
9. Select **Next: Lifecycle**. Specify how long an access package assignment should remain before it expires.
10. Select **Next: Rules**.
11. Select **Next: Review + create**. On the **Review + create** tab, you can review your settings and check for any validation errors.
12. Select **Create** to create the access package and its initial policy.

In addition to using the Microsoft Entra Admin Center, you can also create an access package programmatically, through Microsoft Graph, and through the PowerShell cmdlets for Microsoft Graph. For more information, see [Create an access package programmatically](/en-us/entra/id-governance/entitlement-management-access-package-create#create-an-access-package-programmatically).

## Access request and approval process

Agents can then be assigned access packages through three different request pathways.

- The agent identity itself can programmatically request an access package when needed for its operations, by creating an [accessPackageAssignmentRequest](/en-us/graph/api/entitlementmanagement-post-assignmentrequests?tabs=http).
- The agent's sponsor can request access on behalf of the agent ID, providing human oversight in the access request process. For more information, see [Request an access package on behalf of an agent identity](/en-us/entra/id-governance/entitlement-management-request-behalf#request-an-access-package-on-behalf-of-an-agent-identity).
- An administrator can [directly assign the agent identity or agent's user account to the access package](/en-us/entra/id-governance/entitlement-management-access-package-assignments#directly-assign-an-identity).

After submission, the access request is routed to designated approvers based on the access package policy configuration.

## Request an access package on behalf of another user

Users with the appropriate permissions can request access packages on behalf of another user in their organization.

1. Sign in to the My Access portal at [https://myaccess.microsoft.com](https://myaccess.microsoft.com/). For US Government, the domain in the My Access portal link is `myaccess.microsoft.us`.
2. On the My Access Portal page, select **Access packages**.
3. On the Access packages page, locate the access package you want to request for a direct report and select **Request**.
4. On the Request pane under **Request details**, select requesting for **Others**.
5. Select **Anyone in your organization** and search for the user you want to submit the request for.

    [![Screenshot of selecting Anyone in your organization when requesting an access package on behalf of another user.](../id-governance/media/entitlement-management-request-behalf/request-access-package-for-anyone.png)](../id-governance/media/entitlement-management-request-behalf/request-access-package-for-anyone.png#lightbox)
6. Continue with the remaining request steps to complete the access package request on behalf of the user.

## Access assignment lifecycle

Once an approver accepts the access package assignment request, the agent identity receives time-bound access to the specified resources. The access is granted according to the resource roles defined in the access package. This establishes a clear start and end date for the access the agent might need.

If the assignment is to an agent identity, and a sponsor is set on the agent identity, as the expiry date approaches, the sponsor receives notifications about the pending expiration. The sponsor then has two options: they can request an extension of the access package (if permitted by policy), or they can allow the access package assignment to expire.

If the sponsor requests an extension, this request can trigger a new approval cycle, where approvers again confirm whether continued access is appropriate. If the sponsor takes no action, the access package assignment automatically expires on its end date, and the agent identity loses access to the target resources.
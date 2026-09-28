---
layout: Conceptual
title: Common scenarios in entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-scenarios
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn the high-level steps you should follow for common scenarios in Microsoft Entra entitlement management.
editor: markwahl-msft
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2024-07-15T00:00:00.0000000Z
ms.reviewer: mwahl
locale: en-us
document_id: e4ef6137-abb7-b678-afb1-9550abb722a5
document_version_independent_id: 7274105f-2f2c-38ab-b482-a8cd1e24f6e4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-scenarios.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-scenarios
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-scenarios.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 09897b65-cfbc-cb89-ee15-c70cf27e7b0e
---

# Common scenarios in entitlement management - Microsoft Entra ID Governance | Microsoft Learn

There are several ways that you can configure entitlement management for your organization. However, if you're just getting started, it's helpful to understand the common scenarios for administrators, catalog owners, access package managers, approvers, and requestors.

## Delegate

### Administrator: Delegate management of resources

1. [Watch video: Delegation from IT to department manager](https://learn-video.azurefd.net/vod/player?id=0915072b-63ec-4c78-b2ca-aa5f54a54219)
2. [Delegate users to catalog creator role](entitlement-management-delegate-catalog)

### Catalog creator: Delegate management of resources

- [Create a new catalog](entitlement-management-catalog-create#create-a-catalog)

### Catalog owner: Delegate management of resources

1. [Add co-owners to the catalog](entitlement-management-catalog-create#add-more-catalog-owners)
2. [Add resources to the catalog](entitlement-management-catalog-create#add-resources-to-a-catalog)

### Catalog owner: Delegate management of access packages

1. [Watch video: Delegation from catalog owner to access package manager](https://learn-video.azurefd.net/vod/player?id=b999927c-7cfd-4029-8b3a-a59efa9f5e8c)
2. [Delegate users to access package manager role](entitlement-management-delegate-managers)

## Govern access for users in your organization

### Administrator: Assign employees access automatically

1. [Create a new access package](entitlement-management-access-package-create#start-the-creation-process)
2. [Add groups, Teams, applications, or SharePoint sites to access package](entitlement-management-access-package-create#select-resource-roles)
3. [Add an automatic assignment policy](entitlement-management-access-package-auto-assignment-policy)

### Administrator: Assign employees access from lifecycle workflows

1. [Create a new access package](entitlement-management-access-package-create#start-the-creation-process)
2. [Add groups, Teams, applications, or SharePoint sites to access package](entitlement-management-access-package-create#select-resource-roles)
3. [Add a direct assignment policy](entitlement-management-access-package-request-policy#none-administrator-direct-assignments-only)
4. Add a task to [Request user access package assignment](lifecycle-workflow-tasks#request-user-access-package-assignment) to a workflow when a user joins
5. Add a task to [Remove access package assignment for user](lifecycle-workflow-tasks#remove-access-package-assignment-for-user) to a workflow when a user leaves

### Access package manager: Allow employees in your organization to request access to resources

1. [Create a new access package](entitlement-management-access-package-create#start-the-creation-process)
2. [Add groups, Teams, applications, or SharePoint sites to access package](entitlement-management-access-package-create#select-resource-roles)
3. [Add a request policy to allow users, service principals, and agent identities in your directory to request access](entitlement-management-access-package-create#allow-users-service-principals-and-agent-identities-in-your-directory-to-request-the-access-package)
4. [Specify expiration settings](entitlement-management-access-package-create#specify-a-lifecycle)

### Requestor: Request access to resources

1. [Sign in to the My Access portal](entitlement-management-request-access#sign-in-to-the-my-access-portal)
2. Find access package
3. [Request access](entitlement-management-request-access#request-an-access-package)

### Approver: Approve requests to resources

1. [Open request in My Access portal](entitlement-management-request-approve#open-request)
2. [Approve or deny access request](entitlement-management-request-approve#approve-or-deny-request)

### Requestor: View the resources you already have access to

1. [Sign in to the My Access portal](entitlement-management-request-access#sign-in-to-the-my-access-portal)
2. View active access packages

## Govern access for users outside your organization

### Administrator: Collaborate with an external partner organization

1. [Read how access works for external users](entitlement-management-external-users#how-access-works-for-external-users)
2. [Review settings for external users](entitlement-management-external-users#settings-for-external-users)
3. [Add a connection to the external organization](entitlement-management-organization)

### Access package manager: Collaborate with an external partner organization

1. [Create a new access package](entitlement-management-access-package-create#start-the-creation-process)
2. [Add groups, Teams, applications, or SharePoint sites to access package](entitlement-management-access-package-resources#add-resource-roles)
3. [Add a request policy to allow users not in your directory to request access](entitlement-management-access-package-request-policy#for-users-not-in-your-directory)
4. [Specify expiration settings](entitlement-management-access-package-create#specify-a-lifecycle)
5. [Copy the link to request the access package](entitlement-management-access-package-settings)
6. Send the link to your external partner contact partner to share with their users

### Requestor: Request access to resources as an external user

1. Find the access package link you received from your contact
2. [Sign in to the My Access portal](entitlement-management-request-access#sign-in-to-the-my-access-portal)
3. [Request access](entitlement-management-request-access#request-an-access-package)

### Approver: Approve requests to resources

1. [Open request in My Access portal](entitlement-management-request-approve#open-request)
2. [Approve or deny access request](entitlement-management-request-approve#approve-or-deny-request)

### Requestor: View the resources your already have access to

1. [Sign in to the My Access portal](entitlement-management-request-access#sign-in-to-the-my-access-portal)
2. View active access packages

## Govern access for agents (preview)

Using [Microsoft Entra ID Governance](licensing-fundamentals) for agent identities requires one of the following license plans:

- **Microsoft 365 E7**, which includes Agent 365 and Microsoft Entra Suite, to provide governance of user and agent identities.
- **Microsoft Agent 365** license paired with at least Microsoft Entra P1 or Microsoft 365 E3.

For more information, see [Microsoft Agent 365 plans and pricing](https://www.microsoft.com/microsoft-agent-365#plans-and-pricing). For the full list of agent-specific capabilities, refer to the **Microsoft Agent 365** column in the [Microsoft Entra ID Governance licensing table](licensing-fundamentals).

1. [Create a new access package](entitlement-management-access-package-create#start-the-creation-process)
2. [Add groups or API permissions to access package](entitlement-management-access-package-create#select-resource-roles)
3. [Add a request policy to allow service principals and agent identities in your directory to request access](entitlement-management-access-package-create#allow-users-service-principals-and-agent-identities-in-your-directory-to-request-the-access-package)

## Day-to-day management

### Administrator: View the connected organizations that are proposed and configured

1. [View the list of connected organizations](entitlement-management-organization)

### Access package manager: Update the resources for a project

1. [Watch video: Day-to-day management: Things have changed](https://learn-video.azurefd.net/vod/player?id=cebe87cf-64db-4242-9527-f726b6d227f9)
2. Open the access package
3. [Add or remove groups, Teams, applications, or SharePoint sites](entitlement-management-access-package-resources#add-resource-roles)

### Access package manager: Update the duration for a project

1. [Watch video: Day-to-day management: Things have changed](https://learn-video.azurefd.net/vod/player?id=cebe87cf-64db-4242-9527-f726b6d227f9)
2. Open the access package
3. [Open the lifecycle settings](entitlement-management-access-package-lifecycle-policy#open-lifecycle-settings)
4. [Update the expiration settings](entitlement-management-access-package-lifecycle-policy#specify-a-lifecycle)

### Access package manager: Update how access is approved for a project

1. [Watch video: Day-to-day management: Things have changed](https://learn-video.azurefd.net/vod/player?id=cebe87cf-64db-4242-9527-f726b6d227f9)
2. [Open an existing policy's request settings](entitlement-management-access-package-request-policy#open-an-existing-access-package-and-add-a-new-policy-with-different-request-settings)
3. [Update the approval settings](entitlement-management-access-package-approval-policy#change-approval-settings-of-an-existing-access-package-assignment-policy)

### Access package manager: Update the people for a project

1. [Watch video: Day-to-day management: Things have changed](https://learn-video.azurefd.net/vod/player?id=cebe87cf-64db-4242-9527-f726b6d227f9)
2. [Remove users that no longer need access](entitlement-management-access-package-assignments)
3. [Open an existing policy's request settings](entitlement-management-access-package-request-policy#open-an-existing-access-package-and-add-a-new-policy-with-different-request-settings)
4. [Add identities that need access](entitlement-management-access-package-request-policy#for-users-service-principals-and-agent-identities-in-your-directory)

### Access package manager: Directly assign specific users to an access package

1. [If users need different lifecycle settings, add a new policy to the access package](entitlement-management-access-package-request-policy#open-an-existing-access-package-and-add-a-new-policy-with-different-request-settings)
2. [Directly assign specific identities to the access package](entitlement-management-access-package-assignments#directly-assign-an-identity)

## Assignments and reports

### Administrator: View who has assignments to an access package

1. Open an access package
2. [View assignments](entitlement-management-access-package-assignments#view-who-has-an-assignment)
3. [Archive reports and logs](entitlement-management-logs-and-reporting)

### Administrator: View resources assigned to users

1. [View access packages for a user](entitlement-management-reports#view-access-packages-for-a-user)
2. [View resource assignments for a user](entitlement-management-reports#view-resource-assignments-for-a-user)

## Programmatic administration

You can also manage access packages, catalogs, policies, requests, and assignments using Microsoft Graph. A user in an appropriate role with an application that has the delegated `EntitlementManagement.Read.All` or `EntitlementManagement.ReadWrite.All` permission can call the [entitlement management API](/en-us/graph/api/resources/entitlementmanagement-overview). For more information, see the [Tutorial: manage access to resources - Microsoft Graph](/en-us/graph/tutorial-access-package-api?toc=/azure/active-directory/governance/toc.json&amp;bc=/azure/active-directory/governance/breadcrumb/toc.json). An application with the `EntitlementManagement.Read.All` or `EntitlementManagement.ReadWrite.All` application permissions can also use many of those API functions, except for managing resources in catalogs and access packages. An application that only needs to operate within specific catalogs can be added to the **Catalog owner** or **Catalog reader** roles of a catalog to be authorized to update or read within that catalog.
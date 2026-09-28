---
layout: Conceptual
title: Authorization basics - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/authorization-basics
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn about the basics of authorization in the Microsoft identity platform.
manager: pmwongera
ms.custom: 
ms.date: 2024-08-25T00:00:00.0000000Z
ms.reviewer: 
ms.topic: concept-article
locale: en-us
document_id: 579cd436-819e-e134-15b5-19fd94a3fbef
document_version_independent_id: de84dce6-1e91-a948-75d4-160a99d49f49
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/authorization-basics.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/authorization-basics
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/authorization-basics.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: 22245c6d-cb3b-161f-699a-b940762fb0f9
---

# Authorization basics - Microsoft identity platform | Microsoft Learn

**Authorization** (sometimes abbreviated as *AuthZ*) is used to set permissions that enable evaluation of access to resources or functionality. In contrast, **authentication** (sometimes abbreviated as *AuthN*) is focused on proving that an entity like a user or service is indeed who they claim to be.

Authorization can include specifying the functionality, resources, or data an entity is allowed to access. Authorization also specifies what can be done with the data. This authorization action is often referred to as *access control*.

Authentication and authorization are concepts that aren't limited to only users. Services or daemon applications are often built to make requests for resources as themselves rather than on behalf of a specific user. In this article, the term "entity" is used to refer to either a user or an application.

## Authorization approaches

There are several common approaches to handle authorization. [Role-based access control](custom-rbac-for-developers) is currently the most common approach using Microsoft identity platform.

### Authentication as authorization

Possibly the simplest form of authorization is to grant or deny access based on whether the entity making a request has been authenticated. If the requestor can prove they're who they claim to be, they can access the protected resources or functionality.

### Access control lists

Authorization by using access control lists (ACLs) involves maintaining explicit lists of specific entities who do or don't have access to a resource or functionality. ACLs offer finer control over authentication-as-authorization but become difficult to manage as the number of entities increases.

### Role-based access control

Role-based access control (RBAC) is possibly the most common approach to enforcing authorization in applications. When using RBAC, roles are defined to describe the kinds of activities an entity may perform. An application developer grants access to roles rather than to individual entities. An administrator can then assign roles to different entities to control which ones have access to what resources and functionality.

In advanced RBAC implementations, roles may be mapped to collections of permissions, where a permission describes a granular action or activity that can be performed. Roles are then configured as combinations of permissions. Compute the overall permission set for an entity by combining the permissions granted to the various roles the entity is assigned. A good example of this approach is the RBAC implementation that governs access to resources in Azure subscriptions.

Note

[Application RBAC](custom-rbac-for-developers) differs from [Azure RBAC](/en-us/azure/role-based-access-control/overview) and [Microsoft Entra RBAC](../identity/role-based-access-control/custom-overview#understand-azure-ad-role-based-access-control). Azure custom roles and built-in roles are both part of Azure RBAC, which helps manage Azure resources. Microsoft Entra RBAC allows management of Microsoft Entra resources.

### Attribute-based access control

Attribute-based access control (ABAC) is a more fine-grained access control mechanism. In this approach, rules are applied to the entity, the resources being accessed, and the current environment. The rules determine the level of access to resources and functionality. An example might be only allowing users who are managers to access files identified with a metadata tag of "managers during working hours only" during the hours of 9AM - 5PM on working days. In this case, access is determined by examining the attribute (status as manager) of the user, the attribute (metadata tag on a file) of the resource, and also an environment attribute (the current time).

One advantage of ABAC is that more granular and dynamic access control can be achieved through rule and condition evaluations without the need to create large numbers of specific roles and RBAC assignments.

One method for achieving ABAC with Microsoft Entra ID is using [dynamic membership groups](../identity/users/groups-create-rule). Dynamic groups allow administrators to dynamically assign users to groups based on specific user attributes with desired values. For example, an Authors group could be created where all users with the job title Author are dynamically assigned to the Authors group. Dynamic groups can be used in combination with RBAC for authorization where you map roles to groups and dynamically assign users to groups.

[Azure ABAC](/en-us/azure/role-based-access-control/conditions-overview) is an example of an ABAC solution that is available today. Azure ABAC builds on Azure RBAC by adding role assignment conditions based on attributes in the context of specific actions.

## Implementing authorization

Authorization logic is often implemented within the applications or solutions where access control is required. In many cases, application development platforms offer middleware or other API solutions that simplify the implementation of authorization. Examples include use of the [AuthorizeAttribute](/en-us/aspnet/core/security/authorization/simple?view=aspnetcore-5.0&amp;preserve-view=true) in ASP.NET or [Route Guards](scenario-spa-sign-in?tabs=angular2#sign-in-with-a-pop-up-window) in Angular.

For authorization approaches that rely on information about the authenticated entity, an application evaluates information exchanged during authentication. For example, by using the information that was provided within a [security token](security-tokens). If you are planning on using information from tokens for authorization, we recommend following [this guidance on properly securing apps through claims validation](claims-validation). For information not contained in a security token, an application might make extra calls to external resources.

It's not strictly necessary for developers to embed authorization logic entirely within their applications. Instead, dedicated authorization services can be used to centralize authorization implementation and management.
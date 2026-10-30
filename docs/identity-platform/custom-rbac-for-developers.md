---
layout: Conceptual
title: Custom role-based access control for application developers - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/custom-rbac-for-developers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn about what custom RBAC is and why it's important to implement in applications.
manager: pmwongera
ms.custom: 
ms.date: 2023-01-06T00:00:00.0000000Z
ms.reviewer: 
ms.topic: concept-article
locale: en-us
document_id: 5dc830f1-65af-6a40-c11c-4b394b808b5a
document_version_independent_id: 1443081c-71c8-1606-2312-793f89f0b645
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/custom-rbac-for-developers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/custom-rbac-for-developers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/custom-rbac-for-developers.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: e090ac44-a428-f73e-d398-5ce331059562
---

# Custom role-based access control for application developers - Microsoft identity platform | Microsoft Learn

Role-based access control (RBAC) allows certain users or groups to have specific permissions to access and manage resources. Application RBAC differs from [Azure role-based access control](/en-us/azure/role-based-access-control/overview) and [Microsoft Entra role-based access control](../identity/role-based-access-control/custom-overview#understand-azure-ad-role-based-access-control). Azure custom roles and built-in roles are both part of Azure RBAC, which is used to help manage Azure resources. Microsoft Entra RBAC is used to manage Microsoft Entra resources. This article explains application-specific RBAC. For information about implementing application-specific RBAC, see [How to add app roles to your application and receive them in the token](howto-add-app-roles-in-apps).

## Roles definitions

RBAC is a popular mechanism to enforce authorization in applications. When an organization uses RBAC, an application developer defines roles rather than authorizing individual users or groups. An administrator can then assign roles to different users and groups to control who has access to content and functionality.

RBAC helps an application developer to manage resources and their usage. RBAC also allows an application developer to control the areas of an application that users can access. Administrators can control which users have access to an application using the *User assignment required* property. Developers need to account for specific users within the application and what users can do within the application.

An application developer first creates a role definition within the registration section of the application in the Microsoft Entra admin center. The role definition includes a value that is returned for users who are assigned to that role. A developer can then use this value to implement application logic to determine what those users can or can't do in an application.

## RBAC options

The following guidance should be applied when considering including role-based access control authorization in an application:

- Define the roles that are required for the authorization needs of the application.
- Apply, store, and retrieve the pertinent roles for authenticated users.
- Determine the application behavior based on the roles assigned to the current user.

After the roles are defined, the Microsoft identity platform supports several different solutions that can be used to apply, store, and retrieve role information for authenticated users. These solutions include app roles, Microsoft Entra groups, and the use of custom datastores for user role information.

Developers have the flexibility to provide their own implementation for how role assignments are to be interpreted as application permissions. This interpretation of permissions can involve using middleware or other options provided by the platform of the applications or related libraries. Applications typically receive user role information as claims and then decides user permissions based on those claims.

### App roles

Microsoft Entra ID allows you to [define app roles](howto-add-app-roles-in-apps) for your application and assign those roles to users and other applications. The roles you assign to a user or application define their level of access to the resources and operations in your application.

When Microsoft Entra ID issues an access token for an authenticated user or application, it includes the names of the roles you've assigned the entity (the user or application) in the access token's [`roles`](access-token-claims-reference#payload-claims) claim. An application like a web API that receives that access token in a request can then make authorization decisions based on the values in the `roles` claim.

### Groups

Developers can also use [Microsoft Entra groups](../fundamentals/concept-learn-about-groups) to implement RBAC in their applications, where the memberships of the user in specific groups are interpreted as their role memberships. When an organization uses groups, the token includes a [groups claim](access-token-claims-reference#payload-claims). The group claim specifies the identifiers of all of the assigned groups of the user within the tenant.

Important

When working with groups, developers need to be aware of the concept of an [overage claim](access-token-claims-reference#payload-claims). By default, if a user is a member of more than the overage limit (150 for SAML tokens, 200 for JWT tokens, 6 if using the implicit flow), Microsoft Entra ID doesn't emit a groups claim in the token. Instead, it includes an "overage claim" in the token that indicates the consumer of the token needs to query the Microsoft Graph API to retrieve the group memberships of the user. For more information about working with overage claims, see [Claims in access tokens](access-token-claims-reference). It's possible to only emit groups that are assigned to an application, though [group-based assignment](../identity/enterprise-apps/assign-user-or-group-access-portal) does require Microsoft Entra ID P1 or P2 edition.

### Custom data store

App roles and groups both store information about user assignments in the Microsoft Entra directory. Another option for managing user role information that is available to developers is to maintain the information outside of the directory in a custom data store. For example, in an SQL database, Azure Table storage, or Azure Cosmos DB for Table.

Using custom storage allows developers extra customization and control over how to assign roles to users and how to represent them. However, the extra flexibility also introduces more responsibility. For example, there's no mechanism currently available to include this information in tokens returned from Microsoft Entra ID. Applications must retrieve the roles if role information is maintained in a custom data store. Retrieving the roles is typically done using extensibility points defined in the middleware available to the platform that's being used to develop the application. Developers are responsible for properly securing the custom data store.

## Choose an approach

In general, app roles are the recommended solution. App roles provide the simplest programming model and are purpose made for RBAC implementations. However, specific application requirements may indicate that a different approach would be a better solution.

Developers can use app roles to control whether a user can sign into an application, or an application can obtain an access token for a web API. App roles are preferred over Microsoft Entra groups by developers when they want to describe and control the parameters of authorization in their applications. For example, an application using groups for authorization breaks in the next tenant as both the group identifier and name could be different. An application using app roles remains safe.

Although either app roles or groups can be used for authorization, key differences between them can influence which is the best solution for a given scenario.

| - | App Roles | Microsoft Entra groups | Custom Data Store |
| --- | --- | --- | --- |
| **Programming model** | **Simplest**. They're specific to an application and are defined in the application registration. They move with the application. | **More complex**. Group identifiers vary between tenants and overage claims may need to be considered. Groups aren't specific to an application, but to a Microsoft Entra tenant. | **Most complex**. Developers must implement means by which role information is both stored and retrieved. |
| **Role values are static between Microsoft Entra tenants** | Yes | No | Depends on the implementation. |
| **Role values can be used in multiple applications** | No (Unless role configuration is duplicated in each application registration.) | Yes | Yes |
| **Information stored within directory** | Yes | Yes | No |
| **Information is delivered via tokens** | Yes (roles claim) | Yes (If an overage, *groups claims* may need to be retrieved at runtime) | No (Retrieved at runtime via custom code.) |
| **Lifetime** | Lives in application registration in directory. Removed when the application registration is removed. | Lives in directory. Remain intact even if the application registration is removed. | Lives in custom data store. Not tied to application registration. |
---
layout: Conceptual
title: Secure access control using groups in Microsoft Entra ID - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/secure-group-access-control
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn about how groups are used to securely control access to resources in Microsoft Entra ID.
manager: pmwongera
ms.custom: 
ms.date: 2024-08-25T00:00:00.0000000Z
ms.reviewer: 
ms.topic: concept-article
locale: en-us
document_id: 9a026123-9ffb-daef-13ca-fe25fe1939b8
document_version_independent_id: b725ad6e-a0e2-9c5d-e569-8836b59bb144
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/secure-group-access-control.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/secure-group-access-control
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/secure-group-access-control.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 7e34209a-0feb-fe5c-062a-a8ccfe433b16
---

# Secure access control using groups in Microsoft Entra ID - Microsoft identity platform | Microsoft Learn

Microsoft Entra ID allows the use of groups to manage access to resources in an organization. Use groups for access control to manage and minimize access to applications. When groups are used, only members of those groups can access the resource. Using groups also enables the following management features:

- Attribute-based dynamic membership groups
- External groups synced from on-premises Active Directory
- Administrator managed or self-service managed groups

To learn more about the benefits of groups for access control, see [manage access to an application](../identity/enterprise-apps/what-is-access-management).

While developing an application, authorize access with the groups claim. To learn more, see how to [configure group claims for applications with Microsoft Entra ID](../identity/hybrid/connect/how-to-connect-fed-group-claims).

Today, many applications select a subset of groups with the `securityEnabled` flag set to `true` to avoid scale challenges, that is, to reduce the number of groups returned in the token. Setting the `securityEnabled` flag to be true for a group doesn't guarantee that the group is securely managed.

## Best practices to mitigate risk

The following table presents several security best practices for security groups and the potential security risks each practice mitigates.

| Security best practice | Security risk mitigated |
| --- | --- |
| **Ensure resource owner and group owner are the same principal**. Applications should build their own group management experience and create new groups to manage access. For example, an application can create groups with the `Group.Create` permission and add itself as the owner of the group. This way the application has control over its groups without being over privileged to modify other groups in the tenant. | When group owners and resource owners are different entities, group owners can add users to the group who aren't supposed to access the resource but can then access it unintentionally. |
| **Build an implicit contract between the resource owner and group owner**. The resource owner and the group owner should align on the group purpose, policies, and members that can be added to the group to get access to the resource. This level of trust is non-technical and relies on human or business contract. | When group owners and resource owners have different intentions, the group owner may add users to the group the resource owner didn't intend on giving access to. This action can result in unnecessary and potentially risky access. |
| **Use private groups for access control**. Microsoft 365 groups are managed by the [visibility concept](/en-us/graph/api/resources/group?view=graph-rest-1.0&amp;preserve-view=true#group-visibility-options). This property controls the join policy of the group and visibility of group resources. Security groups have join policies that either allow anyone to join or require owner approval. On-premises-synced groups can also be public or private. Users joining an on-premises-synced group can get access to cloud resource as well. | When you use a public group for access control, any member can join the group and get access to the resource. The risk of elevation of privilege exists when a public group is used to give access to an external resource. |
| **Group nesting**. When you use a group for access control and it has other groups as its members, members of the subgroups can get access to the resource. In this case, there are multiple group owners of the parent group and the subgroups. | Aligning with multiple group owners on the purpose of each group and how to add the right members to these groups is more complex and more prone to accidental grant of access. Limit the number of nested groups or don't use them at all if possible. |
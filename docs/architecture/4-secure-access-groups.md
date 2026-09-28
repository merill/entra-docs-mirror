---
layout: Conceptual
title: Secure external access with groups in Microsoft Entra ID and Microsoft 365 - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/4-secure-access-groups
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Microsoft Entra ID and Microsoft 365 Groups can be used to increase security when external users access your resources.
ms.topic: how-to
ms.date: 2023-02-09T00:00:00.0000000Z
ms.custom: sfi-image-nochange
ms.subservice: architecture
locale: en-us
document_id: 04380f76-b771-d79c-c58a-0704cccfebc6
document_version_independent_id: 9075450a-ca6b-a68a-550a-61b9aefb1d65
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/4-secure-access-groups.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/4-secure-access-groups
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/4-secure-access-groups.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 51d2587c-014d-33c9-392e-3b81619f93d9
---

# Secure external access with groups in Microsoft Entra ID and Microsoft 365 - Microsoft Entra | Microsoft Learn

Groups are part of an access control strategy. You can use Microsoft Entra security groups and Microsoft 365 Groups as the basis for securing access to resources. Use groups for the following access-control mechanisms:

- Conditional Access policies
    - [What is Conditional Access?](../identity/conditional-access/overview)
- Entitlement management access packages
    - [What is entitlement management?](../id-governance/entitlement-management-overview)
- Access to Microsoft 365 resources, Microsoft Teams, and SharePoint sites

Groups have the following roles:

- **Group owners** – manage group settings and its membership
- **Members** – inherit permissions and access assigned to the group
- **Guests** – are members outside your organization

## Before you begin

This article is number 4 in a series of 10 articles. We recommend you review the articles in order. Go to the **Next steps** section to see the entire series.

## Group strategy

To develop a group strategy to secure external access to your resources, consider the security posture that you want.

Learn more: [Determine your security posture for external access](1-secure-access-posture)

### Group creation

Determine who is granted permissions to create groups: Administrators, employees, and/or external users. Consider the following scenarios:

- Tenant members can create Microsoft Entra security groups
- Internal and external users can join groups in your tenant
- Users can create Microsoft 365 Groups
- [Manage who can create Microsoft 365 Groups](/en-us/microsoft-365/solutions/manage-creation-of-groups?view=o365-worldwide&amp;preserve-view=true)
    - Use PowerShell to configure this setting
- [Restrict your Microsoft Entra app to a set of users in a Microsoft Entra tenant](../identity-platform/howto-restrict-your-app-to-a-set-of-users)
- [Set up self-service group management in Microsoft Entra ID](../identity/users/groups-self-service-management)
- [Troubleshoot and resolve groups issues](../identity/users/groups-troubleshooting)

### Invitations to groups

As part of the group strategy, consider who can invite people, or add them, to groups. Group members can add other members, or group owners can add members. Decide who can be invited. By default, external users can be added to groups.

### Assign users to groups

Users are assigned to groups manually, based on user attributes in their user object, or users are assigned based on other criteria. Users are assigned to groups dynamically based on their attributes. For example, you can assign users to groups based on:

- Job title or department
- Partner organization to which they belong
    - Manually, or through connected organizations
- Member or Guest User type
- Participation in a project
    - Manually
- Location

Dynamic groups have users or devices, but not both. To assign users to the dynamic group, add queries based on user attributes. The following screenshot has queries that add users to the group if they are finance department members.

![Screenshot of options and entries under Dynamic membership rules.](media/secure-external-access/4-dynamic-membership-rules.png)

Learn more: [Create or update a dynamic group in Microsoft Entra ID](../identity/users/groups-create-rule)

### Use groups for one function

When using groups, it's important they have a single function. If a group is used to grant access to resources, don't use it for another purpose. We recommend a security-group naming convention that makes the purpose clear:

- Secure\_access\_finance\_apps
- Team\_membership\_finance\_team
- Location\_finance\_building

### Group types

You can create Microsoft Entra security groups and Microsoft 365 Groups in the Azure portal or the Microsoft 365 Admin portal. Use either group type for securing external access.

| Considerations | Manual and dynamic Microsoft Entra security groups | Microsoft 365 Groups |
| --- | --- | --- |
| The group contains | UsersGroupsService principalsDevices | Users only |
| Where the group is created | Azure portalMicrosoft 365 portal, if mail-enabled)PowerShellMicrosoft GraphEnd user portal | Microsoft 365 portalAzure portalPowerShellMicrosoft GraphIn Microsoft 365 applications |
| Who creates, by default | Administrators Users | AdministratorsUsers |
| Who is added, by default | Internal users (tenant members) and guest users | Tenant members and guests from an organization |
| Access is granted to | Resources to which it's assigned. | Group-related resources:(Group mailbox, site, team, chats, and other Microsoft 365 resources)Other resources to which group is added |
| Can be used with | Conditional Accessentitlement managementgroup licensing | Conditional Accessentitlement managementsensitivity labels |

Note

Use Microsoft 365 Groups to create and manage a set of Microsoft 365 resources, such as a Team and its associated sites and content.

## Microsoft Entra security groups

Microsoft Entra security groups can have users or devices. Use these groups to manage access to:

- Azure resources
    - Microsoft 365 Apps
    - Custom apps
    - Software as a Service (SaaS) apps such as Dropbox ServiceNow
- Azure data and subscriptions
- Azure services

Use Microsoft Entra security groups to assign:

- Licenses for services
    - Microsoft 365
    - Dynamics 365
    - Enterprise Mobility + Security
    - See, [Assign or unassign licenses to a group in the Microsoft 365 admin center](/en-us/microsoft-365/admin/manage/manage-group-licenses?view=o365-worldwide&amp;preserve-view=true)
- Elevated permissions
    - See, [Use Microsoft Entra groups to manage role assignments](../identity/role-based-access-control/groups-concept)

Learn more:

- [Manage Microsoft Entra groups and group membership](/en-us/entra/fundamentals/how-to-manage-groups)
- [Microsoft Entra version 2 cmdlets for group management](../identity/users/groups-settings-v2-cmdlets).

Note

Use security groups to assign up to 1,500 applications.

![Screenshot of entries and options under New Group.](media/secure-external-access/4-create-security-group.png)

### Mail-enabled security group

To create a mail-enabled security group, go to the [Microsoft 365 admin center](https://admin.microsoft.com/). Enable a security group for mail during creation. You can't enable it later. You can't create the group in the Azure portal.

### Hybrid organizations and Microsoft Entra security groups

Hybrid organizations have infrastructure for on-premises and a Microsoft Entra ID. Hybrid organizations that use Active Directory can create security groups on-premises and sync them to the cloud. Therefore, only users in the on-premises environment can be added to the security groups.

Important

Protect your on-premises infrastructure from compromise. See, [Protecting Microsoft 365 from on-premises attacks](protect-m365-from-on-premises-attacks).

## Microsoft 365 Groups

Microsoft 365 Groups is the membership service for access across Microsoft 365. They can be created from the Azure portal, or the Microsoft 365 admin center. When you create a Microsoft 365 Group, you grant access to a group of resources for collaboration.

Learn more:

- [Overview of Microsoft 365 Groups for administrators](/en-us/microsoft-365/admin/create-groups/office-365-groups?view=o365-worldwide&amp;preserve-view=true)
- [Create a group in the Microsoft 365 admin center](/en-us/microsoft-365/admin/create-groups/create-groups?view=o365-worldwide&amp;preserve-view=true)
- [Microsoft Entra admin center](https://entra.microsoft.com)
- [Microsoft 365 admin center](https://admin.microsoft.com/)

### Microsoft 365 Groups roles

- **Group owners**
    - Add or remove members
    - Delete conversations from the shared inbox
    - Change group settings
    - Rename the group
    - Update the description or picture
- **Members**
    - Access everything in the group
    - Can't change group settings
    - Can invite guests to join the group
    - [Manage guest access in Microsoft 365 groups](/en-us/microsoft-365/admin/create-groups/manage-guest-access-in-groups)
- **Guests**
    - Are members from outside your organization
    - Have some limits to functionality in Teams

### Microsoft 365 Group settings

Select email alias, privacy, and whether to enable the group for teams.

After setup, add members, and configure settings for email usage, and so on.
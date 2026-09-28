---
layout: Conceptual
title: Using role-based access control for apps - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-use-app-roles-customers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to define application roles for your consumer and business customer applications and assign those roles to users and groups in external tenants.
ms.topic: how-to
ms.date: 2026-04-17T00:00:00.0000000Z
ms.custom: it-pro, sfi-ga-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 699022c2-5402-9b4a-e369-183d9caa01c8
document_version_independent_id: 2e3b1ad6-f27f-c00c-ac0f-e6440eecbcf8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-use-app-roles-customers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-use-app-roles-customers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-use-app-roles-customers.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 54c23c9d-0a3c-6941-2b56-6ff9486ef226
---

# Using role-based access control for apps - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Role-based access control (RBAC) is a popular mechanism to enforce authorization in applications. When an organization uses RBAC, an application developer defines roles for the application. An administrator can then assign roles to different users and groups to control who has access to content and functionality in the application.

Applications typically receive user role information as claims in a security token. Developers can provide their own implementation for how role claims are interpreted as application permissions. This interpretation can involve using middleware or other options provided by the application platform or related libraries.

## App roles

Microsoft Entra External ID allows you to define application roles for your application and assign those roles to users and groups. The roles you assign to a user or group define their level of access to the resources and operations in your application.

When Microsoft Entra External ID issues a security token for an authenticated user, it includes the names of the roles you've assigned the user or group in the security token's roles claim. An application that receives that security token in a request can then make authorization decisions based on the values in the roles claim.

## Groups

Developers can also use security groups to implement RBAC in their applications, where the memberships of the user in specific groups are interpreted as their role memberships. When an organization uses security groups, a groups claim is included in the token. The groups claim specifies the identifiers of all of the groups to which the user is assigned within the current external tenant.

## App roles vs. groups

Though you can use app roles or groups for authorization, key differences between them can influence which you decide to use for your scenario.

| App roles | Groups |
| --- | --- |
| They're specific to an application and are defined in the app registration. | They aren't specific to an app, but to an external tenant. |
| Can't be shared across applications. | Can be used in multiple applications. |
| App roles are removed when their app registration is removed. | Groups remain intact even if the app is removed. |
| Provided in the `roles` claim. | Provided in `groups` claim. |

## Create a security group

Security groups manage user and computer access to shared resources. You can create a security group so that all group members have the same set of security permissions.

To create a security group, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Groups Administrator](../../identity/role-based-access-control/permissions-reference#groups-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to your external tenant from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **Groups** &gt; **All groups**.
4. Select **New group**.
5. Under **Group type** dropdown, select **Security**.
6. Enter **Group name** for the security group, such as *Contoso\_App\_Administrators*.
7. Enter **Group description** for the security group, such as *Contoso app Security Administrator*.
8. Select **Create**.

The new security group appears in the **All groups** list. If you don't see it immediately, refresh the page.

Microsoft Entra External ID can include a user's group membership information in tokens for use within applications. You can learn how to add the group claim to tokens in the Assign users and groups to roles section.

## Declare roles for an application

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to your external tenant from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **App registrations**.
4. Select the application you want to define app roles in.
5. Select **App roles**, and then select **Create app role**.
6. In the **Create app role** pane, enter the settings for the role. The following table describes each setting and its parameters.

    | Field | Description | Example |
    | --- | --- | --- |
    | **Display name** | Display name for the app role that appears in the app assignment experiences. This value may contain spaces. | `Orders manager` |
    | **Allowed member types** | Specifies whether this app role can be assigned to users, applications, or both. | `Users/Groups` |
    | **Value** | Specifies the value of the roles claim that the application should expect in the token. The value should exactly match the string referenced in the application's code. The value can't contain spaces. | `Orders.Manager` |
    | **Description** | A more detailed description of the app role displayed during admin app assignment experiences. | `Manage online orders.` |
    | **Do you want to enable this app role?** | Specifies whether the app role is enabled. To delete an app role, deselect this checkbox and apply the change before attempting the delete operation. | *Checked* |
7. Select **Apply** to create the application role.

### Assign users and groups to roles

Once you've added app roles in your application, administrator can assign users and groups to the roles. Assignment of users and groups to roles can be done through the admin center, or programmatically using [Microsoft Graph](/en-us/graph/api/user-post-approleassignments). When the users assigned to the various app roles sign in to the application, their tokens have their assigned roles in the `roles` claim.

To assign users and groups to application roles by using the Azure portal:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to your external tenant from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **Enterprise apps**.
4. Select **All applications** to view a list of all your applications. If your application doesn't appear in the list, use the filters at the top of the **All applications** list to restrict the list, or scroll down the list to locate your application.
5. Select the application in which you want to assign users or security group to roles.
6. Under **Manage**, select **Users and groups**.
7. Select **Add user/group** to open the **Add Assignment** pane.
8. In the **Add Assignment** pane, select the link under **Users and groups**. A list of users and security groups appears. You can select multiple users and groups in the list.
9. Once you've selected users and groups, choose **Select**.
10. In the **Add assignment** pane, select the link under **Select a role**. All the roles you defined for the application appear.
11. Select a role, and then choose **Select**.
12. Select **Assign** to finish the assignment of users and groups to the app.
13. Confirm that the users and groups you added appear in the **Users and groups** list.

To test your application, sign out and sign in again with the user you assigned the roles. Inspect the security token to make sure that it contains the user's role.

## Add group claims to security tokens

To emit the group membership claims in security tokens, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../../identity/role-based-access-control/permissions-reference#application-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to your external tenant from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **App registrations**.
4. Select the application in which you want to add the groups claim.
5. Under **Manage**, select **Token configuration**.
6. Select **Add groups claim**.
7. Select group types to include in the security tokens.
8. For the **Customize token properties by type**, select **Group ID**.
9. Select **Add** to add the groups claim.

### Add members to a group

Now that you've added app groups claim in your application, add users to the security groups. If you don't have security group, [create one](../../fundamentals/how-to-manage-groups#create-a-basic-group-and-add-members).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](../../identity/role-based-access-control/permissions-reference#groups-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to your external tenant from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **Groups** &gt; **All groups**.
4. Select the group you want to manage.
5. Select **Members**.
6. Select **+ Add members**.
7. Scroll through the list or enter a name in the search box. You can choose multiple names. When you're ready, choose **Select**.
8. The **Group Overview** page updates to show the number of members who are now added to the group.

To test your application, sign out, and then sign in again with the user you added to the security group. Inspect the security token to make sure that it contains the user's group membership.

## Groups and application roles support

An external tenant follows the Microsoft Entra user and group management model and application assignment. Many of the core Microsoft Entra features are being phased into external tenants.

The following table shows which features are currently available.

| **Feature** | **Currently available?** |
| --- | --- |
| Create an application role for a resource | Yes, by modifying the application manifest |
| Assign an application role to users | Yes |
| Assign an application role to groups | Yes, via Microsoft Graph only |
| Assign an application role to applications | Yes, via application permissions |
| Assign a user to an application role | Yes |
| Assign an application to an application role (application permission) | Yes |
| Add a group to an application/service principal (groups claim) | Yes, via Microsoft Graph only |
| Create/update/delete a customer (local user) via the Microsoft Entra admin center | Yes |
| Reset a password for a customer (local user) via the Microsoft Entra admin center | Yes |
| Create/update/delete a customer (local user) via Microsoft Graph | Yes |
| Reset a password for a customer (local user) via Microsoft Graph | Yes, only if the service principal is added to the Global Administrator role |
| Create/update/delete a security group via the Microsoft Entra admin center | Yes |
| Create/update/delete a security group via the Microsoft Graph API | Yes |
| Change security group members using the Microsoft Entra admin center | Yes |
| Change security group members using the Microsoft Graph API | Yes |
| Scale up to 50,000 users and 50,000 groups | Not currently available |
| Add 50,000 users to at least two groups | Not currently available |
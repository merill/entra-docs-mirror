---
layout: Conceptual
title: Add app roles and get them from a token - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/howto-add-app-roles-in-apps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to add app roles to an application registered in Microsoft Entra ID. Assign users and groups to these roles, and receive them in the 'roles' claim in the token.
manager: pmwongera
ms.date: 2026-09-25T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.topic: how-to
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: fbce165f-bacb-eadb-4ae0-4add6f912cc0
document_version_independent_id: 0e07887e-a4b6-aff5-eb26-8f0868192be7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/howto-add-app-roles-in-apps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/howto-add-app-roles-in-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/howto-add-app-roles-in-apps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: fffe76f8-b8a7-e892-18b0-77a1625418f8
---

# Add app roles and get them from a token - Microsoft identity platform | Microsoft Learn

Role-based access control (RBAC) is a popular mechanism to enforce authorization in applications. RBAC allows administrators to grant permissions to roles rather than to specific users or groups. The administrator can then assign roles to different users and groups to control who has access to what content and functionality.

By using RBAC with application role and role claims, developers can securely enforce authorization in their apps with less effort.

Another approach is to use Microsoft Entra groups and group claims as shown in the [active-directory-aspnetcore-webapp-openidconnect-v2](https://aka.ms/groupssample) code sample on GitHub. Microsoft Entra groups and application roles aren't mutually exclusive; they can be used together to provide even finer-grained access control.

## Declare roles for an application

You define app roles by using the [Microsoft Entra admin center](https://entra.microsoft.com) during the [app registration process](quickstart-register-app). App roles are defined on an application registration representing a service, app, or API. When a user signs in to the application, Microsoft Entra ID emits a `roles` claim for each role that the user or service principal was granted, which can be used to implement [claim-based authorization](claims-validation). App roles can be assigned [to a user or a group of users](../identity/enterprise-apps/add-application-portal-assign-users). App roles can also be assigned to the service principal for another application, or [to the service principal for a managed identity](../identity/managed-identities-azure-resources/how-to-assign-app-role-managed-identity).

Currently, if you add a service principal to a group, and then assign an app role to that group, Microsoft Entra ID doesn't add the `roles` claim to tokens it issues.

App roles are declared using App roles UI in the Microsoft Entra admin center:

App roles are subject to a default limit of 700 permission definitions per application or service principal, shared with exposed delegated permission scopes. They also count toward the separate 1,200-entry application manifest limit. For counting rules and guidance for existing objects, see App role limits.

### App roles UI

To create an app role by using the Microsoft Entra admin center's user interface:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to the tenant containing the app registration from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **App registrations** and then select the application you want to define app roles in.
4. Under manage select **App roles**, and then select **Create app role**.

    ![An app registration's app roles pane in the Azure portal](media/howto-add-app-roles-in-apps/app-roles-overview-pane.png)
5. In the **Create app role** pane, enter the settings for the role. The table following the image describes each setting and their parameters.

    ![An app registration's app roles create context pane in the Azure portal](media/howto-add-app-roles-in-apps/app-roles-create-context-pane.png)

    | Field | Description | Example |
    | --- | --- | --- |
    | **Display name** | Display name for the app role that appears in the admin consent and app assignment experiences. This value may contain spaces. | `Survey Writer` |
    | **Allowed member types** | Specifies whether this app role can be assigned to users, applications, or both.When available to `applications`, app roles appear as application permissions in an app registration's **Manage** section &gt; **API permissions &gt; Add a permission &gt; My APIs &gt; Choose an API &gt; Application permissions**. | `Users/Groups` |
    | **Value** | Specifies the value of the roles claim that the application should expect in the token. The value should exactly match the string referenced in the application's code. The value can't contain spaces. | `Survey.Create` |
    | **Description** | A more detailed description of the app role displayed during admin app assignment and consent experiences. | `Writers can create surveys.` |
    | **Do you want to enable this app role?** | Specifies whether the app role is enabled. To delete an app role, deselect this checkbox and apply the change before attempting the delete operation. This setting controls the app role's usage and availability while being able to temporarily or permanently disabling it without removing it entirely. | *Checked* |
6. Select **Apply** to save your changes.

When the app role is set to **Enabled**, any users, applications, or groups who are assigned have the app role included in their tokens. These can be access tokens when your app is the API being called by an app or ID tokens when your app is signing in a user.

When the app role is set to **Disabled**, it becomes inactive and no longer assignable. However, the current app role assignments to users, groups and applications will remain, and the app role will continue to pass in the token(s). Remove the app role from the user, group or application to ensure the app role is also removed from the token(s).

## App role limits

Microsoft Entra ID enforces a default limit of 700 permission definitions on each [application](/en-us/graph/api/resources/application) and [service principal](/en-us/graph/api/resources/serviceprincipal). App roles (`appRoles`) and exposed delegated permission scopes (`api.oauth2PermissionScopes` on an application, or `oauth2PermissionScopes` on a service principal) share this limit because they're stored in the same underlying `Entitlement` collection.

The following counting rules apply:

- The limit counts permission definitions, not the users, groups, or applications assigned to a role. App role assignments have [separate limits](../identity/users/directory-service-limits-restrictions).
- Enabled and disabled definitions both count. Setting `isEnabled` to `false` doesn't free capacity.
- Each distinct permission ID in the combined role and scope collection counts once. A role and a scope that share an ID and have matching shared properties are stored as one definition.
- The count applies to each object's resulting collection, not just the entries added in a request. For a service principal, it includes definitions inherited from the application and definitions added directly to the service principal.

For example, 650 app roles and 50 exposed delegated permission scopes with distinct IDs use all 700 entries. The separate [1,200-entry application manifest limit](reference-microsoft-graph-app-manifest#manifest-limits) doesn't allow you to exceed this limit.

### Existing objects above the limit

Existing objects can have more than 700 permission definitions. The count check allows updates that keep the number of definitions unchanged or reduce it, even when the result remains above the applicable limit. Other validation rules still apply. An update that increases the count above the applicable limit is rejected.

Some existing objects have a higher service-assigned limit. Don't assume that a higher limit on one object applies to another object or tenant. You can't configure this limit through the application manifest.

When the 700-value limit rejects an update, the error can identify the underlying property rather than `appRoles`:

```text
The total count of values: 701 exceeds the set maxValuesCount limit: 700 for property: Entitlement
```

### Design within the limit

Use app roles for stable authorization categories, such as `Reader`, `Writer`, and `Administrator`, rather than defining a role for every resource, customer, or individual action. Keep finer-grained resource permissions in your application's authorization data and enforce them in the application.

Remove obsolete roles and scopes to free capacity. Before deleting an app role, disable it and review its assignments and the application behavior that depends on it. Assigning groups to existing app roles can simplify assignment management, but doesn't increase the number of role definitions you can store.

## Assign application owner

Before you can assign app roles to applications, you need to assign yourself as the application owner.

1. In your app registration, under **Manage**, select **Owners**, and **Add owners**.
2. In the new window, find and select the owner(s) that you want to assign to the application. Selected owners appear in the right panel. Once done, confirm with **Select** and the app owner(s) appear in the owner's list.

Note

Ensure that both the API application and the application you want to add permissions to both have an owner, otherwise the API will not be listed when requesting API permissions.

## Assign app roles to applications

After adding app roles in your application, you can assign an app role to a client app by using the Microsoft Entra admin center or programmatically by using [Microsoft Graph](/en-us/graph/api/serviceprincipal-post-approleassignments?tabs=http). Assigning an app role to an application shouldn't be confused with [assigning roles to users](../identity/role-based-access-control/manage-roles-portal).

When you assign app roles to an application, you create *application permissions*. Application permissions are typically used by daemon apps or back-end services that need to authenticate and make authorized API call as themselves, without the interaction of a user.

To assign app roles to an application by using the Microsoft Entra admin center:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **App registrations** and then select **All applications**.
3. Select **All applications** to view a list of all your applications. If your application doesn't appear in the list, use the filters at the top of the **All applications** list to restrict the list, or scroll down the list to locate your application.
4. Select the application to which you want to assign an app role.
5. Select **API permissions** &gt; **Add a permission**.
6. Select the **My APIs** tab, and then select the app for which you defined app roles.
7. Under **Permission**, select the roles you want to assign.
8. Select the **Add permissions** button complete addition of the roles.

The newly added roles should appear in your app registration's **API permissions** pane.

### Grant admin consent

Because these are *application permissions*, not delegated permissions, an admin must grant consent to use the app roles assigned to the application.

1. In the app registration's **API permissions** pane, select **Grant admin consent for &lt;tenant name&gt;**.
2. Select **Yes** when prompted to grant consent for the requested permissions.

The **Status** column should reflect that consent has been **Granted for &lt;tenant name&gt;**.

## Usage scenario of app roles

If you're implementing app role business logic that signs in the users in your application scenario, first define the app roles in **App registrations**. Then, an admin assigns them to users and groups in the **Enterprise applications** pane. Depending on the scenario, these assigned app roles are included in different tokens that are issued for your application. For example, for an app that signs in users, the roles claims are included in the ID token. When your application calls an API, the roles claims are included in the access token.

If you're implementing app role business logic in an app-calling-API scenario, you have two app registrations. One app registration is for the app, and a second app registration is for the API. In this case, define the app roles and assign them to the user or group in the app registration of the API. When the user authenticates with the app and requests an access token to call the API, a roles claim is included in the token. Your next step is to add code to your web API to check for those roles when the API is called.

To learn how to add authorization to your web API, see [Protected web API: Verify scopes and app roles](scenario-protected-web-api-verification-scope-app-roles).

## App roles vs. groups

Though you can use app roles or groups for authorization, key differences between them can influence which you decide to use for your scenario.

| App roles | Groups |
| --- | --- |
| They're specific to an application and are defined in the app registration. They move with the application. | They aren't specific to an app, but to a Microsoft Entra tenant. |
| App roles are removed when their app registration is removed. | Groups remain intact even if the app is removed. |
| Provided in the `roles` claim. | Provided in `groups` claim. |

Developers can use app roles to control whether a user can sign in to an app or an app can obtain an access token for a web API. To extend this security control to groups, developers and admins can also assign security groups to app roles.

Developers prefer to use app roles when they want to describe and control the parameters of authorization in their app themselves. For example, an app using groups for authorization will break in the next tenant as both the group ID and name could be different. An app using app roles remains safe. In fact, SaaS apps often assign groups to app roles for the same reasons, as it allows the SaaS app to be provisioned in multiple tenants.

## Assign users and groups to Microsoft Entra roles

Once you add app roles in your application, you can assign users and groups to [Microsoft Entra roles](../identity/role-based-access-control/permissions-reference). Assignment of users and groups to roles can be done through the portal's UI, or programmatically using [Microsoft Graph](/en-us/graph/api/user-post-approleassignments). When the users assigned to the various roles sign in to the application, their tokens have the assigned roles in the `roles` claim.

To assign users and groups to roles by using the Microsoft Entra admin center:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to the tenant containing the app registration from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **Enterprise apps**.
4. Select **All applications** to view a list of all your applications. If your application doesn't appear in the list, use the filters at the top of the **All applications** list to restrict the list, or scroll down the list to locate your application.
5. Select the application in which you want to assign users or security group to roles.
6. Under **Manage**, select **Users and groups**.
7. Select **Add user** to open the **Add Assignment** pane.
8. Select the **Users and groups** selector from the **Add Assignment** pane. A list of users and security groups is displayed. You can search for a certain user or group and select multiple users and groups that appear in the list. Select the **Select** button to proceed.
9. Select **Select a role** in the **Add assignment** pane. All the roles that you defined for the application are displayed.
10. Choose a role and select the **Select** button.
11. Select the **Assign** button to finish the assignment of users and groups to the app.

Confirm that the users and groups you added appear in the **Users and groups** list.
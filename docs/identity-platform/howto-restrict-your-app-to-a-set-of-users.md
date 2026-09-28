---
layout: Conceptual
title: Restrict a Microsoft Entra app to a set of users - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/howto-restrict-your-app-to-a-set-of-users
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to restrict access to your apps registered in Microsoft Entra ID to a selected set of users.
manager: pmwongera
ms.custom: 
ms.date: 2024-07-19T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.topic: how-to
locale: en-us
document_id: be62a693-4dfd-ad56-cce2-b4dbc794f34b
document_version_independent_id: bd8bc1b2-925f-a0c3-4286-37eb2f7189f5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/howto-restrict-your-app-to-a-set-of-users.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/howto-restrict-your-app-to-a-set-of-users
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/howto-restrict-your-app-to-a-set-of-users.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 6e40ec9c-6e6d-5c65-98f1-08f969a951fc
---

# Restrict a Microsoft Entra app to a set of users - Microsoft identity platform | Microsoft Learn

Applications registered in a Microsoft Entra tenant are, by default, available to all users of the tenant who authenticate successfully. To restrict your application to a set of users, you can configure your application to require user assignment. Users and services attempting to access the application or services need to be assigned to the application, or they won't be able to sign-in or obtain an access token.

Similarly, in a [multitenant](howto-convert-app-to-be-multi-tenant) application, all users in the Microsoft Entra tenant where the application is provisioned can access the application once they successfully authenticate in their respective tenant.

Tenant administrators and developers often have requirements where an application must be restricted to a certain set of users or apps (services). There are two ways to restrict an application to a certain set of users, apps or security groups:

- Developers can use popular authorization patterns like [Azure role-based access control (Azure RBAC)](howto-implement-rbac-for-apps).
- Tenant administrators and developers can use built-in feature of Microsoft Entra ID.

## Prerequisites

- A Microsoft Entra user account. If you don't already have one, [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- An [application registered in your Microsoft Entra tenant](quickstart-register-app)
- You must be the application owner or be at least a [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator) in your tenant.

## Supported app configurations

The option to restrict an app to a specific set of users, apps or security groups in a tenant works with the following types of applications:

- Applications configured for federated single sign-on with SAML-based authentication.
- Application proxy applications that use Microsoft Entra preauthentication.
- Applications built directly on the Microsoft Entra application platform that use OAuth 2.0/OpenID Connect authentication after a user or admin has consented to that application.

## Update the app to require user assignment

To update an application to require user assignment, you must be owner of the application under Enterprise apps, or be at least a [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. If you have access to multiple tenants, use the **Directories + subscriptions** filter ![](media/common/admin-center-settings-icon.png) in the top menu to switch to the tenant containing the app registration from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **Enterprise apps**, then select **All applications**.
4. Select the application you want to configure to require assignment. Use the filters at the top of the window to search for a specific application.
5. On the application's **Overview** page, under **Manage**, select **Properties**.
6. Locate the setting **Assignment required?** and set it to **Yes**.
7. Select **Save** on the top bar.

When an application requires assignment, user consent for that application isn't allowed. This is true even if users consent for that app would have otherwise been allowed. Be sure to [grant tenant-wide admin consent](../identity/enterprise-apps/grant-admin-consent) to apps that require assignment.

Note

If the user is a Global Administrator, user assignment requirement will not be applicable. Global Administrator is an highly privileged role that allows access to all administrative features in Microsoft Entra ID and can elevate their access to manage all Azure subscriptions and management groups.

## Assign the app to users and groups to restrict access

Once you've configured your app to enable user assignment, you can go ahead and assign the app to users and groups.

1. Under **Manage**, select the **Users and groups** then select **Add user/group**.
2. Under **Users**, select **None Selected**, and the **Users** selector pane opens, where you can select multiple users and groups.
3. Once you're done adding the users and groups, select **Select**.
    1. (Optional) If you have defined app roles in your application, you can use the **Select role** option to assign the app role to the selected users and groups.
4. Select **Assign** to complete the assignments of the app to the users and groups.
5. On return to the **Users and groups** page, the newly added users and groups appear in the updated list.

## Restrict access to an app (resource) by assigning other services (client apps)

Follow the steps in this section to secure app-to-app authentication access for your tenant.

1. Navigate to Service Principal sign-in logs in your tenant to find services authenticating to access resources in your tenant.
2. Check using app ID if a Service Principal exists for both resource and client apps in your tenant that you wish to manage access.

    ```powershell
    Get-MgServicePrincipal `
    -Filter "AppId eq '$appId'"
    ```
3. Create a Service Principal using app ID, if it doesn't exist:

    ```powershell
    New-MgServicePrincipal `
    -AppId $appId
    ```
4. Explicitly assign client apps to resource apps (this functionality is available only in API and not in the Microsoft Entra admin center):

    ```powershell
    $clientAppId = “[guid]”
                   $clientId = (Get-MgServicePrincipal -Filter "AppId eq '$clientAppId'").Id
    New-MgServicePrincipalAppRoleAssignment `
    -ServicePrincipalId $clientId `
    -PrincipalId $clientId `
    -ResourceId (Get-MgServicePrincipal -Filter "AppId eq '$appId'").Id `
    -AppRoleId "00000000-0000-0000-0000-000000000000"
    ```
5. Require assignment for the resource application to restrict access only to the explicitly assigned users or services.

    ```powershell
    Update-MgServicePrincipal -ServicePrincipalId (Get-MgServicePrincipal -Filter "AppId eq '$appId'").Id -AppRoleAssignmentRequired:$true
    ```

Note

If you don't want tokens to be issued for an application or if you want to block an application from being accessed by users or services in your tenant, create a service principal for the application and [disable user sign-in](../identity/enterprise-apps/disable-user-sign-in-portal) for it.
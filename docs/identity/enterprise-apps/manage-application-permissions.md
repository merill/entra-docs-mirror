---
layout: Conceptual
title: Review permissions granted to enterprise applications - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/manage-application-permissions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn how to review and revoke permissions, and invalidate refresh tokens for an application in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-03-03T00:00:00.0000000Z
ms.reviewer: phsignor
zone_pivot_groups: enterprise-apps-all
ms.collection: M365-identity-device-management
ms.custom: enterprise-apps, no-azure-ad-ps-ref
locale: en-us
document_id: a35d8227-9a4b-57a3-dd9b-31d577451c73
document_version_independent_id: 9cb13a07-8fe0-4478-7ca0-ddbb1fa87d6c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/manage-application-permissions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/manage-application-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/manage-application-permissions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 48c5890c-9107-4a97-a9ef-fa59b5dfeb52
---

# Review permissions granted to enterprise applications - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to review permissions granted to applications in your Microsoft Entra tenant. You might need to review permissions when you detect a malicious application, or one that has more permissions than is necessary. You learn how to revoke permissions granted to the application using Microsoft Graph API and existing versions of PowerShell.

The steps in this article apply to all applications that were added to your Microsoft Entra tenant via user or admin consent. For more information on consenting to applications, see [User and admin consent](user-admin-consent-overview).

## Prerequisites

To review permissions granted to applications, you need:

- A Microsoft Entra account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - Cloud Application Administrator
    - Application Administrator.
    - A Service principal owner who isn't an administrator is able to invalidate refresh tokens.

::: zone pivot="portal"

## Review and revoke permissions in the Microsoft Entra admin center

You can access the Microsoft Entra admin center to view the permissions granted to an app. You can revoke permissions granted by admins for your entire organization, and you can get contextual PowerShell scripts to perform other actions.

For information on how to restore revoked or deleted permissions, see [Restore permissions granted to applications](restore-permissions).

To review an application's permissions granted for the entire organization or to a specific user or group:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Select the application that you want to restrict access to.
4. Select **Permissions**.
5. To view permissions that apply to your entire organization, select the **Admin consent** tab. To view permissions granted to a specific user or group, select the **User consent** tab.
6. To view the details of a given permission, select the permission from the list. The **Permission Details** pane opens. After reviewing the permissions granted to an application, you can revoke permissions granted by admins for your entire organization. 
    Note

    You can't revoke permissions in the **User consent** tab using the portal. You can revoke these permissions using Microsoft Graph API calls or PowerShell cmdlets. Go to the PowerShell and Microsoft Graph tabs of this article for more information.

To revoke permissions in the **Admin consent** tab:

1. View the list of permissions in the **Admin consent** tab.
2. Choose the permission you would like to revoke, then select the **...** control for that permission. ![Screenshot shows how to revoke admin consent.](media/manage-application-permissions/revoke-permissions.png)
3. Select **Revoke permission**.

::: zone-end

::: zone pivot="entra-powershell"

## Review and revoke permissions using Microsoft Entra PowerShell

Use the following Microsoft Entra PowerShell script to revoke all permissions granted to an application. You need to sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).

```powershell
Connect-Entra -scopes "Application.ReadWrite.All", "DelegatedPermissionGrant.ReadWrite.All", "AppRoleAssignment.ReadWrite.All" 

# Get Service Principal using objectId
$app_name = "<app-displayName>"
$sp = Get-EntraServicePrincipal -Filter "displayName eq '$app_name'"

# Get all delegated permissions for the service principal
$spOAuth2PermissionsGrants = Get-EntraOAuth2PermissionGrant -All | Where-Object { $_.clientId -eq $sp.ObjectId }

# Remove all delegated permissions granted to the service principal
$spOAuth2PermissionsGrants | ForEach-Object {
    Remove-EntraOAuth2PermissionGrant -ObjectId $_.ObjectId
}

# Get all application permissions for the service principal
$spApplicationPermissions = Get-EntraServicePrincipalAppRoleAssignment -ObjectId $sp.ObjectId -All | Where-Object { $_.PrincipalType -eq "ServicePrincipal" }

# Remove all application permissions
$spApplicationPermissions | ForEach-Object {
    Remove-EntraServicePrincipalAppRoleAssignment -ObjectId $_.PrincipalId -AppRoleAssignmentId $_.objectId
}
```

## Remove all user and group assignments using Microsoft Entra PowerShell

Remove appRoleAssignments for users or groups to the application using the following scripts.

```powershell
connect-entra -scopes "Application.ReadWrite.All", "AppRoleAssignment.ReadWrite.All"
#Retrieve the service principal object ID.
$app_name = "<Your App's display name>"
$sp = Get-EntraServicePrincipal -Filter "displayName eq '$app_name'"
$sp.ObjectId

# Get Microsoft Entra App role assignments using objectId of the Service Principal
$assignments = Get-EntraServicePrincipalAppRoleAssignedTo -ObjectId $sp.ObjectId -All $true

# Remove all users and groups assigned to the application
$assignments | ForEach-Object {
    if ($_.PrincipalType -eq "User") {
        Remove-EntraUserAppRoleAssignment -ObjectId $_.PrincipalId -AppRoleAssignmentId $_.ObjectId
    } elseif ($_.PrincipalType -eq "Group") {
        Remove-EntraGroupAppRoleAssignment -ObjectId $_.PrincipalId -AppRoleAssignmentId $_.ObjectId
    }
}
```

::: zone-end

::: zone pivot="ms-powershell"

## Review and revoke permissions using Microsoft Graph PowerShell

Use the following Microsoft Graph PowerShell script to revoke all permissions granted to an application. You need to sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).

```powershell
Connect-MgGraph -Scopes "Application.ReadWrite.All", "Directory.ReadWrite.All", "DelegatedPermissionGrant.ReadWrite.All", "AppRoleAssignment.ReadWrite.All"

# Get Service Principal using objectId
$sp = Get-MgServicePrincipal -ServicePrincipalID "<ServicePrincipal objectID>"

Example: Get-MgServicePrincipal -ServicePrincipalId 'aaaaaaaa-bbbb-cccc-1111-222222222222'

# Get all delegated permissions for the service principal
$spOAuth2PermissionsGrants= Get-MgOauth2PermissionGrant -All| Where-Object { $_.clientId -eq $sp.Id }

# Remove all delegated permissions
$spOauth2PermissionsGrants |ForEach-Object {
  Remove-MgOauth2PermissionGrant -OAuth2PermissionGrantId $_.Id
}

# Get all application permissions for the service principal
$spApplicationPermissions = Get-MgServicePrincipalAppRoleAssignment -ServicePrincipalId $Sp.Id -All | Where-Object { $_.PrincipalType -eq "ServicePrincipal" }

# Remove all application permissions
$spApplicationPermissions | ForEach-Object {
Remove-MgServicePrincipalAppRoleAssignedTo -ServicePrincipalId $Sp.Id  -AppRoleAssignmentId $_.Id
}
```

## Remove all user and group assignments using Microsoft Graph PowerShell

Remove appRoleAssignments for users or groups to the application using the following scripts.

```powershell
Connect-MgGraph -Scopes "Application.ReadWrite.All", "Directory.ReadWrite.All", "AppRoleAssignment.ReadWrite.All"

# Get Service Principal using objectId
$sp = Get-MgServicePrincipal -ServicePrincipalID "<ServicePrincipal objectID>"

Example: Get-MgServicePrincipal -ServicePrincipalId 'aaaaaaaa-bbbb-cccc-1111-222222222222'

# Get Microsoft Entra App role assignments using objectID of the Service Principal
$spApplicationPermissions = Get-MgServicePrincipalAppRoleAssignedTo -ServicePrincipalID $sp.Id -All | Where-Object { $_.PrincipalType -eq "ServicePrincipal" }

# Revoke refresh token for all users assigned to the application
  $spApplicationPermissions | ForEach-Object {
  Remove-MgServicePrincipalAppRoleAssignment -ServicePrincipalId $_.PrincipalId -AppRoleAssignmentId $_.Id
}
```

::: zone-end

::: zone pivot="ms-graph"

## Review and revoke permissions using Microsoft Graph

To review permissions, Sign in to [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).

You need to consent to the following permissions:

`Application.ReadWrite.All`, `Directory.ReadWrite.All`, `DelegatedPermissionGrant.ReadWrite.All`, `AppRoleAssignment.ReadWrite.All`.

### Delegated permissions

Run the following queries to review delegated permissions granted to an application.

1. Get service principal using the object ID.

    ```http
    GET https://graph.microsoft.com/v1.0/servicePrincipals/{id}
    ```

    Example:

    ```http
    GET https://graph.microsoft.com/v1.0/servicePrincipals/00001111-aaaa-2222-bbbb-3333cccc4444
    ```
2. Get all delegated permissions for the service principal

    ```http
    GET https://graph.microsoft.com/v1.0/servicePrincipals/{id}/oauth2PermissionGrants
    ```
3. Remove delegated permissions using oAuth2PermissionGrants ID.

    ```http
    DELETE https://graph.microsoft.com/v1.0/oAuth2PermissionGrants/{id}
    ```

### Application permissions

Run the following queries to review application permissions granted to an application.

1. Get all application permissions for the service principal

    ```http
    GET https://graph.microsoft.com/v1.0/servicePrincipals/{servicePrincipal-id}/appRoleAssignments
    ```
2. Remove application permissions using appRoleAssignment ID

    ```http
    DELETE https://graph.microsoft.com/v1.0/servicePrincipals/{resource-servicePrincipal-id}/appRoleAssignedTo/{appRoleAssignment-id}
    ```

## Remove all user and group assignments using Microsoft Graph

Run the following queries to remove appRoleAssignments of users or groups to the application.

1. Get Service Principal using objectID.

    ```http
    GET https://graph.microsoft.com/v1.0/servicePrincipals/{id}
    ```

    Example:

    ```http
    GET https://graph.microsoft.com/v1.0/servicePrincipals/aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb
    ```
2. Get Microsoft Entra App role assignments using objectID of the Service Principal.

    ```http
    GET https://graph.microsoft.com/v1.0/servicePrincipals/{servicePrincipal-id}/appRoleAssignedTo
    ```
3. Revoke refresh token for users and groups assigned to the application using appRoleAssignment ID.

    ```http
    DELETE https://graph.microsoft.com/v1.0/servicePrincipals/{servicePrincipal-id}/appRoleAssignedTo/{appRoleAssignment-id}
    ```

::: zone-end

Note

Revoking the current granted permission doesn't stop users from re-consenting to the application's requested permissions. You need to [stop the application from requesting the permissions through dynamic consent](../../identity-platform/howto-update-permissions). If you want to block users from consenting altogether, read [Configure how users consent to applications](configure-user-consent).

## Other authorization to consider

Delegated and application permissions aren't the only ways to grant applications and users access to protected resources. Admins should be aware of other authorization systems that might grant access to sensitive information. Examples of various authorization systems at Microsoft include [Microsoft Entra built-in roles](/en-us/entra/identity/role-based-access-control/permissions-reference), [Exchange RBAC](/en-us/exchange/permissions-exo/application-rbac), and [Teams resource-specific consent](/en-us/microsoftteams/platform/graph-api/rsc/resource-specific-consent).
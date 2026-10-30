---
layout: Conceptual
title: Grant Consent on Behalf of a Single User - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/grant-consent-single-user
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn how to grant consent on behalf of a single user when the user consent is disabled or restricted.
ms.topic: how-to
ms.date: 2024-12-12T00:00:00.0000000Z
ms.reviewer: phsignor
zone_pivot_groups: enterprise-apps-ms-graph-ms-powershell
ms.custom: enterprise-apps
locale: en-us
document_id: 4b1904fc-0df4-01e6-c1f8-8e92673b76ec
document_version_independent_id: 196471b9-4df4-d4a7-6bc5-a20ebc6f50e7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/grant-consent-single-user.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/grant-consent-single-user
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/grant-consent-single-user.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 98ff7910-5a2d-7605-6963-6d64a3514021
---

# Grant Consent on Behalf of a Single User - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to grant consent on behalf of a single user by using PowerShell.

When a user grants consent for themselves, the following events occur more often:

1. A service principal for the client application is created, if it doesn't already exist. A service principal is the instance of an application or a service in your Microsoft Entra tenant. Access granted to the app or service is associated with this service principal object.
2. For each API to which the application requires access, a delegated permission grant to that API is created for the permissions that the application needs. The access is granted on behalf of the user. A delegated permission grant authorizes an application to access an API on behalf of a user, when that user signs in.
3. The user is assigned the client application. Assigning the application to the user ensures that the application is listed in the [My Apps](myapps-overview) portal for that user. The user can review and revoke the access granted on their behalf from the My Apps portal.

## Prerequisites

- A user account with a Privileged Role Administrator, Application Administrator, or Cloud Application Administrator role.
- The following details from the Microsoft Entra admin center:

    - The app ID for the app that you're granting consent for. For purposes of this article, we call it the *client application*.
    - The API permissions that the client application requires. Find out the app ID of the API and the permission IDs or claim values.
    - The username or object ID for the user on whose behalf access is granted.

## Grant consent on behalf of a single user

::: zone pivot="msgraph-powershell"

The example in this article uses [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/get-started) to grant consent on behalf of a single user. The client application is [Microsoft Graph Explorer](https://aka.ms/ge), and we grant access to the Microsoft Graph API.

To grant consent to an application on behalf of one user by using Microsoft Graph PowerShell, you need to sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).

```powershell
# The app for which consent is being granted.
$clientAppId = "de8bc8b5-d9f9-48b1-a8ad-b748da725064" # Your client application

# The API to which access will be granted. Your client application makes API 
# requests to the Microsoft Graph API, so we'll use that here.
$resourceAppId = "00000003-0000-0000-c000-000000000000" # Microsoft Graph API

# The permissions to grant. Here we're including "openid", "profile", "User.Read",
# and "offline_access" (for basic sign-in), as well as "User.ReadBasic.All" (for 
# reading other users' basic profile).
$permissions = @("openid", "profile", "offline_access", "User.Read", "User.ReadBasic.All")

# The user on behalf of whom access will be granted. The app will be able to access 
# the API on behalf of this user.
$userUpnOrId = "user@example.com"

# Step 0. Connect to Microsoft Graph PowerShell. We need User.ReadBasic.All to get
#    users' IDs, Application.ReadWrite.All to list and create service principals, 
#    DelegatedPermissionGrant.ReadWrite.All to create delegated permission grants, 
#    and AppRoleAssignment.ReadWrite.All to assign an app role.
#    WARNING: These are high-privilege permissions!
Connect-MgGraph -Scopes ("User.ReadBasic.All Application.ReadWrite.All " `
                        + "DelegatedPermissionGrant.ReadWrite.All " `
                        + "AppRoleAssignment.ReadWrite.All")

# Step 1. Check if a service principal exists for the client application. 
#     If one doesn't exist, create it.
$clientSp = Get-MgServicePrincipal -Filter "appId eq '$($clientAppId)'"
if (-not $clientSp) {
   $clientSp = New-MgServicePrincipal -AppId $clientAppId
}

# Step 2. Create a delegated permission that grants the client app access to the
#     API, on behalf of the user. (This example assumes that an existing delegated 
#     permission grant does not already exist, in which case it would be necessary 
#     to update the existing grant, rather than create a new one.)
$user = Get-MgUser -UserId $userUpnOrId
$resourceSp = Get-MgServicePrincipal -Filter "appId eq '$($resourceAppId)'"
$scopeToGrant = $permissions -join " "
$grant = New-MgOauth2PermissionGrant -ResourceId $resourceSp.Id `
                                     -Scope $scopeToGrant `
                                     -ClientId $clientSp.Id `
                                     -ConsentType "Principal" `
                                     -PrincipalId $user.Id

# Step 3. Assign the app to the user. This ensures that the user can sign in if assignment
#     is required, and ensures that the app shows up under the user's My Apps portal.
if ($clientSp.AppRoles | ? { $_.AllowedMemberTypes -contains "User" }) {
    Write-Warning ("A default app role assignment cannot be created because the " `
                 + "client application exposes user-assignable app roles. You must " `
                 + "assign the user a specific app role for the app to be listed " `
                 + "in the user's My Apps portal.")
} else {
    # The app role ID 00000000-0000-0000-0000-000000000000 is the default app role
    # indicating that the app is assigned to the user, but not for any specific 
    # app role.
    $assignment = New-MgServicePrincipalAppRoleAssignedTo `
          -ServicePrincipalId $clientSp.Id `
          -ResourceId $clientSp.Id `
          -PrincipalId $user.Id `
          -AppRoleId "00000000-0000-0000-0000-000000000000"
}
```

::: zone-end

::: zone pivot="ms-graph"

To grant consent to an application on behalf of one user who's using the Microsoft Graph API, sign in to [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).

You need to consent to the following permissions: `Application.ReadWrite.All`, `Directory.ReadWrite.All`, `DelegatedPermissionGrant.ReadWrite.All`.

In the following example, you grant delegated permissions defined by a resource API to a client enterprise application on behalf of a single user. In the example:

- The resource enterprise application is Microsoft Graph of object ID `aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb`.
- Microsoft Graph defines the delegated permissions, `User.Read.All` and `Group.Read.All`.
- The consentType is `Principal`, which indicates that you're consenting on behalf of a single user in the tenant.
- The object ID of the client enterprise application is `aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb`.
- The principal ID of the user is `aaaaaaaa-bbbb-cccc-1111-222222222222`.

Caution

Be careful! Permissions granted programmatically are not subject to review or confirmation. They take effect immediately.

1. Retrieve all the delegated permissions that Microsoft Graph (the resource application) defines in your tenant application. Identify the delegated permissions that you want to grant the client application. In this example, the delegation permissions are `User.Read.All` and `Group.Read.All`.

    ```http
    GET https://graph.microsoft.com/v1.0/servicePrincipals?$filter=displayName eq 'Microsoft Graph'&$select=id,displayName,appId,oauth2PermissionScopes
    ```
2. Grant the delegated permissions to the client enterprise application on behalf of the user by running the following request.

    ```http
    POST https://graph.microsoft.com/v1.0/oauth2PermissionGrants
    
    Request body
    {
       "clientId": "00001111-aaaa-2222-bbbb-3333cccc4444",
       "consentType": "Principal",
       "resourceId": "a0a0a0a0-bbbb-cccc-dddd-e1e1e1e1e1e1",
       "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
       "scope": "User.Read.All Group.Read.All"
    }
    ```
3. Confirm that you granted consent to the user by running the following request.

    ```http
    GET https://graph.microsoft.com/v1.0/oauth2PermissionGrants?$filter=clientId eq '00001111-aaaa-2222-bbbb-3333cccc4444' and consentType eq 'Principal'
    ```
4. Assign the app to the user. This assignment ensures that the user can sign in if assignment is required. It also ensures that the app is available through the user's My Apps portal.

    In the following example, `resourceId` represents the client app to which the user is being assigned. The user is assigned the default app role (`00000000-0000-0000-0000-000000000000`).

    ```http
        POST /servicePrincipals/resource-servicePrincipal-id/appRoleAssignedTo
    
        {
        "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
        "resourceId": "a0a0a0a0-bbbb-cccc-dddd-e1e1e1e1e1e1",
        "appRoleId": "00000000-0000-0000-0000-000000000000"
        }
    ```

::: zone-end